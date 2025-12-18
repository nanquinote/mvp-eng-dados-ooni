# Catálogo de Dados — OONI 

## 1. Camada Bronze
**Tabela:** `bronze_ooni`  
**Origem:** API OONI (JSON)  
**Particionamento:** `country`, `year`

| Campo | Tipo | Descrição |
| :--- | :--- | :--- |
| measurement_uid | string | Identificador único da medição |
| measurement_start_time | string | Timestamp original da API |
| probe_cc | string | Código do país (ISO-3166) |
| probe_asn | string | ASN do provedor de internet |
| test_name | string | Nome do teste (ex: whatsapp, telegram) |
| anomaly | boolean | Indica se houve anomalia |
| confirmed | boolean | Indica bloqueio confirmado |
| failure | boolean | Indica falha na execução do teste |
| scores | struct | Objeto contendo métricas de bloqueio |

---

## 2. Camada Silver
**Tabela:** `silver_ooni`  
**Transformações:** Tipagem de data, tratamento de nulos em scores e criação de flag booleana de bloqueio.

| Campo | Tipo | Descrição |
| :--- | :--- | :--- |
| measurement_uid | string | Identificador único |
| measurement_start_time | timestamp | Data e hora normalizada |
| probe_cc | string | Código do país |
| probe_asn | string | ASN do provedor |
| test_name | string | Nome do teste |
| anomaly | boolean | Flag de anomalia |
| confirmed | boolean | Flag de confirmação original |
| failure | boolean | Flag de falha |
| blocking_country | double | Score de bloqueio nacional (Default 0.0) |
| blocking_isp | double | Score de bloqueio por ISP (Default 0.0) |
| blocking_global | double | Score de bloqueio global (Default 0.0) |
| confirmed_blocked | boolean | Bloqueio validado (confirmed == True) |

---

# Catálogo de Dados - Camada Gold (Star Schema)

## Tabela de Fato: fact_measurements
**Descrição:** Contém as métricas individuais de cada medição realizada.

| Campo | Tipo | Domínio / Valores Esperados | Descrição |
| :--- | :--- | :--- | :--- |
| measurement_uid | String | UUID único | Identificador da medição |
| measurement_start_time | Timestamp | 2018-01-01 a 2024-12-31 | Data e hora do início do teste |
| anomaly | Boolean | true, false | Indica se houve comportamento anômalo |
| confirmed | Boolean | true, false | Indica se o bloqueio foi confirmado |
| failure | Boolean | true, false | Indica se o teste falhou tecnicamente |
| fk_country | String | ISO-3166 (ex: 'BR', 'AR', 'VE') | Chave para dim_country |
| fk_test | String | 'web_connectivity', 'whatsapp', etc | Chave para dim_test |

## Tabela de Dimensão: dim_isp
**Descrição:** Atributos dos Provedores de Internet (ISPs).

| Campo | Tipo | Domínio / Valores Esperados | Descrição |
| :--- | :--- | :--- | :--- |
| probe_asn | String | Prefixo 'AS' + número (ex: 'AS28573') | Sistema Autônomo do Provedor |
| isp_name | String | Nomes comerciais | Nome do provedor identificado |

---

## Linhagem e Transformação
1. **Origem:** OONI API (JSON).
2. **Bronze:** Persistência direta do JSON em sistema de arquivos.
3. **Silver:** Limpeza de nulos e normalização de timestamps via Spark.
4. **Gold:** Decomposição da tabela Silver em Fatos e Dimensões para otimização de consultas SQL e suporte ao Esquema Estrela.
