---
title: Aggiorna versione Commerce
description: Scopri come aggiornare la versione di Adobe Commerce nell’ambiente dell’infrastruttura cloud.
feature: Cloud, Upgrade
exl-id: 0cc070cf-ab25-4269-b18c-b2680b895c17
source-git-commit: 7f9aac358effdf200b59678098e6a1635612301b
workflow-type: tm+mt
source-wordcount: '898'
ht-degree: 0%

---

# Aggiorna versione Commerce

Puoi aggiornare la base di codice di Adobe Commerce a una versione più recente. Prima di aggiornare l&#39;ambiente, controllare i [requisiti di sistema](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/system-requirements.html) nella _Guida all&#39;installazione_ per i requisiti della versione più recente del software.

A seconda del tipo di ambiente (Sviluppo, Staging o Produzione), le attività di aggiornamento possono includere quanto segue:

- Aggiornare il file `.magento/services.yaml` con le nuove versioni di MariaDB (MySQL), OpenSearch, RabbitMQ e Redis per verificarne la compatibilità con le nuove versioni di Adobe Commerce.
- Aggiornare il file `.magento.app.yaml` con le nuove impostazioni per hook e variabili di ambiente.
- Aggiorna le estensioni di terze parti alla versione più recente supportata.

{{upgrade-tip}}

{{pro-update-service}}

## File di configurazione

Prima di aggiornare l’applicazione, è necessario aggiornare i file di configurazione del progetto per tenere conto delle modifiche alle impostazioni di configurazione predefinite per Adobe Commerce sull’infrastruttura cloud o l’applicazione. Le impostazioni predefinite più recenti si trovano nell&#39;archivio GitHub [magento-cloud](https://github.com/magento/magento-cloud).

### composer.json

Prima di eseguire l&#39;aggiornamento, verificare sempre che le dipendenze nel file `composer.json` siano compatibili con la versione di Adobe Commerce.

Per aggiornare il file `composer.json` per Adobe Commerce versione 2.4.4 e successive**:

1. Aggiungi `allow-plugins` alla sezione `config`:

   ```json
   "config": {
      "allow-plugins": {
         "dealerdirect/phpcodesniffer-composer-installer": true,
         "laminas/laminas-dependency-plugin": true,
         "magento/*": true
      }
   },
   ```

1. Aggiungi il seguente plug-in alla sezione `require`:

   ```json
   "require": {
       "magento/composer-root-update-plugin": "^2.0.3"
   },
   ```

1. Aggiungi il seguente componente alla sezione `extra:component_paths`:

   ```json
   "extra": {
      "component_paths": {
         "tinymce/tinymce": "lib/web/tiny_mce_5"
      },
   },
   ```

1. Salva il file. Non eseguire ancora il commit o il push delle modifiche nel ramo.

1. Continuare con il processo di aggiornamento.

## Backup dell’ambiente

È consigliabile creare un backup dell’istanza prima di un aggiornamento. Utilizza i seguenti passaggi per eseguire il backup degli ambienti di integrazione, staging e produzione.

**Per eseguire il backup del database e del codice dell&#39;ambiente di integrazione**:

