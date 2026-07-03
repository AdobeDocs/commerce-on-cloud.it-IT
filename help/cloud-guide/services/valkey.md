---
title: Configurare il servizio Valkey
description: Scopri come impostare e ottimizzare Valkey come soluzione di cache back-end per Adobe Commerce su infrastruttura cloud.
feature: Cloud, Cache, Services
exl-id: f8933e0d-a308-4c75-8547-cb26ab6df947
TQID: https://experienceleague.adobe.com/-aBnwClJGQlRkEfugtChxbjLObLzTu0xl1IvkYUVRsk
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: f1e6c9da5dacb144dc3e1a09885c1a9b11ce54ee
workflow-type: tm+mt
source-wordcount: 259
ht-degree: 0%

---

# Configurare il servizio Valkey

[Valkey](https://valkey.io) è una soluzione cache back-end facoltativa che sostituisce `Zend Framework Zend_Cache_Backend_File`, utilizzata da Adobe Commerce per impostazione predefinita. Se sostituisci le versioni predefinite di Commerce 2.4.9+ o patch successive a 2.4.5-p16, 2.4.6-p14, 2.4.7-p9 e alle righe di rilascio 2.4.8-p5, devi utilizzare Valkey.

Vedi [Configurare Valkey](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/best-practices/planning/redis-valkey-service-configuration){target="_blank"} nella _Guida alle best practice per l&#39;implementazione del playbook_.

{{service-instruction}}

**Per sostituire Redis con Valkey, aggiornare la configurazione nei tre file seguenti**:

1. Sostituire la configurazione Redis con il nome e il tipo Valkey richiesti nel file `.magento/services.yaml`.

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

1. Configurare `.magento.env.yaml` per sostituire la configurazione Redis nel modo seguente:.

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

{{valkey-newrelic}}

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
