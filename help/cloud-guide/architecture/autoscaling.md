---
title: Ridimensionamento automatico
description: Scopri come Adobe Commerce sull’infrastruttura cloud può essere scalato per soddisfare le richieste di risorse.
feature: Cloud, Auto Scaling
topic: Architecture
exl-id: 11bfde40-79d1-4d51-9233-150c4cfb80fd
TQID: https://experienceleague.adobe.com/uL--0lHHJ-4SN3BkFU8reAefWhpMQOLBRVG7fX3jTM8
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
subfeature_v2:
  - id: db6b6496-d1b5-4ad4-9e18-dea78dae3aa8
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: d863fc70609dcc66d21eb95e709db80e29114714
workflow-type: tm+mt
source-wordcount: 605
ht-degree: 0%

---

# Ridimensionamento automatico

Il ridimensionamento automatico aggiunge o rimuove automaticamente le risorse all’infrastruttura cloud per mantenere prestazioni ottimali e costi ragionevoli. Attualmente, questa funzione è disponibile solo per i progetti configurati con [Architettura ridimensionata](scaled-architecture.md).

## Nodi del server web

Il [livello Web](scaled-architecture.md#web-tier) viene ridimensionato per soddisfare un aumento delle richieste di elaborazione e requisiti di traffico più elevati. Attualmente, la funzione di ridimensionamento automatico viene ridimensionata solo orizzontalmente aggiungendo o rimuovendo nodi del server web.

Un evento di ridimensionamento automatico si verifica quando l’utilizzo e il traffico di CPU raggiungono una soglia predefinita:

- **Nodi aggiunti**: CPU/core in tutti i nodi Web attivi hanno una capacità del 75% per 1 minuto e il traffico aumenta del 20% per 5 minuti consecutivi.
- **Nodi rimossi**: CPU/core in tutti i nodi Web attivi vengono caricati al 60% per 20 minuti. I nodi vengono rimossi nell’ordine in cui sono stati aggiunti.

Le soglie minima e massima sono determinate e impostate in base ai limiti delle risorse contrattuali di ciascun commerciante; ciò riduce il rischio di scalabilità infinita.

## Monitorare le soglie con New Relic

È possibile utilizzare il servizio [New Relic](../monitor/new-relic-service.md) per monitorare determinate soglie, ad esempio il numero di host e l&#39;utilizzo di CPU. Le query New Relic seguenti utilizzano una notazione variabile per `cluster-id` solo a scopo esemplificativo.

>[!TIP]
>
>Per un riferimento sulla creazione di query, vedere [Sintassi NRQL, clausole e funzioni](https://docs.newrelic.com/docs/query-your-data/nrql-new-relic-query-language/get-started/nrql-syntax-clauses-functions/) nella documentazione di _New Relic_.
>Utilizza le tue query per creare una [dashboard di New Relic](https://docs.newrelic.com/docs/query-your-data/explore-query-data/dashboards/introduction-dashboards/).

### Numero di host

L’esempio di query New Relic che segue mostra il conteggio degli host all’interno dell’ambiente:

```sql
SELECT uniqueCount(SystemSample.entityId) AS 'Infrastructure hosts', uniqueCount(Transaction.host) AS 'APM hosts seen' FROM SystemSample, Transaction where (Transaction.appName = 'cluster-id_stg' AND Transaction.transactionType = 'Web') OR SystemSample.apmApplicationNames LIKE '%|cluster-id_stg|%' TIMESERIES SINCE 3 HOURS AGO
```

Nella schermata seguente, **Host APM visualizzati** si riferisce al numero di host con transazioni registrate durante il periodo selezionato.

![Numero host New Relic](../../assets/new-relic/host-count.png)

### Utilizzo di CPU

L’esempio di query New Relic seguente mostra l’utilizzo di CPU per i nodi web:

```sql
SELECT average(cpuPercent) FROM SystemSample FACET hostname, apmApplicationNames WHERE instanceType LIKE 'c%' TIMESERIES SINCE 3 HOURS AGO
```

![Nodi Web New Relic - Utilizzo CPU](../../assets/new-relic/web-node-cpu-usage.png)

## Abilita ridimensionamento automatico

Per abilitare o disabilitare il ridimensionamento automatico per il progetto di infrastruttura cloud Adobe Commerce, [Invia un ticket di supporto Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html?lang=it#submit-ticket). Scegli i seguenti motivi nel ticket:

- **Motivo contatto**: richiesta di modifica dell&#39;infrastruttura
- **Motivo del contatto per l&#39;infrastruttura Adobe Commerce**: altra richiesta di modifica dell&#39;infrastruttura

>[!IMPORTANT]
>
>La funzione di ridimensionamento automatico acquisisce gli eventi imprevisti. Anche se è stato abilitato il ridimensionamento automatico, Adobe consiglia di continuare a [Inviare un ticket di supporto Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html?lang=it#submit-ticket) se si prevede un evento imminente.

### Test di carico

Adobe abilita prima il ridimensionamento automatico nel cluster _staging_ del progetto cloud. Dopo aver eseguito e completato il test di carico nell’ambiente, Adobe abilita il ridimensionamento automatico nel cluster di produzione. Per informazioni sul test di carico, vedere [Test delle prestazioni](../launch/checklist.md#performance-testing).

### IP

Dopo aver abilitato il ridimensionamento automatico, il traffico del nodo web in uscita proviene dagli indirizzi IP dei nodi di servizio. Se utilizzi un elenco Consentiti di con un servizio di terze parti che non è incluso nel pacchetto con il progetto Adobe Commerce on Cloud Infrastructure, verifica gli indirizzi IP nel inserisco nell&#39;elenco Consentiti di  del servizio di terze parti.

Ad esempio:

- Se il inserisco nell&#39;elenco Consentiti di contiene gli indirizzi IP dei nodi di servizio (1, 2 e 3), non è richiesta alcuna azione.
- Se il inserisco nell&#39;elenco Consentiti di contiene gli indirizzi IP per i nodi di servizio (1, 2 e 3) e i nodi web (4, 5 e 6), in questo caso tutti e sei i nodi, non è richiesta alcuna azione.
- Se il inserisco nell&#39;elenco Consentiti di contiene gli indirizzi IP _only_ per i nodi Web (4, 5 e 6), è necessario aggiornare il inserisco nell&#39;elenco Consentiti di per includere gli indirizzi IP per i nodi di servizio.

