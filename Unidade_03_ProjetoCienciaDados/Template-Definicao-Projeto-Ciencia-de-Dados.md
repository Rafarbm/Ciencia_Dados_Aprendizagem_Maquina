
**Unidade:** III - Gestão de Projetos  
**Metodologia:** PBL + trabalho em equipes  
**Entregável:** Documento de definição do projeto  

> **Finalidade:** delimitar um problema real e orientar o desenvolvimento do projeto de Ciência de Dados. Preencha todos os campos com informações objetivas, verificáveis e coerentes entre si.

---

## 1. Identificação do projeto

| Campo | Preenchimento |
|---|---|
| **Título provisório do projeto** | Análise do comportamento dos usuários e desempenho de restaurantes em uma plataforma de cupons, descontos e eventos |
| **Curso / disciplina** | Sistemas de Informação / Gestão de Projetos (Projeto de Ciência de Dados) |
| **Turma** | Unidade III |
| **Equipe** | GastroMatch Team |
| **Integrantes e funções iniciais** | Rafael Batista Mota (Engenheiro de Dados / Analista) <br> Gabriel Landim Donadel de Farias (Analista de Negócios / Visualização) |
| **Professor(a)** | Prof. Gabriel Oliveira Alves |
| **Data de elaboração** | 16/09/2026 |
| **Versão do documento** | 1.0 |

---

## 2. Visão geral

### 2.1 Resumo do projeto

O projeto tem como objetivo analisar dados de uma plataforma que reúne restaurantes e oferece aos usuários cupons, descontos e eventos. A análise buscará compreender o comportamento dos usuários e o desempenho das ofertas disponibilizadas pelos restaurantes parceiros. Serão analisados dados como acessos, visualizações, utilização de cupons, categorias de restaurantes, descontos e eventos. Os resultados poderão auxiliar restaurantes e administradores da plataforma na identificação de ofertas de maior interesse e no planejamento de novas campanhas e eventos.

### 2.2 Declaração do projeto em uma frase

> Nosso projeto utilizará **dados de utilização da plataforma** para compreender **o comportamento dos usuários e o desempenho de cupons, descontos e eventos**, apoiando **restaurantes parceiros e administradores** na decisão sobre **quais ofertas e campanhas disponibilizar**.

---

## 3. Contexto e definição do problema

### 3.1 Contexto

A plataforma proposta pelo TCC (GastroMatch) tem como finalidade conectar usuários a restaurantes parceiros por meio de cupons, descontos e eventos. Para os restaurantes, é importante conhecer quais ofertas despertam maior interesse dos usuários. Para os usuários, a plataforma deve facilitar a descoberta de oportunidades de economia e experiências gastronômicas.

- **Onde o problema ocorre?** No ambiente digital da plataforma de cupons, descontos e eventos para restaurantes.
- **Quem é afetado?** Usuários da plataforma, restaurantes parceiros e administradores responsáveis pelo gerenciamento da plataforma.
- **Quais sinais, dados ou relatos indicam sua existência?** Dados como visualizações de restaurantes, acessos às ofertas, utilização de cupons, quantidade de participantes em eventos e interações com as ofertas podem indicar quais conteúdos despertam maior interesse.
- **Por que é importante investigá-lo agora?** Porque a análise desses dados pode ajudar a plataforma e os restaurantes parceiros a compreender melhor o comportamento dos usuários e utilizar essas informações para melhorar as ofertas disponibilizadas.

### 3.2 Problema central

> **Problema definido:** Restaurantes parceiros e administradores da plataforma enfrentam dificuldade para identificar padrões de comportamento dos usuários e o real impacto de cupons, descontos e eventos no ambiente digital, produzindo incerteza na criação de ofertas atrativas e no planejamento de novas campanhas gastronômicas.

### 3.3 Evidências iniciais

| Evidência | Fonte | O que ela indica? | Confiabilidade / limitação |
|---|---|---|---|
| **1. Concentração do mercado de delivery** | Pesquisa Abrasel (2026) / Raj & Eggers (2026) | Indica alta dependência de apps de entrega (86% dos restaurantes) e maior taxa de fechamento de estabelecimentos locais. | **Confiabilidade:** Alta. **Limitação:** Foco em consumo fora do salão (delivery). |
| **2. Ausência de busca por experiência física** | Análise comparativa (iFood, TripAdvisor, Google Maps) | Nenhuma plataforma oferece filtragem combinada de "vibe"/atmosfera e cozinha para o salão. | **Confiabilidade:** Média. **Limitação:** Informações de ambiente ficam dispersas em avaliações textuais. |
| **3. Concentração de interesse em ofertas** | Histórico de resgates no Firestore | Variação na taxa de conversão e resgate de cupons/promoções ativas. | **Confiabilidade:** Alta (dados do sistema). **Limitação:** Base inicial com dados fictícios de 188 restaurantes no ambiente de demonstração. |

