---
title: Aggiorna versione Commerce
description: Scopri come aggiornare la versione di Adobe Commerce nel progetto di infrastruttura cloud.
feature: Cloud, Upgrade
exl-id: 0cc070cf-ab25-4269-b18c-b2680b895c17
source-git-commit: 1cea1cdebf3aba2a1b43f305a61ca6b55e3b9d08
workflow-type: tm+mt
source-wordcount: '1547'
ht-degree: 0%

---

# Aggiorna versione Commerce

Puoi aggiornare la base di codice di Adobe Commerce a una versione più recente. Prima di aggiornare il progetto, controllare i [requisiti di sistema](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/system-requirements.html) nella _Guida all&#39;installazione_ per i requisiti della versione più recente del software.

A seconda della configurazione del progetto, le attività di aggiornamento possono includere quanto segue:

- I servizi di aggiornamento, come MariaDB (MySQL), OpenSearch, RabbitMQ e Redis, sono compatibili con le nuove versioni di Adobe Commerce.
- Convertire un file di gestione della configurazione precedente.
- Aggiorna il file con le `.magento.app.yaml` nuove impostazioni per gli hook e le variabili d&#39;ambiente.
- Aggiorna le estensioni di terze parti alla versione più recente supportata.
- Aggiornare il file `.gitignore`.

{{upgrade-tip}}

{{pro-update-service}}

## Aggiornamento da versioni precedenti

Se stai iniziando un aggiornamento da una versione di Commerce precedente alla 2.1, alcune restrizioni nella base di codice di Adobe Commerce possono influire sulla possibilità di _aggiornare_ a una versione specifica degli strumenti ECE o di _aggiornare_ alla versione successiva di Commerce supportata. Utilizzare la tabella seguente per determinare il percorso migliore:

