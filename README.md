# MVP – Pipeline de Dados OONI (Databricks)

Este projeto implementa um **pipeline completo de Engenharia de Dados** utilizando **Databricks e Apache Spark**, com o objetivo de analisar interferências de rede (censura e bloqueios de acesso à internet) a partir dos dados públicos do **Observatório Aberto de Interferência de Rede (OONI)**.

O pipeline contempla as etapas de **busca, coleta, modelagem, carga e análise**, conforme os requisitos do trabalho.

---

## 🎯 Objetivo

O objetivo do MVP é estruturar e disponibilizar dados do OONI em um modelo analítico (Data Warehouse) que permita responder, via SQL, perguntas relacionadas a:

- Comparação regional de censura na América Latina  
- Análise temporal de eventos de bloqueio  
- Identificação de provedores (ASNs) com maior incidência de anomalias no Brasil  
- Avaliação da qualidade e completude dos dados  

A descrição completa do problema e das perguntas de negócio está disponível em:  
📄 [`docs/objetivos.md`](docs/objetivos.md)

---

## 🏗️ Arquitetura do Pipeline

O pipeline segue a arquitetura **Bronze → Silver → Gold**:

- **Bronze**: ingestão dos dados brutos da API do OONI (JSON)
- **Silver**: limpeza, tipagem, deduplicação e flatten dos dados
- **Gold**: modelagem em esquema estrela e criação de tabelas analíticas
- **Análise**: qualidade dos dados e solução das perguntas de negócio

---

## 📊 Catálogo de Dados

A descrição dos atributos, domínios, regras de qualidade e linhagem dos dados está documentada no catálogo:

📘 [`docs/catalogo-dados.md`](docs/catalogo-dados.md)

---

## 📒 Notebooks

Os notebooks abaixo representam cada etapa do pipeline:

- `01_bronze_ingest_ooni.ipynb` – Coleta e ingestão dos dados (Bronze)
- `02_silver_transform_ooni.ipynb` – Limpeza e transformação (Silver)
- `03_gold_model_ooni.ipynb` – Modelagem analítica (Gold)
- `Análise.ipynb` – Qualidade dos dados e respostas às perguntas de negócio

---

## 🧪 Plataforma

- Databricks Community Edition  
- Apache Spark  
- Delta Lake  
- SQL e PySpark  

---

## 📌 Observações

- Os dados utilizados são públicos e disponibilizados pelo OONI.
- Evidências de execução e resultados analíticos podem ser encontradas no próprio notebook de análise e/ou em capturas de tela incluídas no repositório.

---
