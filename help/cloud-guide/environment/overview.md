---
title: Panoramica dei file di configurazione
description: Scopri come configurare l’ambiente dell’infrastruttura cloud per supportare l’implementazione e la gestione dello store Adobe Commerce personalizzato.
feature: Cloud, Configuration, Services, Iaas, Paas
exl-id: 305380b0-1920-4037-a1db-80e72c6af333
TQID: https://experienceleague.adobe.com/mFjzrTN6R7LC3e9ADnzzulcWAwun4k-g3aCjc9Bo3gQ
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: fd3ef8201c368f889344452e334976070a6c7157
workflow-type: tm+mt
source-wordcount: 280
ht-degree: 0%

---

# Panoramica dei file di configurazione

Gli ambienti in Adobe Commerce su infrastrutture cloud includono contenitori con applicazioni, servizi e un database per fornire un sistema completo per la base di codice e i file dell’applicazione Adobe Commerce.

Puoi configurare le impostazioni dell’applicazione, i percorsi, le azioni di build e distribuzione e le notifiche per supportare gli ambienti di progetto utilizzando i seguenti file di configurazione:

| Configurazione | Nome file | Descrizione |
| ------------- | -------- | ----------- |
| [Applicazione](../application/configure-app-yaml.md) | `.magento.app.yaml` | Definisce come generare e distribuire Adobe Commerce, inclusi servizi, hook e processi cron. |
| [Ambiente](configure-env-yaml.md) | `.magento.env.yaml` | Centralizza la gestione delle azioni di generazione e implementazione in tutti gli ambienti, inclusi Pro Staging e Produzione, utilizzando variabili di ambiente. |
| [Route](../routes/routes-yaml.md) | `.magento/routes.yaml` | Configura la memorizzazione in cache, i reindirizzamenti e le inclusioni lato server. |
| [Servizio](../services/services-yaml.md) | `.magento/services.yaml` | Definisce i servizi utilizzati da Adobe Commerce per nome e versione. Ad esempio, questo file può includere versioni di MariaDB, estensioni PHP, Redis, RabbitMQ e Elasticsearch o OpenSearch. È necessario aprire un ticket di supporto per inviare queste modifiche agli ambienti Pro plan di staging e produzione. |
| [Impostazioni PHP](../application/php-settings.md#configure-php) | `php.ini` | File facoltativo che può essere aggiunto al progetto. Le impostazioni contenute in questo file vengono aggiunte a quelle gestite dall’infrastruttura cloud. |

{style="table-layout:auto"}

## Aggiornamenti alla configurazione degli ambienti Pro

Per gli ambienti di produzione e staging Pro di Adobe Commerce su infrastruttura cloud, puoi aggiornare molte opzioni di configurazione nell’ambiente di sviluppo locale e confermare le modifiche per applicarle a tali ambienti. È tuttavia necessario [Inviare un ticket di supporto Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html?lang=it#submit-ticket) per aggiornare le seguenti opzioni di configurazione:

- Installare o aggiornare i servizi nel file `.magento/services.yaml`.
- Modificare la configurazione per le proprietà `mounts` e `disk` nel file `.magento.app.yaml`.

{{pro-self-service-warning}}
