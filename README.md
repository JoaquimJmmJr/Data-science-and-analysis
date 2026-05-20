# Portfólio de Projetos em Dados
**Joaquim Jonkel Magalhães Melo Junior**

> Estudante de Engenharia de Robôs (FEI) com atuação prática em análise de dados, tratamento de qualidade de dados e geração de insights orientados à decisão. Os projetos aqui reunidos demonstram domínio do ciclo completo de análise de dados — da aquisição e limpeza à modelagem, visualização e comunicação de resultados.

---

## Projetos

### Análise Global do Custo de uma Dieta Saudável (2017–2024)

**Tecnologias:** Python · Pandas · Power BI · Excel · CRISP-DM  
**Dados:** FAO/FAOSTAT · 175 países · 8 anos · 1.379 observações  
**ODS:** 2 (Fome Zero) · 1 (Pobreza) · 3 (Saúde) · 10 (Desigualdades)

Análise exploratória estruturada pelo framework **CRISP-DM** sobre o custo global de uma dieta saudável, com dados oficiais da Organização das Nações Unidas para Alimentação e Agricultura (FAO). O projeto abrange todo o ciclo analítico: entendimento do problema, aquisição e qualidade dos dados, preparação, modelagem descritiva e avaliação de resultados.

**Destaques técnicos:**

- Identificação e tratamento de **dados corrompidos** em coluna numérica (valores na ordem de 10¹⁶ em 31 países) e documentação metodológica da exclusão.
- Classificação e imputação de valores faltantes por tipo de *missing* (**MAR** — *Missing At Random*), com justificativa estatística e reprodução dos limiares de categorização originais da FAO.
- Diagnóstico de **inconsistência sistemática** na coluna de região geográfica (países mapeados para continentes incorretos), com decisão fundamentada de descarte da análise regional.
- Análise de **estrutura longitudinal** (*panel data*): distinção entre repetições esperadas e duplicatas reais por chave composta `country_code + year`.
- Identificação e correção de **média de médias** (*unweighted average of group means*) em KPIs do dashboard, com implementação de medida DAX corretiva (`CALCULATE + ALL`).
- Dashboard interativo em **Power BI** com mapa coroplético, série temporal anotada com eventos macroeconômicos, ranking de países por gradiente de cores e análise de distribuição categórica.

**Principais achados:**

- O custo médio diário de uma dieta saudável cresceu **42,1%** entre 2017 e 2024, com o maior salto anual em 2022 (+10,7%), reflexo do choque inflacionário global.
- O custo mínimo registrado cresceu **50,6%** — mais do que a média —, indicando que os países mais frágeis sofreram deterioração proporcionalmente maior.
- Em 2024, **145 de 175 países (83%)** foram classificados como *High Cost*, contra apenas 45 em 2017. Nenhum país permaneceu na faixa *Low Cost*.
- O alto custo em PPP não distingue contextos: Japão (sofisticação alimentar) e Sul do Sudão (crise humanitária) dividiram o topo em 2024 com valores praticamente idênticos ($8,38 e $8,39/dia).

[📂 Acessar projeto completo](<Projeto de Análise de Ciência de Dados com ODS>) · [📊 Ver relatório CRISP-DM](<Projeto de Análise de Ciência de Dados com ODS/README.md>)

---

### Análise Exploratória para Segmentação de Clientes

**Tecnologias:** Python · Pandas · Excel  
**Dados:** Dataset proprietário · 8.000+ registros · variáveis demográficas, socioeconômicas e comportamentais

Projeto de EDA (*Exploratory Data Analysis*) e ETL aplicado a dataset de grande volume, com foco em qualidade de dados e geração de insights para segmentação.

**Destaques técnicos:**

- Análise completa de qualidade: valores faltantes, duplicatas, inconsistências e outliers.
- Aplicação de técnicas de imputação e normalização com base na distribuição e características estatísticas das variáveis.
- Identificação de padrões de comportamento e segmentação de clientes para apoio à tomada de decisão.
- Documentação estruturada orientada à leitura por terceiros.

[📂 Acessar projeto completo](<Dataset de Segmentação de Clientes>)

---

## Competências Demonstradas nos Projetos

| Competência | Projetos |
|---|---|
| Qualidade e limpeza de dados (missing, outliers, duplicatas, corrupção) | Ambos |
| Estruturação de análises com framework (CRISP-DM) | ODS |
| Análise de dados longitudinais (*panel data*) | ODS |
| Classificação de tipos de *missing* (MCAR, MAR, MNAR) | ODS |
| Dashboard interativo e KPIs com Power BI + DAX | ODS |
| Interpretação de dados | Ambos |
| Documentação técnica clara e orientada ao negócio | Ambos |
---

## Estrutura do Repositório

```
├── Projeto de Análise de Dados com ODS/
│   ├── base de dados/
│   │   ├── price_of_healthy_diet_clean.csv      ← dataset original (bruto)
│   │   └── price_of_healthy_diet_clean.xlsx     ← pós-processamento (imputação)
│   ├── Imagens/
│   │   ├── histograma de distribuição do custo por dia.png
│   │   ├── distribuição por categoria.png
│   │   └── evolução do custo anual.png
│   ├── Custo de uma dieta saudável (2017-2024).pbix   ← dashboard Power BI
│   └── README.md                                      ← relatório CRISP-DM completo
├── Dataset de Segmentação de Clientes/
|   ├── Análise Exploratória de Dados para Segmentação de Clientes.pdf
|   ├── Dados para Segmentação de Clientes.xlsx        ← dataset utilizado (pós-processamento)
│   └── README.md                                      ← relatório EDA
└── README.md                                          
```

---

## Sobre

**Formação:** Engenharia de Robôs — Centro Universitário FEI (9º semestre, noturno)  
**Localização:** São Bernardo do Campo – SP  
**Disponibilidade:** Imediata para estágio ou atuação efetiva  
**Idiomas:** Inglês avançado · Francês básico · Libras básico

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Joaquim%20Jonkel-blue)](https://linkedin.com/in/joaquim-jonkel-magalh%C3%A3es-melo-junior) 
[![GitHub](https://img.shields.io/badge/GitHub-JoaquimJmmJr-black)](https://github.com/JoaquimJmmJr)