| Versione corrente | Percorso di aggiornamento |
| ----------------- | ------------ |
| 2.1.3 e versioni precedenti | Prima di continuare, aggiorna Adobe Commerce alla versione 2.1.4 o successiva. Quindi esegui un [aggiornamento una tantum per installare ECE-Tools](../dev-tools/install-package.md). |
| 2.1.4 - 2.1.14 | [Aggiorna pacchetto ECE-Tools](../dev-tools/update-package.md).<br>Consulta le note sulla versione di [2002.0.9](../release-notes/cloud-release-archive.md#v200209) e successive versioni di 2002.0.x. |
| 2.1.15 - 2.1.16 | [Aggiorna pacchetto ECE-Tools](../dev-tools/update-package.md).<br>Consulta le note sulla versione di [2002.0.9](../release-notes/cloud-release-archive.md#v200209) e successive. |
| 2.2.x e versioni successive | [Aggiorna pacchetto ECE-Tools](../dev-tools/update-package.md).<br>Consulta le note sulla versione di [2002.0.8](../release-notes/cloud-release-archive.md#v200208) e successive. |

{style="table-layout:auto"}

{{ece-tools-package}}

## Gestione della configurazione

Le versioni precedenti di Adobe Commerce, ad esempio 2.1.4 o successive alla versione 2.2.x o successive, utilizzavano un file `config.local.php` per la gestione della configurazione. Adobe Commerce versione 2.2.0 e successive utilizzano il file `config.php`, che funziona esattamente come il file `config.local.php`, ma con impostazioni di configurazione diverse che includono un elenco dei moduli abilitati e opzioni di configurazione aggiuntive.

Quando si esegue l&#39;aggiornamento da una versione precedente, è necessario migrare il file `config.local.php` per utilizzare il file `config.php` più recente. Per eseguire il backup del file di configurazione e crearne uno, effettua le seguenti operazioni.

**Per creare un file `config.php` temporaneo**:

1. Creare una copia del file `config.local.php` e denominarlo `config.php`.

1. Aggiungi il file alla cartella `app/etc` del progetto.

1. Aggiungi e invia il file al tuo ramo.

1. Invia il file al ramo di integrazione.

1. Continuare con il processo di aggiornamento.

>[!WARNING]
>
>Dopo l&#39;aggiornamento, è possibile rimuovere il `config.php` file e generare un nuovo file completo. È possibile eliminare questo file solo per sostituirlo questa volta. Dopo aver generato un nuovo file completo `config.php` , non è possibile eliminare il file per generarne uno nuovo. Vedere [Gestione della configurazione e distribuzione](../store/store-settings.md) della pipeline.

### Verifica le dipendenze del compositore di Zend Framework

Quando si esegue l&#39;aggiornamento a **2.3.x o versioni successive dalla 2.2.x**, verificare che le dipendenze di Zend Framework siano state aggiunte alla `autoload` proprietà del file per supportare Laminas `composer.json` . Questo plugin supporta i nuovi requisiti per Zend Framework, che è migrato al progetto Laminas. Vedi [Migrazione di Zend Framework al progetto Laminas](https://community.magento.com/t5/Magento-DevBlog/Migration-of-Zend-Framework-to-the-Laminas-Project/ba-p/443251) in _Magento DevBlog_.

**Per controllare la configurazione `auto-load:psr-4`**:

1. Sulla workstation locale, passa alla directory del progetto.

1. Consulta il ramo dell’integrazione.

1. Aprire il file `composer.json` in un editor di testo.

1. Controllare la sezione `autoload:psr-4` per l&#39;implementazione del gestore del plug-in Zend per la dipendenza dei controller.

   ```json
    "autoload": {
       "psr-4": {
          "Magento\\Framework\\": "lib/internal/Magento/Framework/",
          "Magento\\Setup\\": "setup/src/Magento/Setup/",
          "Magento\\": "app/code/Magento/",
          "Zend\\Mvc\\Controller\\": "setup/src/Zend/Mvc/Controller/"
       },
   }
   ```

1. Se manca la dipendenza Zend, aggiornare il file `composer.json`:

   - Aggiungere la riga seguente alla sezione `autoload:psr-4`.

     ```json
     "Zend\\Mvc\\Controller\\": "setup/src/Zend/Mvc/Controller/"
     ```

   - Aggiornare le dipendenze del progetto.

     ```bash
     composer update
     ```

   - Aggiungi, conferma e invia modifiche al codice.

     ```bash
     git add -A
     ```

     ```bash
     git commit -m "Add Zend plugin manager implementation for controllers dependency for Laminas support"
     ```

     ```bash
     git push origin <branch-name>
     ```

   - Unisci le modifiche apportate all’ambiente di staging e quindi a Produzione.

## File di configurazione

Prima di aggiornare il applicazione, è necessario aggiornare i file di configurazione del progetto per account per le modifiche alle impostazioni di configurazione predefinite per Adobe Systems Commerce in infrastruttura cloud o applicazione. Le impostazioni predefinite più recenti sono disponibili nel [archivio](https://github.com/magento/magento-cloud) GitHub cloud magento-.

### .magento.app.yaml

Controlla sempre i [valori contenuti nel file .magento.app.yaml](../application/configure-app-yaml.md) per la versione installata, perché controlla il modo in cui il applicazione viene compilato e distribuito nel infrastruttura cloud. L&#39;esempio seguente si riferisce alla versione 2.4.8 e utilizza Composer 2.8.4. La `build: flavor:` proprietà non viene utilizzata per Composer 2.x; vedere [Installazione e utilizzo di Composer 2](../application/properties.md#installing-and-using-composer-2).

**Per aggiornare il `.magento.app.yaml` file**:

1. Sulla workstation locale, passa alla directory del progetto.

1. Aprire e modificare il file `magento.app.yaml`.

1. Aggiornare le opzioni PHP.

   ```yaml
   type: php:8.4
   
   build:
       flavor: none
   dependencies:
       php:
           composer/composer: '2.8.4'
   ```

1. Modificare la proprietà `hooks` `build` e i comandi `deploy`.

   ```yaml
   hooks:
       # We run build hooks before your application has been packaged.
       build: |
           set -e
           composer install
           php ./vendor/bin/ece-tools run scenario/build/generate.xml
           php ./vendor/bin/ece-tools run scenario/build/transfer.xml
       # We run deploy hook after your application has been deployed and started.
       deploy: |
           php ./vendor/bin/ece-tools run scenario/deploy.xml
       # We run post deploy hook to clean and warm the cache. Available with ECE-Tools 2002.0.10.
       post_deploy: |
           php ./vendor/bin/ece-tools run scenario/post-deploy.xml
   ```

1. Aggiungi le seguenti variabili di ambiente alla fine del file.

   Per Adobe Commerce da 2.2.x a 2.3.x-

   ```yaml
   variables:
       env:
           CONFIG__DEFAULT__PAYPAL_ONBOARDING__MIDDLEMAN_DOMAIN: 'payment-broker.magento.com'
           CONFIG__STORES__DEFAULT__PAYMENT__BRAINTREE__CHANNEL: 'Magento_Enterprise_Cloud_BT'
           CONFIG__STORES__DEFAULT__PAYPAL__NOTATION_CODE: 'Magento_Enterprise_Cloud'
   ```

   Per Adobe Commerce 2.4.x-

   ```yaml
   variables:
       env:
           CONFIG__DEFAULT__PAYPAL_ONBOARDING__MIDDLEMAN_DOMAIN: 'payment-broker.magento.com'
           CONFIG__STORES__DEFAULT__PAYPAL__NOTATION_CODE: 'Magento_Enterprise_Cloud'
   ```

1. Salva il file. Non eseguire ancora il commit o il push delle modifiche nell&#39;ambiente remoto.

1. Continuare con il processo di aggiornamento.

### composer.json

Prima di eseguire l&#39;aggiornamento `composer.json` , verifica sempre che le dipendenze nel file siano compatibili con la versione di Adobe Systems Commerce.

**Per aggiornare il file `composer.json` per Adobe Commerce versione 2.4.4 e successive**:

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

## Backup del progetto

È consigliabile creare un backup del progetto prima di un aggiornamento. Utilizza i seguenti passaggi per eseguire il backup degli ambienti di integrazione, staging e produzione.

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

1. Impostare la versione di aggiornamento utilizzando la sintassi [version constraint](overview.md#cloud-metapackage).

   ```bash
   composer require "magento/magento-cloud-metapackage":">=CURRENT_VERSION <NEXT_VERSION" --no-update
   ```

   >[!NOTE]
   >
   >Per aggiornare correttamente il pacchetto `ece-tools`, è necessario utilizzare la sintassi del vincolo di versione. È possibile trovare il vincolo di versione nel file `composer.json` per la versione del [modello di applicazione](https://github.com/magento/magento-cloud/blob/master/composer.json) utilizzato per l&#39;aggiornamento.

1. Aggiorna il progetto.

   ```bash
   composer update
   ```

1. Esaminare le patch attualmente applicate:

   - Se nella directory `m2-hotfixes` sono installate patch, [invia un ticket di supporto Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#support-case) e collabora con il supporto Adobe Commerce per verificare quali patch possono ancora essere applicate alla nuova versione. Rimuovere le patch non applicabili dalla directory `m2-hotfixes`.

   - Se nel file `.magento.env.yaml` sono state applicate [patch di qualità], verificare se è ancora possibile applicarle alla nuova versione. Rimuovere le patch non applicabili dalla sezione `QUALITY_PATCHES` del file `.magento.env.yaml`.

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

### Creare un file config.php

Come indicato in [Gestione configurazione](#configuration-management), dopo l&#39;aggiornamento è necessario creare un file `config.php` aggiornato. Completa eventuali modifiche aggiuntive alla configurazione tramite l’Amministratore nell’ambiente di integrazione.

**Per creare un file di configurazione specifico del sistema**:

1. Dal terminale, utilizzare un comando SSH per generare il `/app/etc/config.php` file per l&#39;ambiente.

   ```bash
   ssh <SSH-URL> "<Command>"
   ```

   Ad esempio per Pro, per eseguire il `scd-dump` `integration` sul ramo:

   ```bash
   ssh <project-id-integration>@ssh.us.magentosite.cloud "php vendor/bin/ece-tools config:dump"
   ```

1. Trasferire il `config.php` file alle workstation locali utilizzando `rsync` o `scp`. È possibile aggiungere questo file al ramo solo localmente.

   ```bash
   rsync <SSH-URL>:app/etc/config.php ./app/etc/config.php
   ```

1. Aggiungi, conferma e invia modifiche al codice.

   ```bash
   git add app/etc/config.php && git commit -m "Add system-specific configuration" && git push origin master
   ```

   Questo genera un file aggiornato con un elenco di `/app/etc/config.php` moduli e impostazioni di configurazione.

>[!WARNING]
>
>Per un aggiornamento, eliminare il file `config.php`. Una volta aggiunto il file al codice, devi **non** eliminarlo. Se è necessario rimuovere o modificare le impostazioni, modificare il file manualmente.

### Aggiornare le estensioni

Controlla le pagine delle estensioni e dei moduli di terze parti nel Marketplace o in altri siti aziendali e verifica il supporto per Adobe Commerce e Adobe Commerce sull’infrastruttura cloud. Se devi aggiornare estensioni e moduli di terze parti, Adobe consiglia di lavorare in un nuovo ramo di integrazione con le estensioni disabilitate.

**Per verificare e aggiornare le estensioni**:

1. Crea una filiale sulla workstation locale.

1. Disattiva le estensioni in base alle esigenze.

1. Se disponibile, scarica gli aggiornamenti dell&#39;estensione.

1. Installa l’aggiornamento come descritto nella documentazione di terze parti.

1. Abilita e verifica l’estensione.

1. Aggiungi, esegui il commit e invia le modifiche al codice in remoto.

1. Esegui il push e il test nell&#39;ambiente di integrazione.

1. Esegui il push nell&#39;ambiente di staging per eseguire il test in un ambiente di pre-produzione.

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