---

## 4. Público-alvo e partes interessadas

### 4.1 Público-alvo principal

| Aspecto | Descrição |
|---|---|
| **Quem são os usuários ou beneficiários?** | **Consumidores/Clientes:** Pessoas que buscam comer fora e priorizam a experiência/ambiente (ex.: romântico, familiar, alegre). <br>**Restaurantes parceiros:** Estabelecimentos gastronômicos locais que desejam divulgar cardápios, promoções, cupons e eventos sem custo de anúncio. |
| **Quais necessidades possuem?** | **Clientes:** Encontrar locais por critérios práticos e de experiência em um só lugar. <br>**Restaurantes:** Canal próprio para gestão de ofertas, cupons e visibilidade no salão. |
| **Como são afetados pelo problema?** | Dificuldade em prever a atmosfera do restaurante antes da visita (frustração de expectativa) e baixa visibilidade de pequenos negócios em relação a grandes marcas. |
| **Que decisão ou ação poderão tomar com os resultados?** | **Clientes:** Escolher onde comer fora e resgatar cupons promocionais. <br>**Restaurantes e Plataforma:** Identificar quais ofertas/experiências geram mais interesse para planejar novas campanhas e eventos. |

### 4.2 Partes interessadas

| Parte interessada | Interesse no projeto | Influência | Forma de envolvimento |
|---|---|---|---|
| **Clientes da plataforma** | Descobrir experiências gastronômicas com facilidade e obter descontos via cupons. | Média | Utilização da busca, resgate de cupons, salvamento de favoritos e registro de avaliações. |
| **Restaurantes parceiros** | Atrair clientes para o salão físico e acompanhar o desempenho de cupons e promoções. | Alta | Gerenciamento de cardápios, fotos, promoções, cupons, eventos e validação no caixa. |
| **Administradores da plataforma** | Monitoramento geral, moderação de conteúdo, concessão de destaque e sustentabilidade do sistema. | Alta | Gestão de perfis, concessão de destaques, leitura do Fale Conosco e moderação. |

---

## 5. Objetivos do projeto

### 5.1 Objetivo geral

Analisar os dados de interação dos usuários e o desempenho de ofertas (cupons, promoções e eventos) no ambiente da aplicação web GastroMatch, visando compreender os padrões de escolha do consumidor por experiência/ambiente e apoiar restaurantes e administradores no planejamento estratégico de campanhas.

### 5.2 Objetivos específicos

| Nº | Objetivo específico | Evidência de conclusão |
|---:|---|---|
| **1** | Mapear o volume e o perfil de buscas por tipo de experiência ("vibe"), culinária, localidade e faixa de preço. | Relatório exploratório/painel com a distribuição de buscas por filtros combinados. |
| **2** | Identificar os fatores que influenciam o resgate de cupons de desconto e a adesão a promoções/eventos. | Taxa de conversão por tipo de benefício (%) e contagem de resgates por categoria. |
| **3** | Segmentar os restaurantes parceiros com base na nota média de avaliações e no engajamento dos usuários (favoritos e salvos). | Agrupamento dos restaurantes por faixa de avaliação e volume de interações. |
| **4** | Estruturar um pipeline de tratamento e preparação de dados a partir das coleções NoSQL do Cloud Firestore. | Base de dados tratada, desnormalizada e pronta para análise estatística/exploratória. |

### 5.3 Verificação dos objetivos

Marque após revisar:

- [x] São específicos e escritos com clareza.
- [x] Podem ser verificados por meio de entregáveis ou métricas.
- [x] São viáveis com os dados, recursos e tempo disponíveis.
- [x] Estão diretamente relacionados ao problema central.
- [x] Consideram os usuários e a decisão que será apoiada.

---

## 6. Perguntas de negócio

