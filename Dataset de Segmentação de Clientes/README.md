# Análise Exploratória de Dados para Segmentação de Clientes
**Descrição do Projeto:**
Este projeto tem como objetivo realizar uma análise exploratória de dados (EDA) em um conjunto de dados contendo informações demográficas, socioeconômicas e comportamentais de clientes, com foco em identificar padrões relevantes para segmentação de consumidores e apoio à tomada de decisão.

O dataset analisado contém mais de 8000 registros, incluindo variáveis como idade, estado civil, profissão, experiência profissional, gastos e tamanho da família.

**Objetivos**
Compreender a estrutura e qualidade dos dados.
Identificar inconsistências, valores faltantes e outliers.
Aplicar técnicas de limpeza e tratamento de dados.
Extrair padrões e insights relevantes para segmentação.
Apoiar decisões baseadas em dados.
Etapas da Análise
### 1. Análise de Qualidade dos Dados
* Identificação de valores faltantes por variável.
* Classificação do mecanismo de ausência (MAR – Missing At Random).
* Verificação de duplicatas com base em identificadores únicos.
### 2. Detecção de Inconsistências
* Identificação de inconsistências lógicas entre variáveis (ex: profissão vs. formação).
* Análise de incompatibilidades entre idade e experiência profissional.
* Avaliação de padrões de ausência de dados associados a outras variáveis.
### 3. Análise de Outliers e Distribuição
* Utilização de boxplots para identificação de outliers.
* Avaliação de assimetria e distribuição das variáveis.
* Interpretação dos outliers como valores reais ou possíveis erros.
### 4. Tratamento de Dados
* Estratégias de imputação:
* Moda para variáveis categóricas.
* Mediana para variáveis numéricas com outliers.
* Exclusão de variáveis irrelevantes.
* Padronização e preparação dos dados para análise.
### 5. Normalização de Dados
* Aplicação de técnicas conforme a distribuição:
* Min-Max Scaling para dados com distribuição aproximadamente simétrica.
* Transformação Logarítmica para variáveis com alta assimetria.
* Decisão baseada em análise estatística e visual (boxplots).
### 6. Análise Exploratória (EDA)
* Identificação de padrões de comportamento entre variáveis.
* Análise de segmentação de clientes com base em características demográficas e consumo.
* Exploração de relações entre variáveis como:
* Tamanho da família vs. segmentação.
* Experiência profissional vs. idade.
* Spending score vs. perfil do cliente.
---
**Principais Insights**
* Famílias maiores apresentam maior tendência de pertencer à segmentação D.
* Clientes sem experiência profissional tendem a apresentar baixo nível de gastos.
* A segmentação C apresenta maior concentração de consumidores com gasto médio a alto.
* Foram identificadas inconsistências relevantes em dados de profissão e formação, indicando necessidade de tratamento cuidadoso.
---
**Ferramentas Utilizadas:**
* Excel para exploração e organização inicial dos dados.
* Visualizações com base em análise estatística (boxplots e distribuições).
---
**Aprendizados:**
* Importância da qualidade dos dados antes de qualquer modelagem.
* Necessidade de interpretar outliers antes de removê-los.
* Relevância da análise exploratória na geração de insights.
* Tomada de decisão baseada em evidências e não apenas em modelos.