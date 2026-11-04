**Profa. Kadidja Valéria | UDF**  
Ciência de Dados e Aprendizado de Máquina · Sistemas de Informação · 2026.2

# Aula 1 — Conceitos e classificação de problemas

## Identificação

- Estudante ou equipe: RAFAEL BATISTA MOTA
- Turma: Sistemas de Informação — 8º Semestre
- Data de realização: 04/11/2026
- Integrantes e contribuições: RAFAEL BATISTA MOTA (Resolução individual do exercício)

## Objetivos

Distinguir programação tradicional e Machine Learning, identificar atributos e alvo e diferenciar classificação, regressão e agrupamento.

## 1. Explicação com suas palavras

1. **Como um modelo aprende com dados?**  
   O processo de aprendizado ocorre pela identificação de padrões matemáticos nos dados históricos fornecidos. O algoritmo analisa os atributos de entrada e compara suas previsões com as respostas reais (quando existentes), realizando ajustes sucessivos em seus parâmetros internos para minimizar a taxa de erro. Após essa fase de ajuste, o modelo consolida essas regras aprendidas e passa a aplicá-las em novos dados. A diferença central em relação à programação tradicional é que, em vez de o desenvolvedor programar manualmente cada regra lógica, o próprio sistema infere o conjunto de regras a partir dos dados observados.

2. **Qual diferença entre algoritmo e modelo?**  
   O algoritmo representa o procedimento matemático ou o método computacional responsável pelo aprendizado (como o K-Means ou a Árvore de Decisão). O modelo, por sua vez, é o resultado concreto gerado após a execução desse algoritmo sobre um conjunto de dados específico. Ele armazena os parâmetros e pesos ajustados, atuando como a estrutura que efetivamente recebe novas entradas e realiza as previsões. Assim, o mesmo algoritmo treinado em bases de dados distintas produzirá modelos inteiramente diferentes.

3. **Compare uma regra de bloqueio de palavra com um modelo de spam.**  
   A regra baseada em palavras pertence à programação tradicional: um desenvolvedor define uma condição rígida, como "bloquear caso contenha o termo 'grátis'". Essa abordagem é simples e direta, porém inflexível, sujeita a falsos positivos e facilmente burlada por variações do tipo "gr4tis". Em contrapartida, o modelo preditivo de spam aprende analisando simultaneamente múltiplos fatores (remetente, presença de links, horário e vocabulário) extraídos de mensagens previamente rotuladas. Ele atribui probabilidades e consegue generalizar melhor perante novas fraudes, embora dependa de dados históricos de qualidade e seja menos transparente que uma regra condicional simples.

4. **Dê um exemplo de atributo e alvo e defina o momento da previsão.**  
   Em um contexto de análise de risco de crédito imobiliário, os atributos podem incluir a renda mensal declarada, a idade do solicitante, a pontuação no serasa/spc e o comprometimento de renda. O alvo é a ocorrência de inadimplência superior a 90 dias nos primeiros 12 meses (`Sim` ou `Não`). O momento ideal da previsão é a etapa de análise da proposta, antecedendo a assinatura do contrato e a liberação do recurso. Por essa razão, apenas variáveis disponíveis até esse instante podem ser consultadas; utilizar o histórico de pagamentos de parcelas futuras configuraria vazamento de dados (*data leakage*).

## 2. Quadro comparativo

| Critério | Supervisionado | Não supervisionado |
| --- | --- | --- |
| Presença de alvo no treino | Sim. Cada exemplo de treino traz a resposta conhecida (rótulo). | Não. Os dados têm apenas atributos, sem resposta associada. |
| Pergunta que pode responder | "Qual é a classe ou o valor deste novo caso?" Ex.: este cliente vai pagar? Quanto vamos vender? | "Que padrões ou grupos existem nos dados? O que foge do normal?" |
| Tipo de saída | Uma categoria (classificação) ou um número (regressão). | Grupos, estruturas, pontuação de anomalia ou representação reduzida dos dados. |
| Tarefas e exemplo | Classificação (spam/legítima) e regressão (tempo de espera em minutos). | Agrupamento (perfis de compra), detecção de anomalias e redução de dimensionalidade. |
| Dados necessários | Histórico com atributos e alvo rotulado, em quantidade e qualidade suficientes. | Atributos relevantes e comparáveis entre si (geralmente normalizados), sem necessidade de rótulo. |
| Forma de avaliação | Comparação das previsões com as respostas reais em dados de teste separados: acurácia, precisão, recall e F1 (classificação); MAE, RMSE e R² (regressão). | Sem gabarito: métricas internas, como silhueta e inércia, mais interpretação e validação por especialistas do negócio. |
| Limitação | Rotular é caro e demorado; rótulos errados ou enviesados são aprendidos; o modelo tem dificuldade com situações ausentes do histórico. | Resultado difícil de validar; os grupos podem não ter significado prático; depende de escolhas do analista (número de grupos, variáveis, escala). |

## 3. Situações-problema

Os casos são cenários didáticos. Escolha **pelo menos cinco** e justifique sua classificação pelo significado do alvo ou por sua ausência.

