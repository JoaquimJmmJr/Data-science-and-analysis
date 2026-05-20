# Projeto de Análise de Ciência e Visualização de Dados

> **Relatório estruturado de acordo com o framework CRISP-DM**  
> Curso: CCD210 – Fundamentos de Ciência e Visualização de Dados  
> Instituição: FEI – Fundação Educacional Inaciana "Pe. Sabóia de Medeiros"

---

## Sumário

1. [Entendimento do Negócio](#1-entendimento-do-negócio)
2. [Entendimento dos Dados](#2-entendimento-dos-dados)
3. [Preparação dos Dados](#3-preparação-dos-dados)
4. [Modelagem](#4-modelagem)
5. [Avaliação](#5-avaliação)
6. [Referências](#6-referências)

---

## 1. Entendimento do Negócio

### 1.1 Contexto e Motivação

O acesso a uma alimentação saudável é um dos pilares do desenvolvimento humano sustentável. Segundo a Organização das Nações Unidas para Alimentação e Agricultura (FAO), em 2022 aproximadamente 3,1 bilhões de pessoas ao redor do mundo não podiam arcar com os custos de uma dieta saudável — um número que cresceu de forma expressiva após a pandemia de COVID-19 e os choques inflacionários de 2021–2024.

Este projeto analisa a evolução e a distribuição global do custo de uma dieta saudável entre 2017 e 2024, investigando disparidades regionais, tendências temporais e relações com indicadores socioeconômicos. O trabalho se insere no contexto do **Objetivo de Desenvolvimento Sustentável 2 da ONU (ODS 2 – Fome Zero e Agricultura Sustentável)**, que prevê o fim da fome e o acesso universal a alimentos nutritivos e suficientes.

Conexões adicionais com os ODS:
- **ODS 1 – Erradicação da Pobreza**: em muitos países, o custo diário de uma dieta saudável supera a linha de pobreza internacional de US$ 2,15/dia (PPP).
- **ODS 3 – Saúde e Bem-estar**: a inacessibilidade alimentar contribui para má nutrição, doenças crônicas e piora dos indicadores de saúde pública.
- **ODS 10 – Redução das Desigualdades**: as disparidades entre países de diferentes níveis de renda evidenciam iniquidades estruturais no sistema alimentar global.

### 1.2 Definição do Problema

> **Pergunta central:** Como o custo de uma dieta saudável evoluiu globalmente entre 2017 e 2024, e quais grupos de países enfrentam as maiores barreiras de acessibilidade alimentar?

Questões secundárias orientadoras da análise:

- Quais países apresentaram os maiores aumentos percentuais no custo da dieta no período?
- Como os eventos de 2020–2022 (pandemia e inflação global) impactaram os custos alimentares?
- Qual é a relação entre o custo da dieta e o custo de vida, considerando o ajuste por paridade de poder de compra (PPP)?
- Quais países concentram as maiores barreiras de acessibilidade alimentar em 2024?

### 1.3 Escopo do Projeto

O projeto abrange:

- Análise exploratória descritiva do dataset global do custo da dieta saudável (FAO/FAOSTAT, 2017–2024).
- Análise temporal da evolução dos custos e do impacto dos eventos macroeconômicos de 2020–2022.
- Análise de distribuição e disparidades entre países com visualizações geográficas e estatísticas.

**Fora do escopo:** a etapa de Implementação/Deployment não será realizada conforme orientação do projeto. A análise por região geográfica foi descartada em função de inconsistências identificadas na coluna `region` do dataset (detalhadas na seção 2.2.4).

### 1.4 Métricas de Sucesso

A análise será considerada bem-sucedida se for capaz de:

- Quantificar a evolução global do custo da dieta entre 2017 e 2024 com precisão descritiva;
- Identificar os países mais vulneráveis em termos de acessibilidade alimentar;
- Quantificar o impacto dos eventos de 2020–2022 sobre os custos;
- Produzir visualizações e narrativas que comuniquem os achados de forma acessível (*data storytelling*).

---

## 2. Entendimento dos Dados

### 2.1 Fonte e Aquisição

| Atributo | Descrição |
|---|---|
| **Fonte** | Food and Agriculture Organization – FAO/FAOSTAT |
| **Relatório de origem** | SOFI 2025 (*State of Food Security and Nutrition in the World*), publicado em julho de 2025 |
| **Disponibilização** | Kaggle – dataset público, licença FAO Open Data Policy |
| **Última atualização** | 30 de janeiro de 2026 |
| **URL** | `https://www.kaggle.com/datasets/ibrahimshahrukh/global-price-of-healthy-diet-dataset` |

O dataset foi obtido diretamente pela plataforma Kaggle em formato CSV (UTF-8), sem necessidade de pré-processamento de codificação. A metodologia da FAO é baseada em Diretrizes Alimentares Baseadas em Alimentos (FBDGs), preços de varejo e otimização de custo mínimo para atendimento dos requisitos nutricionais, com preços convertidos em dólares PPP para comparabilidade internacional.

**Nota metodológica:** o ano de **2021** é o ano de referência do dataset, pois foi quando o ICP (*International Comparison Program*) coletou os dados desagregados de preços de varejo. Para os demais anos (2017–2020 e 2022–2024), os custos são estimados aplicando o índice nacional de preços ao consumidor (CPI) de alimentos sobre o valor base de 2021. Isso explica por que as colunas de componentes alimentares (`cost_vegetables_ppp_usd`, `cost_fruits_ppp_usd` e `total_food_components_cost`) estão disponíveis apenas para 2021.

### 2.2 Descrição do Conjunto de Dados

**Dimensões:** 1.379 observações × 11 colunas

> Se todos os 175 países tivessem dados para todos os 8 anos do período: 175 × 8 = 1.400 linhas. O dataset contém 1.379 → 21 combinações país–ano não disponíveis, o que é esperado para países com dados insuficientes de CPI alimentar.

**Período coberto:** 2017 a 2024 (8 anos)  
**Cobertura geográfica:** 175 países

#### 2.2.1 Descrição dos Atributos

| Coluna | Tipo | Descrição |
|---|---|---|
| `country_code` | Numérica (inteiro) | Código numérico de país segundo a classificação ONU M49 |
| `country` | Categórica | Nome do país |
| `region` | Categórica | Região geográfica — **coluna com inconsistências** (ver seção 2.2.4) |
| `year` | Numérica (inteiro) | Ano de referência (2017–2024) |
| `cost_healthy_diet_ppp_usd` | Numérica (contínua) | Custo **diário** de uma dieta saudável em dólares PPP |
| `annual_cost_healthy_diet_usd` | Numérica (contínua) | Custo **anual** da dieta (365 × custo diário), em dólares nominais |
| `cost_vegetables_ppp_usd` | Numérica (contínua) | Custo diário dos vegetais na dieta — **disponível apenas para 2021** |
| `cost_fruits_ppp_usd` | Numérica (contínua) | Custo diário das frutas na dieta — **disponível apenas para 2021** |
| `total_food_components_cost` | Numérica (contínua) | Soma dos 6 grupos alimentares do detalhamento ICP — **disponível apenas para 2021, com valores corrompidos em 31 países** (ver seção 2.2.4) |
| `cost_category` | Categórica ordinal | Categorização do custo: `Low Cost` / `Medium Cost` / `High Cost` |
| `data_quality` | Categórica | Indicador de qualidade — valor único `"Estimated value"` para todas as 1.379 linhas (zero variância) |

#### 2.2.2 Distribuição da Variável-Alvo

A variável principal de análise é `cost_healthy_diet_ppp_usd` (custo diário da dieta em dólares PPP).

| Estatística | 2017 | 2024 |
|---|---|---|
| Mínimo | US$ 1,70 | US$ 2,56 |
| Média | US$ 3,14 | US$ 4,46 |
| Máximo | US$ 5,48 | US$ 8,39 |
| Variação acumulada (média) | — | **+42,1%** |
| Variação acumulada (mínimo) | — | **+50,6%** |

> O crescimento do **piso** (+50,6%) supera o crescimento da **média** (+42,1%), indicando que os países com custos diários mais baratos sofreram deterioração proporcionalmente maior — evidência de ampliação da vulnerabilidade alimentar nos países de menor renda.

![Histograma de distribuição do custo por dia](<Imagens/Histograma de distribuição do custo por dia.png>)!

#### 2.2.3 Distribuição por Categoria de Custo

A tabela abaixo mostra a evolução da distribuição de países por categoria ao longo do período. Em 2017, a maior parte dos países (127 de 175) tinha custo considerado médio. Em 2024, apenas 26 permaneciam nessa faixa, enquanto 145 já eram classificados como alto custo, e nenhum país registrou custo baixo.

| Ano | Low Cost | Medium Cost | High Cost |
|---|---|---|---|
| 2017 | 3 | 127 | 45 |
| 2018 | 2 | 123 | 47 |
| 2019 | 2 | 115 | 55 |
| 2020 | 1 | 101 | 70 |
| 2021 | 1 | 82 | 90 |
| 2022 | 0 | 47 | 125 |
| 2023 | 0 | 28 | 144 |
| 2024 | 0 | 26 | 145 |

Limiares de categorização (FAO): 
- **Low Cost** < US$ 2,00 
- **Medium Cost** US$ 2,00–3,50 
- **High Cost** > US$ 3,50

![Distribuição por categoria de custo](<Imagens/Gráfico de pizza com a distribuição de custo.png>)

#### 2.2.4 Valores Faltantes, Duplicatas e Inconsistências

| Verificação | Resultado | Observação |
|---|---|---|
| Linhas completamente duplicadas | 0 | Nenhuma duplicata encontrada. A chave composta `country_code + year` é única para todas as 1.379 linhas. |
| `cost_vegetables_ppp_usd`, `cost_fruits_ppp_usd`, `total_food_components_cost` | 1.213 valores faltantes (anos ≠ 2021) | Ausência estrutural esperada — colunas disponíveis apenas para o ano de referência ICP (2021). |
| `cost_category` | 11 valores faltantes (no arquivo original) | Tipo de *missing data*: **MAR** (*Missing At Random*) — ausência relacionada à variável observada `cost_healthy_diet_ppp_usd`, que está presente em todos os 11 registros, permitindo imputação direta. |
| `country_code`, `country`, `year` | Até 8 repetições por país | Esperado — estrutura longitudinal (*panel data*): 1 registro por combinação país–ano. |
| `data_quality` | Valor único: `"Estimated value"` | Zero variância — coluna sem poder informativo. Excluída do dashboard. |
| `total_food_components_cost` | 31 de 166 registros com valores corrompidos | Países como Brasil, China, Bélgica e Croácia apresentam valores na ordem de 10¹⁶, incompatíveis com qualquer custo alimentar real. Mediana plausível: US$ 1,50. Coluna excluída do dashboard. |
| `region` | 312 a 409 repetições por valor | **Coluna com inconsistência crítica:** países como Brasil, Japão e EUA estão mapeados para regiões geograficamente incorretas. A análise por região foi descartada (ver abaixo). |

As repetições nas colunas `country_code`, `country`, `year` e `region` são inerentes à estrutura longitudinal do dataset, em que cada observação representa um par país–ano único. A chave composta `country_code + year` é única para todas as 1.379 linhas, confirmando a ausência de duplicatas reais.

Os 11 valores faltantes em `cost_category` foram classificados como **MAR** (*Missing At Random*), pois sua ausência está relacionada a uma variável observada no próprio dataset (`cost_healthy_diet_ppp_usd`). A imputação foi realizada aplicando os limiares de categorização da FAO: Low Cost (< US$ 2,00), Medium Cost (US$ 2,00–3,50) e High Cost (> US$ 3,50).

**Inconsistência na coluna `region`:** a análise exploratória identificou que os países estão atribuídos a regiões geograficamente incorretas no dataset original — por exemplo, Brasil, Japão e Albânia foram agrupados como "África"; França e EUA como "Américas" e "Europa", respectivamente. A causa provável é um erro de codificação na origem dos dados, possivelmente baseado em intervalos numéricos do `country_code` em vez de classificação geográfica real. Diante disso, **a análise por região foi descartada** neste projeto. Para estudos futuros que dependam desse recorte, recomenda-se recriar a coluna `region` a partir de uma tabela de referência confiável (ex: ISO 3166, dados do Banco Mundial).

#### 2.2.5 Análise Temporal

O gráfico abaixo apresenta a evolução da soma do custo anual de todos os países entre 2017 e 2024. Entre 2017 e 2019, o crescimento foi moderado (+3,1%). A partir de 2020, os impactos da pandemia de COVID-19 e, posteriormente, do choque inflacionário de 2021–2022 aceleraram a trajetória de alta.

| Período | Custo total (soma) | Variação |
|---|---|---|
| 2017 | US$ 200.593 | — |
| 2018 | US$ 200.385 | −0,1% |
| 2019 | US$ 206.864 | +3,2% |
| 2020 | US$ 215.197 | +4,0% |
| 2021 | US$ 227.421 | +5,7% |
| 2022 | US$ 251.741 | +10,7% |
| 2023 | US$ 270.213 | +7,3% |
| 2024 | US$ 278.557 | +3,1% |

> Nota: 2018 registrou a única redução da série (−0,1%), sinalizando deflação alimentar pontual em alguns países antes da retomada de alta em 2019.

![Evolução do custo anual da dieta](<Imagens/Gráfico de linhas com a evolução do custo anual da dieta.png>)
---

## 3. Preparação dos Dados

### 3.1 Limpeza dos Dados

As seguintes etapas de limpeza foram realizadas sobre o arquivo original (CSV):

1. **Verificação de duplicatas:** nenhuma linha completamente duplicada foi encontrada. A chave composta `country_code + year` é única para todas as 1.379 observações, confirmando a integridade estrutural do dataset.

2. **Imputação de `cost_category`:** 11 registros apresentavam valor faltante na coluna `cost_category`. Classificados como **MAR**, foram imputados pela aplicação dos limiares da FAO sobre `cost_healthy_diet_ppp_usd` via fórmula condicional no Excel:  
   `=IFS(E2<=2;"Low Cost"; E2<=3,5;"Medium Cost"; E2>3,5;"High Cost")`  
   O arquivo com a imputação aplicada foi salvo como `.xlsx`, mantendo o `.csv` original para rastreabilidade.

3. **Exclusão de `data_quality`:** a coluna apresenta valor único (`"Estimated value"`) para todas as 1.379 linhas — zero variância e zero poder informativo. Excluída do dashboard no Power BI.

4. **Exclusão de `total_food_components_cost` do dashboard:** 31 dos 166 registros de 2021 com dados nessa coluna apresentam valores na ordem de 10¹⁶ (ex: Brasil = 1,36 × 10¹⁶), incompatíveis com qualquer custo alimentar real. A mediana da coluna é US$ 1,50 (plausível), mas a presença de valores corrompidos torna a média e qualquer agregação sem sentido. A coluna foi mantida no dataset para documentação, mas removida do dashboard.

5. **Descarte da análise por `region`:** inconsistências sistemáticas na atribuição de países a regiões inviabilizaram qualquer agrupamento geográfico baseado nessa coluna.

### 3.2 Dataset Final

| Dimensão | Valor |
|---|---|
| Número de linhas | 1.379 |
| Número de colunas utilizadas | 9 (excluídas `data_quality` e `total_food_components_cost` do dashboard) |
| Países cobertos | 175 |
| Período | 2017–2024 |

---

## 4. Modelagem

### 4.1 Abordagem Analítica

Dado o caráter exploratório e descritivo deste projeto, as técnicas aplicadas foram:

| Técnica | Objetivo |
|---|---|
| Análise descritiva (mín., média, máx.) | Caracterizar a distribuição global e temporal dos custos |
| Análise temporal (série de tempo) | Identificar tendências e quantificar impacto de eventos externos |
| Categorização ordinal | Classificar países em faixas de custo e acompanhar migração entre categorias |
| Visualização geográfica (mapa coroplético) | Comunicar disparidades espaciais entre países |
| Ranking de países | Identificar extremos de custo diário médio no período |

### 4.2 Análise Descritiva

As estatísticas descritivas abaixo referem-se à variável principal `cost_healthy_diet_ppp_usd` (custo diário, em dólares PPP):

| Estatística | Valor (todos os anos) |
|---|---|
| Média geral | US$ 3,68/dia |
| Custo anual médio geral | US$ 1.342/ano |
| Mínimo absoluto (2017) | US$ 1,70/dia |
| Máximo absoluto (2024) | US$ 8,39/dia |

**Países com maior custo diário médio (2017–2024):**

| Ranking | País | Custo médio diário (PPP) |
|---|---|---|
| 1º | Japão | US$ 6,26 |
| 2º | Guiana | US$ 5,70 |
| 3º | República da Coreia | US$ 5,55 |
| 4º | Mongólia | US$ 5,43 |
| 5º | Suriname | US$ 5,28 |

**Países com menor custo diário médio (2017–2024):**

| Ranking | País | Custo médio diário (PPP) |
|---|---|---|
| 1º | Reino Unido | US$ 2,04 |
| 2º | Bélgica | US$ 2,36 |
| 3º | EUA | US$ 2,42 |
| 4º | Irlanda | US$ 2,44 |
| 5º | Áustria | US$ 2,47 |

> Importante: o custo mais alto em PPP não indica necessariamente menor acessibilidade. Países de alta renda como Japão e Coreia têm custos elevados em PPP porque seus sistemas alimentares são sofisticados e os preços refletem alto padrão de qualidade — muito diferente do Sul do Sudão, que atingiu o maior custo diário em 2024 (US$ 8,39) em contexto de crise humanitária.

### 4.3 Análise Temporal

A evolução do custo anual (soma de todos os países) revela três fases distintas:

**Fase 1 — Estabilidade (2017–2019):** o custo total oscilou entre US$ 200.385 e US$ 206.864, com crescimento acumulado de apenas 3,1%. O ano de 2018 registrou a única redução de toda a série (−0,1%), indicando deflação alimentar pontual em parte dos países.

**Fase 2 — Aceleração pós-pandemia (2020–2021):** os impactos da COVID-19 sobre cadeias de abastecimento e logística global elevaram o custo total de US$ 215.197 (2020) para US$ 227.421 (2021), crescimento de +5,7%.

**Fase 3 — Choque inflacionário (2022–2023):** o período de maior aceleração. O custo saltou de US$ 227.421 (2021) para US$ 251.741 (2022), alta de **+10,7% em um único ano** — o maior crescimento anual da série. Em 2023, o crescimento desacelerou para +7,3%, sugerindo acomodação dos preços.

**2024:** crescimento de +3,1%, o menor desde 2018, indicando possível estabilização — embora o custo acumulado já seja 38,9% superior ao de 2017.

A liderança do custo diário por ano confirma que o **Japão liderou de 2017 a 2023** com custo diário crescendo de US$ 5,48 para US$ 7,29. Em 2024, o **Sul do Sudão** assumiu o topo com US$ 8,39/dia (vs. US$ 8,38 do Japão), refletindo dinâmicas completamente distintas: no Japão, custo alto por sofisticação do sistema alimentar; no Sul do Sudão, custo alto por colapso de cadeias de suprimento em contexto de crise humanitária.

### 4.4 Análise de Categorias

A migração de países entre categorias de custo ao longo do período é um dos achados mais expressivos:

- Em **2017**: 3 países em Low Cost, 127 em Medium Cost, 45 em High Cost.
- Em **2022**: nenhum país em Low Cost, 47 em Medium Cost, 125 em High Cost.
- Em **2024**: nenhum país em Low Cost, 26 em Medium Cost, 145 em High Cost.

Entre 2017 e 2024, **100 países migraram de Medium Cost para High Cost**, e os 3 países que estavam em Low Cost em 2017 subiram para Medium ou High Cost. O choque inflacionário de 2022 foi o principal responsável pela aceleração dessa migração: naquele ano, 78 países cruzaram o limiar de US$ 3,50/dia e foram recategorizados como High Cost.

---

## 5. Avaliação

### 5.1 Resultados e Principais Achados

- **Achado 1 – Tendência global:** o custo médio diário de uma dieta saudável cresceu **42,1%** entre 2017 e 2024 (de US$ 3,14 para US$ 4,46), com aceleração notável entre 2021 e 2022 (+11,3% em um único ano).

- **Achado 2 – Deterioração do piso:** o custo mínimo registrado cresceu **50,6%** no período (de US$ 1,70 para US$ 2,56), superando o crescimento médio. Isso indica que os países mais baratos sofreram deterioração proporcionalmente maior, ampliando a vulnerabilidade alimentar nas economias mais frágeis.

- **Achado 3 – Impacto dos eventos macroeconômicos:** a pandemia de 2020 e o pico inflacionário de 2022 produziram impactos mensuráveis e distintos. A pandemia elevou os custos em +5,7% (2020–2021), enquanto a inflação global de 2022 gerou o maior salto anual da série (+10,7%). Em 2024, o crescimento desacelerou para +3,1%, sugerindo acomodação.

- **Achado 4 – Colapso da acessibilidade:** em 2017, apenas 45 países (26%) tinham dieta classificada como High Cost. Em 2024, esse número chegou a 145 (83%), e nenhum país permaneceu na categoria Low Cost. A faixa intermediária (Medium Cost) praticamente desapareceu, passando de 127 para 26 países.

- **Achado 5 – Dupla natureza do alto custo:** o país com maior custo diário variou entre Japão (2017–2023) e Sul do Sudão (2024), revelando que custos elevados em PPP podem refletir tanto riqueza e sofisticação alimentar quanto crise humanitária e colapso logístico — contextos opostos que o indicador de custo isolado não distingue.

### 5.2 Avaliação em Relação aos Objetivos

| Questão orientadora | Respondida? | Síntese |
|---|---|---|
| Evolução global 2017–2024 | ✅ | Crescimento de 42,1% na média diária, com três fases distintas: estabilidade (2017–2019), aceleração pós-pandemia (2020–2021) e choque inflacionário (2022–2023). |
| Países com maior aumento | ✅ | Análise de ranking por custo médio: Japão lidera 2017–2023; Sul do Sudão assume em 2024 por razões opostas (crise vs. sofisticação). |
| Impacto da pandemia e inflação | ✅ | Pandemia: +5,7% (2020→2021). Inflação de 2022: +10,7% — maior crescimento anual da série. |
| Acessibilidade alimentar | ✅ | 100 países migraram de Medium para High Cost entre 2017 e 2024. Em 2022, nenhum país permaneceu em Low Cost. |
| Análise por região | ❌ | Descartada por inconsistências sistemáticas na coluna `region` do dataset original. Requer recodificação com fonte externa para estudos futuros. |

### 5.3 Limitações

- O dataset não inclui dados de consumo real da população, apenas o custo estimado de uma dieta teoricamente mínima.
- A coluna `region` apresenta inconsistências que inviabilizaram a análise geográfica agregada. Para superar essa limitação, seria necessário recriar a variável a partir de uma tabela de referência como ISO 3166 ou dados do Banco Mundial.
- A coluna `total_food_components_cost` contém valores corrompidos para 31 dos 166 países com dados de 2021, tornando qualquer análise baseada nessa coluna não confiável sem tratamento adicional.
- As colunas de componentes alimentares (`cost_vegetables_ppp_usd`, `cost_fruits_ppp_usd`) estão disponíveis apenas para 2021, limitando análises de composição da dieta a um único ponto no tempo.
- A metodologia FAO assume uma dieta de menor custo possível — não necessariamente representativa dos padrões culturais ou nutricionais de cada país.
- Comparações de acessibilidade com dados de renda per capita requerem cruzamento com fontes externas (Banco Mundial), o que introduz possível defasagem temporal.

### 5.4 Conclusão

Entre 2017 e 2024, o custo global de uma dieta saudável cresceu 42,1%, com impactos desproporcionais sobre os países mais vulneráveis — cujo custo mínimo aumentou 50,6% no mesmo período. O choque inflacionário de 2022 foi o evento de maior impacto isolado da série, responsável por mover 78 países da faixa Medium para High Cost em apenas um ano. Em 2024, 145 dos 175 países analisados (83%) classificavam-se como High Cost, e nenhum permanecia em Low Cost.

Esses resultados têm implicações diretas para a **ODS 2 (Fome Zero)**: o acesso universal a uma dieta saudável, já desafiador em 2017, tornou-se ainda mais distante ao longo do período analisado. Os dados reforçam a urgência de políticas públicas que combinem suporte às cadeias alimentares locais, proteção social para populações de baixa renda e estratégias de mitigação de choques inflacionários sobre alimentos básicos — ações igualmente relevantes para as **ODS 1** (erradicação da pobreza), **ODS 3** (saúde e bem-estar) e **ODS 10** (redução das desigualdades).

---

## 6. Referências

- Food and Agriculture Organization of the United Nations (FAO). (2025). *Cost and Affordability of a Healthy Diet (CoAHD) Database*. FAOSTAT. Disponível em: https://www.fao.org/faostat
- FAO, IFAD, UNICEF, WFP & WHO. (2025). *The State of Food Security and Nutrition in the World 2025*. Rome: FAO.
- United Nations. *Transforming our world: the 2030 Agenda for Sustainable Development*. Resolução A/RES/70/1. Disponível em: https://sdgs.un.org/goals
- Kaggle. *Global Price of Healthy Diet Dataset*. Disponível em: https://www.kaggle.com/datasets/ibrahimshahrukh/global-price-of-healthy-diet-dataset
