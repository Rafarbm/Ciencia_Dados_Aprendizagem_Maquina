
---

## 1. Método C.A.L.M.A. (Justificativas)

* **C - Comando:** Propor um painel de atendimentos médicos com duas entidades principais e um relacionamento $N:N$, um indicador com denominador, prevenção de erro na interface e teste para a regra de duplicidade.
* **A - Assunto:** Modelagem Relacional, SQL Server (T-SQL), Indicadores de Saúde/Operacionais e Interação Homem-Computador (IHC).
* **L - Leitura:** Necessidade de gerenciar a ocupação de médicos e a agenda de atendimentos, evitando duplicidades de horário para o mesmo paciente.
* **M - Marcação:** Descartada a modelagem sem tabela intermediária, pois um paciente pode realizar múltiplos atendimentos e um médico atende diversos pacientes.
* **A - Avaliação:** O script atende a todas as exigências do desafio com código executável em T-SQL e consultas estruturadas.

---

## 2. Resumo da Solução

1. **Entidades:** `PACIENTE` e `MEDICO` | **Relacionamento N:N:** `ATENDIMENTO`
2. **Indicador:** Taxa de Ocupação da Agenda do Médico ($\%$ de capacidade diária preenchida).
3. **Prevenção de Erro (IHC):** Filtrar médicos disponíveis no dia sem sobrepor agendas ativas.
4. **Teste de Duplicidade:** Impedir que o mesmo paciente agende o mesmo médico no mesmo dia e horário.

---

## 3. Script SQL Server (T-SQL)

