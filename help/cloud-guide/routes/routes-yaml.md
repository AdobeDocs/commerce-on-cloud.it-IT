---
title: Configurare le route
description: Scopri come definire le route per le richieste HTTPS in arrivo per Adobe Commerce negli ambienti dell’infrastruttura cloud.
feature: Cloud, Configuration, Routes
source-git-commit: 1e789247c12009908eabb6039d951acbdfcc9263
workflow-type: tm+mt
source-wordcount: '886'
ht-degree: 0%

---

# Configurare le route

Il file `routes.yaml` nella directory `.magento/routes.yaml` definisce le route per gli ambienti di integrazione dell&#39;infrastruttura cloud, staging e produzione Adobe Commerce. Le route determinano il modo in cui l&#39;applicazione elabora le richieste HTTP e HTTPS in ingresso.

Il file predefinito `routes.yaml` specifica i modelli di route per l&#39;elaborazione delle richieste HTTP come HTTPS nei progetti con un singolo dominio predefinito e nei progetti configurati per più domini:

```yaml
"http://{default}/":
    type: upstream
    upstream: "mymagento:http"
"http://{all}/":
    type: upstream
    upstream: "mymagento:http"
```

Utilizzare l&#39;interfaccia della riga di comando `magento-cloud` per visualizzare un elenco delle route configurate:

```bash
magento-cloud environment:routes

+-------------------+----------+---------------+
| Route             | Type     | To            |
+-------------------+----------+---------------+
| http://{default}/ | upstream | mymagento     |
+-------------------+----------+---------------+
```

## Aggiornamenti alla configurazione degli ambienti Pro

{{pro-self-service-warning}}

## Modelli di percorso

Il file `routes.yaml` è un elenco di route con modelli e relative configurazioni. Nei modelli di percorso è possibile utilizzare i segnaposto seguenti:

- Il segnaposto `{default}` rappresenta il nome di dominio qualificato configurato come predefinito per il progetto.

  Ad esempio, un progetto con il dominio predefinito `example.com` e i seguenti modelli di route:

  ```text
  https://www.{default}/
  https://{default}/blog
  ```

  Questi modelli vengono risolti nei seguenti URL in un ambiente di produzione:

  ```text
  https://www.example.com/
  https://example.com/blog
  ```

- Il segnaposto `{all}` rappresenta tutti i nomi di dominio configurati per il progetto.

  Ad esempio, un progetto con domini `example.com` e `example1.com` con i seguenti modelli di route:

  ```text
  https://www.{all}/
  
  https://{all}/blog
  ```

  Questi modelli consentono di risolvere i percorsi seguenti per tutti i domini del progetto:

  ```text
  https://www.example.com/
  
  https://www.example1.com/
  
  https://example.com/blog
  
  https://example1.com/blog
  ```

  Il segnaposto `{all}` è utile per i progetti configurati per più domini. In un ramo non di produzione, `{all}` è sostituito con l&#39;ID progetto e l&#39;ID ambiente per ciascun dominio.

  Se in un progetto non è configurato alcun dominio, operazione comune durante lo sviluppo, il segnaposto `{all}` si comporta come il segnaposto `{default}`.

Adobe Commerce genera inoltre route per ogni ambiente di integrazione attivo. Per gli ambienti di integrazione, il segnaposto `{default}` è sostituito dal seguente nome di dominio:

```text
[branch]-[per-environment-random-string]-[project-id].[region].magentosite.cloud
```

Ad esempio, il ramo `refactorcss` per il progetto `mswy7hzcuhcjw` ospitato nel cluster `us` ha il seguente dominio:

```text
https://refactorcss-oy3m2pq-mswy7hzcuhcjw.us.magentosite.cloud/
```

>[!NOTE]
>
>Se il progetto Cloud supporta più store, segui le istruzioni di configurazione del percorso per [più siti Web o store](../store/multiple-sites.md).

