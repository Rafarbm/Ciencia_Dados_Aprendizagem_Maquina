**Profa. Kadidja Valéria | UDF**  
Ciência de Dados e Aprendizado de Máquina · Sistemas de Informação · 2026.2

# PBL — FitLife Fitness em Foco

## Identificação

- Estudante ou equipe: RAFAEL BATISTA MOTA
- Turma: Sistemas de Informação — 8º Semestre
- Data de realização: 04/11/2026
- Integrantes e contribuições: RAFAEL BATISTA MOTA (Resolução e elaboração do Canvas didático)

## Situação-problema

A rede de academias FitLife Fitness enfrenta sobrecarga nos equipamentos de musculação em faixas horárias específicas (picos das 18h às 21h) e, ao mesmo tempo, regista uma taxa de evasão (churn) de 15% dos alunos nos primeiros 90 dias de matrícula. A coordenação operacional deseja otimizar o fluxo de treino e aumentar a retenção de alunos. Este é um cenário didático.

**Público-alvo:** alunos da academia, equipe de personal trainers/professores de recepção e gestão operacional.

**Questão norteadora:** como os dados de catraca, treinos e uso de modalidades podem orientar a escala de professores e ações de retenção sem expor dados pessoais ou discriminar os praticantes?

## Investigação em equipe

1. Delimitem o problema e a decisão a apoiar.
2. Registrem o que já sabem e o que precisam investigar.
3. Formulem duas perguntas de negócio.
4. Definam a unidade de análise, os atributos e o alvo, quando houver.
5. Justifiquem a abordagem e indiquem se uma análise descritiva já seria suficiente.
6. Proponham avaliação, cuidados com os dados e limitações.

## Canvas da equipe

| Campo | Registro |
| --- | --- |
| **Problema e decisão** | A academia enfrenta filas para uso de aparelhos de musculação no horário de pico noturno e ociosidade no período da tarde, além de um índice elevado de cancelamentos de planos nos 3 primeiros meses. As decisões a apoiar são: (1) quantos professores escalar por turno na área de musculação; (2) quais alunos em declínio de frequência devem receber uma oferta de acompanhamento personalizado antes de cancelarem a matrícula. |
| **Público-alvo** | Alunos (que sofrem com espera em aparelhos e falta de orientação); professores de musculação (escalados conforme a demanda real); gestão da unidade (que decide investimentos em equipamentos, escalas e promoções de retenção). |
| **O que sabemos** | A academia dispõe de catracas eletrónicas com registros de data/hora de entrada, aplicativo móvel com registo de check-in em treinos, histórico de modalidades praticadas (dança, pilates, musculação, crossfit) e plano contratado (Básico vs. Black/VIP). O calendário de férias e o início do ano letivo/verão influenciam os picos de adesão. |
| **O que precisamos investigar** | Qual a duração média exata do treino por faixa horária; em quais dias da semana o pico é mais severo; qual a taxa de queda de frequência antecede o cancelamento da matrícula; se a evasão ocorre por falta de orientação ou superlotação. |
| **Pergunta de negócio 1** | Quantos check-ins por faixa horária (de 1 hora) devemos esperar no setor de musculação nas próximas semanas para ajustar a escala de professores e evitar filas nos aparelhos? |
| **Pergunta de negócio 2** | É possível prever se um aluno irá cancelar o plano no mês seguinte com base no declínio da sua frequência e duração dos treinos nos últimos 30 dias? |
| **Unidade de análise e período** | Pergunta 1: faixa horária de 1 hora por dia (dia × hora) na recepção/catraca. Pergunta 2: histórico mensal do aluno (aluno × mês). Período de análise: últimos 12 meses para capturar variações sazonais. |
| **Atributos, unidades e origem pretendida** | Data, dia da semana e faixa horária (do sistema de catracas); tipo de plano (`Básico` ou `Black`); histórico de check-ins por semana (contagem do app); duração média das sessões em minutos (do app de treino); modalidade principal praticada (do sistema de turmas); idade e tempo de matrícula em meses (do cadastro). |
| **Alvo e momento em que será conhecido, ou ausência de alvo** | Pergunta 1: volume de alunos na hora (alvo numérico contínuo), conhecido ao fim da faixa horária. A previsão é feita 1 semana antes para montar a escala. Pergunta 2: situação do plano no mês seguinte (`0` = Ativo, `1` = Cancelou/Churn), conhecida ao término do mês financeiro. |
| **Abordagem e justificativa** | Inicialmente, análise descritiva com mapas de calor por dia/horário para entender os picos reais. Para a Pergunta 1, usa-se **Regressão Supervisionada**, pois o alvo é a quantidade contínua de alunos por hora. Para a Pergunta 2, aplica-se **Classificação Supervisionada** (Random Forest/Regressão Logística) para identificar antecipadamente o rótulo de risco de evasão. |
| **Alternativa sem ML** | Cálculo da média simples de alunos por horário no mês anterior para definir a escala; envio automático de e-mail de "sentimos sua falta" para quem não passa na catraca há 15 dias corridos; pesquisa física de satisfação. |
| **Como avaliar a proposta** | Regressão: Erro Médio Absoluto (MAE) no número de alunos por hora comparado com a média simples. Classificação: Métrica de **Recall** (alvo > 0.80) para garantir que o máximo de alunos prestes a cancelar sejam identificados a tempo. Negócio: redução no tempo de espera por aparelho e queda de 10% na taxa geral de cancelamento. |
| **Privacidade e limitações** | **Privacidade (LGPD):** Dados individualizados devem ser pseudonimizados. Nenhum dado biométrico, de saúde clínica ou histórico de dados sensíveis pode ser exposto. Não utilizar variáveis como gênero ou idade para restringir acesso a modalidades. **Limitações:** A catraca mede a entrada, mas não o tempo exato em cada aparelho de musculação; alunos que treinam em dupla podem alterar o tempo de permanência sem registro no sistema. |

