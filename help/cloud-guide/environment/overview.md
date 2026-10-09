---
title: Panoramica dei file di configurazione
description: Scopri come configurare l’ambiente dell’infrastruttura cloud per supportare l’implementazione e la gestione dello store Adobe Commerce personalizzato.
feature: Cloud, Configuration, Services, Iaas, Paas
exl-id: 305380b0-1920-4037-a1db-80e72c6af333
TQID: 'https://experienceleague.adobe.com/mFjzrTN6R7LC3e9ADnzzulcWAwun4k-g3aCjc9Bo3gQ'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: 5a951749-fac9-5bc7-9a98-ebe4ff066437
    internal-label: Cloud
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
  - id: 00451af3-7b97-5414-9992-3a6c269e413f
    internal-label: Paas
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
    internal-label: Architecture
subfeature_v2:
  - id: df5e974b-6742-4873-a687-a6bedaafdaa2
    internal-label: IaaS
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: e6e0bd8e116b2f0b93557b6aeb2aac7cbb8e1d8a
workflow-type: tm+mt
source-wordcount: '286'
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
| [Servizio](../services/services-yaml.md) | `.magento/services.yaml` | Definisce i servizi utilizzati da Adobe Commerce per nome e versione. Ad esempio, questo file può includere versioni di MariaDB, estensioni PHP, Redis o Valkey, RabbitMQ e Elasticsearch o OpenSearch. È necessario aprire un ticket di supporto per inviare queste modifiche agli ambienti Pro plan di staging e produzione. |
| [Impostazioni PHP](../application/php-settings.md#configure-php) | `php.ini` | File facoltativo che può essere aggiunto al progetto. Le impostazioni contenute in questo file vengono aggiunte a quelle gestite dall’infrastruttura cloud. |

{style="table-layout:auto"}

## Aggiornamenti alla configurazione degli ambienti Pro

Per gli ambienti di produzione e staging Pro di Adobe Commerce su infrastruttura cloud, puoi aggiornare molte opzioni di configurazione nell’ambiente di sviluppo locale e confermare le modifiche per applicarle a tali ambienti. È tuttavia necessario [Inviare un ticket di supporto Adobe Commerce](https://experienceleague.adobe.com/en/docs/support-resources/adobe-support-tools-guide/adobe-commerce-support/adobe-commerce-help-center-user-guide#submit-ticket) per aggiornare le seguenti opzioni di configurazione:

- Installare o aggiornare i servizi nel file `.magento/services.yaml`.
- Modificare la configurazione per le proprietà `mounts` e `disk` nel file `.magento.app.yaml`.

{{pro-self-service-warning}}
