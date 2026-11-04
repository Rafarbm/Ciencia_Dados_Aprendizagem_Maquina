<img src="assets/logo-udf.jpg" alt="UDF Centro Universitário" width="230">

**Profa. Kadidja Valéria | UDF**  
Ciência de Dados e Aprendizado de Máquina · Sistemas de Informação · 2026.2

# Questões de revisão — Registro individual

## Identificação

- Estudante ou equipe: RAFAEL BATISTA MOTA
- Turma: **Sistemas de Informação — 8º Semestre**
- Data de realização: **04/11/2026**
- Integrantes e contribuições: RAFAEL BATISTA MOTA (Resolução e revisão individual)

Responda com suas palavras e apresente os cálculos quando solicitados. Os números dos exercícios manuais não são os resultados do laboratório.

---

## 1. Explique a diferença entre regra programada para bloquear uma palavra e modelo de spam treinado com exemplos.

**Resposta:** A regra programada baseia-se em lógica condicional explícita definida por um humano (ex.: `se texto contém 'oferta', então bloquear`). Embora transparente, é uma abordagem rígida: gera falsos positivos em mensagens legítimas, é facilmente burlada por variações sintáticas (ex.: `0ferta`) e exige manutenção manual constante. O modelo de Machine Learning aprende a partir de exemplos pré-rotulados, analisando múltiplos atributos simultaneamente (remetente, vocabulário, links, horários). Ele infere padrões estatísticos flexíveis, generalizando melhor para novas ameaças, mas depende de dados de treino rotulados de alta qualidade e requer monitorização contínua contra degradação de desempenho.

---

## 2. Por que codificar evadiu/permaneceu como 1/0 não transforma classificação em regressão?

**Resposta:** O tipo de tarefa de aprendizagem de máquina é determinado pela natureza conceitual da variável-alvo, não pelo seu formato de armazenamento digital. Os dígitos `0` e `1` funcionam como meras etiquetas categóricas (equivalentes a "Ativo" ou "Evasão"). Não existe continuidade numérica, relação de ordem nem sentido matemático na diferença de valores (não existe "0,5 de evasão"). A tarefa permanece sendo uma classificação binária e a sua avaliação é realizada através da matriz de confusão e métricas de classe (Precisão, Recall), e não por métricas de distância contínua como MAE ou RMSE.

---

## 3. Uma biblioteca quer estimar empréstimos e descobrir perfis. Que tarefas correspondem a cada pergunta?

**Resposta:** 
- **Estimar empréstimos:** Corresponde a uma tarefa de **Regressão** (Aprendizagem Supervisionada). O alvo é uma variável numérica contínua (ex.: quantidade de empréstimos por semana) e o modelo é treinado com um histórico rotulado contendo os valores reais passados.
- **Descobrir perfis:** Corresponde a uma tarefa de **Agrupamento / Clustering** (Aprendizagem Não Supervisionada). Não existem categorias prévias de perfis; o algoritmo agrupa utilizadores ou sessões por similaridade comportamental (horários, frequência, tipo de acervo), cabendo aos especialistas interpretar o significado de cada cluster.

---

## 4. O que são atributo, alvo e unidade de análise no laboratório educacional?

**Resposta:**
- **Unidade de análise:** É cada instância individual da base de dados (uma linha da tabela), representada por um aluno registado num determinado semestre.
- **Atributos:** São as variáveis explicativas conhecidas até ao momento da previsão (fim da semana 4), designadamente `% de frequência` (`frequencia_sem4`), `média de notas` (`nota_sem4`) e `entregas de tarefas` (`entregas_sem4`).
- **Alvo:** É a variável de desfecho que se pretende prever (`evasao_fim_semestre`), categórica binária (`0 = permaneceu`, `1 = evadiu`), conhecida apenas ao término do período letivo.

---

## 5. Por que calcular a mediana antes de dividir os dados pode invalidar a avaliação?

**Resposta:** Porque calcular a mediana sobre todo o conjunto de dados antes do particionamento resulta em **vazamento de dados (data leakage)**. A estatística calculada incorporaria informações contidas no lote de teste, contaminando a fase de treino. Consequentemente, o lote de teste deixaria de ser um conjunto estritamente "não visto", produzindo métricas de avaliação irrealisticamente otimistas. O procedimento correto consiste em realizar a divisão dos dados em primeiro lugar e aplicar a imputação calculando a mediana exclusivamente com base nos dados de treino.

---

## 6. Em uma matriz didática com TN=80, FP=5, FN=10, TP=5, calcule acurácia e sensibilidade. O resultado é suficiente para aprovar o modelo?

**Resposta:**

- Total de amostras = $80 + 5 + 10 + 5 = 100$.
- **Acurácia:** $\frac{TN + TP}{\text{Total}} = \frac{80 + 5}{100} = \frac{85}{100} = \mathbf{0,85 \text{ (85,0\%)}}$.
- **Sensibilidade (Recall):** $\frac{TP}{TP + FN} = \frac{5}{5 + 10} = \frac{5}{15} = \mathbf{0,333 \text{ (33,3\%)}}$.

**Conclusão:** **Não é suficiente para aprovar o modelo.** Embora a acurácia seja de 85%, o conjunto de dados possui um forte desbalanceamento de classes (85 casos negativos contra 15 positivos). Um modelo simplório (baseline) que previsse continuamente a classe negativa obteria exatamente os mesmos 85% de acurácia com 0% de sensibilidade. O modelo falha ao omitir dois terços (10 em 15) dos casos positivos reais (FN=10), demonstrando ser ineficaz para o objetivo de detecção.

