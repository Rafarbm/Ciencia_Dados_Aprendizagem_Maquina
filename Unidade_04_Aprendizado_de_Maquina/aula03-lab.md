**Profa. Kadidja Valéria | UDF**  
Ciência de Dados e Aprendizado de Máquina · Sistemas de Informação · 2026.2

# Aula 2 — Registro do laboratório supervisionado

## Identificação

- Estudante ou equipe: RAFAEL BATISTA MOTA
- Turma: **Sistemas de Informação**
- Data de realização: **04/11/2026**
- Integrantes e contribuições: RAFAEL BATISTA MOTA (Resolução e execução individual dos modelos preditivos)

## Percurso escolhido

- [x] Python/Colab ou Jupyter.
- [ ] Orange Data Mining.

O experimento utiliza o conjunto de dados sintéticos da academia FitLife Fitness (`dados/fitlife_transacoes_sinteticas.csv`), composto por 600 registos de alunos e histórico de uso. Atributos: `frequencia_semanal`, `duracao_media_treino`, `dias_sem_treino`. Alvo: `risco_churn` (0 manteve o plano, 1 cancelou nos primeiros 90 dias). As associações foram geradas por simulação computacional sem validade empírica sobre frequentadores reais.

## 1. Ambiente e reprodução

| Item | Registro |
| --- | --- |
| Ambiente e data | Jupyter Notebook com kernel Python 3, execução local sequencial em 04/11/2026. |
| Versões das ferramentas/bibliotecas | Python 3.13.16, NumPy 2.5.3, pandas 3.0.5, matplotlib 3.11.2, scikit-learn 1.9.1. |
| Semente aleatória | 42 (`SEMENTE`), aplicada na divisão dos dados, validação cruzada e algoritmo de Decision Tree/Random Forest. |
| Caminho do notebook executado | [notebooks/laboratorio-equipe.ipynb](notebooks/laboratorio-equipe.ipynb). Resultados salvos em [notebooks/resultados_execucao.json](notebooks/resultados_execucao.json). |
| Origem dos dados e condição sintética | Base gerada por simulação computacional (600 registos sintéticos). Dados exclusivamente acadêmicos sem representação de indivíduos reais. |

## 2. Problema e preparação

- Pergunta de negócio: **Quais alunos apresentam risco iminente de evasão (churn) no mês seguinte e devem receber acompanhamento personalizado da equipa de instrução?**
- Unidade de análise e horizonte: **Um aluno registado. A previsão ocorre ao final dos primeiros 30 dias de matrícula para antecipar o desfecho do 3º mês.**
- Atributos disponíveis no instante da previsão: **`frequencia_semanal` (média de acessos à catraca por semana), `duracao_media_treino` (minutos por sessão) e `dias_sem_treino` (maior hiato sem comparência no mês). Todos registados até ao 30º dia de contrato. Nenhum dado biométrico sensível entra no modelo.**
- Variável-alvo e sua natureza: **`risco_churn`, categórica binária (0 = ativo/manteve o plano, 1 = evadiu/cancelou). Distribuição na base: 60,0% mantiveram o plano (0) e 40,0% cancelaram (1).**
- Ausências e outros problemas encontrados: **30 valores ausentes em `duracao_media_treino` (5% da amostra), introduzidos para simulação de falhas de sincronização da aplicação móvel de treino.**
- Tratamentos e conjunto usado para aprendê-los: **Imputação pela mediana via `SimpleImputer` contido num `Pipeline` de treino, garantindo o isolamento do conjunto de teste.**

## 3. Desenvolvimento e teste

- Método de divisão e justificativa: **Divisão aleatória estratificada (`train_test_split`, `test_size=0.25`, `stratify=y`). A estratificação garante a conservação da proporção original da classe positiva (churn) entre treino e teste.**
- Quantidades de treino e teste: **450 registos de treino e 150 registos de teste.**
- Procedimento de validação no treino: **Validação cruzada estratificada em 5 dobras (`StratifiedKFold`, `shuffle=True`, semente 42) restrita aos dados de treino.**
- Parâmetros da árvore e como foram escolhidos: **Aprofundamento `max_depth` avaliado em 2, 3, 5 e ilimitado. A profundidade 5 atingiu a maior acurácia média (0,7311) na validação cruzada. Configuração final: `max_depth=5`, `min_samples_leaf=10`, `random_state=42`.**
- Como o teste ficou fora da seleção: **A seleção dos hiperparâmetros deu-se exclusivamente na fase de validação no treino. O lote de teste de 25% permaneceu isolado até à medição conclusiva do modelo final.**

### Alternativa Orange

**Fluxo e método de avaliação realmente utilizados:** Não se aplica: utilizou-se o percurso em Python/Scikit-Learn. A avaliação utilizou validação cruzada em 5 dobras sobre o treino e teste independente final.

## 4. Resultados calculados de classificação

| Modelo | Configuração | Acurácia de treino | Acurácia de validação e dispersão | Acurácia de teste |
| --- | --- | --- | --- | --- |
| Referência | `DummyClassifier(strategy='most_frequent')`: prevê sempre 0 (manteve o plano) | 0,6000 (média da validação cruzada) | 0,6000 ± 0,0000 | 0,6000 |
| Árvore final | `DecisionTreeClassifier(max_depth=5, min_samples_leaf=10)` com imputação | 0,8222 (treino completo) | 0,7311 ± 0,0350 | 0,7867 |

**Matriz de Confusão: classe positiva = 1 (Cancelou o plano).**

| Real / previsto | Manteve o plano (0) | Cancelou o plano (1) |
| --- | --- | --- |
| Manteve o plano (0) | 77 (TN) | 13 (FP) |
| Cancelou o plano (1) | 19 (FN) | 41 (TP) |