| Nº | Pergunta de negócio | Decisão apoiada | Dados necessários | Análise ou indicador possível |
|---:|---|---|---|---|
| **1** | Quais combinações de "vibe" (experiência) e tipo de cozinha possuem maior volume de busca no catálogo? | Definição de categorias em destaque na homepage e criação de campanhas temáticas. | Coleções `RESTAURANTES`, logs/parâmetros de busca da aplicação. | Frequência absoluta e relativa de combinações de filtros (ex.: Romântica + Japonesa). |
| **2** | Qual o perfil de cupom de desconto (porcentagem vs. item grátis) apresenta maior taxa de resgate pelos clientes? | Formatação de novas ofertas pelos restaurantes para maximizar a conversão no caixa. | Coleção `CUPONS` e `ingressos_cupons` (resgates). | Taxa média de resgates por tipo de benefício e limite total atingido. |
| **3** | Promoções vinculadas a eventos gastronômicos possuem maior taxa de resgate/salvamento do que promoções independentes? | Decisão de aderir ou não aos eventos globais criados pela administração da plataforma. | Coleções `EVENTOS`, `PROMOCAOS` e `SALVOS`. | Comparativo da quantidade média de salvos/resgates por grupo (com vínculo vs. sem vínculo). |
| **4** | Existe correlação entre a quantidade de fotos do salão e a nota média ou número de favoritos do restaurante? | Recomendação aos restaurantes sobre a importância de completar o perfil com imagens do ambiente. | Coleções `RESTAURANTES` (fotos, nota), `FAVORITOS`. | Coeficiente de correlação de Spearman/Pearson entre total de fotos e favoritos/nota. |

---

## 7. Hipóteses iniciais

| Hipótese | Como poderá ser testada? | Resultado que a refutaria? |
|---|---|---|
| **H1.** Restaurantes cadastrados com experiências "Romântica" ou "Sofisticada" apresentam uma nota média de avaliação superior aos demais tipos. | Comparando a distribuição das notas médias (coleção `RESTAURANTES`) entre as diferentes categorias de "vibe" por testes de hipótese (ANOVA / Kruskal-Wallis). | A ausência de diferença estatisticamente significativa entre as médias de avaliação por categoria ($p > 0{,}05$). |
| **H2.** Cupons com percentual de desconto acima de 15% esgotam o limite de resgates no dobro da velocidade dos cupons com brindes. | Analisando o tempo decorrido entre a data inicial do cupom e o atingimento do limite de resgates (`resgatesAtuais == limiteTotal`). | Cupons de brindes apresentarem taxa de resgate idêntica ou superior no mesmo período. |
| **H3.** O estabelecimento ter selo de Destaque (concedido pelo admin) aumenta em no mínimo 50% o número de vezes que ele é salvo como favorito. | Comparando o volume de registros na coleção `FAVORITOS` de restaurantes destacados vs. não destacados com faixas de preço semelhantes. | O volume de favoritos de restaurantes destacados não apresentar diferença superior a 50% em relação ao grupo de controle. |

---

## 8. Dados necessários e viabilidade

| Conjunto ou fonte de dados | Variáveis principais | Formato | Acesso / responsável | Qualidade esperada |
|---|---|---|---|---|
| **`RESTAURANTES`** | `id`, `nomeFantasia`, `cozinha`, `experiencias`, `bairro`, `cidade`, `nota`, `fotos` | NoSQL (Firestore JSON) | Leitura pública / Gabriel & Rafael | Alta. Campos padronizados por vocabulário fechado. |
| **`CUPONS` / `ingressos_cupons`** | `codigo`, `dataInicio`, `dataFim`, `limiteResgates`, `resgatesAtuais`, `status` | NoSQL (Firestore JSON) | Restrito (Admin) / Gabriel & Rafael | Alta. Controlado por transações no banco. |
| **`AVALIACOES`** | `id`, `slugRestaurante`, `nota` (1 a 5), `comentario`, `criadoEm` | NoSQL (Firestore JSON) | Restrito (Admin) / Gabriel & Rafael | Média. Comentários opcionais (texto livre de até 500 caracteres). |
| **`FAVORITOS` / `SALVOS`** | `uidCliente`, `slugRestaurante`, `tipoItem`, `dataSalvo` | NoSQL (Firestore JSON) | Restrito (Admin) / Gabriel & Rafael | Alta. IDs compostos impedem duplicidade. |

### 8.1 Avaliação inicial dos dados

