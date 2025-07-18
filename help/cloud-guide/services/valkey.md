---
title: Configurare il servizio Valkey
description: Scopri come impostare e ottimizzare Valkey come soluzione di cache back-end per Adobe Commerce su infrastruttura cloud.
feature: Cloud, Cache, Services
exl-id: f8933e0d-a308-4c75-8547-cb26ab6df947
source-git-commit: cf2e659267445603b3f5eaf877f4eb7ac0c1b54c
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---

# Configurare il servizio Valkey

[Valkey](https://valkey.io) è una soluzione cache back-end facoltativa che sostituisce `Zend Framework Zend_Cache_Backend_File`, utilizzata da Adobe Commerce per impostazione predefinita.

Vedi [Configurazione di Valkey](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cache/valkey/config-valkey.html){target="_blank"} nella _Guida alla configurazione_.

{{service-instruction}}

**Per sostituire Redis con Valkey, aggiornare la configurazione nei tre file seguenti**:

1. Aggiungere il nome e il tipo richiesti al file `.magento/services.yaml`.

   ```yaml
   cache:
       type: valkey:<version>
   ```

   Per fornire la tua configurazione Valkey, aggiungi una chiave `core_config` nel file `.magento/services.yaml`:

   ```yaml
   cache:
       type: valkey:8.0
   ```

1. Configurare le relazioni nel file `.magento.app.yaml`.

   ```yaml
   relationships:
       valkey: "cache:valkey"
   ```

1. Configura `.magento.env.yaml` come segue:.

   ```yaml
    stage:
        deploy:
        VALKEY_USE_SLAVE_CONNECTION: true
        VALKEY_BACKEND: '\Magento\Framework\Cache\Backend\RemoteSynchronizedCache'
   ```

1. Aggiungi, esegui il commit e invia le modifiche al codice.

   ```bash
   git add .magento/services.yaml .magento.app.yaml .magento.env.yaml && git commit -m "Enable valkey service" && git push origin <branch-name>
   ```

1. [Verificare le relazioni del servizio](services-yaml.md#service-relationships).

{{service-change-tip}}

## Utilizzo di Valkey CLI

Se la relazione Valkey è denominata `valkey`, è possibile accedervi utilizzando lo strumento `valkey-cli`.

1. Utilizza SSH per connettersi all’ambiente di integrazione con Valkey installato e configurato.

1. Aprire un tunnel SSH a un host.

   ```bash
   valkey-cli -h valkey.internal
   ```

## Scarica versione di Valkey installata

Utilizza il seguente comando per ottenere la versione di Valkey installata in un ambiente di integrazione:

```bash
valkey-cli -h valkey.internal info | grep version
```

Risposta:

```
valkey_version:8.0.1
gcc_version:12.2.0
```

### Valkey su staging e produzione Pro

Per ottenere la versione di Valkey installata in un ambiente di staging o produzione, utilizzare il comando `valkey-server`:

```bash
valkey-server -v
```

```bash
Valkey server v=8.0.1 ...
```

Utilizzate il seguente comando per installare la configurazione Valkey in un ambiente di staging o produzione Pro:

```bash
echo $MAGENTO_CLOUD_RELATIONSHIPS | base64 -d | json_pp
```

Risposta:

```json
"valkey" : [
    {
        "cluster" : "project-master-abc0003",
        "epoch" : 0,
        "fragment" : null,
        "host" : "valkeycache.internal",
        "host_mapped" : false,
        "hostname" : "oblahblahblahblahe.cache.service._.magentosite.cloud",
        "instance_ips" : [
        "123.456.789.012"
        ],
        "ip" : "123.456.789.012",
        "password" : null,
        "path" : null,
        "port" : 6379,
        "public" : false,
        "query" : {},
        "rel" : "valkey",
        "scheme" : "valkey",
        "service" : "cache",
        "type" : "valkey:8.0",
        "username" : null
    }
]
```