### Barra finale

Le definizioni di route contengono una barra finale per indicare una cartella o una directory; tuttavia, lo stesso contenuto può essere distribuito con o senza una barra finale. I seguenti URL vengono risolti nello stesso modo, ma possono essere interpretati come _due URL_ diversi:

```text
https://www.example.com/blog/

https://www.example.com/blog
```

>[!TIP]
>
>È consigliabile utilizzare una barra finale per le directory, ma qualunque sia il metodo scelto, è importante **mantenere la coerenza** per evitare di generare due posizioni.

## Protocolli di route

Tutti gli ambienti supportano sia HTTP che HTTPS automaticamente.

- Se la configurazione specifica solo la route HTTP, le route HTTPS vengono create automaticamente, consentendo di gestire il sito sia da HTTP che da HTTPS senza richiedere reindirizzamenti.

  Ad esempio, un progetto con il dominio predefinito `example.com` e il seguente modello di route:

  ```text
  http://{default}/
  ```

  Questo modello viene risolto nei seguenti URL:

  ```text
  http://example.com/
  
  https://example.com/
  ```

- Se la configurazione specifica solo la route HTTPS, tutte le richieste HTTP vengono reindirizzate a HTTPS.

  Ad esempio, un progetto con il dominio predefinito `example.com` con il seguente modello di route:

  ```text
  https://{default}/
  ```

  Questo modello viene risolto nel seguente URL:

  ```text
  https://example.com/
  ```

  Inoltre, elabora il seguente reindirizzamento:

  `http://example.com/` ==> `https://example.com/`

Distribuisci tutte le pagine su TLS. Per questa configurazione, devi configurare i reindirizzamenti per tutte le richieste non crittografate all’equivalente TLS utilizzando uno dei seguenti metodi:

- Modificare il protocollo in HTTPS nel file `routes.yaml`.

  ```yaml
  "https://{default}/":
      type: upstream
      upstream: "mymagento:http"
  "https://{all}/":
      type: upstream
      upstream: "mymagento:http"
  ```

- Per gli ambienti di staging e produzione, abilita l&#39;opzione [Force TLS on Fastly](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/redirect-http-to-https-for-all-pages-on-cloud-force-tls.html) dall&#39;interfaccia utente amministratore. Quando si utilizza questa opzione, Fastly gestisce il reindirizzamento a HTTPS, pertanto non è necessario aggiornare la configurazione `routes.yaml`.

## Opzioni ciclo di lavorazione

Configurare ogni route separatamente utilizzando le proprietà seguenti:

| Proprietà | Descrizione |
| ---------------- | ----------- |
| `type: upstream` | Distribuisce un&#39;applicazione. Inoltre, ha una proprietà `upstream` che specifica il nome dell&#39;applicazione (come definito in `.magento.app.yaml`) seguito dall&#39;endpoint `:http`. |
| `type: redirect` | Reindirizza a un&#39;altra route. È seguito dalla proprietà `to`, che è un reindirizzamento HTTP a un&#39;altra route identificata dal relativo modello. |
| `cache:` | Controlla [il caching per la route](caching.md). |
| `redirects:` | Controlla [regole di reindirizzamento](redirects.md). |
| `ssi:` | Controlla l&#39;abilitazione di [Server Side Includes](server-side-includes.md). |

## Percorsi semplici

Negli esempi seguenti, la configurazione della route indirizza il dominio apex e il sottodominio `www` all&#39;applicazione `mymagento`. Questa route non reindirizza le richieste HTTPS.

**Esempio 1:**

```yaml
"http://{default}/":
    type: upstream
    upstream: "mymagento:http"

"http://www.{default}/":
    type: redirect
    to: "http://{default}/"
```

In questo esempio, il ciclo di richieste segue le regole seguenti:

- Il server risponde direttamente alle richieste con il seguente pattern URL:

  ```text
  http://example.com/path
  ```