- Acurácia calculada manualmente pela matriz: **(TN + TP) / Total = (77 + 41) / 150 = 118 / 150 = 0,7867 (78,67%).**
- Sensibilidade (Recall) da classe 1: **TP / (TP + FN) = 41 / (41 + 19) = 41 / 60 = 0,6833 (68,33%). O modelo sinaliza 68,3% dos alunos em risco efetivo de cancelamento.**
- Comparação com referência: **O modelo supera o baseline em 18,67 pontos percentuais de acurácia. O baseline tem sensibilidade nula (0%), enquanto o modelo identifica 41 potenciais evasões.**
- Consequências dos falsos positivos: **13 alunos satisfeitos receberiam um contacto preventivo da equipa. Trata-se de um custo reduzido (envio de mensagem e oferta voluntária de orientação).**
- Consequências dos falsos negativos: **19 alunos com intenção de cancelar não seriam sinalizados atempadamente, resultando em perda de receita para a academia. É o erro de maior impacto no negócio.**
- Interpretação da árvore: **A primeira regra da árvore separa os dados por `dias_sem_treino > 12.5`. Para alunos com elevado hiato de acessos e frequência semanal inferior a 1.5 sessões, a taxa de cancelamento ascende a 88%.**

## 5. Experimentos no treino

| Experimento | Alteração | Resultado de validação | Interpretação |
| --- | --- | --- | --- |
| 1 | `min_samples_leaf` alterado para 5, 10, 20 e 40 com `max_depth=5` | 0,7244 ± 0,0310; 0,7311 ± 0,0350; 0,7333 ± 0,0410; 0,7355 ± 0,0280. | Folhas maiores reduzem a variação entre treino e validação, atenuando o sobreajuste (overfitting). Mantiveram-se 10 amostras por folha para evitar retreino do lote de teste. |
| 2 | Remoção de um atributo de cada vez | Sem `dias_sem_treino`: 0,6311; Sem `frequencia_semanal`: 0,7044; Sem `duracao_media_treino`: 0,7222. | O hiato de dias sem treino é o preditor com maior impacto no modelo: a sua remoção reduz o desempenho em 10 pontos percentuais. |

Respostas conceituais:

1. Como a profundidade e o tamanho das folhas afetam o sobreajuste? **Profundidades elevadas e folhas reduzidas permitem ao modelo memorizar ruídos do treino. A limitação da profundidade em 5 níveis estabiliza a generalização do classificador.**
2. Retirar um atributo e observar mudança no desempenho prova causalidade? **Não. Indica utilidade preditiva na amostra observada. Uma redução na frequência prediz o churn, mas a causa real do cancelamento pode ser motivos financeiros ou insatisfação com a estrutura.**
3. Se 95% mantêm o plano, o que acontece com um modelo que prevê sempre a permanência? **Atingiria 95% de acurácia com sensibilidade zero (0%), sendo ineficaz para o objetivo de negócio.**

## 6. Regressão — Previsão de lotação (Seção independente)

Alvo numérico contínuo: `checkins_por_hora` no setor de musculação.

| Item | Registro |
| --- | --- |
| Atributos e alvo | Atributos: `alunos_ativos_unidade` (200 a 2000) e `temperatura_ambiente` (15°C a 35°C). Alvo: `checkins_por_hora` (numérico contínuo). 300 registos sintéticos. |
| Divisão e preparação | Divisão aleatória de 25% para teste (`random_state=42`). Pipeline contendo `SimpleImputer` e `LinearRegression`. Baseline: `DummyRegressor(strategy='mean')`. |
| MAE do modelo | 6,42 alunos/hora no lote de teste. |
| MAE da referência | 22,15 alunos/hora no lote de teste. O modelo reduz o erro médio de estimativa a menos de um terço do baseline. |
| R² do teste | 0,8650. O baseline exibe R² = -0,0041 no lote de teste. |
| Interpretação dos resíduos | Os resíduos mantêm-se distribuídos em redor de zero com variação constante, confirmando a linearidade da relação entre alunos ativos e frequência horária. |
| Limitação de extrapolação | O modelo foi treinado no intervalo de 200 a 2000 alunos. Projetar a lotação para uma unidade com 10.000 inscritos configuraria extrapolação inválida. |

**Por que o R² não é porcentagem de acertos?** O R² mede a proporção da variância total do alvo que é explicada pelo modelo em comparação com a média. Em regressoes continuas não existem "acertos" categóricos binários, mas sim margens de erro em torno da resposta real.

## 7. Evidências e conclusão

- Link relativo do notebook: **[notebooks/laboratorio-equipe.ipynb](notebooks/laboratorio-equipe.ipynb). Resultados em [notebooks/resultados_execucao.json](notebooks/resultados_execucao.json).**
- Links das imagens: **[Matriz de confusão](assets/lab-matriz-confusao.png), [Árvore de decisão](assets/lab-arvore.png), [Resíduos da regressão](assets/lab-residuos.png).**
- Principal aprendizado: **A sensibilidade (Recall) é a métrica essencial em modelos de retenção. Uma acurácia isolada de 78% esconde o facto de que 31% dos alunos em risco continuam sem sinalização.**
- Limitações e vieses: **Amostras sintéticas com regras predefinidas. Na operação real, oscilações sazonais (ex.: férias de verão) exigem validações temporais contínuas.**
- Cuidados com privacidade (LGPD): **Dados pseudonimizados sem exposição de registos biométricos ou médicos. O modelo é utilizado estritamente para suporte e otimização das escalas de treino, sendo vedada qualquer punição ao utilizador.**

![Matriz de confusão do teste](assets/lab-matriz-confusao.png)

![Resíduos da regressão no teste](assets/lab-residuos.png)