---

## 7. Valores reais 100, 120, 140 e previsões 110, 115, 130. Calcule MAE e informe a unidade se o alvo for vendas em reais.

**Resposta:**

- Erros absolutos individuais:  
  $|100 - 110| = 10$  
  $|120 - 115| = 5$  
  $|140 - 130| = 10$  

- **MAE (Erro Médio Absoluto):** $\frac{10 + 5 + 10}{3} = \frac{25}{3} \approx \mathbf{8,33}$.
- **Unidade de medida:** **Reais (R$)**. Em média, as estimativas do modelo desviam-se R$ 8,33 em relação ao valor real de vendas, para mais ou para menos.

---

## 8. Um R² de -0,2 significa “20% de acertos negativos”? Explique.

**Resposta:** **Não.** O coeficiente de determinação ($R^2$) não é uma porcentagem de acertos, mas sim uma métrica de comparação entre o erro quadrático do modelo e o erro quadrático de prever continuamente a média dos dados reais:  
$$R^2 = 1 - \frac{\sum (y - \hat{y})^2}{\sum (y - \bar{y})^2}$$  
Um valor de $R^2 = -0,2$ indica que a soma dos erros quadráticos do modelo é **20% superior** ao erro de um modelo ingénuo que utilizasse apenas a média do alvo. Ou seja, a capacidade preditiva do modelo é pior do que a utilização da simples média histórica.

---

## 9. Uma árvore tem acurácia 1,00 no treino e 0,65 na validação. Que hipótese investigar e como?

**Resposta:** A principal hipótese a investigar é o **sobreajuste (overfitting)**, situação em que a Árvore de Decisão decorou os ruídos e particularidades do conjunto de treino, perdendo capacidade de generalização.

**Procedimento de investigação:**
1. Analisar a profundidade da árvore (`max_depth`) e o número mínimo de amostras por folha (`min_samples_leaf`).
2. Executar validação cruzada restrita ao treino testando hiperparâmetros mais conservadores (ex.: limitar profundidade a 3 ou 5 e aumentar a folha mínima para 10 ou 20).
3. Avaliar se a diferença entre a acurácia de treino e validação diminui enquanto a acurácia de validação melhora.
4. Comparar o desempenho final obtido na validação cruzada com a linha de base (classificador por classe majoritária).

---

## 10. Por que escolher a profundidade pelo teste prejudica a estimativa final?

**Resposta:** Porque utilizar o conjunto de teste para selecionar a profundidade da árvore provoca contaminação dos dados (data leakage). O lote de teste passa a integrar o processo de afinação do modelo, selecionando a configuração que casualmente se ajustou melhor àquela amostra específica de 150 exemplos. Assim, as métricas obtidas deixam de representar uma avaliação imparcial sobre dados desconhecidos, resultando em estimativas de desempenho irrealisticamente otimistas. O lote de teste deve ser reservado e executado estritamente uma única vez após a consolidação final do modelo.

---

## 11. Baixa frequência associada à evasão demonstra causa? Proponha explicação alternativa.

**Resposta:** **Não.** Uma correlação estatística entre duas variáveis não estabelece uma relação de causa e efeito. 

**Explicação alternativa:** Pode existir uma **variável de confusão (terceira causa)** que provoca simultaneamente a diminuição da frequência e a evasão, como uma alteração severa na rotina de trabalho do aluno, problemas graves de saúde ou limitações financeiras. Nestes cenários, forçar o aumento da frequência por imposição de regras não resolveria a causa raiz do abandono. Adicionalmente, pode ocorrer **causalidade reversa**, na qual o aluno decide previamente cancelar a inscrição e, como consequência, deixa de frequentar as instalações.

---

## 12. Um modelo sinaliza um estudante como possível evasão. Que ação responsável pode ser adotada?

**Resposta:** A sinalização emitida pelo modelo deve ser tratada exclusivamente como um indicador orientativo para a **oferta voluntária de suporte técnico**, nunca como uma certeza absoluta ou instrumento punitivo.

**Ações responsáveis recomendadas:**
1. **Revisão Humana:** Um instrutor/profissional analisa os registos operacionais do aluno antes de qualquer abordagem presencial ou remota.
2. **Abordagem Acolhedora:** Envio de um convite privado e opcional oferecendo consultoria de treino ou reavaliação física, sem fazer menção ao risco de cancelamento.
3. **Direito de Recusa e Autonomia:** O aluno mantém total autonomia para recusar o atendimento sem qualquer penalização contratual ou financeira.
4. **Governança de Dados (LGPD):** Garantir acesso restrito às sinalizações e assegurar a eliminação dos escores ao final do ciclo de atendimento.
5. **Canais Abertos de Atendimento:** Manter os serviços de suporte acessíveis a toda a comunidade de utilizadores, compensando os falsos negativos do modelo.

---

## Fontes adicionais consultadas

Material didático da disciplina: *Material do Estudante do Módulo IV — Aprendizado de Máquina* (Profa. Kadidja Valéria, UDF, 2026). Declaração de uso de assistente virtual: utilização de ferramenta de linguagem para estruturação e revisão das respostas. Todos os cálculos matemáticos das questões 6 e 7 foram efetuados e validados manualmente.

[Voltar ao início](README.md).
