# Catálogo de Dados — OONI (MVP)

## Tabela: bronze_ooni

**Descrição:**  
Dados brutos coletados da API do OONI, sem regras de negócio aplicadas.

| Campo | Tipo | Descrição |
|------|------|-----------|
| measurement_uid | string | Identificador único da medição |
| measurement_start_time | timestamp | Data/hora da medição |
| test_name | string | Tipo de teste (web_connectivity, whatsapp, telegram, facebook_messenger) |
| anomaly | boolean | Indica anomalia detectada |
| confirmed | boolean | Bloqueio confirmado |
| failure | boolean | Falha na medição |
| probe_cc | string | País do probe (ISO-3166) |
| probe_asn | string | ASN do provedor |
| report_id | string | ID do relatório |
| measurement_url | string | URL da medição bruta |
| scores | struct | Resultados técnicos detalhados |
| country | string | País (derivado) |
| year | integer | Ano da medição (derivado) |

Camada: **Bronze**  
Formato: **JSON**

---

## Tabela: silver_ooni

**Descrição:**  
Dados limpos e padronizados, com JSON achatado e campos relevantes selecionados.

| Campo | Tipo | Descrição |
|------|------|-----------|
| measurement_uid | string | Identificador da medição |
| measurement_date | date | Data da medição |
| test_name | string | Tipo de teste |
| anomaly | boolean | Anomalia detectada |
| confirmed | boolean | Bloqueio confirmado |
| failure | boolean | Falha |
| probe_cc | string | País |
| probe_asn | string | ASN |
| blocking_global | double | Score de bloqueio global |
| blocking_isp | double | Score de bloqueio por ISP |
| blocking_local | double | Score de bloqueio local |
| year | integer | Ano |

Camada: **Silver**  
Formato: **Parquet / Delta**

---

## Tabela: gold_censorship_summary

**Descrição:**  
Tabela analítica agregada para responder perguntas de negócio.

| Campo | Tipo | Descrição |
|------|------|-----------|
| country | string | País |
| test_name | string | Tipo de serviço/teste |
| year | integer | Ano |
| total_measurements | long | Total de medições |
| anomaly_count | long | Total de anomalias |
| confirmed_blocked_count | long | Bloqueios confirmados |
| anomaly_rate | double | Percentual de anomalias |

Camada: **Gold**  
Formato: **Delta / Tabela SQL**
