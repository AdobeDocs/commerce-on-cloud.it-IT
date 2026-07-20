---
title: Note sulla versione della suite di strumenti cloud
description: Scopri gli ultimi miglioramenti alla suite di strumenti cloud per Adobe Commerce.
feature: Cloud, Release Notes
exl-id: ee2bc2e9-bdf4-4f7b-9724-8f4dd1e61378
TQID: https://experienceleague.adobe.com/eQQvGGEwj4D6pOlhZqNA-SMdc6JxH-Wg-hBRZaR1C-M
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
subfeature_v2:
  - id: db6b6496-d1b5-4ad4-9e18-dea78dae3aa8
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 5169e0e93bf44d18ebdce9e0680f80c7cc8be6dc
workflow-type: tm+mt
source-wordcount: 220
ht-degree: 3%

---

# Note sulla versione di Commerce Cloud Tools Suite

Queste informazioni sulla versione descrivono gli ultimi miglioramenti apportati ai pacchetti della suite di strumenti cloud per Commerce progettati per distribuire e gestire le installazioni e gli aggiornamenti di Adobe Commerce sulla piattaforma Cloud.

| Note sulla versione | Versione | Descrizione | Source |
| ----------------- |----------| ---------------------------------------- | --------------------------- |
| [pacchetto di strumenti ece](ece-tools-package.md) | 2002.2.12 | Un set di script e strumenti progettati per gestire e distribuire progetti Cloud | [`magento/ece-tools`](https://github.com/magento/ece-tools/tree/2002.2.12) |
| [Patch cloud per Commerce](cloud-patches.md) | 1.1.15 | Un set di patch che migliorano l’integrazione di tutte le versioni di Adobe Commerce con gli ambienti Cloud. Questo pacchetto include patch di Adobe Commerce e hotfix disponibili applicati quando si utilizza `ece-tools` per la distribuzione | [`magento/magento-cloud-patches`](https://github.com/magento/magento-cloud-patches/tree/1.1.15) |
| [Docker cloud per Commerce](cloud-docker.md) | 1.4.9 | Funzionalità e file di configurazione per le immagini Docker per distribuire Adobe Commerce in un ambiente cloud locale | [`magento/magento-cloud-docker`](https://github.com/magento/magento-cloud-docker/tree/1.4.9) |
| [Componenti cloud di Commerce](cloud-components.md) | 1.1.4 | Funzionalità Adobe Commerce di base estesa per i siti distribuiti nell’infrastruttura Cloud | [`magento/magento-cloud-components`](https://github.com/magento/magento-cloud-components/tree/1.1.4) |

Quando si esegue l&#39;aggiornamento a ECE-Tools 2002.1.0 o versione successiva, si esegue automaticamente l&#39;aggiornamento alle versioni più recenti degli altri pacchetti, che rappresentano le dipendenze per il pacchetto `ece-tools`. Per un elenco delle dipendenze, consulta [Cloud metapackage](../development/overview.md#cloud-metapackage).