| Caso | Situação-problema |
| --- | --- |
| 1 Educação | Prever evadiu/permaneceu com histórico rotulado de turmas anteriores. |
| 2 Saúde | Estimar o tempo de espera em minutos a partir de registros de atendimento. |
| 3 Comércio | Descobrir perfis de compra sem categorias prévias de clientes. |
| 4 Finanças | Prever inadimplente/adimplente com contratos e desfechos conhecidos. |
| 5 Segurança digital | Distinguir spam/legítima com mensagens já revisadas. |
| 6 Comércio | Estimar o total de vendas em reais na próxima semana. |
| 7 Educação | Agrupar perfis de acesso ao ambiente virtual sem rótulo de evasão. |
| 8 Saúde | Classificar exames em categorias previamente definidas por especialistas. |

| Caso escolhido | Alvo ou ausência de alvo | Categoria, quantidade ou grupos? | Abordagem e justificativa | Dados necessários e limitação |
| --- | --- | --- | --- | --- |
| 1 Educação | Alvo: situação final do aluno (`evadiu` / `permaneceu`) registrada em turmas passadas. | Categoria | Supervisionado (classificação). O histórico rotulado permite que o algoritmo aprenda quais atributos apontam para o abandono antes do término do período letivo. | Frequência às aulas, notas das avaliações iniciais e acessos ao ambiente de aprendizagem. Limitação: fatores externos não mapeados (como crises financeiras pessoais) não são previstos pelo histórico. |
| 6 Comércio | Alvo: volume total de vendas semanais mensurado em moeda (`R$`). | Quantidade | Supervisionado (regressão). Trata-se da estimativa de uma variável contínua contada numericamente a partir de históricos de vendas passadas. | Registros diários de receita, histórico de promoções, dias úteis e datas comemorativas. Limitação: flutuações repentinas no mercado ou interrupções de estoque distorcem as projeções. |
| 8 Saúde | Alvo: diagnóstico final do exame laudado por junta médica especialista. | Categoria | Supervisionado (classificação multiclasse). Cada amostra contém rótulos clínicos prévios determinando o enquadramento do laudo. | Parâmetros laboratoriais, dados demográficos do paciente e imagens clínicas. Limitação: a acurácia do modelo fica limitada à precisão e padronização dos laudos históricos. |
| 3 Comércio | Ausência de alvo: não há divisão ou categorização prévia sobre a carteira de clientes. | Grupos | Não supervisionado (agrupamento/clustering). Busca-se formar grupos de clientes por proximidade de hábitos sem a existência de rótulo orientador. | Histórico de transações, ticket médio de compras, recência e categorias de produtos preferidas. Limitação: a validação e definição do número de grupos exigem análise interpretativa do especialista. |
| 4 Finanças | Alvo: status de pagamento final do contrato (`adimplente` / `inadimplente`). | Categoria | Supervisionado (classificação). O resultado encerrado dos contratos atua como variável alvo para classificar novos pedidos de empréstimo. | Renda mensal, histórico de pagamentos prévios, tempo de emprego e valor solicitado. Limitação: viés de amostragem (dados cobrem apenas quem obteve aprovação no passado) e restrições da LGPD. |

## 4. Raciocínio crítico

“Detectar fraude” define sozinho o tipo de aprendizado? Compare o uso de exemplos rotulados e a busca de operações atípicas sem rótulos.

Não. O objetivo de "detectar fraudes" estabelece uma meta de negócio, mas não determina diretamente a abordagem computacional a ser aplicada. A escolha do tipo de aprendizado é condicionada pela disponibilidade e pela qualidade dos dados existentes, principalmente no que tange à presença ou ausência de um alvo rotulado.

Caso a instituição disponha de um histórico de operações auditadas e devidamente classificadas como fraudes ou transações legítimas, a abordagem é **supervisionada de classificação**. Nessa estratégia, o modelo mapeia as características dos golpes já conhecidos e prevê a probabilidade de uma nova operação ser fraudulenta. A vantagem reside no cálculo objetivo de métricas de precisão e recall. Como limitações, destaca-se o alto desbalanceamento das classes (fraudes costumam ser minoria) e a dificuldade em identificar golpes com mecânicas totalmente novas.

Se não houver base rotulada ou a intenção for rastrear comportamentos desconhecidos, a abordagem passa a ser **não supervisionada (detecção de anomalias)**. O algoritmo aprende os padrões de comportamento padrão dos clientes (como horários, faixas de valores e locais usuais) e emite alertas quando ocorrem transações discrepantes desse perfil. A grande vantagem é capturar ameaças inéditas sem necessidade de treinamento rotulado prévio. Contudo, a principal desvantagem é a geração de falsos positivos, visto que desvios de padrão (como compras em viagens) nem sempre representam ilícitos.

Em ecossistemas de produção reais, as duas técnicas atuam de maneira complementar: o aprendizado não supervisionado detecta comportamentos suspeitos em tempo real e gera alertas para auditoria humana, cujos pareceres alimentam uma base rotulada que, por sua vez, retreina os classificadores supervisionados.

## Entrega

Salve este arquivo preenchido. Critérios: distinção conceitual, pertinência dos dados, justificativa e clareza. [Voltar ao início](README.md).
