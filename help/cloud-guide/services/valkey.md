---
title: Configurare il servizio Valkey
description: Scopri come impostare e ottimizzare Valkey come soluzione di cache back-end per Adobe Commerce sull’infrastruttura cloud, inclusa la sostituzione di Redis e la personalizzazione delle impostazioni di back-end della cache.
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
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
source-git-commit: d5d947f9858ab15e2e5daed7848163846580f883
workflow-type: tm+mt
source-wordcount: 701
ht-degree: 0%

---

# Configurare il servizio Valkey

[Valkey](https://valkey.io) è una soluzione di cache back-end opzionale per Adobe Commerce sull&#39;infrastruttura cloud. Valkey è richiesto quando si esegue l’override della configurazione predefinita della cache in Adobe Commerce 2.4.9 e versioni successive, o nelle versioni patch successive a 2.4.5-p16, 2.4.6-p14, 2.4.7-p9 e 2.4.8-p4.

{{service-instruction}}

## Configura Valkey

Per sostituire Redis con Valkey, aggiornare i seguenti file:

- `.magento/services.yaml`
- `.magento.app.yaml`

### Configurare il servizio

In `.magento/services.yaml`, sostituire la definizione del servizio Redis con una definizione del servizio Valkey. Sostituisci `<version>` con una versione di Valkey supportata dalla versione di Adobe Commerce e dal modello Cloud corrente.

```yaml
cache:
  type: valkey:<version>
```

**Esempio**

```yaml
cache:
  type: valkey:8.0
```

La versione di esempio non è universale. Le versioni predefinite e supportate effettive dipendono dalla versione di Adobe Commerce e dal modello Cloud corrente. Utilizza la versione specificata dal modello di progetto corrente. Per ulteriori informazioni, vedere [Configurare i servizi](services-yaml.md#service-versions).

>[!WARNING]
>
>Se modifichi l’ID del servizio, il servizio esistente viene rimosso e viene creato un nuovo servizio. I dati esistenti nel servizio rimosso vengono eliminati in modo permanente. Esegui il backup dell’ambiente prima di rinominare un servizio.

Non presumere che la cache e i dati della sessione persistano quando si modifica il valore `type` da `redis:<version>` a `valkey:<version>`, anche quando si mantiene lo stesso ID servizio. Considera la migrazione come creazione di una nuova cache: la cache esistente e i dati della sessione non vengono conservati e gli utenti vengono disconnessi al termine della migrazione.

### Configurare la relazione di servizio

In `.magento.app.yaml` configurare la relazione tra l&#39;applicazione e il servizio Valkey:

```yaml
relationships:
  valkey: "cache:valkey"
```

La chiave di relazione `valkey` è il nome utilizzato dall&#39;applicazione per accedere al servizio. Il valore `cache:valkey` fa riferimento all&#39;ID servizio e al tipo di servizio definiti in `.magento/services.yaml`.

>[!TIP]
>
>Adobe Commerce comunica con Valkey tramite la libreria client `credis`, che per impostazione predefinita funziona su socket PHP normali. Per migliorare le prestazioni, abilitare l&#39;estensione PHP `redis` in `.magento.app.yaml`. `credis` utilizza automaticamente l&#39;estensione compilata quando è disponibile.
>
>```yaml
>runtime:
>   extensions:
>       - redis
>```

### Eseguire il commit e distribuire le modifiche

Aggiungi, esegui il commit e invia le modifiche di configurazione:

```terminal
git add .magento/services.yaml .magento.app.yaml
git commit -m "Enable Valkey service"
git push origin <branch-name>
```

Al termine della distribuzione, verificare che la relazione del servizio Valkey sia disponibile.

{{service-change-tip}}

{{valkey-newrelic}}

## Personalizzare la configurazione Valkey

Per i consigli relativi a cache, sessione, L2 e connessione di replica, vedere [Best practice per la configurazione del servizio Valkey e Redis](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/best-practices/planning/redis-valkey-service-configuration) nella _Guida alle best practice per l&#39;implementazione della playbook_.

## Verifica la relazione di servizio

Per visualizzare l&#39;oggetto `MAGENTO_CLOUD_RELATIONSHIPS` decodificato, eseguire il comando seguente da un contenitore di applicazioni dopo la distribuzione della configurazione:

Utilizza SSH per connettersi all’ambiente cloud remoto, quindi esegui:

```terminal
echo "$MAGENTO_CLOUD_RELATIONSHIPS" | base64 -d | json_pp
```

Il comando visualizza tutte le relazioni di servizio configurate. Per identificare i dettagli di connessione Valkey, individuare la relazione valkey.

**Output di esempio**

L&#39;esempio abbreviato seguente mostra la relazione `valkey`. Non è uno schema universale.

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
   "valkey" : [
      {
         "host" : "valkey.internal",
         "port" : 6379,
         "path" : null,
         "scheme" : "valkey"
      }
   ]
}
```

L’output varia in base all’ambiente e alla configurazione del servizio. Non inserire nel codice rigido nomi host, porte, indirizzi IP, nomi di cluster, versioni di servizi, nomi utente o password di questo esempio. Utilizzare i valori restituiti da `MAGENTO_CLOUD_RELATIONSHIPS` nell&#39;ambiente di destinazione.

Se `jq` è disponibile, visualizzare solo la relazione Valkey:

```terminal
printf '%s' "$MAGENTO_CLOUD_RELATIONSHIPS" \
  | base64 -d \
  | jq '{valkey: .valkey}'
```

Per ulteriori informazioni sulle relazioni tra i servizi, vedere [Configurare i servizi](services-yaml.md).

## Utilizzo di Valkey CLI

Supponendo che la relazione Valkey sia denominata `valkey`, utilizzare l&#39;host e la porta restituiti da `MAGENTO_CLOUD_RELATIONSHIPS` per connettersi a Valkey:

```terminal
valkey-cli -h <host> -p <port>
```

**Esempio**

```terminal
valkey-cli -h valkey.internal -p 6379
```

## Scarica la versione installata di Valkey

>[!BEGINTABS]

>[!TAB Ambiente di integrazione]

In un ambiente di integrazione, utilizzare l&#39;host e la porta restituiti dalla relazione `valkey` per eseguire:

```terminal
valkey-cli -h <host> -p <port> info | grep version
```

**Risposta di esempio**

```text
valkey_version:<installed-version>
gcc_version:<gcc-version>
```

I dettagli della versione e della build variano a seconda dell’ambiente. Non trattare una versione di esempio visualizzata come una versione richiesta o di servizio universale.

>[!TAB Gestione temporanea e produzione Pro]

Negli ambienti di staging e produzione Pro, eseguire:

```terminal
valkey-server -v
```

**Risposta di esempio**

```text
Valkey server v=<installed-version> ...
```

I dettagli della versione e della build variano a seconda dell’ambiente. Non trattare una versione di esempio visualizzata come una versione richiesta o di servizio universale.

>[!ENDTABS]

## Risoluzione dei problemi di Valkey

### Gli errori di pulizia della cache fanno riferimento a Redis in una cache configurata con Valkey

Un errore di pulizia della cache pre-distribuzione può visualizzare il codice di errore `[107]` (`clean-redis-cache`) e un messaggio `Connection to Redis` anche quando il servizio `cache` è configurato come Valkey. `ece-tools` utilizza questo codice di errore e questo messaggio per il passaggio di pulizia della cache indipendentemente dal fatto che il servizio cache di backup sia Redis o Valkey.

Se l&#39;errore sottostante è un errore DNS, ad esempio `Name or service not known` per l&#39;host di relazione, il passaggio di distribuzione è stato eseguito prima che la relazione di servizio fosse disponibile oppure il nome della relazione in `.magento.app.yaml` non corrisponde all&#39;ID del servizio in `.magento/services.yaml`. Vedere [Verificare la relazione del servizio](#verify-the-service-relationship).
