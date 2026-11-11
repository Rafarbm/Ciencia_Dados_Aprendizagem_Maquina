<img src="assets/logo-udf.jpg" alt="UDF Centro Universitário" width="230">

**Profa. Kadidja Valéria | UDF**  
Ciência de Dados e Aprendizado de Máquina · Sistemas de Informação · 2026.2

# Autoavaliação e conferência da entrega

## Identificação

- Estudante ou equipe: RAFAEL BATISTA MOTA
- Turma: **Sistemas de Informação — 8º Semestre**
- Data de realização: **04/11/2026**
- Integrantes e contribuições: RAFAEL BATISTA MOTA (Resolução e autoavaliação individual)

---

## Checklist

- [x] Diferenciei IA, Ciência de Dados e ML com um exemplo. *(ver "Reflexão individual" abaixo)*[cite: 6]
- [x] Completei o quadro supervisionado/não supervisionado. *([01](01-aula1-conceitos.md), seção 2)*[cite: 6]
- [x] Justifiquei pelo menos cinco situações-problema. *([01](01-aula1-conceitos.md), seção 3: casos 1, 6, 8, 3 e 4)*[cite: 6]
- [x] Registrei a investigação da academia FitLife Fitness. *([02](02-pbl-biblioteca.md))*[cite: 6]
- [x] Identifiquei atributos, alvo, unidade e momento da previsão. *([03](03-aula2-laboratorio.md), seção 2)*[cite: 6]
- [x] Executei e documentei a prática em Python ou Orange. *([notebook](notebooks/laboratorio-equipe.ipynb))*[cite: 6]
- [x] Escolhi configurações usando treino/validação. *(validação cruzada de 5 partes no treino)*[cite: 6]
- [x] Mantive o teste fora do ajuste e da seleção. *(experimentos antes da célula de teste; nenhuma troca posterior)*[cite: 6]
- [x] Interpretei acurácia, matriz, MAE e R². *([03](03-aula2-laboratorio.md), seções 4 e 6)*[cite: 6]
- [x] Comparei com uma referência e discuti erros. *(classe majoritária e média; FP e FN)*[cite: 6]
- [x] Registrei limitações, dados sintéticos, privacidade e vieses. *([03](03-aula2-laboratorio.md), seção 7; [04](04-pbl-permanencia.md), seção 6)*[cite: 6]
- [x] Formulei recomendações de apoio com revisão humana. *([04](04-pbl-permanencia.md), seção 7)*[cite: 6]
- [x] Respondi às questões individuais. *([05](05-revisao.md))*[cite: 6]
- [x] Conferi os links e os arquivos de evidências.[cite: 6]
- [x] Substituí os campos PREENCHER ou justifiquei os não aplicáveis. *(campo de feedback em [02](02-pbl-biblioteca.md) aguardando a apresentação presencial)*[cite: 6]

---

## Reflexão individual

- **O que aprendi e consigo explicar:** Consigo diferenciar claramente os três conceitos através do domínio da **FitLife Fitness**[cite: 6]. *Inteligência Artificial* é o campo amplo focado na automatização de decisões (ex.: o sistema global de recomendação e acompanhamento da academia)[cite: 6]. *Machine Learning* é a vertente em que o sistema aprende os padrões a partir de dados históricos (ex.: o algoritmo de Árvore de Decisão que identifica o risco de churn com base na frequência dos alunos)[cite: 6]. *Ciência de Dados* engloba todo o ciclo de valor, desde o entendimento do negócio, limpeza e validação SQL via DuckDB até à geração de dashboards e recomendação de suporte aos instrutores[cite: 6].
- **Qual foi minha principal dificuldade:** Garantir o rigor de isolamento do conjunto de teste[cite: 6]. Compreender na prática que pequenas variações de acurácia na validação cruzada (como alterar a folha mínima da árvore de 10 para 40) não justificavam trocar a configuração final após a medição no conjunto de teste, sob pena de contaminar a avaliação[cite: 6].
- **Qual evidência mostra meu avanço:** O [notebook executado](notebooks/laboratorio-equipe.ipynb) e os ficheiros de relatório preenchidos (`03-aula2-laboratorio.md` e `05-revisao.md`)[cite: 6]. A resolução manual das métricas da matriz de confusão e a interpretação de que acurácias elevadas podem ser enganosas perante classes desbalanceadas demonstram o domínio prático dos conceitos[cite: 6].
- **Como contribuí com a equipe:** Realizei a atividade individualmente, executando os scripts em Python/DuckDB, modelando os classificadores, preenchendo as documentações Markdown (`01` a `06`) e configurando o repositório no padrão exigido pela disciplina[cite: 6].
- **O que preciso revisar:** Aprofundar o estudo em técnicas de validação temporal com dados reais em séries temporais e explorar algoritmos adicionais de tratamento de desbalanceamento de classes, como SMOTE e pesagem de classes[cite: 6].
- **Ferramentas de apoio utilizadas e verificação:** Python 3.13, Pandas, NumPy, Scikit-Learn, DuckDB, Matplotlib e Seaborn. Utilizei o assistente de IA como ferramenta de apoio para organização e revisão dos relatórios. Todas as métricas foram verificadas manualmente e validadas através da execução do código no notebook `laboratorio-equipe.ipynb`[cite: 6].

---

## Critérios de avaliação

Escala sugerida do material: nível 3 consistente, 2 adequado com lacunas, 1 parcial, 0 ausente/incoerente[cite: 6]. Nota do critério = peso × nível/3[cite: 6].

| Critério | Peso aula 1 | Peso aula 2/PBL |
| --- | --- | --- |
| Problema e conceitos | 3,0 | 2,0 |
| Dados e justificativa | 2,0 | 2,0 |
| Método e avaliação | 1,0 | 3,0 |
| Interpretação e responsabilidade | 2,0 | 2,0 |
| Clareza e colaboração | 2,0 | 1,0 |
| **Total** | **10,0** | **10,0** |

---

## Fontes de apoio

- SCIKIT-LEARN. *User Guide*. https://scikit-learn.org/stable/user_guide.html[cite: 6].
- SCIKIT-LEARN. *Common pitfalls and recommended practices*. https://scikit-learn.org/stable/common_pitfalls.html[cite: 6].
- DUCKDB. *Documentation*. https://duckdb.org/docs/.

[Voltar ao início](README.md)[cite: 6].
