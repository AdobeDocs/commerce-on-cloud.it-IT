---
title: Configurazione del servizio Redis
description: Scopri come impostare e ottimizzare Redis come soluzione di cache back-end per Adobe Commerce sull’infrastruttura cloud.
feature: Cloud, Cache, Services
exl-id: be6f2462-0878-47e3-b906-ebdd4aa319f2
TQID: https://experienceleague.adobe.com/Q3w1Y1sRuQSwqmbxGfEBavrvHe0ecI9qWJjsfVc2yPU
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: c1579802-ddd4-4214-8a91-97b2066abe11
source-git-commit: df2792f9d653c4561e4e40cbc71499095f63ff71
workflow-type: tm+mt
source-wordcount: 710
ht-degree: 0%

---

# Configurazione del servizio Redis

[Redis](https://redis.io) è una soluzione cache back-end facoltativa che sostituisce `Zend Framework Zend_Cache_Backend_File`, utilizzata da Adobe Commerce per impostazione predefinita.

>[!IMPORTANT]
>
>La cache Redis non è supportata per Adobe Commerce 2.4.9 o versioni patch successive a 2.4.5-p16, 2.4.6-p14, 2.4.7-p9 e 2.4.8-p4. Utilizza [Valkey](valkey.md) per la configurazione della cache in cui Redis non è supportato. Consulta [Requisiti di sistema](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/system-requirements) per i servizi di cache supportati per versione.

{{service-instruction}}

## Abilita Redis

Per abilitare Redis, aggiornare i seguenti file:

- `.magento/services.yaml`
- `.magento.app.yaml`

### Configurare il servizio

In `.magento/services.yaml`, aggiungere la definizione del servizio Redis. Sostituisci `<version>` con una versione di Redis supportata dalla tua versione di Adobe Commerce e dal modello Cloud corrente.

```yaml
cache:
  type: redis:<version>
```

Ad esempio, per una versione di Commerce e un modello Cloud che supporta Redis 7.2:

```yaml
cache:
  type: redis:7.2
```

La versione di esempio non è universale. Le versioni predefinite e supportate effettive dipendono dalla versione di Adobe Commerce, dal livello di patch e dal modello Cloud corrente. Verificare la combinazione supportata in [Requisiti di sistema](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/system-requirements) e nel modello di progetto corrente.

### Configurare la relazione di servizio

In `.magento.app.yaml` configurare la relazione tra l&#39;applicazione e il servizio Redis:

```yaml
runtime:
  extensions:
    - redis

relationships:
  redis: "cache:redis"
```

La chiave di relazione `redis` è il nome utilizzato dall&#39;applicazione per accedere al servizio. Il valore `cache:redis` è costituito dall&#39;ID servizio (`cache`) e dal tipo di servizio (`redis`) definiti in `.magento/services.yaml`.

### Eseguire il commit e distribuire le modifiche

Aggiungi, esegui il commit e invia le modifiche di configurazione:

```terminal
git add .magento/services.yaml .magento.app.yaml
git commit -m "Enable Redis service"
git push origin <branch-name>
```

Al termine della distribuzione, verificare che la relazione del servizio Redis sia disponibile.

{{service-change-tip}}

## Verifica la relazione di servizio

Dopo aver distribuito la configurazione, eseguire il comando seguente da un contenitore di applicazioni per visualizzare l&#39;oggetto `MAGENTO_CLOUD_RELATIONSHIPS` decodificato:

Utilizza SSH per connettersi all’ambiente cloud remoto, quindi esegui:

```terminal
echo "$MAGENTO_CLOUD_RELATIONSHIPS" | base64 -d | json_pp
```

Il comando visualizza tutte le relazioni di servizio configurate. Individuare la relazione `redis` per identificare i dettagli della connessione Redis.

L&#39;esempio abbreviato seguente mostra la relazione `redis`. Non è uno schema universale.

```json
{
   "database" : [
      {
         "host" : "database.internal",
         "port" : 3306,
         "path" : "main",
         "scheme" : "mysql"
      }
   ],
   "opensearch" : [
      {
         "host" : "opensearch.internal",
         "port" : 9200,
         "path" : null,
         "scheme" : "http"
      }
   ],
   "redis" : [
      {
         "host" : "redis.internal",
         "port" : 6379,
         "path" : null,
         "scheme" : "redis"
      }
   ]
}
```

L’output varia in base all’ambiente e alla configurazione del servizio. Non inserire nel codice rigido nomi host, porte, indirizzi IP, nomi di cluster, versioni di servizi, nomi utente o password di questo esempio. Utilizzare i valori restituiti da `MAGENTO_CLOUD_RELATIONSHIPS` nell&#39;ambiente di destinazione.

Se `jq` è disponibile, utilizzare il comando seguente per visualizzare solo la relazione Redis:

```terminal
printf '%s' "$MAGENTO_CLOUD_RELATIONSHIPS" \
  | base64 -d \
  | jq '{redis: .redis}'
```

Per ulteriori informazioni sulle relazioni tra i servizi, vedere [Configurare i servizi](services-yaml.md).

## Personalizzare la configurazione Redis

Per i consigli relativi a cache, sessione, L2 e connessione di replica, vedere [Best practice per la configurazione del servizio Valkey e Redis](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/best-practices/planning/redis-valkey-service-configuration) nella _Guida alle best practice per l&#39;implementazione della playbook_.

## Utilizzo di Redis CLI

Se la relazione Redis si chiama `redis`, utilizzare l&#39;host e la porta restituiti da `MAGENTO_CLOUD_RELATIONSHIPS` per connettersi a Redis.

Connettersi all&#39;ambiente con Redis installato e configurato ed eseguire il comando seguente:

```terminal
redis-cli -h <host> -p <port>
```

**Esempio**

```terminal
redis-cli -h redis.internal -p 6379
```

## Scarica la versione Redis installata

>[!BEGINTABS]

>[!TAB Ambiente di integrazione]

In un ambiente di integrazione, utilizzare l&#39;host e la porta restituiti dalla relazione `redis` per eseguire:

```terminal
redis-cli -h <host> -p <port> info | grep version
```

**Risposta di esempio**

```text
redis_version:<installed-version>
gcc_version:<gcc-version>
```

I dettagli della versione e della build variano a seconda dell’ambiente. Non trattare una versione di esempio visualizzata come una versione richiesta o di servizio universale.

>[!TAB Gestione temporanea e produzione Pro]

Negli ambienti di staging e produzione Pro, eseguire:

```terminal
redis-server -v
```

**Risposta di esempio**

```text
Redis server v=<installed-version> ...
```

I dettagli della versione e della build variano a seconda dell’ambiente. Non trattare una versione di esempio visualizzata come una versione richiesta o di servizio universale.

>[!ENDTABS]

## Risoluzione dei problemi di Redis

Consulta i seguenti articoli sul supporto Adobe Commerce per assistenza nella risoluzione dei problemi Redis:

- [Avvisi gestiti su Adobe Commerce: avviso di memoria Redis](https://experienceleague.adobe.com/en/docs/commerce-operations/tools/managed-alerts-for-adobe-commerce/managed-alerts-on-magento-commerce-redis-memory-warning-alert)
- [Avvisi gestiti su Adobe Commerce: Avvisi critici per la memoria Redis](https://experienceleague.adobe.com/en/docs/commerce-operations/tools/managed-alerts-for-adobe-commerce/managed-alerts-on-magento-commerce-redis-memory-critical-alert)

### Gli errori di pulizia della cache fanno riferimento a Redis in una cache configurata con Valkey

Un errore di pulizia della cache pre-distribuzione può visualizzare il codice di errore `[107]` (`clean-redis-cache`) e un messaggio `Connection to Redis` anche quando il servizio `cache` è configurato come Valkey. `ece-tools` utilizza questo codice di errore e messaggio legacy orientato a Redis per il passaggio di pulizia della cache, indipendentemente dal servizio che supporta la relazione `cache`, pertanto il testo non indica che Redis è installato.

Se l&#39;errore sottostante è un errore DNS, ad esempio `Name or service not known` per l&#39;host di relazione, il passaggio di distribuzione è stato eseguito prima che la relazione di servizio fosse disponibile oppure il nome della relazione in `.magento.app.yaml` non corrisponde all&#39;ID del servizio in `.magento/services.yaml`. Vedere [Verificare la relazione del servizio](#verify-the-service-relationship).
