---
source-git-commit: 67ed09e3b7c5f5218407b6648e8ca2c32933bbda
workflow-type: tm+mt
source-wordcount: '1008'
ht-degree: 0%

---
# Snippet cloud

## Avvertenza di Elasticsearch {#elasticsearch-support}

>[!WARNING]
>
>Elasticsearch 7 e versioni successive non è supportato per Adobe Commerce sull’infrastruttura cloud. Adobe Commerce 2.4.4 e versioni successive supportano il servizio OpenSearch.

## Integrazione avanzata {#enhanced-integration-envs}

>[!NOTE]
>
>I progetti eseguiti prima del 5 giugno 2020 disponevano di più ambienti di integrazione più piccoli. Se hai bisogno di un ambiente di integrazione più ampio per i test e lo sviluppo, richiedi un aggiornamento per gli ambienti di integrazione avanzata. Per informazioni dettagliate, consulta l&#39;articolo [Richiesta ambiente di integrazione](https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-27242) nel _Centro assistenza Adobe Commerce_.

## Opzioni di unione {#merge-options}

Per impostazione predefinita, il processo di distribuzione sovrascrive tutte le impostazioni nel file `env.php`. Tuttavia, è possibile scegliere di unire uno o più valori per una configurazione del servizio senza sovrascrivere tutti i valori.

Impostare l&#39;opzione `_merge` su una delle opzioni seguenti:

- `true`—**Unisci** i valori del servizio configurati con i valori delle variabili di ambiente.
- `false`—**Sovrascrivi** i valori del servizio configurati con i valori delle variabili di ambiente.

## Archivio privato {#private-repository}

>[!NOTE]
>
>Adobe consiglia di utilizzare un archivio privato per il progetto di infrastruttura cloud Adobe Commerce on per proteggere informazioni proprietarie o attività di sviluppo, come estensioni e configurazioni sensibili.

## Avvertenza self-service Pro {#pro-self-service-warning}