- **Disponibilidade:** Dados coletados diretamente do banco Cloud Firestore do protótipo GastroMatch.
- **Volume e período coberto:** Base demonstrativa inicial composta por 188 restaurantes cadastrados e histórico de commits do projeto (21/10/2026 a 10/11/2026).
- **Dados ausentes, duplicados ou inconsistentes previstos:** Proteção nativa no banco por IDs compostos (ex.: `cliente+restaurante` em favoritos) e regras de validação no Firestore que barram duplicatas e caracteres inválidos (`< > "` e grave).
- **Necessidade de integração entre fontes:** Integração interna entre coleções NoSQL (ex.: associar dados de resgate de `ingressos_cupons` com características de `RESTAURANTES` e `PROMOCAOS`).
- **Restrições legais, contratuais ou institucionais:** Conformidade total com a LGPD. O sistema utiliza identificadores sigilosos (HMAC) para CPF/CNPJ e restringe o compartilhamento de dados pessoais.

### 8.2 Privacidade, ética e segurança

- [x] A equipe verificou se há dados pessoais ou sensíveis.
- [x] A coleta e o uso dos dados possuem finalidade legítima e explícita.
- [x] O acesso será limitado às pessoas autorizadas.
- [x] Dados pessoais serão minimizados, anonimizados ou pseudonimizados quando necessário.
- [x] Possíveis vieses e impactos sobre grupos serão analisados.
- [x] A divulgação dos resultados evitará reidentificação ou exposição indevida.

**Cuidados específicos deste projeto:**

O CPF/CNPJ é visível unicamente para o titular. Seu controle de duplicidade é realizado no servidor via HMAC com chave secreta, sem armazenar o número como ID. Nas avaliações e nos históricos de resgate de cupons exibidos aos restaurantes, é exposto apenas o primeiro nome do cliente. O envio de textos ao serviço externo de Inteligência Artificial (GroqCloud) restringe-se às preferências de busca e dados públicos de restaurantes, omitindo qualquer dado pessoal do usuário.

---

## 9. Escopo do projeto

| Dentro do escopo | Fora do escopo |
|---|---|
| Tratamento e extração de dados exportados do Cloud Firestore. | Pagamento de valores ou transações financeiras na plataforma. |
| Análise exploratória sobre padrões de preferência por "vibe", cozinha e faixa de preço. | Confirmação de reservas diretamente no site (realizada externamente via WhatsApp). |
| Avaliação de desempenho de cupons (taxas de resgate) e eventos. | Recomendação preditiva baseada em histórico/machine learning no app web. |
| Criação de visualizações e relatórios analíticos de apoio à decisão. | Testes de usabilidade e coleta de dados com usuários reais no ambiente de demonstração. |

**Restrições conhecidas:** 

Uso do plano gratuito (Spark) do Firebase e limites de leitura/gravação diários do Cloud Firestore; protótipo demonstrativo com dados fictícios; e dependência das regras de segurança configuradas nas coleções.

---

## 10. Resultados e entregáveis previstos

| Entregável | Descrição | Formato | Responsável | Critério de aceite |
|---|---|---|---|---|
| **Base tratada** | Dataset consolidado a partir das coleções do Firestore limpo e desnormalizado. | CSV / Pandas DataFrame | Gabriel Landim | Ausência de duplicatas, colunas tipadas corretamente e sem dados sensíveis expostos. |
| **Análise exploratória** | Estudo descritivo e estatístico sobre preferências dos usuários e conversão de cupons. | Notebook Jupyter / Relatório (`.md`) | Rafael Batista | Resposta completa às 4 perguntas de negócio formuladas no item 6. |
| **Visualizações / painel** | Gráficos interativos apresentando a distribuição de "vibes", notas e cupons. | Dashboard (Streamlit / Power BI) | Gabriel & Rafael | Gráficos responsivos, legíveis e alinhados às hipóteses H1, H2 e H3. |
| **Relatório final** | Documentação completa do projeto de ciência de dados relacionando o TCC à análise realizada. | PDF / Documento final | Rafael Batista | Aprovação e coerência integral com a modelagem do sistema. |

---

## 11. Critérios de sucesso

| Critério | Indicador ou evidência | Meta | Forma de verificação |
|---|---|---|---|
| **Relevância para o problema** | Respostas conclusivas para as perguntas de negócio formuladas. | 100% das 4 perguntas respondidas com dados | Validação no relatório de análise exploratória. |
| **Qualidade dos dados** | Integridade e conformidade com as regras de negócio (RN01 a RN70). | 0% de dados sensíveis vazados / 100% registros válidos | Auditar dataset tratado via scripts de validação de qualidade. |
| **Qualidade da análise** | Validação/refutação estatística das hipóteses iniciais (H1, H2, H3). | Coeficientes e testes de hipóteses calculados ($p\text{-valor}$) | Execução dos testes estatísticos no Notebook. |
| **Utilidade para o público-alvo** | Geração de insights aplicáveis ao cadastramento de novas promoções/cupons. | Apresentar no mínimo 3 recomendações práticas | Seção de recomendações estratégicas no relatório. |
| **Comunicação dos resultados** | Clareza visual dos dashboards e gráficos produzidos. | Interface gráfica fluida e de fácil interpretação | Apresentação para o professor/orientador. |

