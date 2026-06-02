---
title: Acquisizione dei dati
description: Scopri come visualizzare e gestire l’acquisizione dei dati di Commerce in New Relic.
feature: Cloud, Observability
exl-id: b457b4de-deeb-4e92-b95a-c2b89d6f7a05
TQID: https://experienceleague.adobe.com/60hhI0IvazUSrw6cCRoXfbGjA4fkLLPXb8Q4Q08AqeE
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: fd3ef8201c368f889344452e334976070a6c7157
workflow-type: tm+mt
source-wordcount: 209
ht-degree: 0%

---

# Acquisizione dei dati

New Relic dipende dai dati avanzati per fornire un monitoraggio e un&#39;analisi efficaci, ma i set di dati di grandi dimensioni possono influire su risultati, prestazioni e conformità tempestivi. Questo argomento fornisce alcune indicazioni sulla gestione dell’acquisizione dei dati e sulle strategie per perfezionare i dati in modo che siano più efficaci.

New Relic fornisce una visualizzazione di _Gestione dati_ che riepiloga l&#39;utilizzo del piano per origine dati.

**Per visualizzare i dati e le origini di acquisizione**:

1. Dal menu utente di New Relic, fare clic su **[!UICONTROL Manage your data]**.
1. Fare clic su **[!UICONTROL Data management]** nell&#39;elenco _Amministrazione_.

   ![Gestione dati](../../assets/new-relic/data-ingestion.png)

   Nella scheda **[!UICONTROL Data ingestion]** vengono visualizzati i dati acquisiti per il giorno e l&#39;origine dei dati.
La scheda Conservazione dei dati mostra e controlla per quanto tempo vengono memorizzati i dati.

1. Selezionare la scheda **[!UICONTROL Limits]** e visualizzare i limiti per l&#39;account.

Le origini dati per Adobe Commerce includono:

- **Eventi APM**: dati evento utilizzati nei grafici e nei dashboard
- **Infrastruttura**: metriche di processo e host, ad esempio CPU, archiviazione, rete
- **Registrazione**: registri per CDN, APM e server applicazioni

I dati di registro contribuiscono in larga misura all’acquisizione. Scopri come [visualizzare e analizzare i dati di registro](log-management.md#view-and-analyze-log-data) e collaborare con il tuo rappresentante Adobe per definire una strategia per le esigenze di acquisizione e conservazione dei dati. Ulteriori informazioni sulla [gestione dell&#39;acquisizione dei dati](https://docs.newrelic.com/docs/data-apis/manage-data/manage-data-coming-new-relic/) sono disponibili nella _documentazione di New Relic_.
