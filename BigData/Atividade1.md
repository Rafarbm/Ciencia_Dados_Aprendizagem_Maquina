19/08

# Atividade Prática — Detetives dos Dados

## Ciência de Dados e Aprendizagem de Máquina — Aula 01

**Tema:** Introdução à Ciência de Dados e Big Data
**Metodologia:** Trabalho em equipe
**Tempo:** 20 minutos
**Entregável:** Mapa do Problema de Ciência de Dados

---

## 1. Identificação da equipe

| Campo             | Resposta |
| ----------------- | -------- |
| **Turma:**        | SI 7/8 Noturno |
| **Data:**         | 19/08/2026 |
| **Equipe:**       |  |
| **Integrante 1:** | Rafael Batista Mota |
| **Integrante 2:** | Thiago Regis Vieira Rocha |
| **Integrante 3:** | Gabriel Landim Donadel de Farias |
| **Integrante 4:** | Eduardo Santos Morais |
| **Integrante 5:** | -- |
| **Integrante 6:** | -- |

---

## 2. Objetivo da atividade

Nesta atividade, sua equipe deverá analisar um **problema real** e pensar como uma equipe de Ciência de Dados poderia utilizar dados para compreender a situação e apoiar uma decisão.

O objetivo não é desenvolver um sistema ou modelo de Machine Learning neste momento.

O objetivo é aprender a **pensar como um cientista de dados**:

> **Problema → Dados → Informação → Análise → Decisão → Benefício**

---

## 3. Escolha do problema

Área escolhida:

* [x] Comércio
* [ ] Banco
* [ ] Saúde
* [ ] Transporte
* [ ] Educação
* [ ] Entretenimento
* [ ] Indústria
* [ ] Meio ambiente
* [ ] Esportes
* [ ] Outra: __________________________

### Problema escolhido

**Descreva, em poucas linhas, o problema que sua equipe pretende analisar.**

> Uma loja de roupas de shopping está acumulando muita mercadoria no estoque que não vende, gerando prejuízo e ocupando espaço que poderia ser usado para produtos novos.
---

## 4. Quem possui esse problema?

**Quem possui ou enfrenta esse problema?**

> Os gestores e o setor de compras/estoque da loja de roupas.

### Quem é afetado pelo problema?

> A empresa (que perde dinheiro com capital parado) e os clientes (que encontram menos variedade de novidades na arara).

---

## 5. Por que esse problema é importante?

**Qual é o impacto do problema?**

> O impacto financeiro e operacional é severo. Manter mercadorias paradas gera custos de armazenagem, depreciação acelerada do produto (roupa sai de moda rápido), risco de perdas por avaria e, principalmente, custo de oportunidade, já que o dinheiro investido naqueles itens parados poderia estar alocado em coleções novas e de alta demanda. Investigar isso com dados permite estancar o sangramento financeiro e otimizar a saúde do caixa da empresa

---

## 6. Qual decisão precisa ser tomada?

**Qual decisão a organização precisa tomar?**

> A organização precisa decidir qual seria a media ideal de produtos (quantidades) deve ser encomendado para as próximas coleções, além de definir estratégias dinâmicas de preço para escoar o estoque atual parado de forma a recuperar o máximo de valor possível sem prejudicar a marca
---

# 7. Identificação dos dados

| Nº | Dado necessário | Por que esse dado é importante? |
| -: | --------------- | ------------------------------- |
| 1 | Frequência às aulas (presenças/faltas por disciplina) | Queda de frequência é um dos primeiros sinais de desengajamento e possível evasão. |
| 2 | Notas e histórico de reprovações | Baixo desempenho acadêmico está fortemente associado à desistência. |
| 3 | Situação financeira (mensalidades em atraso, bolsas, financiamento) | Dificuldade financeira é uma das principais causas de abandono em instituições privadas. |
| 4 | Dados socioeconômicos (idade, se trabalha, distância casa–faculdade, renda) | Ajudam a entender o contexto do aluno e a carga que ele enfrenta para permanecer no curso. |
| 5 | Interações no ambiente virtual (acessos ao AVA, entregas de atividades) | Mostram o engajamento fora da sala de aula, mesmo quando o aluno ainda frequenta as aulas. |
| 6 | Registros de trancamentos, transferências e evasões anteriores | Servem de base histórica para identificar padrões de quem desistiu no passado. |

---

# 8. Que informações queremos descobrir?

### Pergunta 1

> Quais categorias de vestuário e faixas de preço apresentam a maior taxa de encalhe após 90 dias da chegada a loja?

### Pergunta 2