- Il server genera un reindirizzamento _301_ per le richieste con il seguente pattern URL:

  ```text
  http://www.example.com/mypath
  ```

  Queste richieste vengono reindirizzate al dominio apex, ad esempio:

  ```text
  http://example.com/mypath
  ```

Nell’esempio seguente, la configurazione della route non reindirizza gli URL dal dominio www al dominio apex. Le richieste vengono invece gestite sia dal dominio www che da quello apex.

**Esempio 2:**

```yaml
"http://{default}/":
    type: upstream
    upstream: "mymagento:http"

"http://www.{default}/":
    type: upstream
    upstream: "mymagento:http"
```

## Route con caratteri jolly

Adobe Commerce su infrastruttura cloud supporta percorsi con caratteri jolly, in modo da poter mappare più sottodomini alla stessa applicazione. Questo funziona per le route di reindirizzamento e upstream. La route deve essere preceduta da un asterisco (\*). Ad esempio, le seguenti route alla stessa applicazione:

- `*.example.com`
- `www.example.com`
- `blog.example.com`
- `us.example.com`

Questo funziona come dominio onnicomprensivo in un ambiente live.

### Indirizzare un dominio non mappato

È possibile indirizzare a un sistema non mappato a un dominio utilizzando un punto (`.`) per separare il sottodominio.

**Esempio:**

Un progetto con un ramo `add-theme` viene indirizzato al seguente URL:

```text
http://add-theme-projectID.us.magento.com/
```

Se si definisce il seguente modello di ciclo di lavorazione:

```text
http://www.{default}/
```

La route viene risolta nel seguente URL:

```text
http://www.add-theme-projectID.us.magento.com/
```

Puoi inserire qualsiasi sottodominio prima che il punto e la route si risolvano.

**Esempio:**

Definire il seguente modello di ciclo di lavorazione:

```text
http://*.{default}/
```

Questo modello risolve entrambi i seguenti URL:

```text
http://foo.add-theme-projectID.us.magentosite.cloud/
http://bar.add-theme-projectID.us.magentosite.cloud/
```

È possibile visualizzare il pattern di route per i domini non mappati stabilendo una connessione SSH all&#39;ambiente e utilizzando la CLI `magento-cloud` per elencare le route:

```bash
vendor/bin/ece-tools env:config:show routes

Magento Cloud Routes:
+------------------------------------------+--------------------------------------------------------------+
| Route configuration                      | Value                                                        |
+------------------------------------------+--------------------------------------------------------------+
| http://www.add-theme-projectID.us.magento.com/:                                                         |
+------------------------------------------+--------------------------------------------------------------+
| primary                                  | false                                                        |
| id                                       | null                                                         |
| attributes                               |                                                              |
| type                                     | upstream                                                     |
| to                                       | mymagento                                                    |
| original_url                             | https:/{default}/                                            |
+------------------------------------------+--------------------------------------------------------------+
| https://*.add-theme-projectID.us.magentosite.cloud/:                                                    |
+------------------------------------------+--------------------------------------------------------------+
| primary                                  | false                                                        |
| id                                       | null                                                         |
| attributes                               |                                                              |
| type                                     | upstream                                                     |
| to                                       | mymagento                                                    |
| original_url                             | https://*.{default}/                                         |
+------------------------------------------+--------------------------------------------------------------+
```

## Reindirizzamenti e caching

Come descritto più dettagliatamente in [Reindirizzamenti](redirects.md), puoi gestire regole di reindirizzamento complesse, ad esempio _reindirizzamenti parziali_, e specificare regole per il [caching](caching.md) basato su route:

```yaml
https://www.{default}/:
    type: redirect
    to: https://{default}/
https://{default}/:
    cache:
        cookies: [""]
        default_ttl: 0
        enabled: true
        headers:
            - Accept
            - Accept-Language
    ssi:
        enabled: false
    type: upstream
    upstream: mymagento:http
```
