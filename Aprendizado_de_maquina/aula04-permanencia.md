<img src="assets/logo-udf.jpg" alt="UDF Centro Universitário" width="230">

**Profa. Kadidja Valéria | UDF**  
Ciência de Dados e Aprendizado de Máquina · Sistemas de Informação · 2026.2

# PBL integrador — Apoio à Permanência e Retenção de Alunos

## Identificação

- Estudante ou equipe: RAFAEL BATISTA MOTA
- Turma: **Sistemas de Informação**
- Data de realização: **04/11/2026**
- Integrantes e contribuições: RAFAEL BATISTA MOTA (Resolução e elaboração da proposta de retenção preventiva)

## Contexto

A rede de academias FitLife Fitness pretende compreender os sinais preditivos associados ao cancelamento de planos (churn) nos primeiros 90 dias de contrato e oferecer suporte personalizado antes que o aluno abandone o treino. Público-alvo: alunos matriculados, equipe de personal trainers e recepcionistas. O cenário é didático e a prática utiliza dados sintéticos.

**Questão norteadora:** como identificar comportamentos de risco de evasão e oferecer suporte individualizado, reconhecendo as margens de erro do modelo e os fatores externos que os dados de catraca não capturam?

## Proposta da equipe

### 1. Delimitação

- Problema e público: **Uma parcela dos alunos inscritos deixa de frequentar a academia nos primeiros 90 dias, e a equipe de recepção/treino só toma conhecimento após a formalização do cancelamento. O público-alvo é composto pelos alunos recém-matriculados (potenciais beneficiários de orientação) e pela equipe de instrutores (que possui capacidade de atendimento limitada e necessita de priorização).**
- Decisão que o resultado pode apoiar: **Ao final dos primeiros 30 dias de matrícula, priorizar quais alunos receberão um convite discreto e voluntário para uma sessão de reavaliação física e ajuste de ficha de treino. O resultado não altera valores de mensalidade, não aplica multas e não cancela contratos automaticamente; apenas organiza a oferta de suporte presencial.**
- Definição de evasão, unidade e horizonte: **Evasão (Churn): o aluno matriculado que cancela ou não renova o plano ao término do período inicial de 90 dias. Reduzir a frequência de treinos por motivos de férias não constitui churn se o contrato permanecer ativo. Unidade de análise: um aluno por contrato. Horizonte: previsão realizada ao 30º dia para antecipar o desfecho ao 90º dia.**

### 2. Perguntas de negócio

1. **Quais indicadores operacionais registrados até o 30º dia de matrícula se associam ao cancelamento do plano, e qual o ganho preditivo de uma Árvore de Decisão em relação a um classificador de referência?**
2. **Qual a proporção de cancelamentos que o modelo deixa de identificar (falsos negativos), e como a equipe pode acolher esses alunos sem depender exclusivamente do sistema preditivo?**

### 3. Dados necessários

| Dado | Papel no projeto | Disponível quando? | Origem pretendida | Necessidade e risco |
| --- | --- | --- | --- | --- |
| Frequência semanal (acessos) | Atributo | Fim do 30º dia | Sistema de catracas eletrónicas | Necessário. Risco: falhas no leitor da catraca ou registro manual incorreto na recepção. |
| Duração média das sessões (minutos) | Atributo | Fim do 30º dia (pode faltar) | Aplicativo móvel de treino | Necessário. Risco: falta de sincronização do aplicativo por parte do aluno. |
| Maior hiato sem treino (dias consecutivos) | Atributo | Fim do 30º dia | Sistema de frequência | Necessário. Risco: alunos que treinam em viagens ou ao ar livre sem registrar presença. |
| Situação da matrícula no 90º dia (`ativo`/`cancelou`) | Alvo | Fim do 90º dia | Sistema financeiro de contratos | Indispensável para treinamento e validação. Risco: inconsistência na data de cancelamento efetivo. |
| Identificador pseudonimizado | Controle de duplicatas | No ato da matrícula | Sistema de gestão de alunos | Necessário para separar treino e teste sem vazar dados do indivíduo. Risco: reidentificação; manter isolado e com acesso restrito. |
| Tipo de plano (`Básico` / `Black`) | Controle operacional | No ato da matrícula | Contrato comercial | Necessário para identificar se a evasão difere pelo tipo de plano contratado. |
| Capacidade de atendimento dos instrutores | Restrição de decisão | Início de cada mês | Gestão de escala de pessoal | Determina a quantidade limite de convites que a equipe consegue atender. Sem risco pessoal. |
| Motivos de saúde, lesões prévias, renda, raça, gênero | Não coletar para o modelo | — | — | Sensíveis sob a LGPD e desnecessários para a oferta de suporte técnico aos treinos. |