>[!WARNING]
>
>Alcuni **progetti Pro** richiedono l&#39;assistenza del supporto Adobe per aggiornare le configurazioni delle route nel file `routes.yaml` e le configurazioni cron nel file `.magento.app.yaml`. Adobe consiglia di apportare e convalidare prima tutte le modifiche di configurazione YAML in un ambiente di integrazione e quindi distribuirle nell’ambiente di staging.
>
>
>Se le modifiche non vengono applicate ai siti di gestione temporanea dopo la ridistribuzione e nel registro non sono presenti messaggi di errore correlati, **è necessario** [inviare un ticket di supporto Adobe Commerce](https://experienceleague.adobe.com/en/docs/support-resources/adobe-support-tools-guide/adobe-commerce-support/adobe-commerce-help-center-user-guide#submit-ticket). Nel ticket, descrivi chiaramente le modifiche di configurazione tentate e allega eventuali file di configurazione YAML aggiornati.

## Backup Pro {#pro-backups}

>[!TIP]
>
>Per recuperare un backup specifico negli ambienti di staging e produzione Pro, [invia un ticket di supporto Adobe Commerce](https://experienceleague.adobe.com/en/docs/support-resources/adobe-support-tools-guide/adobe-commerce-support/adobe-commerce-help-center-user-guide#submit-ticket) indicando la data, l&#39;ora e il fuso orario nel ticket.
>
>Adobe **non** ripristina alcun ambiente da un backup automatico. Per informazioni su come scegliere un metodo per ripristinare uno snapshot di staging o produzione, vedere [Ripristinare uno snapshot del database da staging o produzione](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/how-to/restore-a-db-snapshot-from-staging-or-production).

## Avviso di ridistribuzione {#redeploy-warning}

>[!WARNING]
>
>Il processo di distribuzione inizia quando si esegue un&#39;unione, un push o una sincronizzazione dell&#39;ambiente oppure quando si attiva una ridistribuzione manuale, durante la quale l&#39;applicazione [!DNL Commerce] è in modalità manutenzione. Per un ambiente di produzione, Adobe consiglia di completare questo lavoro nelle ore non di punta per evitare interruzioni del servizio.

## Segnaposto percorso {#route-placeholder}

>[!NOTE]
>
>Negli esempi di configurazione di route riportati di seguito vengono utilizzati modelli di route con segnaposto. Il segnaposto `{default}` rappresenta il dominio predefinito configurato per il sito. Se il progetto ha più domini, utilizzare il segnaposto `{all}` per configurare il routing per il dominio predefinito e per tutti gli alias. Vedere [Configurare le route](/help/cloud-guide/routes/routes-yaml.md).

## Tempistica SCD {#scd-timing-warning}

>[!WARNING]
>
>In caso di problemi con i file di contenuto statico nell’applicazione dopo la distribuzione, ad esempio se mancano file di tema personalizzati, aumenta il tempo di esecuzione massimo previsto a 900 secondi o più.

## Distribuzione basata su scenari {#scenarios}

>[!NOTE]
>
>Con [!DNL ECE-Tools] 2002.1.0 e versioni successive, è possibile utilizzare la funzionalità di distribuzione basata su scenari per personalizzare i processi di compilazione, distribuzione e post-distribuzione per il progetto Adobe Commerce su infrastruttura cloud. Vedi [Distribuzione basata su scenari](/help/cloud-guide/deploy/scenario-based.md).

## Seconda gestione temporanea {#second-staging}

>[!NOTE]
>
>Alcuni progetti richiedono un flusso di lavoro di sviluppo più sofisticato. Per supportare questa esigenza, Adobe offre un [ambiente di staging aggiuntivo](/help/cloud-guide/test/second-staging.md) come opzione aggiuntiva all&#39;infrastruttura cloud.

## Istruzione di servizio {#service-instruction}

Utilizzare le istruzioni seguenti per la configurazione del servizio negli ambienti di integrazione Pro e negli ambienti Starter, incluso il ramo `master`.

>[!NOTE]
>
>Per modificare la configurazione del servizio negli ambienti Pro Production e Staging, [Invia un ticket di supporto Adobe Commerce](https://experienceleague.adobe.com/en/docs/support-resources/adobe-support-tools-guide/adobe-commerce-support/adobe-commerce-help-center-user-guide#submit-ticket). Per informazioni sui requisiti di pianificazione e sulla disponibilità dei clienti, vedere [Supporto dei servizi Pro](https://experienceleague.adobe.com/en/docs/cloud-guide/services/services-yaml.md#pro-services-support) in _Configurazione dei servizi_.

## Modifica del servizio {#service-change-tip}

>[!TIP]
>
>Dopo la configurazione iniziale del servizio, è possibile modificare la versione del software per un servizio installato aggiornando i file di configurazione `services.yaml` e `.magento.app.yaml`. Per informazioni sull&#39;aggiornamento o il downgrade di un servizio, vedere [Modifica versione del servizio](/help/cloud-guide/services/services-yaml.md#change-service-version). Questo metodo self-service non è applicabile agli ambienti Pro Staging o Production. Vedere [Supporto servizi Pro](https://experienceleague.adobe.com/en/docs/cloud-guide/services/services-yaml.md#pro-services-support) in _Configurazione servizi_.

## Suggerimento distribuzione bloccata {#stuck-deployment-tip}

>[!TIP]
>
>Per informazioni sulle distribuzioni bloccate, utilizzare lo strumento di risoluzione dei problemi di distribuzione di [Adobe Commerce](https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-29640) nel _Centro assistenza di Commerce_.

## Aggiornamento a ECE-Tools {#ece-tools-package}

>[!NOTE]
>
>Per rimuovere i pacchetti obsoleti nelle versioni di Adobe Commerce sull&#39;infrastruttura cloud che non contengono il pacchetto `ece-tools`, è necessario eseguire un [aggiornamento una tantum](/help/cloud-guide/dev-tools/install-package.md) al progetto cloud. Se si utilizza il pacchetto `ece-tools` e si desidera aggiornarlo, vedere [Aggiornare il pacchetto ECE-Tools](/help/cloud-guide/dev-tools/update-package.md).

## Suggerimento per l&#39;aggiornamento {#upgrade-tip}

>[!TIP]
>
>Prima di iniziare un aggiornamento o un processo di applicazione di patch, crea un ramo attivo dall’ambiente di integrazione ed estrai il nuovo ramo sulla workstation locale. La destinazione di un ramo all’aggiornamento o al processo di patch consente di evitare interferenze con il lavoro in corso.

## Valkey in New Relic {#valkey-newrelic}

>[!NOTE]
>
>New Relic potrebbe mostrare Redis anche dopo la migrazione a Valkey.
>
>È previsto che New Relic continui a fare riferimento al servizio cache come Redis anche dopo la migrazione dell’ambiente a Valkey.
>
>Valkey è un fork open-source di Redis, e alcuni strumenti e integrazioni continuano a identificare il servizio utilizzando la denominazione Redis piuttosto che un&#39;etichetta Valkey distinta. Questo comportamento non indica necessariamente che Redis è ancora installato.

<!-- Fastly-related snippets begin -->

## Accesso amministratore {#admin-login-step}

1. [Accedi](/help/get-started/onboarding.md#access-your-admin-panel) all&#39;amministratore.

## Automatizzare l&#39;implementazione di snippet VCL personalizzato {#automate-vcl-snippet-deployment}

>[!NOTE]
>
>Anziché caricare manualmente snippet VCL personalizzati, è possibile aggiungere snippet alla directory `$MAGENTO_CLOUD_APP_DIR/var/vcl_snippets_custom` nell&#39;ambiente. I frammenti in questa directory vengono caricati automaticamente quando si fa clic su _carica VCL in Fastly_ in Commerce Admin. Consulta [Distribuzione automatizzata di snippet VCL personalizzati](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/CUSTOM-VCL-SNIPPETS.md#automated-custom-vcl-snippets-deployment) nel modulo Fastly CDN per la documentazione di Magento 2.

<!-- Fastly-related snippets end -->