> Existe algum desbalanceamento na grade de tamanhos (por exemplo, compramos muito o tamanho GG e falta o M)?

### Pergunta 3

> Existe relação entre queda de frequência/acesso ao AVA e a desistência semanas depois?

### Pergunta 4

> Quais perfis de alunos (trabalhador, bolsista, distante da faculdade etc.) têm maior risco de evadir?

---

# 9. Quais padrões podemos procurar?

* [x] Tendências
* [x] Comparações
* [x] Grupos semelhantes
* [x] Comportamentos recorrentes
* [x] Valores fora do padrão
* [x] Relações entre variáveis
* [x] Mudanças ao longo do tempo
* [ ] Outros: __________________________

### Explique um padrão que vocês gostariam de encontrar

> Gostaríamos de encontrar um padrão de "sinais de alerta": por exemplo, alunos que reduzem a frequência abaixo de 75%, deixam de acessar o AVA por mais de duas semanas e atrasam uma mensalidade tendem a evadir no semestre seguinte. Identificando essa combinação de comportamentos, a instituição poderia agir antes da desistência.

---

# 10. Qual análise poderia ser realizada?

* [x] Análise descritiva
* [x] Comparação entre grupos
* [x] Análise temporal
* [x] Visualização por gráficos
* [x] Identificação de padrões
* [x] Classificação
* [x] Previsão
* [x] Agrupamento
* [ ] Outra: __________________________

### Explique

> Primeiro, uma análise descritiva e temporal para entender o cenário (quantos evadem, quando e de quais cursos), com gráficos comparando grupos (trabalhadores × não trabalhadores, bolsistas × pagantes). Depois, um agrupamento para identificar perfis de alunos e, futuramente, um modelo de classificação/previsão que estime o risco de evasão de cada aluno a partir do histórico.

---

# 11. Qual decisão poderia ser tomada?

> Com base nos resultados, a instituição poderia criar um **programa de retenção direcionado**: gerar mensalmente uma lista de alunos em risco e acionar a ação certa para cada perfil — renegociação e bolsas para quem tem dificuldade financeira, monitoria e tutoria para quem tem baixo desempenho, e contato ativo da coordenação para quem apresenta queda de frequência e engajamento.

---

# 12. Qual seria o benefício?

> Para os alunos: maior chance de concluir a graduação e receber apoio no momento certo. Para a instituição: redução da taxa de evasão, aumento de receita e melhora nos indicadores de qualidade. Para a sociedade: mais profissionais formados. Além disso, os recursos de retenção passam a ser aplicados de forma mais eficiente, no público que realmente precisa.

---

# 13. Os 5 Vs do Big Data

| V              | Pergunta                                                   | Resposta da equipe |
| -------------- | ---------------------------------------------------------- | ------------------ |
| **Volume**     | Existe uma grande quantidade de dados?                     | Sim. São milhares de alunos, cada um com registros de frequência por aula, notas, acessos ao AVA e histórico financeiro acumulados por vários semestres. |
| **Velocidade** | Os dados são gerados ou processados rapidamente?           | Sim. Presenças e acessos ao AVA são gerados diariamente; o risco de evasão pode mudar de uma semana para outra. |
| **Variedade**  | Existem diferentes tipos ou formatos de dados?             | Sim. Dados estruturados (notas, faltas, pagamentos), logs de sistemas (AVA) e até textos (atendimentos, ouvidoria, respostas de questionários). |
| **Veracidade** | Os dados podem apresentar erros ou problemas de qualidade? | Sim. Chamadas lançadas com atraso ou erro, cadastros desatualizados, dados socioeconômicos autodeclarados e registros incompletos. |
| **Valor**      | Os dados podem gerar algum benefício ou apoiar decisões?   | Sim. Permitem prever o risco de evasão e direcionar ações de retenção, gerando valor para alunos e instituição. |

### Qual dos 5 Vs é mais relevante para o problema?

> Valor.

### Justifique

> De nada adianta ter muitos dados acadêmicos e financeiros se eles não forem transformados em decisões. O grande diferencial aqui é converter registros que a instituição já possui em ações concretas de retenção — ou seja, extrair valor dos dados. A veracidade também é crítica, pois um alerta baseado em dados errados pode direcionar recursos para o aluno errado.

---

# 14. Mapa do Problema de Ciência de Dados

