---
title: Ripristino da guasto componente
description: Scopri come ripristinare se un componente non viene distribuito correttamente in Adobe Commerce sull’infrastruttura cloud.
feature: Cloud, Deploy
exl-id: f5e79366-5548-40dd-ac2a-56dc84c5d4e2
TQID: https://experienceleague.adobe.com/1krotAWilGcnp3OUMk-fl5iHFObGpWFUC8EpYSPjQfU
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: c1579802-ddd4-4214-8a91-97b2066abe11
source-git-commit: fd3ef8201c368f889344452e334976070a6c7157
workflow-type: tm+mt
source-wordcount: 220
ht-degree: 0%

---

# Ripristino da guasto componente

In questo argomento viene illustrato come ripristinare se un componente non viene distribuito correttamente. Esempi tipici includono componenti che hanno dipendenze non soddisfatte dall’ambiente remoto, come le versioni PHP incompatibili.

È possibile eseguire il ripristino da una distribuzione non riuscita in uno dei modi seguenti:

- [Ripristinare un backup](../storage/snapshots.md#restore-a-snapshot)
- Rimuovi progetto e codice da modifiche precedenti e ridistribuiscili

## Pulizia, rimozione e ridistribuzione

Per eseguire la pulizia dalla distribuzione precedente, identifica il componente aggiunto o aggiornato e quindi rimuovilo. Eseguire innanzitutto l&#39;accesso all&#39;ambiente remoto e cancellare manualmente il contenuto della directory `var`. Quindi rimuovere il componente dal file `composer.json` e ridistribuire l&#39;ambiente.

**Per pulire le directory `var`**:

1. Sulla workstation locale, passa alla directory del progetto.

1. Utilizza SSH per accedere all’ambiente remoto.

   ```bash
   magento-cloud ssh
   ```

1. Cancella le directory `var`.

   ```shell
   rm -rf var/*
   ```

1. Disconnetti.

**Per rimuovere il componente**:

1. Sulla workstation locale, passa alla directory del progetto.

1. Cancella la cache.

   ```bash
   composer clear-cache
   ```

1. Rimuovere il componente dal file `composer.json`.

   ```bash
   composer remove <component-name>:<version>
   ```

   Se viene visualizzato il seguente messaggio, non è necessario eseguire ulteriori operazioni:

   ```
   Package "<name>:<version>" listed for update is not installed. Ignoring.
   ```

1. Aggiornamento delle dipendenze in corso. Attendi.

1. Aggiungi, conferma e invia modifiche al codice.

   ```bash
   git add -A
   ```

   ```bash
   git commit -m "<message>"
   ```

   ```bash
   git push origin <environment-ID>
   ```

{{redeploy-warning}}

Ulteriori informazioni sul ripristino di un ambiente senza backup in [Ripristinare un ambiente](../development/restore-environment.md).

{{stuck-deployment-tip}}
