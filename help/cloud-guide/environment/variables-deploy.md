---
title: Distribuire le variabili
description: Consulta l’elenco delle variabili di ambiente che controllano le azioni nella fase di implementazione di Adobe Commerce su infrastruttura cloud.
feature: Cloud, Configuration, Cache, Deploy, SCD, Storage, Search
recommendations: noDisplay, catalog
role: Developer
exl-id: 980ec809-8c68-450a-9db5-29c5674daa16
TQID: https://experienceleague.adobe.com/TNuUxXzCiXnKefww0DmKbjfJygEz2HFG-0PjCsCy2nA
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
source-git-commit: bdc2bedd2696e7dde0ffb55f846a8bced2dbd25d
workflow-type: tm+mt
source-wordcount: 3106
ht-degree: 0%

---

# Distribuire le variabili

Le seguenti variabili _deploy_ controllano le azioni nella fase di distribuzione e possono ereditare ed eseguire l&#39;override dei valori dalle [variabili globali](variables-global.md). Inserisci queste variabili nella fase `deploy` del file `.magento.env.yaml`:

```yaml
stage:
  deploy:
    DEPLOY_VARIABLE_NAME: value
```

Per ulteriori informazioni sulla personalizzazione del processo di compilazione e distribuzione:

- [Configurazione della distribuzione](configure-env-yaml.md)
- [Processo di distribuzione](../deploy/process.md)

## `CACHE_CONFIGURATION`

- **Predefinito**—_Non impostato_

Utilizzare `CACHE_CONFIGURATION` per unire o sostituire le opzioni front-end e back-end della cache generate durante la distribuzione.

Per Adobe Commerce sull&#39;infrastruttura cloud, non modificare direttamente `app/etc/env.php`. Il pacchetto `ece-tools` genera la configurazione di distribuzione da `.magento.env.yaml`, le relazioni di servizio e le variabili di distribuzione supportate.

Utilizza `VALKEY_BACKEND` o `REDIS_BACKEND` per selezionare la cache supportata o l&#39;implementazione L2 per la versione esatta di Adobe Commerce. Utilizza `CACHE_CONFIGURATION` per personalizzare opzioni quali nuovi tentativi di connessione, timeout di lettura, prefissi di cache o chiavi di precaricamento.

