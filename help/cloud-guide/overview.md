---
title: Commerce su infrastruttura cloud
description: Informazioni sulla creazione, distribuzione e gestione dell’infrastruttura cloud per Commerce.
exl-id: a37d0403-df14-4bb9-8cc4-25436560ba0c
TQID: https://experienceleague.adobe.com/-sgz85xapPKNipyFVB4yMrLilEku3ff5IJg3OddymsA
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: ba9e5be9-7de1-4f71-a5d2-baead0e425eeid: dac87252-6066-4d6e-a9d2-f6d84c323de7id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
subfeature_v2: id: f8ddfd3b-6194-46e8-a176-0e918039be56
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: d095671a-1355-40aa-8b5f-06c33c68080b
source-git-commit: efe0f95c16d9aab9af6a9c263034b08dce4d7c93
workflow-type: tm+mt
source-wordcount: 323
ht-degree: 3%

---

# Commerce su infrastruttura cloud

Adobe Commerce su infrastruttura cloud fornisce una piattaforma di hosting automatizzata con un approccio **self-service** per la creazione, la distribuzione e la gestione dell&#39;applicazione [!DNL Commerce] in un ambiente nativo per il cloud. Adobe Commerce on cloud infrastructure è dotato di funzioni aggiuntive che lo distinguono dalle piattaforme Adobe Commerce e Magento Open Source on-premise:

- Infrastruttura preconfigurata che include PHP, MySQL (MariaDB), Redis, servizi della coda messaggi ([!DNL RabbitMQ] o [!DNL ActiveMQ]) e tecnologie dei motori di ricerca supportate.
- Flusso di lavoro basato su Git con generazione e distribuzione automatiche per uno sviluppo rapido e una distribuzione continua efficienti ogni volta che si inviano modifiche al codice in un ambiente Platform as a Service (PaaS).
- File di configurazione dell’ambiente altamente personalizzabili e strumenti CLI (Command-Line Interface) per la gestione e l’implementazione.
- Hosting Amazon Web Services (AWS) che offre un ambiente scalabile e sicuro per le vendite online e la vendita al dettaglio.

![Vantaggi per il cloud](../assets/CloudBenefits.svg)

>[!NOTE]
>
>Per ulteriori informazioni sulla protezione, fare riferimento all&#39;[elenco di controllo per l&#39;avvio della protezione](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/launch/checklist#security-configuration).

Visualizza lo [stack di tecnologia](architecture/tech-stack.md) in dettaglio o scopri ulteriori informazioni sulle caratteristiche specifiche e sui prodotti supportati nell&#39;architettura [Cloud per Commerce](architecture/cloud-architecture.md).

<div id="recs-overview-body-1"></div>
<div id="recs-overview-body-2"></div>
<div id="recs-overview-body-3"></div>
<div id="recs-overview-body-4"></div>
<div id="recs-overview-body-5"></div>
<div id="recs-overview-body-6"></div>

## Aree geografiche cloud

Le sezioni seguenti forniscono dettagli sulle diverse aree geografiche di AWS e Azure disponibili per Adobe Commerce sull’infrastruttura cloud.

## Aree geografiche di AWS

![Diagramma che mostra le aree geografiche di AWS](../assets/aws-regions.png){zoomable="yes"}

>[!NOTE]
>
> Solo on-premise in Cina e in Russia.

## Aree geografiche di Azure

![Diagramma che mostra le aree geografiche di Azure](../assets/azure-regions.png){zoomable="yes"}

>[!NOTE]
>
> Solo on-premise in Cina e in Russia. Tutti i commercianti che richiedono ambienti di integrazione devono utilizzare aree geografiche degli Stati Uniti.

## Documentazione di Adobe Commerce

La guida all’infrastruttura cloud di Commerce presuppone che tu abbia una certa conoscenza operativa e comprensione dell’applicazione Adobe Commerce. Fare riferimento alle guide per sviluppatori e utenti di [!DNL Commerce] di seguito:

- [Documentazione per gli sviluppatori di Adobe Commerce](https://developer.adobe.com/commerce/docs/) (sito Adobe Developer): sviluppo, personalizzazione, integrazione, estensione e utilizzo di funzionalità avanzate

- [Documentazione di Adobe Commerce](https://experienceleague.adobe.com/docs/commerce.html) (Adobe Experience League): pianificazione, implementazione, funzionamento, aggiornamento e manutenzione dei [!DNL Commerce] progetti

{{$include /help/_includes/templated/whats-new.md}}

<!-- Last updated from includes: 2026-05-13 23:38:24 -->