## Registro de colaboração

| Integrante | Papel | Contribuição |
| --- | --- | --- |
| RAFAEL BATISTA MOTA | Responsável único (trabalho individual) | Definição do problema da academia, formulação das perguntas de negócio, mapeamento dos atributos e alvos, estruturação do Canvas e análise dos impactos de privacidade. |

## Conclusão da equipe

**Proposta:** Iniciar pela higienização da base e análise descritiva com mapas de calor de frequência. Utilizar modelos de regressão para estimar a lotação dos horários e redimensionar a escala de instrutores. Em paralelo, utilizar classificação supervisionada (Random Forest) para mapear alunos com risco iminente de evasão e oferecer suporte antes do término do contrato.

**Dúvida ainda aberta:** Como medir com precisão a desistência invisível (alunos que chegam na porta da academia, veem a lotação e vão embora sem passar a catraca)? Isso demanda a inclusão de pesquisas curtas no aplicativo da academia.

**Feedback recebido e melhoria realizada:** Validação do indicador de Recall como métrica primária do modelo de retenção, garantindo prioridade à prevenção de perdas de clientes.

## Síntese para apresentação (2 minutos)

A rede FitLife Fitness enfrenta dois grandes desafios: superlotação na musculação nos horários de pico e evasão de 15% dos alunos novos nos primeiros três meses.

Formulamos duas perguntas de negócio. A primeira busca prever a quantidade de alunos por faixa horária para ajustar a escala de personal trainers na área de musculação. A segunda busca antecipar quais alunos correm risco de cancelar o plano no mês seguinte.

A base de dados conta com entradas pela catraca, histórico de treinos pelo app, tipo de plano e tempo de matrícula. A unidade de análise varia entre faixas de 1 hora para a escala e o histórico mensal do aluno para o modelo de retenção.

A abordagem combina um mapa de calor descritivo, regressão para prever o fluxo de pessoas por hora e classificação com Random Forest para detectar o risco de churn. Avaliamos a solução com métricas de Recall (alvo acima de 80%) e redução do MAE nas previsões de lotação.

Em relação à LGPD e ética: os dados individuais são pseudonimizados, não utilizados para restringir o uso de modalidades e restritos à melhoria operacional. Uma limitação é a impossibilidade de medir pelo sistema os alunos que desistem de treinar ao verem a fila na recepção.