```sql
-- Criando o banco de dados hospitalar
CREATE DATABASE PAINEL_HOSPITALAR;
GO
USE PAINEL_HOSPITALAR;
GO

-- 1. Criando as Tabelas Principais (Entidades)
CREATE TABLE ESPECIALIDADE (
    co_especialidade INT NOT NULL,
    nome VARCHAR(100) NOT NULL,
    CONSTRAINT PK_ESPECIALIDADE PRIMARY KEY (co_especialidade)
);

CREATE TABLE MEDICO (
    co_medico INT NOT NULL,
    crm VARCHAR(20) NOT NULL,
    nome VARCHAR(100) NOT NULL,
    co_especialidade INT NOT NULL,
    nu_capacidade_dia INT NOT NULL, -- DENOMINADOR do indicador (limite de consultas/dia)
    
    CONSTRAINT PK_MEDICO PRIMARY KEY (co_medico),
    CONSTRAINT FK_MEDICO_ESPECIALIDADE FOREIGN KEY (co_especialidade) REFERENCES ESPECIALIDADE (co_especialidade),
    CONSTRAINT CK_MEDICO_CAPACIDADE CHECK (nu_capacidade_dia > 0) -- Impede denominador zero
);

CREATE TABLE PACIENTE (
    co_paciente INT NOT NULL,
    cpf CHAR(11) NOT NULL,
    nome VARCHAR(100) NOT NULL,
    dt_nascimento DATE NOT NULL,
    sg_sexo CHAR(1) NULL,
    
    CONSTRAINT PK_PACIENTE PRIMARY KEY (co_paciente),
    CONSTRAINT UK_PACIENTE_CPF UNIQUE (cpf)
);

-- 2. Tabela Intermediária (Relacionamento N:N)
CREATE TABLE ATENDIMENTO (
    co_paciente INT NOT NULL,
    co_medico INT NOT NULL,
    dt_atendimento DATE NOT NULL,
    st_atendimento CHAR(1) NOT NULL, -- A = Agendado, R = Realizado, C = Cancelado
    hr_atendimento TIME NOT NULL,

    -- Regra de duplicidade: impede que o mesmo paciente agende dois atendimentos 
    -- com o mesmo médico na mesma data e horário.
    CONSTRAINT PK_ATENDIMENTO PRIMARY KEY (co_paciente, co_medico, dt_atendimento, hr_atendimento),
    CONSTRAINT FK_ATENDIMENTO_PACIENTE FOREIGN KEY (co_paciente) REFERENCES PACIENTE (co_paciente),
    CONSTRAINT FK_ATENDIMENTO_MEDICO FOREIGN KEY (co_medico) REFERENCES MEDICO (co_medico),
    CONSTRAINT CK_ATENDIMENTO_STATUS CHECK (st_atendimento IN ('A', 'R', 'C'))
);

-- ----------------------------------------------------
-- Carga de Dados de Exemplo
-- ----------------------------------------------------

INSERT INTO ESPECIALIDADE (co_especialidade, nome) VALUES
(1, 'Cardiologia'),
(2, 'Pediatria');

INSERT INTO MEDICO (co_medico, crm, nome, co_especialidade, nu_capacidade_dia) VALUES
(101, 'CRM-DF 12345', 'Dr. Roberto Silva', 1, 4), -- Capacidade máxima de 4 atendimentos/dia
(102, 'CRM-DF 67890', 'Dra. Mariana Costa', 2, 3); -- Capacidade máxima de 3 atendimentos/dia

INSERT INTO PACIENTE (co_paciente, cpf, nome, dt_nascimento, sg_sexo) VALUES
(1, '11122233344', 'Lucas Mendes', '1990-04-12', 'M'),
(2, '22233344455', 'Beatriz Rocha', '1985-08-25', 'F'),
(3, '33344455566', 'Gabriel Oliveira', '2012-01-10', 'M'),
(4, '44455566677', 'Fernanda Lima', '1998-11-05', 'F');

INSERT INTO ATENDIMENTO (co_paciente, co_medico, dt_atendimento, hr_atendimento, st_atendimento) VALUES
(1, 101, '2026-11-12', '08:00', 'A'),
(2, 101, '2026-11-12', '09:00', 'A'),
(3, 101, '2026-11-12', '10:00', 'A'),
(4, 101, '2026-11-12', '11:00', 'C'), -- Cancelado
(3, 102, '2026-11-12', '08:30', 'A');

-- ----------------------------------------------------
-- 3) INDICADOR: Taxa de Ocupação da Agenda do Médico (%)
--    Numerador   = Atendimentos AGENDADOS ou REALIZADOS no dia
--    Denominador = Capacidade diária do médico (nu_capacidade_dia)
-- ----------------------------------------------------

SELECT 
    m.co_medico,
    m.nome AS medico,
    e.nome AS especialidade,
    COUNT(a.co_paciente) AS agendados_ativos,
    m.nu_capacidade_dia AS capacidade_maxima,
    CAST(100.0 * COUNT(a.co_paciente) / NULLIF(m.nu_capacidade_dia, 0) 
        AS DECIMAL(5, 1)) AS taxa_ocupacao_pct
FROM MEDICO m
INNER JOIN ESPECIALIDADE e 
        ON e.co_especialidade = m.co_especialidade
LEFT JOIN ATENDIMENTO a 
       ON a.co_medico = m.co_medico
      AND a.dt_atendimento = '2026-11-12'
      AND a.st_atendimento IN ('A', 'R') -- Ignora cancelados
GROUP BY m.co_medico, m.nome, e.nome, m.nu_capacidade_dia
ORDER BY taxa_ocupacao_pct DESC;

-- ----------------------------------------------------
-- 4) PREVENÇÃO DE ERRO (Apoio à Interface - IHC)
--    Exibe apenas médicos com vaga na agenda para a data informada
--    e onde o paciente selecionado (ex: paciente 1) ainda NÃO agendou.
-- ----------------------------------------------------

SELECT 
    m.co_medico,
    m.nome AS medico,
    m.nu_capacidade_dia - COUNT(a.co_paciente) AS vagas_restantes
FROM MEDICO m
LEFT JOIN ATENDIMENTO a 
       ON a.co_medico = m.co_medico
      AND a.dt_atendimento = '2026-11-12'
      AND a.st_atendimento IN ('A', 'R')
WHERE NOT EXISTS (
    SELECT 1 
    FROM ATENDIMENTO x
    WHERE x.co_paciente = 1 -- Código do paciente selecionado
      AND x.co_medico = m.co_medico
      AND x.dt_atendimento = '2026-11-12'
      AND x.st_atendimento IN ('A', 'R')
)
GROUP BY m.co_medico, m.nome, m.nu_capacidade_dia
HAVING COUNT(a.co_paciente) < m.nu_capacidade_dia;

-- ----------------------------------------------------
-- 5) TESTE DA REGRA DE DUPLICIDADE
-- ----------------------------------------------------

-- CT02: Mesmo paciente com OUTRO médico -> Esperado: ACEITO
INSERT INTO ATENDIMENTO (co_paciente, co_medico, dt_atendimento, hr_atendimento, st_atendimento)
VALUES (1, 102, '2026-11-12', '14:00', 'A');

-- CT03: Reagendamento após cancelamento -> Esperado: ACEITO
UPDATE ATENDIMENTO
SET st_atendimento = 'A',
    co_paciente = 4
WHERE co_medico = 101 
  AND dt_atendimento = '2026-11-12' 
  AND hr_atendimento = '11:00';

-- CT01: Paciente 1 tentando agendar novamente no mesmo horário com mesmo médico
-- Esperado: ERRO de violação da chave primária composta (Comportamento esperado)
INSERT INTO ATENDIMENTO (co_paciente, co_medico, dt_atendimento, hr_atendimento, st_atendimento)
VALUES (1, 101, '2026-11-12', '08:00', 'A');

-- CT01 (Verificação): Esperado total = 1 registro
SELECT COUNT(*) AS total_agendamentos
FROM ATENDIMENTO
WHERE co_paciente = 1 
  AND co_medico = 101 
  AND dt_atendimento = '2026-11-12' 
  AND hr_atendimento = '08:00';
```
