---
title: Reindirizzare le richieste a un back-end CMS
description: Scopri come reindirizzare le richieste in arrivo da un archivio Adobe Commerce a un sito WordPress separato utilizzando il modulo Fastly Edge.
feature: Cloud, Configuration, Routes
exl-id: ef024c68-395b-4d47-9362-a8404a93dbbe
TQID: https://experienceleague.adobe.com/zRM-iTFGNPgSmT5xu1B9Lo3-onUtCHh-tVY-WPPiVC8
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: d863fc70609dcc66d21eb95e709db80e29114714
workflow-type: tm+mt
source-wordcount: 322
ht-degree: 0%

---

# Reindirizzare le richieste a un back-end CMS

Reindirizza le richieste in arrivo da un archivio Adobe Commerce a un sito WordPress separato utilizzando il modulo Fastly Edge _Altra integrazione CMS/backend_ con un dizionario Edge. Puoi seguire una procedura simile per indirizzare nuovamente le richieste ad altri backend di CMS.

Utilizza Fastly Edge Modules per creare e caricare un codice VCL personalizzato dall’amministratore, anziché scrivere manualmente il codice VCL e caricarlo utilizzando l’API Fastly.

>[!NOTE]
>
>È consigliabile aggiungere configurazioni VCL personalizzate a un ambiente di staging in cui è possibile testarle prima di aggiornare la configurazione del servizio Fastly nell’ambiente di produzione.

**Prerequisiti**

{{$include /help/_includes/vcl-snippet-prerequisites.md}}

**Per reindirizzare le richieste da Adobe Commerce a WordPress**:

1. Abilitare Fastly Edge Modules nell’ambiente di staging o produzione.

   - Accedi all’amministratore.

   - Passa a **Archivi** > Impostazioni > **Configurazione** > **Avanzate** > **Sistema** > **Cache a pagina intera** > **Configurazione rapida** > **Configurazione avanzata**.

   - Imposta il valore per **Moduli Edge veloci** su **Sì**.

   - Salva la configurazione.

1. Identificare i percorsi URL da reindirizzare al backend di WordPress.

1. Completa le seguenti attività per configurare il servizio Fastly e crea il codice VCL personalizzato per reindirizzare le richieste al backend WordPress.

   - Crea un dizionario Edge che specifichi i percorsi da deviare dall’archivio Adobe Commerce al backend.

   - Aggiungi il backend WordPress alla configurazione del servizio Fastly e allega la condizione di richiesta per le riscritture dell’URL.

   - Configura l&#39;_altra integrazione CMS/backend_ modulo Edge per gestire le riscritture URL da Adobe Commerce al backend WordPress.

     Per istruzioni dettagliate, consulta [Moduli Fastly Edge - Altra integrazione CMS/Backend](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/Edge-Modules/EDGE-MODULE-OTHER-CMS-INTEGRATION.md) nella documentazione di _Modulo Fastly CDN per Magento 2_.

1. Dopo aver aggiornato la configurazione del servizio Fastly, verifica l’archivio di Adobe Commerce per assicurarti che le richieste URL specificate per WordPress vengano reindirizzate correttamente.

<!-- Last updated from includes: 2025-01-27 17:16:28 -->

