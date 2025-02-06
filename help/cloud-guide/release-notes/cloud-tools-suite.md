---
title: Note sulla versione della suite di strumenti cloud
description: Scopri gli ultimi miglioramenti alla suite di strumenti cloud per Adobe Commerce.
feature: Cloud, Release Notes
exl-id: ee2bc2e9-bdf4-4f7b-9724-8f4dd1e61378
source-git-commit: 3c6800bc14d8ed43d85fb87eeb24decff72ac77d
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 1%

---

# Note sulla versione per la suite di strumenti Commerce Cloud

Queste informazioni sulla versione descrivono gli ultimi miglioramenti apportati ai pacchetti della suite di strumenti cloud per Commerce progettati per distribuire e gestire le installazioni e gli aggiornamenti di Adobe Commerce sulla piattaforma Cloud.

| Note sulla versione | Versione | Descrizione | Source |
| ----------------- |-----------| ---------------------------------------- | --------------------------- |
| [`ece-tools` pacchetto](ece-tools-package.md) | 2002.2.1 | Un set di script e strumenti progettati per gestire e distribuire progetti Cloud | [`magento/ece-tools`](https://github.com/magento/ece-tools/tree/2002.2.1) |
| [Patch cloud per Commerce](cloud-patches.md) | 1.1.3. | Un set di patch che migliorano l’integrazione di tutte le versioni di Adobe Commerce con gli ambienti Cloud. Questo pacchetto include patch di Adobe Commerce e hotfix disponibili applicati quando si utilizza `ece-tools` per la distribuzione | [`magento/magento-cloud-patches`](https://github.com/magento/magento-cloud-patches/tree/1.1.3) |
| [Docker cloud per Commerce](cloud-docker.md) | 1.4.1. | Funzionalità e file di configurazione per le immagini Docker per distribuire Adobe Commerce in un ambiente cloud locale | [`magento/magento-cloud-docker`](https://github.com/magento/magento-cloud-docker/tree/1.4.1) |
| [Componenti cloud di Commerce](cloud-components.md) | 1.1.1. | Funzionalità Adobe Commerce di base estesa per i siti distribuiti nell’infrastruttura Cloud | [`magento/magento-cloud-components`](https://github.com/magento/magento-cloud-components/tree/1.1.1) |

Quando si esegue l&#39;aggiornamento a ECE-Tools 2002.1.0 o versione successiva, si esegue automaticamente l&#39;aggiornamento alle versioni più recenti degli altri pacchetti, che rappresentano le dipendenze per il pacchetto `ece-tools`. Per un elenco delle dipendenze, consulta [Cloud metapackage](../development/overview.md#cloud-metapackage).

La nuova versione di `ece-tools` (2002.2.0) è disponibile solo con PHP versione 8.1 e successive (8.2, 8.3). Le versioni precedenti di PHP sono state dichiarate obsolete (7.4, 7.3, 7.2). È possibile utilizzare le versioni precedenti di `ece-tools` con le versioni PHP precedenti.
