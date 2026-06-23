---
title: Best practice per l’aggiornamento del progetto
description: Consulta un elenco di best practice per l’aggiornamento dei file di progetto.
feature: Cloud, Best Practices, Upgrade
exl-id: 64f92739-9170-4cbf-90ef-aab6593a37ca
TQID: https://experienceleague.adobe.com/Nnr9fNMT210WTnaLTWyRM-YCWRXrZuOv0m-EZYpzKVw
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: d863fc70609dcc66d21eb95e709db80e29114714
workflow-type: tm+mt
source-wordcount: 696
ht-degree: 0%

---

# Best practice per l’aggiornamento del progetto

Segui le best practice per le build e la distribuzione e utilizza il flusso di lavoro [Aggiornamenti e patch](../development/commerce-version.md) per aggiornare l&#39;applicazione. Per pianificare il lavoro di aggiornamento e post-aggiornamento, attenersi alle seguenti linee guida:

- **Esegui il backup del progetto**-Prima di aggiornare Adobe Commerce ed eventuali estensioni di terze parti o personalizzate, esegui il backup del database negli ambienti di integrazione, staging e produzione. Vedere [Backup del database](../development/commerce-version.md#project-backup).

- **Verifica la presenza di problemi di compatibilità**-

   - Assicurati che tutti i temi personalizzati siano compatibili con la nuova versione di Adobe Commerce

   - Dopo l&#39;aggiornamento di estensioni di terze parti e personalizzate, utilizzare il comando `magento-cloud local:build` per convalidare le dipendenze del Compositore prima della distribuzione ed eseguire [Upgrade Compatibility Tool](#use-the-upgrade-compatibility-tool) per identificare le incompatibilità a livello di codice tra la versione corrente e quella di destinazione. Quindi utilizzare lo [strumento di compatibilità per l&#39;aggiornamento](https://fluffyjaws.adobe.com/#use-the-upgrade-compatibility-tool) per identificare e assegnare la priorità alle incompatibilità a livello di codice prima di distribuirle in Integration, Staging o Production.

   - Consulta le note sulla versione e la documentazione dell’estensione di Adobe Commerce per assicurarti di aver implementato tutte le soluzioni alternative o le modifiche alla configurazione necessarie per risolvere problemi funzionali noti e bug correlati all’aggiornamento della versione e delle estensioni di Adobe Commerce.

   - Assicurati che le versioni del servizio installate siano compatibili con la nuova versione di Adobe Commerce e aggiorna i servizi secondo necessità. Vedi [Servizi](../services/services-yaml.md).

   - Verifica il database per risolvere eventuali problemi introdotti dagli aggiornamenti della versione e delle estensioni di Adobe Commerce.

   - Apporta gli aggiornamenti necessari alle impostazioni specifiche dell’ambiente prima di distribuirle nell’ambiente remoto.

   - Verificare che la versione del servizio di ricerca sia compatibile con la versione del client PHP. Consulta [Configurare Elasticsearch](../services/elasticsearch.md) o [Configurare OpenSearch](../services/opensearch.md).

- **Verifica la connettività del database e l&#39;archiviazione disponibile negli ambienti remoti**-

   - Utilizzare SSH per accedere al server remoto e verificare la connessione al database MySQL. Vedi [Connetti al database](../services/mysql.md#connect-to-the-database).

   - Verificare l&#39;archiviazione disponibile nell&#39;ambiente remoto. Utilizzare il comando `disk free` per visualizzare e gestire lo spazio su disco disponibile negli ambienti cloud. Vedere [Gestione spazio su disco](../storage/manage-disk-space.md).

      - Controllare le dimensioni del database aggiornato e verificare che nel file `services.yaml` sia allocato spazio su disco sufficiente.

      - Liberare spazio su disco. Cancellare la cache e pulire le directory `/log` e `/tmp` prima della distribuzione.

- **Pianifica ed esegui un aggiornamento riuscito negli ambienti locali e di integrazione, prima di implementarlo nell&#39;ambiente di staging**-Dopo l&#39;aggiornamento, verifica l&#39;implementazione e risolvi eventuali problemi.

- **Unisci il codice nell&#39;ambiente di staging, quindi nell&#39;ambiente di produzione**-verifica e risolvi eventuali problemi nell&#39;ambiente di staging prima di inviare le modifiche all&#39;ambiente di produzione.

- **Completare le attività post aggiornamento**-

   - Utilizzare SSH per accedere al server remoto e verificare quanto segue:

      - Controlla lo stato dell’indicizzatore e reindicizza in base alle esigenze. Vedi [Gestione degli indicizzatori](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/manage-indexers.html?lang=it) nella _Guida alla configurazione_.

      - Controllare i registri `cron` e la tabella `cron_schedule` nel database di Adobe Commerce per verificare lo stato cron ed eseguire nuovamente i processi cron in base alle esigenze.
Consulta [Registrazione](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs.html?lang=it#logging) nella _Guida alla configurazione_.

   - Completa il test di accettazione utente post-aggiornamento sugli ambienti di staging e produzione e risolve eventuali problemi relativi agli aggiornamenti di estensioni di terze parti e personalizzati.

## Utilizzare Upgrade Compatibility Tool

Esegui Upgrade Compatibility Tool (UCT) come parte dell’analisi pre-aggiornamento per comprendere l’ambito e l’impatto di un aggiornamento.

- La funzione UCT confronta l’istanza corrente con una versione di Adobe Commerce di destinazione, restituendo un elenco di problemi critici, errori e avvisi che devono essere corretti prima dell’aggiornamento.
- Utilizza `--coming-version (-c)` per eseguire il confronto con la versione di destinazione pianificata e `--ignore-current-version-compatibility-issues` per concentrarti solo sui nuovi problemi introdotti dall&#39;aggiornamento.
- Considera il rapporto HTML UCT come un input per l’elenco di controllo per l’aggiornamento, insieme alla compatibilità delle estensioni, alle versioni del servizio e ai controlli del database.

Per informazioni dettagliate sulla configurazione e sull’utilizzo, consulta:

- [Panoramica di Upgrade Compatibility Tool](https://experienceleague.adobe.com/it/docs/commerce-operations/upgrade-guide/upgrade-compatibility-tool/overview)
- [Eseguire Upgrade Compatibility Tool](https://experienceleague.adobe.com/it/docs/commerce-operations/upgrade-guide/upgrade-compatibility-tool/use-upgrade-compatibility-tool/run)

Per i commercianti di Cloud che utilizzano lo strumento di analisi a livello di sito, puoi anche attivare l’UCT dalla dashboard e scaricare il rapporto HTML direttamente dal widget. Consulta Integrare lo [strumento di analisi a livello di sito](https://experienceleague.adobe.com/it/docs/commerce-operations/upgrade-guide/upgrade-compatibility-tool/use-upgrade-compatibility-tool/integrate-analysis-tool).

