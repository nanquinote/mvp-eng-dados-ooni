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

## 3. Camada Gold
**Descrição:** Tabelas agregadas para consumo analítico.

### Tabela: `gold_anomalias`
*Agregação por país e teste.*
* `probe_cc`, `test_name`, `total_medicoes`, `qtd_anomalias`, `taxa_anomalia`.

### Tabela: `gold_confirmed`
*Foco em bloqueios confirmados.*
* `probe_cc`, `test_name`, `total_medicoes`, `qtd_confirmed_blocked`, `taxa_confirmed_blocked`.

### Tabela: `gold_isps_br`
*Ranking de provedores no Brasil.*
* `probe_asn`, `total_medicoes`, `qtd_anomalias`, `taxa_anomalia`.

### Tabela: `gold_temporal`
*Evolução anual por país.*
* `year`, `probe_cc`, `test_name`, `total_medicoes`, `qtd_anomalias`, `taxa_anomalia`.
