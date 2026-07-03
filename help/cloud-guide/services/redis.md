---
title: Configurazione del servizio Redis
description: Scopri come impostare e ottimizzare Redis come soluzione di cache back-end per Adobe Commerce sull’infrastruttura cloud.
feature: Cloud, Cache, Services
exl-id: be6f2462-0878-47e3-b906-ebdd4aa319f2
TQID: https://experienceleague.adobe.com/Q3w1Y1sRuQSwqmbxGfEBavrvHe0ecI9qWJjsfVc2yPU
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
source-git-commit: 5951c3001d665423634f06cd7cc277cd0fd80bbd
workflow-type: tm+mt
source-wordcount: 391
ht-degree: 0%

---

# Configurazione del servizio Redis

[Redis](https://redis.io) è una soluzione cache back-end opzionale che sostituisce Zend Framework Zend_Cache_Backend_File, utilizzato da Adobe Commerce per impostazione predefinita.

>[!IMPORTANT]
>
>La cache Redis non è supportata per Adobe Commerce 2.4.9 o versioni di patch successive a 2.4.5-p16, 2.4.6-p14, 2.4.7-p9 e 2.4.8-p5. Utilizza Valkey per la configurazione della cache quando Redis non è supportato. Consulta [Requisiti di sistema](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/system-requirements) per i servizi di cache supportati per versione.

{{service-instruction}}

**Per abilitare Redis**:

1. Aggiungere il nome e il tipo richiesti al file `.magento/services.yaml`.

   ```yaml
   myredis:
       type: redis:<version>
   ```

   Per fornire la tua configurazione Redis, aggiungi una chiave `core_config` nel file `.magento/services.yaml`:

   ```yaml
   cache:
       type: redis:<version>
   ```

1. Configurare le relazioni nel file `.magento.app.yaml`.

   ```yaml
   runtime:
       extensions:
           - redis
   
   relationships:
       redis: "redis:redis"
   ```

1. Aggiungi, esegui il commit e invia le modifiche al codice.

   ```bash
   git add .magento/services.yaml .magento.app.yaml && git commit -m "Enable redis service" && git push origin <branch-name>
   ```

1. [Verificare le relazioni del servizio](services-yaml.md#service-relationships).

{{service-change-tip}}

## Personalizzare la configurazione Redis

Per informazioni dettagliate sulla personalizzazione della configurazione Redis, vedere [Configure Redis](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/best-practices/planning/redis-valkey-service-configuration) nella _Guida alle best practice per l&#39;implementazione di Playbook_.

## Utilizzo di Redis CLI

Se la relazione Redis si chiama `redis`, è possibile accedervi utilizzando lo strumento `redis-cli`.

1. Utilizza SSH per connettersi all’ambiente di integrazione con Redis installato e configurato.

1. Aprire un tunnel SSH a un host.

   ```bash
   redis-cli -h redis.internal
   ```

## Ottieni versione Redis installata

Utilizza il seguente comando per installare la versione di Redis in un ambiente di integrazione:

```bash
redis-cli -h redis.internal info | grep version
```

Risposta di esempio:

```
redis_version:7.0.5
gcc_version:8.3.0
```

### Redis su staging e produzione Pro

Per ottenere la versione Redis installata in un ambiente di staging o produzione, utilizzare il comando `redis-server`:

```bash
redis-server -v
```

```
Redis server v=7.0.5 ...
```

Utilizzate il seguente comando per installare la configurazione Redis in un ambiente Pro Staging o Production:

```bash
echo $MAGENTO_CLOUD_RELATIONSHIPS | base64 -d | json_pp
```

Risposta di esempio:

```json
"redis" : [
    {
        "cluster" : "project-master-123abc4",
        "fragment" : null,
        "host" : "redis.internal",
        "host_mapped" : false,
        "hostname" : "oblahblahblahblahe.redis.service._.magentosite.cloud",
        "ip" : "169.254.10.10",
        "password" : null,
        "path" : null,
        "port" : 6379,
        "public" : false,
        "query" : {},
        "rel" : "redis",
        "scheme" : "redis",
        "service" : "redis",
        "type" : "redis:7.0.5",
        "username" : null
    }
]
```

## Risoluzione dei problemi di Redis

Consulta i seguenti articoli sul supporto Adobe Commerce per assistenza nella risoluzione dei problemi Redis:

- [Ritardo nell’accesso o nell’estrazione dell’amministratore per problema Redis](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/redis-issue-delay-magento-admin-login-or-checkout.html)
- [Implementazione della cache Redis estesa con Adobe Commerce 2.3.5+](https://experienceleague.adobe.com/docs/commerce-operations/implementation-playbook/best-practices/planning/redis-service-configuration.html)
- [Avvisi gestiti su Adobe Commerce: avviso di memoria Redis](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/support-tools/managed-alerts/managed-alerts-on-magento-commerce-redis-memory-warning-alert.html)
- [Avvisi gestiti su Adobe Commerce: Avvisi critici per la memoria Redis](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/support-tools/managed-alerts/managed-alerts-on-magento-commerce-redis-memory-critical-alert.html)
