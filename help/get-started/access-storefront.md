---
title: Accedere al pannello di amministrazione di Commerce
description: Scopri come accedere al pannello di amministrazione di Commerce.
recommendations: noDisplay, catalog
exl-id: 827417b0-9048-44d8-8c82-07befba476c7
TQID: https://experienceleague.adobe.com/V3BXuCc9aqT5YuyIS8WAZgUdPAYNhQunAgg2i2FCaOs
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: ba9e5be9-7de1-4f71-a5d2-baead0e425ee
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: fd3ef8201c368f889344452e334976070a6c7157
workflow-type: tm+mt
source-wordcount: 361
ht-degree: 0%

---

# Accedere al pannello di amministrazione di Commerce

Gli utenti con accesso amministrativo al pannello di amministrazione di Commerce possono aggiungere utenti, configurare servizi di store, completare il lavoro di configurazione e personalizzazione dello store e altro ancora.

Per un nuovo progetto, il primo passaggio dopo aver ricevuto l’e-mail di benvenuto è proteggere l’accesso dell’amministratore al progetto modificando la password sull’account Proprietario della licenza. Il nome utente predefinito per questo account è l’indirizzo e-mail del Proprietario della licenza.

È possibile inviare una richiesta di modifica della password utilizzando uno dei metodi seguenti:

- Individua l’e-mail di benvenuto inviata all’indirizzo e-mail del Proprietario della licenza, segui il collegamento e cambia la password.

- Copiare l&#39;URL dell&#39;archivio da [[!DNL Cloud Console]](../cloud-guide/project/overview.md) in un browser. Quindi, aggiungi `/admin` alla fine dell&#39;URL per aprire la pagina di accesso. Fai clic sulla **password dimenticata?** collegamento per inviare una richiesta di modifica della password all’indirizzo e-mail del Proprietario della licenza.

Dopo aver inviato la richiesta di modifica della password, controllare l&#39;e-mail per la notifica di reimpostazione della password. Se non ricevi l’e-mail, controlla la cartella di posta indesiderata.

>[!TIP]
>
>Se la reimpostazione della password non riesce o non è possibile accedere al pannello Amministratore, un utente con accesso amministratore può connettersi al progetto utilizzando SSH e aggiungere un utente amministratore utilizzando il comando CLI `admin:user:create`. Consulta [Creare, modificare o sbloccare un account amministratore](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/tutorials/admin.html) nella _Guida all&#39;installazione_.

## Monitorare lo stato del sito

[Site-Wide Analysis Tool](https://experienceleague.adobe.com/en/docs/commerce-operations/tools/site-wide-analysis-tool/intro) è uno strumento proattivo self-service e un archivio centrale che include informazioni dettagliate sul sistema e raccomandazioni per garantire la sicurezza e l&#39;operabilità dell&#39;installazione di Adobe Commerce. Fornisce monitoraggio delle prestazioni in tempo reale, report e consigli 24 ore su 24, 7 giorni su 7 per identificare potenziali problemi e migliorare la visibilità delle configurazioni di salute, sicurezza e applicazioni del sito. Consente di ridurre i tempi di risoluzione e di migliorare la stabilità e le prestazioni del sito. Puoi accedere allo strumento di analisi a livello di sito direttamente dal [pannello di amministrazione](https://experienceleague.adobe.com/en/docs/commerce-operations/tools/site-wide-analysis-tool/access#option-2-logging-in-to-your-site-wide-analysis-tool-dashboard-from-your-stores-admin-panel).