**Diferença entre a simulação e o cenário real:** A simulação utiliza 600 registros fictícios baseados em três variáveis operacionais (`frequencia_semanal`, `duracao_media_treino` e `dias_sem_treino`) com atribuição probabilística simulada. Uma implementação real exigiria validação temporal entre semestres letivos passados, dados históricos de instabilidades operacionais e governança rigorosa sobre o tratamento de dados sob a LGPD.

### 4. Abordagem e algoritmo

- Formulation: **Classificação binária supervisionada. O alvo é discreto e binário (`0 = manteve`, `1 = cancelou`). A codificação numérica não transforma a tarefa em regressão. O agrupamento (clustering) serviria apenas para identificar perfis de uso, mas não prediz o risco direto de cancelamento.**
- Algoritmo escolhido: **Árvore de Decisão (`DecisionTreeClassifier`) integrada em um `Pipeline` com imputação de dados pela mediana via `SimpleImputer`. Oferece interpretabilidade direta para os instrutores na ponta e não exige padronização de escala de atributos.**
- Referência simples: **Classificador por classe majoritária (`DummyClassifier(strategy='most_frequent')`), que prevê continuamente "manteve o plano". Serve como baseline mínimo de comparação.**

### 5. Avaliação

- Divisão e validação: **Validação estratificada com 75% dos dados para treino (450) e 25% para teste (150), fixando a semente 42. A profundidade da árvore foi selecionada via validação cruzada estratificada em 5 dobras nos dados de treino.**
- Métricas escolhidas: **Acurácia (comparação com o baseline), Matriz de Confusão e Sensibilidade/Recall da classe "cancelou" (TP/(TP+FN)), priorizando a minimização de omissões (falsos negativos).**
- Resultados calculados: **Profundidade otimizada: 5 (validação de 0,7311 ± 0,0350). Acurácia de teste: 0,7867 (contra 0,6000 da referência). Matriz de teste: TN = 77, FP = 13, FN = 19, TP = 41. Sensibilidade (Recall): 0,6833. Precisão: 0,7593. Evidências em [notebooks/laboratorio-equipe.ipynb](notebooks/laboratorio-equipe.ipynb) e [assets/lab-matriz-confusao.png](assets/lab-matriz-confusao.png).**
- Impacto dos erros: **19 dos 60 alunos propensos a cancelar (31,6%) não foram identificados pelo modelo (FN). Este representa o erro de maior custo operacional. Por outro lado, 13 alunos satisfeitos (FP) receberiam um convite desnecessário, o que gera um impacto operacional insignificante, visto que o suporte é voluntário.**

### 6. Limites e proteção