```text
┌─────────────────────┐
│       PROBLEMA      │
│  Alta evasão de     │
│  alunos no noturno  │
└──────────┬──────────┘
           ↓
┌─────────────────────┐
│        DADOS        │
│ Frequência, notas,  │
│ financeiro, AVA,    │
│ perfil socioecon.   │
└──────────┬──────────┘
           ↓
┌─────────────────────┐
│     INFORMAÇÕES     │
│ Fatores e perfis    │
│ associados à        │
│ desistência         │
└──────────┬──────────┘
           ↓
┌─────────────────────┐
│       ANÁLISE       │
│ Descritiva, temporal│
│ agrupamento e       │
│ previsão de risco   │
└──────────┬──────────┘
           ↓
┌─────────────────────┐
│       DECISÃO       │
│ Programa de retenção│
│ direcionado por     │
│ perfil de risco     │
└──────────┬──────────┘
           ↓
┌─────────────────────┐
│      BENEFÍCIO      │
│ Menos evasão, mais  │
│ formados e recursos │
│ bem aplicados       │
└─────────────────────┘
```

### Resuma cada etapa

**Problema:**

> Alta evasão de alunos em cursos superiores noturnos, detectada tarde demais.

**Dados:**

> Frequência, notas, situação financeira, perfil socioeconômico, acessos ao AVA e histórico de evasões anteriores.

**Informação:**

> Quais fatores, momentos e perfis estão associados à desistência, e quais alunos apresentam sinais de risco.

**Análise:**

> Análise descritiva e temporal, comparação entre grupos, agrupamento de perfis e previsão do risco de evasão.

**Decisão:**

> Acionar ações de retenção personalizadas (financeira, pedagógica ou de acompanhamento) para os alunos em risco.

**Benefício:**

> Redução da evasão, mais alunos formados, melhoria de indicadores e uso eficiente dos recursos de retenção.

---

# 15. Preparação para apresentação

### 1. Nosso problema

> A evasão de alunos em cursos superiores noturnos, que costuma ser percebida só depois que o aluno já desistiu.

### 2. Precisamos destes dados

> Frequência, notas, situação financeira, dados socioeconômicos, acessos ao AVA e histórico de evasões.

### 3. Queremos descobrir

> Quais fatores e perfis estão associados à desistência e quais alunos apresentam sinais de risco antes de evadir.

### 4. Pretendemos analisar

> O cenário geral (descritiva e gráficos), a evolução no tempo, grupos de alunos semelhantes e, por fim, a previsão do risco individual.

### 5. A decisão poderia ser

> Criar um programa de retenção direcionado, com a ação certa (financeira, pedagógica ou de acompanhamento) para cada perfil de risco.

### 6. O benefício esperado é

> Menos evasão, mais alunos concluindo o curso, melhores indicadores para a instituição e recursos aplicados onde realmente fazem diferença.

---

# 16. Checklist da equipe

* [x] Definimos um problema real.
* [x] Identificamos quem é afetado pelo problema.
* [x] Explicamos por que o problema é importante.
* [x] Identificamos pelo menos 5 dados necessários.
* [x] Definimos perguntas que queremos responder.
* [x] Identificamos possíveis padrões.
* [x] Indicamos como os dados poderiam ser analisados.
* [x] Definimos uma possível decisão.
* [x] Identificamos o benefício esperado.
* [x] Analisamos os 5 Vs do Big Data.
* [x] Preenchemos o Mapa do Problema.
* [x] Estamos preparados para apresentar em 2 minutos.

---

# 17. Reflexão final

> **Ter muitos dados significa necessariamente tomar boas decisões? Por quê?**

**Resposta:**

> Não. Dados em grande quantidade só geram boas decisões quando têm qualidade (veracidade), quando são analisados com as perguntas certas e quando os resultados chegam a quem decide, no momento certo. Uma instituição pode ter todo o histórico dos alunos e mesmo assim continuar perdendo estudantes se ninguém transformar esses registros em informação e ação. Além disso, dados ruins ou mal interpretados podem levar a decisões piores do que a intuição — por exemplo, classificar como "em risco" alunos com base em registros de frequência lançados errados. Ou seja: o valor não está no volume de dados, mas na capacidade de convertê-los em decisões corretas.

---

## Entrega

### Produto final

**Mapa do Problema de Ciência de Dados**

```text
Problema: evasão de alunos no ensino superior noturno
   ↓
Dados necessários: frequência, notas, financeiro, AVA, perfil socioeconômico
   ↓
Informações desejadas: fatores, perfis e sinais de risco de evasão
   ↓
Análise: descritiva, temporal, agrupamento e previsão de risco
   ↓
Decisão: programa de retenção direcionado por perfil
   ↓
Benefício esperado: menos evasão, mais formados, recursos bem aplicados
```

**Formato:** Markdown.
**Apresentação:** 2 minutos por equipe.