1. Creare un backup locale del database remoto.

   ```bash
   magento-cloud db:dump
   ```

   >[!NOTE]
   >
   >Il comando `magento-cloud db:dump` esegue il comando [mysqldump](https://dev.mysql.com/doc/refman/8.0/en/mysqldump.html) con il flag `--single-transaction`, che consente di eseguire il backup del database senza bloccare le tabelle.

1. Eseguire il backup del codice e dei supporti.

   ```bash
   php bin/magento setup:backup --code [--media]
   ```

   Se si desidera, è possibile omettere `[--media]` se il numero di file statici che si trovano già nel controllo del codice sorgente è elevato.

**Per eseguire il backup del database dell&#39;ambiente di staging o di produzione prima della distribuzione**:

1. Utilizza SSH per accedere all’ambiente remoto.

1. Crea un dump del database [&#128279;](../storage/database-dump.md). Per scegliere una directory di destinazione per il dump del database, utilizzare l&#39;opzione `--dump-directory`.

   ```bash
   vendor/bin/ece-tools db-dump
   ```

   L&#39;operazione di dump crea un file di archivio `dump-<timestamp>.sql.gz` nella directory di progetto remota. Vedere [Backup del database](../storage/database-dump.md).

## Aggiornamento dell’applicazione

Prima di aggiornare l&#39;applicazione, esaminare le informazioni sulle [versioni del servizio](../services/services-yaml.md#service-versions) per conoscere i requisiti delle versioni più recenti del software.

**Per aggiornare la versione dell&#39;applicazione**:

1. Sulla workstation locale, passa alla directory del progetto.

1. Impostare il vincolo di versione [&#128279;](overview.md#cloud-metapackage) per la versione di aggiornamento di destinazione. Questo passaggio è necessario solo se la versione di destinazione non rientra nel vincolo esistente.

   ```bash
   composer require-commerce "magento/magento-cloud-metapackage":">=CURRENT_VERSION <NEXT_VERSION" --no-update
   ```

   >[!NOTE]
   >
   >Per aggiornare correttamente il pacchetto `ece-tools`, è necessario utilizzare la sintassi del vincolo di versione. È possibile trovare il vincolo di versione nel file `composer.json` per la versione del [modello di applicazione](https://github.com/magento/magento-cloud/blob/master/composer.json) utilizzato per l&#39;aggiornamento.

1. Aggiorna il file `composer.json` con la versione di aggiornamento di base di Commerce.

   ```bash
   composer require-commerce magento/product-enterprise-edition 2.4.8 --no-update
   ```

1. Se utilizzi B2B, aggiorna il file `composer.json` con la [versione supportata](https://experienceleague.adobe.com/en/docs/commerce-operations/release/product-availability#adobe-authored-extensions) per Commerce.

   ```bash
   composer require-commerce magento/extension-b2b 1.5.2 --no-update
   ```

1. Aggiornare le dipendenze del progetto.

   ```bash
   composer update
   ```

1. Esaminare le patch attualmente applicate:

   - Se nella directory `m2-hotfixes` sono installate patch, [invia un ticket di supporto Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#support-case) e collabora con il supporto Adobe Commerce per verificare quali patch possono ancora essere applicate alla nuova versione. Rimuovere le patch non applicabili dalla directory `m2-hotfixes`.

   - Se nel file [ sono state applicate ]patch di qualità`.magento.env.yaml`, verificare se è ancora possibile applicarle alla nuova versione. Rimuovere le patch non applicabili dalla sezione `QUALITY_PATCHES` del file `.magento.env.yaml`.

   **Metodo 1**: [Verificare le versioni applicabili nelle note sulla versione delle patch di qualità](https://experienceleague.adobe.com/en/docs/commerce-operations/tools/quality-patches-tool/release-notes)

   **Metodo 2**: [Visualizzare le patch e lo stato disponibili](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/develop/upgrade/apply-patches#view-available-patches-and-status)

   **Metodo 3**: [Cerca patch](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=en)


1. Aggiungi, conferma e invia modifiche al codice.

   ```bash
   git add -A
   ```

   ```bash
   git commit -m "Upgrade"
   ```

   ```bash
   git push origin <branch-name>
   ```

   `git add -A` è necessario per aggiungere tutti i file modificati al controllo del codice sorgente a causa del modo in cui i pacchetti di base di Marshals Composer vengono eseguiti. Entrambi i file di marshalling `composer install` e `composer update` dal pacchetto di base (`magento/magento2-base` e `magento/magento2-ee-base`) nella radice del pacchetto.

   I file che Composer marshalling appartengono alla nuova versione di Adobe Commerce, per sovrascrivere la versione obsoleta degli stessi file. Attualmente, il marshalling è disabilitato in Adobe Commerce, pertanto è necessario aggiungere i file marshallati al controllo del codice sorgente.

1. Attendere il completamento della distribuzione.

1. Verifica l’aggiornamento nell’ambiente di integrazione, staging o produzione utilizzando SSH per accedere e controllare la versione.

   ```bash
   php bin/magento --version
   ```

### Aggiornare le estensioni

Controlla le pagine delle estensioni e dei moduli di terze parti nel Marketplace o in altri siti aziendali e verifica il supporto per Adobe Commerce e Adobe Commerce sull’infrastruttura cloud. Se devi aggiornare estensioni e moduli di terze parti, Adobe consiglia di lavorare in un nuovo ramo di integrazione con le estensioni disabilitate.

**Per verificare e aggiornare le estensioni**:

1. Crea una filiale sulla workstation locale.

1. Disattiva le estensioni in base alle esigenze.

1. Se disponibile, scarica gli aggiornamenti dell&#39;estensione.

1. Installa l’aggiornamento come descritto nella documentazione di terze parti.

1. Abilita e verifica l’estensione.

1. Aggiungi, esegui il commit e invia le modifiche al codice in remoto.

1. Effettua il push e il test nell’ambiente di integrazione.

1. Effettua il push all’ambiente di staging per il test in un ambiente di pre-produzione.

Adobe consiglia vivamente di aggiornare l&#39;ambiente di produzione _prima_, incluse le estensioni aggiornate nel processo di avvio del sito.

>[!NOTE]
>
>Quando si aggiorna la versione dell&#39;applicazione, il processo di aggiornamento viene aggiornato automaticamente alla versione più recente del [modulo CDN Fastly](../cdn/fastly.md#fastly-cdn-module-for-magento-2).

## Risoluzione dei problemi di aggiornamento

Se l’aggiornamento non è riuscito, viene visualizzato un messaggio di errore nel browser che indica che non è possibile accedere alla vetrina o al pannello di amministrazione:

```
There has been an error processing your request
Exception printing is disabled by default for security reasons.
  Error log record number: <error-number>
```

**Per risolvere l&#39;errore**:

1. Sulla workstation locale, passa alla directory del progetto.

1. Utilizza SSH per accedere all’ambiente remoto.

   ```bash
   magento-cloud ssh
   ```

1. Aprire il file `./app/var/report/<error number>`.

1. [Esaminare i registri](../test/log-locations.md) e determinare l&#39;origine del problema.

1. Aggiungi, conferma e invia modifiche al codice.

   ```bash
   git add -A && git commit -m "Fixed deployment failure" && git push origin <branch-name>
   ```
