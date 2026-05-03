# 📊 Modelagem Dimensional — Star Schema com Financial Sample

## 🎯 Objetivo

Este projeto tem como objetivo a construção de um modelo dimensional no formato **Star Schema**, utilizando a base **Financial Sample**, com foco na análise de dados de vendas no Power BI.

A proposta consiste em transformar uma tabela única (modelo relacional) em um modelo analítico estruturado, facilitando consultas, melhorando a performance e permitindo análises multidimensionais.

---

## 🧠 Contexto do Projeto

Este projeto foi desenvolvido como parte do **desafio do módulo 4 da Formação Power BI Analyst**, da DIO (Digital Innovation One).

O foco do desafio foi aplicar conceitos de:

* Modelagem dimensional
* Criação de tabelas fato e dimensão
* Transformações no Power Query (ETL)
* Uso de DAX para análise temporal

Aqui está o ponto-chave:
o projeto demonstra a capacidade de transformar dados operacionais em um modelo analítico eficiente.

---

## ⭐ Estrutura do Modelo

O modelo foi construído no padrão **Star Schema**, composto por:

* 1 tabela fato (central)
* múltiplas tabelas dimensão (descritivas)

---

## 🟡 Tabela Fato

### `F_Vendas`

Tabela central responsável por armazenar os eventos de vendas.

Contém:

* SK_ID (chave substituta)
* ID_Produto
* Produto
* Units Sold
* Sale Price
* Discount Band
* Segment
* Country
* Sales
* Profit
* Date

Essa estrutura permite análises como:

👉 vendas por produto
👉 desempenho por país
👉 análise por segmento
👉 evolução temporal

---

## 🔵 Tabelas Dimensão

As dimensões foram criadas a partir da tabela original, selecionando e organizando os dados relevantes:

### `D_Produtos`

* ID_produto
* Produto
* Média de unidades vendidas
* Média de vendas
* Mediana de vendas
* Valor máximo e mínimo de vendas

### `D_Produtos_Detalhes`

* ID_produto
* Discount Band
* Sale Price
* Units Sold
* Manufacturing Price

### `D_Descontos`

* ID_produto
* Discount
* Discount Band

### `D_Detalhes`

Tabela complementar com informações não contempladas nas demais dimensões.

---

## 🧩 Criação da Chave Substituta (SK_ID)

Foi criada uma chave substituta (`SK_ID`) a partir da combinação de colunas:

* Product
* Country
* Segment
* Sales

### Processo:

1. Criação de uma tabela auxiliar (`D_Detalhes_aux`)
2. Geração de uma chave textual combinando os campos
3. Remoção de duplicatas
4. Criação de índice (SK_ID)
5. Mesclagem com a tabela fato (`F_Vendas`)

👉 Isso permitiu criar um relacionamento do tipo:

```text
F_Vendas (N) → (1) D_Detalhes_aux
```

---

## 📅 Dimensão de Datas (DAX)

Foi criada uma tabela de calendário utilizando DAX:

```DAX
Calendar = CALENDARAUTO(12)
```

---

## 🧠 Colunas derivadas com DAX

```DAX
Day of the week = WEEKDAY('Calendar'[Date])
```

```DAX
Day of the week 2 = FORMAT('Calendar'[Date], "DDDD")
```

```DAX
Month Number = MONTH('Calendar'[Date])
```

```DAX
Month Name = FORMAT(DATE(1,'Calendar'[Month Number],1), "MMM")
```

```DAX
MonthYear = FORMAT('Calendar'[Date], "MM-YYYY")
```

```DAX
Week Number = WEEKNUM('Calendar'[Date])
```

```DAX
Year = YEAR('Calendar'[Date])
```

👉 Essas colunas permitem análises temporais mais completas.

---

## ⚡ Etapas do Projeto

O desenvolvimento seguiu as seguintes etapas:

1. Criação de cópia da tabela original (`Financials_origem`)
2. Separação em tabelas dimensão
3. Criação da tabela fato (`F_Vendas`)
4. Construção de chave substituta (SK_ID)
5. Criação de dimensão de datas com DAX
6. Definição de relacionamentos (Star Schema)
7. Organização do modelo para análise

---

## 🧠 Tecnologias Utilizadas

* Power BI
* Power Query (M)
* DAX (Data Analysis Expressions)
* Modelagem Dimensional

---

## ⚡ Benefícios do Modelo

* Melhor desempenho em consultas
* Organização clara dos dados
* Facilidade de análise
* Estrutura otimizada para BI

---

## 🧠 Aprendizados

Durante o desenvolvimento, foram aplicados conceitos fundamentais como:

* Transformação de modelo relacional em dimensional
* Criação de chaves substitutas
* Uso de funções DAX
* Estruturação de dados para análise

---

## 🚀 Possíveis Evoluções

* Criação de dashboards analíticos
* Implementação de medidas avançadas em DAX
* Otimização de performance
* Separação de dimensões mais granular

---

## 🔗 Autor

**Bianca Esteves**
Analista de BI | Dados e Processos

📧 Email: [biancaaesteves@icloud.com](mailto:biancaaesteves@icloud.com)
💼 LinkedIn: [https://www.linkedin.com/in/biancaaesteves](https://www.linkedin.com/in/biancaaesteves)

---

## 🏷️ Tags

`#PowerBI` `#DataAnalytics` `#StarSchema` `#DataModeling` `#BusinessIntelligence`

---

## 💙 Considerações Finais

Este projeto demonstra a importância da modelagem de dados na construção de soluções de BI, destacando como uma estrutura bem definida impacta diretamente na performance e na qualidade das análises.