La combinazione di back-end e servizio cache supportata dipende dal livello di versione e patch di Commerce. Redis non è supportato per Adobe Commerce 2.4.9 o per versioni patch successive a 2.4.5-p16, 2.4.6-p14, 2.4.7-p9 e 2.4.8-p4. Utilizza Valkey per le versioni in cui [requisiti di sistema](https://experienceleague.adobe.com/it/docs/commerce-operations/installation-guide/system-requirements) lo richiedono.

>[!NOTE]
>
>Per istruzioni più dettagliate sulla configurazione del servizio Redis e Valkey, vedi [Best practice per la configurazione del servizio Valkey e Redis](https://experienceleague.adobe.com/it/docs/commerce-operations/implementation-playbook/best-practices/planning/redis-valkey-service-configuration)

Per impostazione predefinita, il processo di distribuzione sovrascrive la configurazione della cache corrispondente. Per unire i valori specificati alla configurazione generata, impostare `_merge` su `true`:

```yaml
stage:
  deploy:
    CACHE_CONFIGURATION:
      _merge: true
      frontend:
        default:
          backend_options:
            connect_retries: 3
          remote_backend_options:
            read_timeout: 10
```

Per sostituire la configurazione esistente con i valori specificati in `CACHE_CONFIGURATION`, impostare `_merge` su `false`.

>[!IMPORTANT]
>
> Non copiare le opzioni `bin/magento setup:config:set` locali, ad esempio `cm_cache_backend_redis`, direttamente in `CACHE_CONFIGURATION`. Nei progetti Cloud, `ece-tools` ottiene i dettagli della connessione al servizio dalle relazioni configurate. Utilizza la struttura documentata per la versione di Commerce e l’implementazione della cache selezionate.

Nell&#39;esempio seguente le assegnazioni di database vengono unite in una configurazione cache esistente. Utilizza questo tipo di sostituzione solo se il backend selezionato e la versione di Commerce lo supportano. Applica le impostazioni front-end a `symfony_l2` solo se la documentazione corrente di Symfony L2 supporta esplicitamente l&#39;opzione.

```yaml
stage:
  deploy:
    CACHE_CONFIGURATION:
      _merge: true
      frontend:
        default:
          backend_options:
            database: 10
        page_cache:
          backend_options:
            database: 11
```

Nell&#39;esempio seguente viene utilizzata la [funzionalità di precaricamento Redis](https://experienceleague.adobe.com/it/docs/commerce-operations/configuration-guide/cache/redis/redis-pg-cache#redis-preload-feature) definita nella _Guida alla configurazione_. Per le versioni che utilizzano Valkey, utilizza le linee guida di Valkey corrispondenti.

```yaml
stage:
  deploy:
    CACHE_CONFIGURATION:
      _merge: true
      frontend:
        default:
          id_prefix: '061_'
          backend_options:
            preload_keys:
              - '061_EAV_ENTITY_TYPES:hash'
              - '061_GLOBAL_PLUGIN_LIST:hash'
              - '061_DB_IS_UP_TO_DATE:hash'
              - '061_SYSTEM_DEFAULT:hash'
```

Per utilizzare un modello [REDIS_BACKEND](#redis_backend) personalizzato non incluso nell&#39;elenco Consentiti, impostare `_custom_redis_backend` su `true` in modo che gli strumenti ece applichino la convalida appropriata:

```yaml
stage:
  deploy:
    CACHE_CONFIGURATION:
      frontend:
        default:
          _custom_redis_backend: true
          backend: '\CustomRedisModel'
```

## `CLEAN_STATIC_FILES`

- **Predefinito**—`true`

Abilita o disabilita la pulizia di [file di contenuto statico](https://experienceleague.adobe.com/it/docs/commerce-operations/configuration-guide/cli/static-view/static-view-file-deployment) generati durante la fase di compilazione o distribuzione. Utilizza il valore predefinito _true_ nello sviluppo come best practice.

- **`true`** - Rimuove tutto il contenuto statico esistente prima di distribuire il contenuto statico aggiornato.
- **`false`** - La distribuzione sovrascrive i file di contenuto statico esistenti solo se il contenuto generato contiene una versione più recente.

Se modifichi il contenuto statico tramite un processo separato, imposta il valore su _false_.

```yaml
stage:
  deploy:
    CLEAN_STATIC_FILES: false
```

La mancata pulizia dei file di visualizzazione statica prima della distribuzione può causare problemi se si distribuiscono aggiornamenti ai file esistenti senza rimuovere le versioni precedenti. A causa di [regole di fallback del file statico](https://developer.adobe.com/commerce/frontend-core/guide/css/preprocess#clean-static-view-files), le operazioni di fallback possono visualizzare il file errato se la directory contiene più versioni dello stesso file.

## `CRON_CONSUMERS_RUNNER`

- **Predefinito**—`cron_run = false`, `max_messages = 1000`

Utilizzare questa variabile di ambiente per verificare che le code di messaggi siano in esecuzione dopo una distribuzione.

- `cron_run` - Valore booleano che abilita o disabilita il processo cron `consumers_runner`. Il valore predefinito è `false`.
- `max_messages` - Numero massimo di messaggi elaborati da ogni consumer prima della chiusura. Il valore predefinito è `1000`. Per impedire la chiusura del consumer, impostarlo su `0`.
- `consumers` - Matrice di stringhe che specifica i nomi dei consumer da eseguire. Un array vuoto esegue _tutti_ i consumer.
- `multiple_processes`-Numero di processi da generare per ogni consumatore. Questa opzione è supportata in Adobe Commerce 2.4.4 e versioni successive.

>[!NOTE]
>
>Per elencare i consumer della coda di messaggi disponibili, eseguire il comando `./bin/magento queue:consumers:list` nell&#39;ambiente remoto.

Nell&#39;esempio seguente vengono eseguiti i consumatori selezionati e vengono avviati più processi per ciascuno di essi:

```yaml
stage:
  deploy:
    CRON_CONSUMERS_RUNNER:
      cron_run: true
      max_messages: 1000
      consumers:
       example_consumer_1
       example_consumer_2
      multiple_processes:
        example_consumer_1: 4
        example_consumer_2: 3
```

Nell&#39;esempio seguente vengono eseguiti tutti i consumer:

```yaml
stage:
  deploy:
    CRON_CONSUMERS_RUNNER:
      cron_run: true
      max_messages: 1000
      consumers: []
```

Per impostazione predefinita, il processo di distribuzione sovrascrive le impostazioni corrispondenti nel file `env.php`. Consulta [Gestione delle code di messaggi](https://experienceleague.adobe.com/it/docs/commerce-operations/configuration-guide/message-queues/manage-message-queues) nella _Guida alla configurazione di Commerce_ per Adobe Commerce locale.

## `CONSUMERS_WAIT_FOR_MAX_MESSAGES`

- **Predefinito**—`false`

Configurare il modo in cui `consumers` elabora i messaggi dalla coda di messaggi scegliendo una delle opzioni seguenti:

- `false`—`Consumers` elabora i messaggi disponibili, chiude la connessione TCP e termina indipendentemente dal limite di `max_messages` specificato nella variabile di distribuzione `CRON_CONSUMERS_RUNNER`.

- `true`—`Consumers` continua a elaborare i messaggi dalla coda dei messaggi fino a raggiungere il numero massimo di messaggi (`max_messages`) specificato nella variabile di distribuzione `CRON_CONSUMERS_RUNNER` prima di chiudere la connessione TCP e terminare il processo consumer. Se la coda si svuota prima di raggiungere `max_messages`, il consumatore attende l&#39;arrivo di altri messaggi.

>[!WARNING]
>
>Se si utilizzano i processi di lavoro per eseguire `consumers` invece di utilizzare un processo cron, impostare questa variabile su true.

```yaml
stage:
  deploy:
    CONSUMERS_WAIT_FOR_MAX_MESSAGES: false
```

## `CRYPT_KEY`

- **Predefinito**—_Non impostato_

>[!WARNING]
>
>Per evitare di esporre la chiave nell&#39;archivio del codice sorgente, impostare il valore `CRYPT_KEY` tramite [!DNL Cloud Console] anziché il file `.magento.env.yaml`. Consulta [Impostare le variabili di ambiente e di progetto](https://experienceleague.adobe.com/it/docs/commerce-on-cloud/user-guide/project/overview#configure-environment).

Quando si sposta il database da un ambiente a un altro senza un processo di installazione, è necessario disporre delle informazioni di crittografia corrispondenti. Adobe Commerce utilizza il valore della chiave di crittografia impostato in [!DNL Cloud Console] come valore `crypt/key` nel file `env.php`.

## `DATABASE_CONFIGURATION`

- **Predefinito**—_Non impostato_

Se hai definito un database nella proprietà [relations](../application/properties.md#relationships) del file `.magento.app.yaml`, puoi personalizzare le connessioni al database per la distribuzione.

```yaml
stage:
  deploy:
    DATABASE_CONFIGURATION:
      some_config: 'some_value'
```

{{merge-options}}

Nell&#39;esempio seguente i nuovi valori vengono uniti a una configurazione esistente:

```yaml
stage:
  deploy:
    DATABASE_CONFIGURATION:
      some_config: 'some_new_value'
      _merge: true
```

È inoltre possibile configurare un prefisso di tabella.

>[!WARNING]
>
>Se non utilizzi l’opzione di unione con il prefisso della tabella, devi fornire le impostazioni di connessione predefinite, altrimenti la distribuzione non riesce la convalida.

Nell&#39;esempio seguente viene utilizzato il prefisso della tabella `ece_` con le impostazioni di connessione predefinite anziché l&#39;opzione `_merge`:

```yaml
stage:
  deploy:
    DATABASE_CONFIGURATION:
      connection:
        default:
          username: user
          host: host
          dbname: magento
          password: password
      table_prefix: 'ece_'
```

Output di esempio:

```
MariaDB [main]> SHOW TABLES;
+-------------------------------------+
| Tables_in_main                      |
+-------------------------------------+
| ece_admin_passwords                 |
| ece_admin_system_messages           |
| ece_admin_user                      |
| ece_admin_user_session              |
| ece_adminnotification_inbox         |
| ece_amazon_customer                 |
| ece_authorization_rule              |
| ece_cache                           |
| ece_cache_tag                       |
| ece_captcha_log                     |
...
```

## `ELASTICSUITE_CONFIGURATION`

- **Predefinito**—_Non impostato_

Mantiene le impostazioni personalizzate del servizio [!DNL Elastic Suite] tra le distribuzioni e le utilizza nella sezione &#39;system/default/smile_elasticsuite_core_base_settings&#39; della configurazione principale di [!DNL Elastic Suite]. Se il pacchetto del compositore [!DNL Elastic Suite] è installato, viene configurato automaticamente.

```yaml
stage:
  deploy:
    ELASTICSUITE_CONFIGURATION:
      es_client:
        servers: 'remote-host:9200'
      indices_settings:
        number_of_shards: 1
        number_of_replicas: 0
```

>[!NOTE]
>
>In un cluster Pro Staging/Produzione con tre nodi (o tre nodi di servizio in [Architettura scalata](https://experienceleague.adobe.com/it/docs/commerce-on-cloud/user-guide/architecture/scaled-architecture#service-tier)), `indices_settings` deve essere impostato come segue:
>
>```yaml
>           indices_settings:
>               number_of_shards: 1
>               number_of_replicas: 2
>```

{{merge-options}}

L’esempio che segue unisce un nuovo valore alla configurazione esistente:

```yaml
stage:
  deploy:
    ELASTICSUITE_CONFIGURATION:
      indices_settings:
        number_of_shards: 1
        number_of_replicas: 2
      _merge: true
```

**Limitazioni note**:

- La modifica del motore di ricerca in un tipo diverso da `elasticsuite` causa un errore di distribuzione accompagnato da un errore di convalida appropriato
- La rimozione del servizio Elasticsearch causa un errore di distribuzione accompagnato da un errore di convalida appropriato

>[!NOTE]
>
>Per informazioni dettagliate sull&#39;utilizzo o sulla risoluzione dei problemi relativi al plug-in [!DNL Elastic Suite] con Adobe Commerce, consulta la [[!DNL Elastic Suite] documentazione](https://github.com/Smile-SA/elasticsuite).

## `ENABLE_GOOGLE_ANALYTICS`

- **Predefinito**—`false`

Abilita e disabilita Google Analytics durante la distribuzione in ambienti di staging e integrazione. Per impostazione predefinita, Google Analytics è true solo per l’ambiente di produzione. Per abilitare Google Analytics negli ambienti di gestione temporanea e integrazione, impostare questo valore su `true`.

- **`true`**: abilita Google Analytics negli ambienti di staging e integrazione.
- **`false`**: disabilita Google Analytics negli ambienti di staging e integrazione.

Aggiungere la variabile di ambiente `ENABLE_GOOGLE_ANALYTICS` alla fase `deploy` nel file `.magento.env.yaml`:

```yaml
stage:
  deploy:
    ENABLE_GOOGLE_ANALYTICS: true
```

>[!NOTE]
>
>Il processo di distribuzione abilita sempre Google Analytics negli ambienti di produzione.

## `FORCE_UPDATE_URLS`

- **Predefinito**—`true`

Durante la distribuzione negli ambienti Pro o Starter di staging e produzione, questa variabile sostituisce gli URL di base di Adobe Commerce nel database con gli URL del progetto specificati dalla variabile [`MAGENTO_CLOUD_ROUTES`](variables-cloud.md). Per ignorare il comportamento predefinito della variabile di distribuzione [UPDATE_URLS](#update_urls), utilizzare questa impostazione.

```yaml
stage:
  deploy:
    FORCE_UPDATE_URLS: true
```

## `LOCK_PROVIDER`

- **Predefinito**: negli ambienti di produzione e di gestione temporanea, il valore predefinito è `file` e non può essere modificato. Per l&#39;integrazione Pro e gli ambienti di avvio, il valore predefinito è `db`.

Il provider di blocchi impedisce l&#39;esecuzione di processi cron duplicati e di gruppi cron. Adobe Commerce on Cloud supporta i provider di blocchi `file` e `db`.

Negli ambienti di staging e produzione Pro, `MAGENTO_CLOUD_LOCKS_DIR` configura il provider `file`. Non è possibile ignorare questa impostazione. Negli ambienti Pro Integration e Starter, `ece-tools` imposta il provider `db` per impostazione predefinita. Per ottimizzare le prestazioni locali ed eseguire il mirroring dell&#39;architettura di produzione, impostare il provider su `file` in tali ambienti.

```yaml
stage:
  deploy:
    LOCK_PROVIDER: 'file'
```

## `MYSQL_USE_SLAVE_CONNECTION`

- **Predefinito**—`false`

>[!TIP]
>
>La variabile `MYSQL_USE_SLAVE_CONNECTION` è supportata solo in Adobe Commerce su cluster di Staging e Production Pro dell&#39;infrastruttura cloud. Non è supportato nei progetti iniziali.

Adobe Commerce può leggere più database in modo asincrono. Impostare su `true` per utilizzare automaticamente una connessione _di sola lettura_ al database per ricevere traffico di sola lettura su un nodo non principale. Questa connessione migliora le prestazioni tramite il bilanciamento del carico, perché solo un nodo gestisce il traffico di lettura-scrittura. Per rimuovere qualsiasi array di connessione di sola lettura esistente dal file `env.php`, impostare su `false`.

```yaml
stage:
  deploy:
    MYSQL_USE_SLAVE_CONNECTION: true
```

Quando la variabile `MYSQL_USE_SLAVE_CONNECTION` è impostata su `true`, il sistema imposta il parametro `synchronous_replication` su `true` per impostazione predefinita nel file `env.php` negli ambienti di staging e produzione Pro. Quando `MYSQL_USE_SLAVE_CONNECTION` è impostato su `false`, il parametro `synchronous_replication` non è configurato.

## `QUEUE_CONFIGURATION`

- **Predefinito**—_Non impostato_

Utilizzare questa variabile di ambiente per mantenere le impostazioni personalizzate del servizio di coda tra le distribuzioni. Questa variabile supporta sia i protocolli AMQP (per RabbitMQ) che STOMP (per ActiveMQ Artemis). Ad esempio, se preferisci utilizzare un servizio di coda messaggi esistente invece di affidarti all&#39;infrastruttura cloud per crearlo, utilizza la variabile di ambiente `QUEUE_CONFIGURATION` per connetterlo al sito:

```yaml
stage:
  deploy:
    QUEUE_CONFIGURATION:
      amqp:
        host: test.host
        port: 1234
      amqp2:
        host: test.host2
        port: 12345
      mq:
        host: mq.host
        port: 1234
```

Per ActiveMQ Artemis con protocollo STOMP:

```yaml
stage:
  deploy:
    QUEUE_CONFIGURATION:
      stomp:
        host: activemq.host
        port: 61616
        user: username
        password: password
```

{{merge-options}}

Nell&#39;esempio seguente i nuovi valori vengono uniti a una configurazione esistente:

```yaml
stage:
  deploy:
    QUEUE_CONFIGURATION:
      _merge: true
      amqp:
        host: changed1.host
        port: 5672
      amqp2:
        host: changed2.host2
        port: 12345
      mq:
        host: changedmq.host
        port: 1234
```

## `REDIS_BACKEND`

- **Predefinito**—`Cm_Cache_Backend_Redis`

Specifica la configurazione del modello back-end per la cache Redis.

La cache Redis non è supportata per Adobe Commerce 2.4.9 o per versioni patch successive a 2.4.5-p16, 2.4.6-p14, 2.4.7-p9 e 2.4.8-p4. Per queste versioni, utilizzare Valkey e la configurazione `VALKEY_BACKEND` corrispondente. Verificare sempre il servizio cache supportato nei [requisiti di sistema](https://experienceleague.adobe.com/it/docs/commerce-operations/installation-guide/system-requirements).

Per le versioni supportate da Redis, i modelli di back-end disponibili includono:

- `Cm_Cache_Backend_Redis`
- `\Magento\Framework\Cache\Backend\Redis`
- `\Magento\Framework\Cache\Backend\RemoteSynchronizedCache`

L&#39;esempio seguente abilita il back-end della cache sincronizzata in remoto e la cache L2:

```yaml
stage:
  deploy:
    REDIS_BACKEND: '\Magento\Framework\Cache\Backend\RemoteSynchronizedCache'
```

>[!NOTE]
>
> Quando `\Magento\Framework\Cache\Backend\RemoteSynchronizedCache` è selezionato, `ece-tools` genera automaticamente la configurazione della cache L2. Per personalizzare la configurazione generata, utilizzare [`CACHE_CONFIGURATION`](#cache_configuration).

## `REDIS_USE_SLAVE_CONNECTION`

- **Predefinito**—`false`

>[!TIP]
>
>`REDIS_USE_SLAVE_CONNECTION` è supportato solo in cluster Adobe Commerce su Cloud Staging e Production Pro. Non è supportato nei progetti iniziali.

Adobe Commerce può leggere più istanze Redis in modo asincrono. Impostare questa variabile su `true` per utilizzare una connessione di sola lettura a una replica Redis per il traffico di lettura mentre l&#39;istanza primaria gestisce il traffico di lettura/scrittura. Per rimuovere un array di connessione di sola lettura esistente da `env.php`, impostarlo su `false`.

```yaml
stage:
  deploy:
    REDIS_USE_SLAVE_CONNECTION: true
```

Devi avere un servizio [Redis configurato](../services/redis.md) nei file `.magento.app.yaml` e `services.yaml`.

[ECE-Tools versione 2002.0.18](../release-notes/cloud-release-archive.md#v2002018) e successive utilizza impostazioni più a tolleranza di errore. Se Adobe Commerce non è in grado di leggere i dati dalla replica Redis, viene eseguito il fallback all’istanza primaria Redis.

La connessione di sola lettura non è disponibile nell’ambiente di integrazione. Se si utilizza [`CACHE_CONFIGURATION`](#cache_configuration), unire le modifiche nella configurazione generata e verificare che la configurazione risultante mantenga la connessione di replica.

## `VALKEY_BACKEND`

- **Predefinito**—`Cm_Cache_Backend_Redis`
- **Versione**—Versioni di Adobe Commerce che supportano Valkey

`VALKEY_BACKEND` specifica il modello di back-end per la configurazione della cache di Valkey. Il valore predefinito utilizza un nome di classe legacy compatibile con Redis; ciò non significa che il servizio debba essere Redis.

Per le versioni di Adobe Commerce precedenti alla 2.4.9 che supportano Valkey, i modelli di back-end includono:

- `Cm_Cache_Backend_Redis`
- `\Magento\Framework\Cache\Backend\Redis`
- `\Magento\Framework\Cache\Backend\RemoteSynchronizedCache`

Adobe Commerce 2.4.9 e versioni successive supportano anche `symfony_l2`, l&#39;implementazione L2 basata su Symfony Cache. `symfony_l2` è supportato solo con Valkey.

### Configurare la cache sincronizzata remota

Per Adobe Commerce 2.4.8, utilizza la seguente configurazione quando è appropriata l’implementazione della cache sincronizzata in remoto:

```yaml
stage:
  deploy:
    VALKEY_BACKEND: '\Magento\Framework\Cache\Backend\RemoteSynchronizedCache'
```

Se si specifica il back-end sincronizzato in remoto, la cache L2 verrà attivata e `ece-tools` genererà automaticamente la configurazione della cache. Vedere il [file di configurazione di esempio](https://experienceleague.adobe.com/it/docs/commerce-operations/implementation-playbook/best-practices/planning/redis-valkey-service-configuration#customize-the-symfony-l2-cache-configuration). Per personalizzare la configurazione generata, utilizzare [`CACHE_CONFIGURATION`](#cache_configuration).

### Configurare l’implementazione della cache L2 di Symfony moderna

Per Adobe Commerce 2.4.9 e versioni successive, utilizza l’implementazione di Symfony L2:

```yaml
stage:
  deploy:
    VALKEY_BACKEND: 'symfony_l2'
```

Se si specifica `symfony_l2` come modello di back-end Valkey, la cache L2 verrà attivata e `ece-tools` genererà automaticamente la configurazione della cache L2 dai dettagli di connessione al servizio Valkey, inclusi i front-end `default` e `stale_cache_enabled`. Definire `CACHE_CONFIGURATION` solo quando è necessario personalizzare le opzioni di back-end supportate, ad esempio la directory della cache locale. Consulta [Implementazione della cache L2 di Symfony](https://experienceleague.adobe.com/it/docs/commerce-operations/implementation-playbook/best-practices/planning/redis-valkey-service-configuration#configure-symfony-l2-cache){target="_blank"} nella _Guida alla configurazione di Adobe Commerce_.

>[!NOTE]
>
>Adobe Commerce 2.4.9 include miglioramenti alla cache di Symfony L2, tra cui l&#39;archiviazione dei tag della cache, l&#39;annullamento della validità e la compressione, con la patch ACP2E-5132, la riduzione dell&#39;I/O del disco, l&#39;eliminazione delle voci di cache obsolete e la riduzione del sovraccarico di memoria e rete.

## `VALKEY_USE_SLAVE_CONNECTION`

- **Predefinito**—`false`
- **Versione**—Adobe Commerce 2.4.8 e versioni successive

>[!TIP]
>
>`VALKEY_USE_SLAVE_CONNECTION` è supportato solo in cluster Adobe Commerce su Cloud Staging e Production Pro. Non è supportato nei progetti iniziali.

Adobe Commerce può leggere più istanze di Valkey in modo asincrono. Impostare `VALKEY_USE_SLAVE_CONNECTION` su `true` per utilizzare una connessione _di sola lettura_ a una replica di Valkey per il traffico di sola lettura mentre l&#39;istanza primaria gestisce il traffico di lettura/scrittura. Questa connessione migliora le prestazioni tramite il bilanciamento del carico, perché solo un nodo gestisce il traffico di lettura-scrittura. Per rimuovere un array di connessione di sola lettura esistente da `env.php`, impostarlo su `false`.

```yaml
stage:
  deploy:
    VALKEY_USE_SLAVE_CONNECTION: true
```

Devi avere un servizio [Valkey configurato](../services/valkey.md) in `.magento.app.yaml` e `.magento/services.yaml`. La disponibilità di una connessione di replica dipende dalla topologia del progetto e dalla versione installata di `ece-tools`.

Prima di affidarsi a questa impostazione, controllare il valore `MAGENTO_CLOUD_RELATIONSHIPS` decodificato e verificare che sia presente una relazione di replica. Ad esempio:

```bash
echo "$MAGENTO_CLOUD_RELATIONSHIPS" | base64 -d | json_pp
```

Per `symfony_l2`, il supporto delle repliche richiede gli aggiornamenti rilevanti di `ece-tools` e delle patch cloud. Eseguire l&#39;aggiornamento alla versione `ece-tools` più recente prima di abilitare questa impostazione. Se dopo la ridistribuzione non è presente alcuna relazione di replica, contattare il supporto Adobe Commerce.

Quando si utilizza [`CACHE_CONFIGURATION`](#cache_configuration), unire le sostituzioni supportate nella configurazione generata anziché sostituire la struttura di connessione generata.

## `RESOURCE_CONFIGURATION`

- **Predefinito**—Non impostato

Associa un nome di risorsa a una connessione al database. Questa configurazione corrisponde alla sezione `resource` del file `env.php`.

{{merge-options}}

Nell&#39;esempio seguente i nuovi valori vengono uniti a una configurazione esistente:

```yaml
stage:
  deploy:
    RESOURCE_CONFIGURATION:
      _merge: true
      default_setup:
        connection: default
```

## `SCD_COMPRESSION_LEVEL`

- **Predefinito**—`4`

Specifica il livello di compressione [gzip](https://www.gnu.org/software/gzip) (da `0` a `9`) da utilizzare per la compressione del contenuto statico. Impostarlo su `0` per disabilitare la compressione.

```yaml
stage:
  deploy:
    SCD_COMPRESSION_LEVEL: 5
```

## `SCD_COMPRESSION_TIMEOUT`

- **Predefinito**—`600`

Quando il tempo necessario per comprimere le risorse statiche supera il limite di timeout di compressione, il processo di distribuzione viene interrotto. Imposta il tempo massimo di esecuzione, in secondi, per il comando di compressione del contenuto statico.

```yaml
stage:
  deploy:
    SCD_COMPRESSION_TIMEOUT: 800
```

## `SCD_MATRIX`

- **Predefinito**—_Non impostato_

È possibile configurare più impostazioni internazionali per tema. Questa personalizzazione velocizza il processo di distribuzione riducendo il numero di file dei temi non necessari. Ad esempio, puoi distribuire il tema _magento/backend_ in inglese e un tema personalizzato in altre lingue.

L&#39;esempio seguente distribuisce il tema `Magento/backend` con tre impostazioni internazionali:

```yaml
stage:
  deploy:
    SCD_MATRIX:
      "magento/backend":
        language:
          - en_US
          - fr_FR
          - af_ZA
```

Inoltre, puoi scegliere di _non_ distribuire un tema:

```yaml
stage:
  deploy:
    SCD_MATRIX:
      "magento/backend": [ ]
```

## `SCD_MAX_EXECUTION_TIME`

- **Predefinito**—_Non impostato_

Consente di aumentare il tempo massimo di esecuzione previsto per la distribuzione del contenuto statico.

Per impostazione predefinita, Adobe Commerce imposta l’esecuzione massima prevista su 900 secondi, ma alcuni scenari richiedono più tempo per completare la distribuzione di contenuto statico per un progetto Cloud.

```yaml
stage:
  deploy:
    SCD_MAX_EXECUTION_TIME: 3600
```

{{scd-timing-warning}}

## `SCD_NO_PARENT`

- **Predefinito**—`false`

Nella fase di distribuzione, impostare `SCD_NO_PARENT: true` in modo che la generazione di contenuto statico per i temi principali non venga eseguita durante la fase di distribuzione. Questa impostazione consente di ridurre al minimo i tempi di distribuzione e di evitare i tempi di inattività del sito che possono verificarsi se la generazione di contenuto statico non riesce durante la distribuzione. Vedi [Distribuzione di contenuto statico](../deploy/static-content.md).

```yaml
stage:
  deploy:
    SCD_NO_PARENT: true
```

## `SCD_STRATEGY`

- **Predefinito**—`quick`

Consente di personalizzare la [strategia di distribuzione](https://experienceleague.adobe.com/it/docs/commerce-operations/configuration-guide/cli/static-view/static-view-file-strategy) per il contenuto statico. Vedere [Distribuire i file di visualizzazione statici](https://experienceleague.adobe.com/it/docs/commerce-operations/configuration-guide/cli/static-view/static-view-file-deployment).

Utilizza queste opzioni _only_ se hai più di una lingua:

- `standard`: distribuisce tutti i file di visualizzazione statica per tutti i pacchetti.
- `quick`—(_default_) riduce al minimo i tempi di distribuzione.
- `compact`: consente di risparmiare spazio su disco nel server.

```yaml
stage:
  deploy:
    SCD_STRATEGY: "compact"
```

## `SCD_THREADS`

- **Predefinito**—Automatico

Imposta il numero di thread per la distribuzione del contenuto statico. Il valore predefinito è impostato in base al numero di thread CPU rilevati e non supera il valore 4. L&#39;aumento del numero di thread velocizza la distribuzione dei contenuti statici. La riduzione del numero di thread ne rallenta il rallentamento. Puoi impostare il valore del thread, ad esempio:

```yaml
stage:
  deploy:
    SCD_THREADS: 2
```

Per ridurre ulteriormente il tempo di distribuzione, utilizzare [Gestione configurazione](../store/store-settings.md) con il comando `scd-dump` per spostare la distribuzione statica nella fase di compilazione.

## `SEARCH_CONFIGURATION`

- **Predefinito**—_Non impostato_

Utilizza questa variabile di ambiente per mantenere le impostazioni del servizio di ricerca personalizzate tra le distribuzioni. Ad esempio:

Configurazione Elasticsearch:

```yaml
stage:
  deploy:
    SEARCH_CONFIGURATION:
      engine: elasticsearch
      elasticsearch_server_hostname: http://elasticsearch.internal
      elasticsearch_server_port: '9200'
      elasticsearch_index_prefix: magento2
      elasticsearch_server_timeout: '15'
```

Configurazione di OpenSearch (per Commerce 2.4.6 e versioni successive):

```yaml
stage:
  deploy:
    SEARCH_CONFIGURATION:
      engine: opensearch
      opensearch_server_hostname: 'http://opensearch.internal'
      opensearch_server_port: '9200'
      opensearch_index_prefix: 'magento2'
      opensearch_server_timeout: '15'
```

{{merge-options}}

L’esempio che segue unisce un nuovo valore alla configurazione esistente:

```yaml
stage:
  deploy:
    SEARCH_CONFIGURATION:
      engine: elasticsearch
      elasticsearch_server_port: '9200'
      _merge: true
```

## `SESSION_CONFIGURATION`

- **Predefinito**—_Non impostato_

Utilizzare `SESSION_CONFIGURATION` per configurare l&#39;archiviazione della sessione. L’esempio seguente utilizza la struttura di configurazione delle sessioni compatibile con Redis. Utilizzala solo con la combinazione di denominazione e servizio archiviazione sessione supportata dalla versione esatta di Commerce. Per le sessioni con Valkey, seguire l&#39;esempio [Sessione Valkey-Storage](https://experienceleague.adobe.com/it/docs/commerce-operations/implementation-playbook/best-practices/planning/redis-valkey-service-configuration#apply-all-best-practice-recommendations).

Non presumere che le variabili della cache come `VALKEY_BACKEND` o `REDIS_BACKEND` configurino le sessioni. La configurazione della cache e della sessione è indipendente. Nei progetti Cloud, utilizza la relazione di servizio e la configurazione generata laddove possibile; non codificare valori specifici dell’ambiente senza sostituire l’host e la porta di esempio.

```yaml
stage:
  deploy:
    SESSION_CONFIGURATION:
      redis:
        bot_first_lifetime: 100
        bot_lifetime: 10001
        database: 0
        disable_locking: 1
        host: 'redis.internal'
        max_concurrency: 10
        max_lifetime: 10001
        min_lifetime: 100
        port: 6379
      save: redis
```

Sostituire `redis.internal` e `6379` con l&#39;host e la porta del servizio sessione per l&#39;ambiente di destinazione quando la configurazione della distribuzione richiede dettagli di connessione espliciti.

{{merge-options}}

L’esempio che segue unisce un nuovo valore alla configurazione esistente:

```yaml
stage:
  deploy:
    SESSION_CONFIGURATION:
      _merge: true
      redis:
        max_concurrency: 10
```

## `SKIP_SCD`

- **Predefinito**— _Non impostato_

Imposta su `true` per saltare la distribuzione del contenuto statico durante la fase di distribuzione.

Nella fase di distribuzione, impostare `SKIP_SCD: true` in modo che la compilazione del contenuto statico non avvenga durante la fase di distribuzione. Questa impostazione consente di ridurre al minimo i tempi di distribuzione e di evitare i tempi di inattività del sito che possono verificarsi se la generazione di contenuto statico non riesce durante la distribuzione. Vedi [Distribuzione di contenuto statico](../deploy/static-content.md).

```yaml
stage:
  deploy:
    SKIP_SCD: true
```

## `UPDATE_URLS`

- **Predefinito**—`true`

Durante la distribuzione, sostituire gli URL di base di Adobe Commerce nel database con gli URL del progetto specificati dalla variabile [`MAGENTO_CLOUD_ROUTES`](variables-cloud.md). Questa configurazione è utile per lo sviluppo locale, dove gli URL di base sono impostati per l’ambiente locale. Quando distribuisci in un ambiente Cloud, gli URL vengono aggiornati in modo da poter accedere alla vetrina e all’amministratore tramite gli URL del progetto.

Se è necessario aggiornare gli URL durante la distribuzione in ambienti di staging e produzione Pro o Starter, utilizzare la variabile [`FORCE_UPDATE_URLS`](#force_update_urls).

```yaml
stage:
  deploy:
    UPDATE_URLS: false
```

## `USE_LUA`

- **Predefinito**—`false`
- **Versione**—Adobe Commerce 2.4.7 e versioni successive

Controlla l&#39;opzione di back-end della cache `use_lua` in `env.php` per il front-end della cache predefinito (e, quando si utilizza il backend `symfony_l2`, le opzioni di back-end remoto del front-end `stale_cache_enabled`). Opzione non applicata al front-end `page_cache`.

Utilizzare il valore predefinito `false` a meno che il supporto Adobe non fornisca esplicitamente indicazioni diverse.

```yaml
stage:
  deploy:
    USE_LUA: false
```

>[!WARNING]
>
>In Adobe Commerce 2.4.7 e 2.4.8, l&#39;impostazione `USE_LUA: true` può causare il danneggiamento della cache e problemi di mancato recapito della cache di GraphQL.
>
>A partire da Adobe Commerce 2.4.9, utilizza le linee guida per la configurazione della cache di Valkey per la versione di Commerce e non fare affidamento su `USE_LUA` per le nuove distribuzioni.

## `LUA_KEY`

La variabile `LUA_KEY` è obsoleta. Se `LUA_KEY` è incluso in `.magento.env.yaml`, rimuoverlo durante la migrazione. Utilizzare le variabili `USE_LUA` e `USE_LUA_ON_GC`.

## `USE_LUA_ON_GC`

- **Predefinito**—`true`
- **Versione**—Adobe Commerce 2.4.8 e versioni successive

Controlla l&#39;opzione di back-end della cache `use_lua_on_gc` in `env.php` per il front-end predefinito della cache (e, quando si utilizza il backend `symfony_l2`, le opzioni di back-end remoto del front-end `stale_cache_enabled`) per la raccolta di oggetti inattivi. Opzione non applicata al front-end `page_cache`.

Utilizzare il valore predefinito `true` per mantenere la pulizia dei tag della cache atomica durante il processo cron `backend_clean_cache`.

```yaml
stage:
  deploy:
    USE_LUA_ON_GC: true
```

>[!WARNING]
>
>In Adobe Commerce 2.4.8, l&#39;impostazione di `USE_LUA_ON_GC: false` può causare un errore invisibile all&#39;utente e richiedere il ripristino di uno svuotamento completo della cache.
>
>Nella versione 2.4.9 o successiva, seguire le [istruzioni del servizio cache](https://experienceleague.adobe.com/it/docs/commerce-operations/configuration-guide/cache/redis/redis-pg-cache) per la versione installata.

## `VERBOSE_COMMANDS`

- **Predefinito**—_Non impostato_

Attiva o disattiva il livello di dettaglio di debug [Symfony](https://symfony.com/doc/current/console/verbosity.html) per i comandi CLI `bin/magento` eseguiti durante la fase di distribuzione.

>[!NOTE]
>
>Per utilizzare l&#39;impostazione VERBOSE_COMMANDS per controllare i dettagli nell&#39;output del comando sia per i comandi CLI `bin/magento` riusciti che non riusciti, è necessario impostare [MIN_LOGGING_LEVEL](variables-global.md#minlogginglevel) `debug`.

Scegli il livello di dettaglio fornito nei registri:

- `-v`= output normale
- `-vv`= output più dettagliato
- `-vvv` = output dettagliato ideale per il debug

```yaml
stage:
  deploy:
    VERBOSE_COMMANDS: "-vv"
```