- Ausência de causalidade: **O modelo identifica correlações estatísticas entre padrão de frequência e cancelamento, e não causas determinísticas. Redução na frequência pode ser decorrente de mudanças na rotina de trabalho ou fatores de saúde. Aumentar artificialmente a frequência de um aluno não remove a causa raiz da insatisfação.**
- Limitações de dados sintéticos: **Os dados sintéticos refletem regras pré-programadas pela equipe de geração e não reproduzem a complexidade de comportamento da carteira real de clientes da FitLife Fitness.**
- Equidade e grupos mal representados: **Alunos que realizam treinos externos, frequentadores de horários periféricos (madrugada) ou pessoas com baixa adesão ao aplicativo de celular podem apresentar registos incompletos. Para mitigar o viés, o modelo deve passar por auditorias periódicas por categoria de plano e unidade.**
- Privacidade (LGPD) e retenção: **Os dados são pseudonimizados. O acesso aos indicadores é restrito à equipe técnica de atendimento. Os escores de risco são descartados ao término de cada trimestre, retendo-se apenas dados agregados para atualização dos modelos.**
- Revisão humana e contestação: **Nenhum cancelamento ou alteração contratual ocorre de forma automatizada. Cada alerta emitido pelo modelo é analisado por um instrutor antes da abordagem. O aluno pode solicitar o descredenciamento de mensagens preventivas a qualquer momento.**

### 7. Recomendações de apoio

- Ação voluntária proposta: **No 35º dia de contrato, alunos sinalizados pelo sistema recebem uma mensagem cortês oferecendo uma consultoria gratuita de 15 minutos com um personal trainer para adequação de treino, sem custos adicionais.**
- Acolhimento amplo aos não sinalizados: **Considerando a taxa de 31,6% de falsos negativos, o canal de solicitação de revisão de ficha de treino deve permanecer aberto a todos os alunos via aplicativo e totem presencial, garantindo atendimento independente da sinalização do modelo.**
- Pré-requisitos para produção: **(1) Validação da definição operacional de churn com o setor financeiro; (2) Teste de validação temporal em dados históricos reais de trimestres anteriores; (3) Avaliação de conformidade com os termos da LGPD e aprovação pela diretoria da FitLife Fitness.**

## Apresentação de cinco minutos

| Tempo | Conteúdo | Responsável |
| --- | --- | --- |
| 1 minuto | Problema e dados | RAFAEL BATISTA MOTA |
| 2 minutos | Método e resultados | RAFAEL BATISTA MOTA |
| 1 minuto | Limitações do modelo | RAFAEL BATISTA MOTA |
| 1 minuto | Plano de retenção e suporte | RAFAEL BATISTA MOTA |

### Roteiro da apresentação

**Problema e dados (1 min).** Uma parcela considerável dos alunos cancela a matrícula nos primeiros 90 dias de treino. O objetivo é utilizar dados do primeiro mês (frequência, duração de treinos e hiatos) para antecipar o risco de evasão e oferecer suporte antes que o aluno abandone a atividade física.

**Método e resultados (2 min).** Trata-se de uma tarefa de classificação binária. O modelo de Árvore de Decisão ajustado com profundidade 5 alcançou 78,67% de acurácia no lote de teste, superando o baseline de 60%. O modelo identificou 41 dos 60 alunos em risco efetivo de cancelamento na amostra de teste.

**Limitações (1 min).** O modelo identifica associações e não relações de causa e efeito. Dados de frequência não capturam motivações de ordem pessoal ou financeira. Cerca de 31,6% dos alunos em risco não foram sinalizados pelo sistema.

**Recomendações (1 min).** Utilizar a saída do algoritmo estritamente para ordenar o agendamento de suporte técnico orientativo de treino. Manter canais abertos a todos os frequentadores para atendimento espontâneo e assegurar o cumprimento das normas de privacidade sob a LGPD.

## Contribuições

| Integrante | Contribuição verificável |
| --- | --- |
| RAFAEL BATISTA MOTA | Elaboração completa do documento de proposta (`04-pbl-permanencia.md`), condução e documentação do notebook preditivo (`notebooks/laboratorio-equipe.ipynb`) e estruturação do roteiro de apresentação. |

**Dúvida que ainda exige investigação:** Avaliar se a sensibilidade do classificador mantém estabilidade em épocas de sazonalidade acentuada (ex.: início do ano versus período de férias escolares).

[Voltar ao início](README.md).
