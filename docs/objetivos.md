# MVP ENG. DADOS

## Problema a Ser Resolvido

A opacidade e a dificuldade analítica em rastrear e quantificar a interferência de rede  
(censura, bloqueio de sites e aplicativos) em escala global e regional. Dados como os  
fornecidos pelo Observatório Aberto de Interferência de Rede (OONI) são volumosos,  
amplamente distribuídos e, frequentemente, em formato JSON semi-estruturado. A  
ausência de um pipeline de Engenharia de Dados robusto e de um modelo de dados  
otimizado (Data Warehouse) impede a análise comparativa ágil e a geração de insights  
acionáveis sobre as tendências de bloqueio e a responsabilidade dos provedores de  
internet (ISPs).

![Arquitetura do pipeline](arquitetura.png)

O objetivo deste MVP é construir um pipeline completo de Engenharia de Dados utilizando  
a plataforma Databricks/Spark para coletar, transformar e modelar as medições do OONI  
do Brasil, garantindo que a informação seja acessível via SQL para responder a questões  
críticas sobre a liberdade de acesso à internet na região.

## Perguntas de Negócio a Serem Respondidas

As perguntas abaixo guiarão a Modelagem de Dados (Esquema Estrela) e a Análise  
(Solução do Problema).

1. Comparação de Censura Regional: Quais são os sites e/ou aplicativos (ex:  
   Telegram, WhatsApp) mais consistentemente bloqueados ou com maior taxa de  
   anomalias por país na América Latina no último ano? A taxa de anomalias  
   observada no Brasil está acima ou abaixo da média regional?

2. Impacto Temporal: Existe uma correlação estatística entre períodos de grandes  
   eventos cívicos/políticos e picos no volume de medições de censura bem-sucedidas  
   (confirmed_blocked=true) em países-chave?

3. Análise de Provedores: Quais são os provedores de internet (ASNs) específicos  
   no Brasil que registram o maior percentual de resultados anômalos, indicando  
   possível interferência na rede?

4. Qualidade dos Dados: Qual a taxa de completude e consistência dos metadados  
   de localização (probe_cc, probe_asn) nos dados brutos, e quais transformações  
   de qualidade de dados foram implementadas no ETL para mitigar inconsistências?