---

## 12. Plano inicial de trabalho

| Etapa | Atividades principais | Responsável(is) | Prazo | Dependências |
|---|---|---|---|---|
| **1. Definição** | Alinhamento do escopo, perguntas de negócio e preenchimento do template. | Rafael & Gabriel | 16/09/2026 | Aprovação da proposta inicial. |
| **2. Obtenção dos dados** | Extração das coleções NoSQL do Cloud Firestore do ambiente GastroMatch. | Gabriel Landim | 25/10/2026 | Instância do Firestore e credenciais de admin. |
| **3. Preparação dos dados** | Limpeza, tratamento de tipos, pseudonimização/HMAC e estruturação tabular. | Rafael Batista | 30/10/2026 | Extração dos dados concluída. |
| **4. Análise / modelagem** | Análise exploratória de dados (EDA), verificação de correlações e testes de hipóteses. | Rafael & Gabriel | 05/11/2026 | Base tratada e sanitizada. |
| **5. Validação** | Validação das estatísticas obtidas e consolidação das respostas de negócio. | Gabriel Landim | 08/11/2026 | Análise exploratória concluída. |
| **6. Comunicação** | Construção do painel visual, redação do documento de entrega e apresentação final. | Rafael Batista | 10/11/2026 | Validação das análises. |

---

## 13. Riscos do projeto

| Risco | Probabilidade | Impacto | Estratégia de resposta | Responsável |
|---|---|---|---|---|
| **1. Volume insuficiente de dados em coleções secundárias** | Média | Médio | Utilizar scripts de geração de massa de dados sintéticos mantendo o padrão das regras de negócio (RN). | Gabriel Landim |
| **2. Exceder cotas de leitura do plano gratuito do Firestore (Spark)** | Baixa | Alto | Realizar exportações pontuais em lote (lotes paginados) e trabalhar localmente com dataframes estáticos. | Rafael Batista |
| **3. Inconsistência de esquema por ser banco NoSQL** | Baixa | Médio | Implementar rotinas robustas de validação de esquema na etapa de pré-processamento dos dados. | Gabriel Landim |

---

## 14. Organização da equipe

| Integrante | Papel principal | Responsabilidades | Apoio necessário |
|---|---|---|---|
| **Rafael Batista Mota** | Engenheiro de Dados / Analista | Extração e sanitização dos dados NoSQL, tratamento de privacidade (LGPD/HMAC), teste de hipóteses e documentação. | Acesso com privilégios ao Firebase Console. |
| **Gabriel Landim Donadel de Farias** | Analista de Negócios / Visualização | Estruturação das perguntas de negócio, análise exploratória estatística, construção dos dashboards e validação. | Dados tratados fornecidos na Etapa 3. |

---

## 15. Validação da definição do projeto

Antes da entrega, confirme:

- [x] O problema é real, relevante e delimitado.
- [x] O público-alvo e as partes interessadas estão identificados.
- [x] O objetivo geral e os objetivos específicos são coerentes.
- [x] As perguntas de negócio orientam decisões concretas.
- [x] Há dados potencialmente disponíveis para responder às perguntas.
- [x] O escopo é compatível com o prazo e os recursos.
- [x] Os critérios de sucesso são mensuráveis.
- [x] Riscos, privacidade, ética e segurança foram considerados.
- [x] Funções e responsabilidades foram distribuídas.

---

## 16. Aprovação e registro de ajustes

| Responsável | Validação / observação | Data |
|---|---|---|
| **Representante da equipe** | Rafael Batista Mota | 16/09/2026 |
| **Professor(a) / orientador(a)** | Prof. Gabriel Oliveira Alves | 16/09/2026 |

### Ajustes solicitados após a apresentação inicial

1. Confirmação do escopo restrito a análises descritivas/exploratórias sem obrigatoriedade de disponibilização de modelo preditivo em tempo real no app.
2. Garantia de anonimização estrita e cálculo sigiloso de identificadores de CPF/CNPJ via servidor.
