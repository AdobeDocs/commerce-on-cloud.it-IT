---
source-git-commit: b29ca0d786bf8cd15e5a3ba1ee8218f3bed2ae2f
workflow-type: tm+mt
source-wordcount: '13671'
ht-degree: 0%

---
# magento-cloud (Adobe Commerce su infrastruttura cloud)

<!-- The template to render with above values -->

**Versione**: 1.47.0

Questo riferimento contiene 123 comandi disponibili tramite lo strumento della riga di comando `magento-cloud`.
L&#39;elenco iniziale viene generato automaticamente utilizzando il comando `magento-cloud list` in Adobe Commerce sull&#39;infrastruttura cloud.

## Generale

Questo riferimento viene generato dalla base di codice dell&#39;applicazione. Per modificare il contenuto, è possibile aggiornare il codice sorgente per l&#39;implementazione del comando corrispondente nell&#39;archivio [codebase](https://github.com/magento/magento-cloud-cli) e inviare le modifiche per la revisione. Un altro modo consiste nel _inviarci un feedback_ (trovare il collegamento in alto a destra). Per le linee guida sui contributi, consulta [Contributi codice](https://developer.adobe.com/commerce/contributor/guides/code-contributions/).

### Opzioni globali

#### `--help`, `-h`

Visualizza questo messaggio della Guida

- Predefinito: `false`
- Non accetta un valore

#### `--version`, `-V`

Visualizza questa versione dell&#39;applicazione

- Predefinito: `false`
- Non accetta un valore

#### `--verbose`, `-v|-vv|-vvv`

Aumentare la gravità dei messaggi

- Predefinito: `false`
- Non accetta un valore

#### `--quiet`, `-q`

Stampa solo l&#39;output necessario. Eliminare altri messaggi ed errori. Ciò implica: nessuna interazione. Viene ignorato in modalità dettagliata.

- Predefinito: `false`
- Non accetta un valore

#### `--yes`, `-y`

Rispondi &quot;sì&quot; alle domande di conferma; accetta il valore predefinito per altre domande; disattiva l’interazione

- Predefinito: `false`
- Non accetta un valore

#### `--no-interaction`

Non fare domande interattive; accetta valori predefiniti. Equivalente all’utilizzo della variabile di ambiente: MAGENTO_CLOUD_CLI_NO_INTERACTION=1

- Predefinito: `false`
- Non accetta un valore


## `clear-cache`

```bash
magento-cloud cc
```

Cancellare la cache CLI

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).


## `console`

```bash
magento-cloud web [--browser BROWSER] [--pipe] [-p|--project PROJECT] [-e|--environment ENVIRONMENT]
```

Apri il progetto nella console

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--browser`

Browser da utilizzare per aprire l’URL. Impostate 0 su none.

- Richiede un valore

#### `--pipe`

Invia l’URL a stdout.

- Predefinito: `false`
- Non accetta un valore

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore

#### `--environment`, `-e`

ID ambiente. Utilizza &quot;.&quot; per selezionare l’ambiente predefinito del progetto.

- Richiede un valore


## `decode`

```bash
magento-cloud decode [-P|--property PROPERTY] [--] <value>
```

Decodificare una stringa codificata come MAGENTO_CLOUD_VARIABLES

### Argomenti

#### `value`

Valore della variabile da decodificare

- Obbligatorio

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--property`, `-P`

Proprietà da visualizzare all’interno della variabile

- Richiede un valore


## `docs`

```bash
magento-cloud docs [--browser BROWSER] [--pipe] [--] [<search>]...
```

Apri la documentazione online

### Argomenti

#### `search`

Cerca termini

- Predefinito: `[]`
- Array

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--browser`

Browser da utilizzare per aprire l’URL. Impostate 0 su none.

- Richiede un valore

#### `--pipe`

Invia l’URL a stdout.

- Predefinito: `false`
- Non accetta un valore


## `help`

```bash
magento-cloud help [--format FORMAT] [--raw] [--] [<command_name>]
```

Visualizza la Guida per un comando

```
The help command displays help for a given command:

  magento-cloud help list

You can also output the help in other formats by using the --format option:

  magento-cloud help --format=json list

To display the list of available commands, please use the list command.
```

### Argomenti

#### `command_name`

Nome del comando

- Predefinito: `help`

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--format`

Il formato di output (txt, json o md)

- Predefinito: `txt`
- Richiede un valore

#### `--raw`

Per visualizzare la guida dei comandi raw

- Predefinito: `false`
- Non accetta un valore


## `list`

```bash
magento-cloud list [--raw] [--format FORMAT] [--all] [--] [<namespace>]
```

Elenca i comandi

```
The list command lists all commands:

  magento-cloud list

You can also display the commands for a specific namespace:

  magento-cloud list project

You can also output the information in other formats by using the --format option:

  magento-cloud list --format=xml

It's also possible to get raw list of commands (useful for embedding command runner):

  magento-cloud list --raw
```

### Argomenti

#### `command`

Comando da eseguire

- Obbligatorio


#### `namespace`

Nome dello spazio dei nomi

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--raw`

Per generare l&#39;elenco dei comandi raw

- Predefinito: `false`
- Non accetta un valore

#### `--format`

Il formato di output (txt, xml, json o md)

- Predefinito: `txt`
- Richiede un valore

#### `--all`

Mostra tutti i comandi, inclusi quelli nascosti

- Predefinito: `false`
- Non accetta un valore


## `multi`

```bash
magento-cloud multi [-p|--projects PROJECTS] [--continue] [--sort SORT] [--reverse] [--] <cmd> (<cmd>)...
```

Eseguire un comando su più progetti

### Argomenti

#### `cmd`

Comando da eseguire

- Predefinito: `[]`
- Obbligatorio

- Array

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--projects`, `-p`

Elenco di ID progetto, separati da virgole e/o spazi

- Richiede un valore

#### `--continue`

Continua l&#39;esecuzione dei comandi anche in caso di eccezione

- Predefinito: `false`
- Non accetta un valore

#### `--sort`

Proprietà in base alla quale ordinare l&#39;elenco delle opzioni di progetto

- Predefinito: `title`
- Richiede un valore

#### `--reverse`

Inverti l&#39;ordine delle opzioni di progetto

- Predefinito: `false`
- Non accetta un valore


## `activity:cancel`

```bash
magento-cloud activity:cancel [-t|--type TYPE] [-x|--exclude-type EXCLUDE-TYPE] [-a|--all] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--] [<id>]
```

Annullare un’attività

### Argomenti

#### `id`

L’ID attività. Viene impostata automaticamente sull&#39;attività annullabile più recente.

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--type`, `-t`

Filtra per tipo (quando selezioni un’attività predefinita). I valori possono essere divisi da virgole (ad esempio, &quot;a,b,c&quot;) e/o spazi vuoti. È possibile utilizzare i caratteri % o * come carattere jolly per il tipo, ad esempio &#39;%var%&#39; per selezionare attività correlate alla variabile.

- Predefinito: `[]`
- Richiede un valore

#### `--exclude-type`, `-x`

Escludi per tipo (quando selezioni un’attività predefinita). I valori possono essere divisi da virgole (ad esempio, &quot;a,b,c&quot;) e/o spazi vuoti. I caratteri % o * possono essere utilizzati come caratteri jolly per escludere i tipi.

- Predefinito: `[]`
- Richiede un valore

#### `--all`, `-a`

Controlla le attività recenti in tutti gli ambienti (quando selezioni un’attività predefinita)

- Predefinito: `false`
- Non accetta un valore

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore

#### `--environment`, `-e`

ID ambiente. Utilizza &quot;.&quot; per selezionare l’ambiente predefinito del progetto.

- Richiede un valore


## `activity:get`

```bash
magento-cloud activity:get [-P|--property PROPERTY] [-t|--type TYPE] [-x|--exclude-type EXCLUDE-TYPE] [--state STATE] [--result RESULT] [-i|--incomplete] [-a|--all] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT] [--] [<id>]
```

Visualizzare informazioni dettagliate su una singola attività

### Argomenti

#### `id`

L’ID attività. Viene impostata automaticamente l&#39;attività più recente.

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--property`, `-P`

Proprietà da visualizzare

- Richiede un valore

#### `--type`, `-t`

Filtra per tipo (quando selezioni un’attività predefinita). I valori possono essere divisi da virgole (ad esempio, &quot;a,b,c&quot;) e/o spazi vuoti. È possibile utilizzare i caratteri % o * come carattere jolly per il tipo, ad esempio &#39;%var%&#39; per selezionare attività correlate alla variabile.

- Predefinito: `[]`
- Richiede un valore

#### `--exclude-type`, `-x`

Escludi per tipo (quando selezioni un’attività predefinita). I valori possono essere divisi da virgole (ad esempio, &quot;a,b,c&quot;) e/o spazi vuoti. I caratteri % o * possono essere utilizzati come caratteri jolly per escludere i tipi.

- Predefinito: `[]`
- Richiede un valore

#### `--state`

Filtra per stato (quando si seleziona un’attività predefinita): in_progress, pending, complete, o annullato. I valori possono essere divisi da virgole (ad esempio, &quot;a,b,c&quot;) e/o spazi vuoti.

- Predefinito: `[]`
- Richiede un valore

#### `--result`

Filtra per risultato (quando si seleziona un’attività predefinita): operazione riuscita o non riuscita

- Richiede un valore

#### `--incomplete`, `-i`

Includi solo le attività incomplete (quando si seleziona un’attività predefinita). Stenografia per —state=in_progress,pending

- Predefinito: `false`
- Non accetta un valore

#### `--all`, `-a`

Controlla le attività recenti in tutti gli ambienti (quando selezioni un’attività predefinita)

- Predefinito: `false`
- Non accetta un valore

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore

#### `--environment`, `-e`

ID ambiente. Utilizza &quot;.&quot; per selezionare l’ambiente predefinito del progetto.

- Richiede un valore

#### `--format`

Il formato di output: tabella, csv, tsv o normale

- Predefinito: `table`
- Richiede un valore

#### `--columns`, `-c`

Colonne da visualizzare. I caratteri % o * possono essere utilizzati come caratteri jolly. I valori possono essere divisi da virgole (ad esempio, &quot;a,b,c&quot;) e/o spazi vuoti.

- Predefinito: `[]`
- Richiede un valore

#### `--no-header`

Non generare l’intestazione della tabella

- Predefinito: `false`
- Non accetta un valore

#### `--date-fmt`

Il formato data (come stringa di formato data PHP)

- Predefinito: `c`
- Richiede un valore


## `activity:list`

```bash
magento-cloud activities [-t|--type TYPE] [-x|--exclude-type EXCLUDE-TYPE] [--limit LIMIT] [--start START] [--state STATE] [--result RESULT] [-i|--incomplete] [-a|--all] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT]
```

Ottenere un elenco delle attività per un ambiente o un progetto

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--type`, `-t`

Filtra le attività per tipo I valori possono essere suddivisi tra virgole (ad esempio, &quot;a,b,c&quot;) e/o spazi vuoti. La prima parte del nome dell’attività può essere omessa, ad esempio &quot;cron&quot; può selezionare le attività &quot;environment.cron&quot;. È possibile utilizzare i caratteri % o * come carattere jolly, ad esempio &#39;%var%&#39; per selezionare attività correlate alla variabile.

- Predefinito: `[]`
- Richiede un valore

#### `--exclude-type`, `-x`

Escludi attività per tipo. I valori possono essere divisi da virgole (ad esempio, &quot;a,b,c&quot;) e/o spazi vuoti. La prima parte del nome dell’attività può essere omessa, ad esempio &quot;cron&quot; può escludere le attività &quot;environment.cron&quot;. I caratteri % o * possono essere utilizzati come caratteri jolly per escludere i tipi.

- Predefinito: `[]`
- Richiede un valore

#### `--limit`

Limita il numero di risultati visualizzati

- Predefinito: `10`
- Richiede un valore

#### `--start`

Verranno elencate solo le attività create prima di questa data

- Richiede un valore

#### `--state`

Filtra attività per stato: in_corso, in sospeso, completo o annullato. I valori possono essere divisi da virgole (ad esempio, &quot;a,b,c&quot;) e/o spazi vuoti.

- Predefinito: `[]`
- Richiede un valore

#### `--result`

Filtra attività per risultato: operazione riuscita o non riuscita

- Richiede un valore

#### `--incomplete`, `-i`

Elencare solo le attività incomplete

- Predefinito: `false`
- Non accetta un valore

#### `--all`, `-a`

Elencare attività in tutti gli ambienti

- Predefinito: `false`
- Non accetta un valore

#### `--format`

Il formato di output: tabella, csv, tsv o normale

- Predefinito: `table`
- Richiede un valore

#### `--columns`, `-c`

Colonne da visualizzare. Colonne disponibili: id*, creato*, descrizione*, avanzamento*, stato*, risultato*, completato, ambienti, time_build, time_deploy, time_execute, time_wait, tipo (* = colonne predefinite). Il carattere &quot;+&quot; può essere utilizzato come segnaposto per le colonne predefinite. I caratteri % o * possono essere utilizzati come caratteri jolly. I valori possono essere divisi da virgole (ad esempio, &quot;a,b,c&quot;) e/o spazi vuoti.

- Predefinito: `[]`
- Richiede un valore

#### `--no-header`

Non generare l’intestazione della tabella

- Predefinito: `false`
- Non accetta un valore

#### `--date-fmt`

Il formato data (come stringa di formato data PHP)

- Predefinito: `c`
- Richiede un valore

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore

#### `--environment`, `-e`

ID ambiente. Utilizza &quot;.&quot; per selezionare l’ambiente predefinito del progetto.

- Richiede un valore


## `activity:log`

```bash
magento-cloud activity:log [--refresh REFRESH] [-t|--timestamps] [--type TYPE] [-x|--exclude-type EXCLUDE-TYPE] [--state STATE] [--result RESULT] [-i|--incomplete] [-a|--all] [--date-fmt DATE-FMT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--] [<id>]
```

Visualizzare il registro di un’attività

### Argomenti

#### `id`

L’ID attività. Viene impostata automaticamente l&#39;attività più recente.

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--refresh`

Intervallo di aggiornamento attività (secondi). Impostate questo valore su 0 per disattivare l&#39;aggiornamento.

- Predefinito: `3`
- Richiede un valore

#### `--timestamps`, `-t`

Visualizza un timestamp accanto a ogni messaggio

- Predefinito: `false`
- Non accetta un valore

#### `--type`

Filtra per tipo (quando selezioni un’attività predefinita). I valori possono essere divisi da virgole (ad esempio, &quot;a,b,c&quot;) e/o spazi vuoti. È possibile utilizzare i caratteri % o * come carattere jolly per il tipo, ad esempio &#39;%var%&#39; per selezionare attività correlate alla variabile.

- Predefinito: `[]`
- Richiede un valore

#### `--exclude-type`, `-x`

Escludi per tipo (quando selezioni un’attività predefinita). I valori possono essere divisi da virgole (ad esempio, &quot;a,b,c&quot;) e/o spazi vuoti. I caratteri % o * possono essere utilizzati come caratteri jolly per escludere i tipi.

- Predefinito: `[]`
- Richiede un valore

#### `--state`

Filtra per stato (quando si seleziona un’attività predefinita): in_progress, pending, complete, o annullato. I valori possono essere divisi da virgole (ad esempio, &quot;a,b,c&quot;) e/o spazi vuoti.

- Predefinito: `[]`
- Richiede un valore

#### `--result`

Filtra per risultato (quando si seleziona un’attività predefinita): operazione riuscita o non riuscita

- Richiede un valore

#### `--incomplete`, `-i`

Includi solo le attività incomplete (quando si seleziona un’attività predefinita). Stenografia per —state=in_progress,pending

- Predefinito: `false`
- Non accetta un valore

#### `--all`, `-a`

Controlla le attività recenti in tutti gli ambienti (quando selezioni un’attività predefinita)

- Predefinito: `false`
- Non accetta un valore

#### `--date-fmt`

Il formato data (come stringa di formato data PHP)

- Predefinito: `c`
- Richiede un valore

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore

#### `--environment`, `-e`

ID ambiente. Utilizza &quot;.&quot; per selezionare l’ambiente predefinito del progetto.

- Richiede un valore


## `app:config-get`

```bash
magento-cloud app:config-get [-P|--property PROPERTY] [--refresh] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [-i|--identity-file IDENTITY-FILE]
```

Visualizzare la configurazione di un’app

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--property`, `-P`

Proprietà di configurazione da visualizzare

- Richiede un valore

#### `--refresh`

Se aggiornare la cache

- Predefinito: `false`
- Non accetta un valore

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore

#### `--environment`, `-e`

ID ambiente. Utilizza &quot;.&quot; per selezionare l’ambiente predefinito del progetto.

- Richiede un valore

#### `--app`, `-A`

Nome dell&#39;applicazione remota

- Richiede un valore

#### `--identity-file`, `-i`

[Opzione obsoleta, non più utilizzata]

- Richiede un valore


## `app:list`

```bash
magento-cloud apps [--refresh] [--pipe] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header]
```

Elencare le app nel progetto

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--refresh`

Se aggiornare la cache

- Predefinito: `false`
- Non accetta un valore

#### `--pipe`

Genera solo un elenco di nomi di app

- Predefinito: `false`
- Non accetta un valore

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore

#### `--environment`, `-e`

ID ambiente. Utilizza &quot;.&quot; per selezionare l’ambiente predefinito del progetto.

- Richiede un valore

#### `--format`

Il formato di output: tabella, csv, tsv o normale

- Predefinito: `table`
- Richiede un valore

#### `--columns`, `-c`

Colonne da visualizzare. Colonne disponibili: nome*, tipo*, disco, percorso, dimensione (* = colonne predefinite). Il carattere &quot;+&quot; può essere utilizzato come segnaposto per le colonne predefinite. I caratteri % o * possono essere utilizzati come caratteri jolly. I valori possono essere divisi da virgole (ad esempio, &quot;a,b,c&quot;) e/o spazi vuoti.

- Predefinito: `[]`
- Richiede un valore

#### `--no-header`

Non generare l’intestazione della tabella

- Predefinito: `false`
- Non accetta un valore


## `auth:api-token-login`

```bash
magento-cloud auth:api-token-login
```

Accedi a Magento Cloud utilizzando un token API

```
Use this command to log in to your Magento Cloud account using an API token.

You can create an account at:
    https://business.adobe.com/it/products/magento/magento-commerce.html

If you have an account, but you do not already have an API token, you can create one here:
    https://accounts.magento.cloud/user/api-tokens

Alternatively, to log in to the CLI with a browser, run:
    magento-cloud auth:browser-login
```

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).


## `auth:browser-login`

```bash
magento-cloud login [-f|--force] [--method METHOD] [--max-age MAX-AGE] [--browser BROWSER] [--pipe]
```

Accedi a Magento Cloud tramite un browser

```
Use this command to log in to the Magento Cloud CLI using a web browser.

It launches a temporary local website which redirects you to log in if
necessary, and then captures the resulting authorization code.

Your system's default browser will be used. You can override this using the
--browser option.

Alternatively, to log in using an API token (without a browser), run:
magento-cloud auth:api-token-login

To authenticate non-interactively, configure an API token using the
MAGENTO_CLOUD_CLI_TOKEN environment variable.
```

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--force`, `-f`

Accedi di nuovo, anche se hai già effettuato l’accesso

- Predefinito: `false`
- Non accetta un valore

#### `--method`

Richiedi metodi di autenticazione specifici

- Predefinito: `[]`
- Richiede un valore

#### `--max-age`

Durata massima (in secondi) della sessione di autenticazione Web

- Richiede un valore

#### `--browser`

Browser da utilizzare per aprire l’URL. Impostate 0 su none.

- Richiede un valore

#### `--pipe`

Invia l’URL a stdout.

- Predefinito: `false`
- Non accetta un valore


## `auth:info`

```bash
magento-cloud auth:info [--no-auto-login] [-P|--property PROPERTY] [--refresh] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--] [<property>]
```

Visualizzare le informazioni sull&#39;account

### Argomenti

#### `property`

Proprietà account da visualizzare

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--no-auto-login`

Ignora l&#39;accesso automatico. Se non si è connessi, non verrà generato nulla e il codice di uscita sarà 0, supponendo che non vi siano altri errori.

- Predefinito: `false`
- Non accetta un valore

#### `--property`, `-P`

Proprietà dell&#39;account da visualizzare (sintassi alternativa)

- Richiede un valore

#### `--refresh`

Se aggiornare la cache

- Predefinito: `false`
- Non accetta un valore

#### `--format`

Il formato di output: tabella, csv, tsv o normale

- Predefinito: `table`
- Richiede un valore

#### `--columns`, `-c`

Colonne da visualizzare. I caratteri % o * possono essere utilizzati come caratteri jolly. I valori possono essere divisi da virgole (ad esempio, &quot;a,b,c&quot;) e/o spazi vuoti.

- Predefinito: `[]`
- Richiede un valore

#### `--no-header`

Non generare l’intestazione della tabella

- Predefinito: `false`
- Non accetta un valore


## `auth:logout`

```bash
magento-cloud logout [-a|--all] [--other]
```

Esci da Magento Cloud

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--all`, `-a`

Disconnetti da tutte le sessioni locali

- Predefinito: `false`
- Non accetta un valore

#### `--other`

Disconnetti da altre sessioni locali

- Predefinito: `false`
- Non accetta un valore


## `autoscaling:get`

```bash
magento-cloud autoscaling [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header]
```

Visualizzare la configurazione di scalabilità automatica di app e processi di lavoro in un ambiente

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore

#### `--environment`, `-e`

ID ambiente. Utilizza &quot;.&quot; per selezionare l’ambiente predefinito del progetto.

- Richiede un valore

#### `--format`

Il formato di output: tabella, csv, tsv o normale

- Predefinito: `table`
- Richiede un valore

#### `--columns`, `-c`

Colonne da visualizzare. Colonne disponibili: service*, metric*, direction*, threshold*, duration*, enabled*, instance_count*, cooldown, max_instances, min_instances (* = colonne predefinite). Il carattere &quot;+&quot; può essere utilizzato come segnaposto per le colonne predefinite. I caratteri % o * possono essere utilizzati come caratteri jolly. I valori possono essere divisi da virgole (ad esempio, &quot;a,b,c&quot;) e/o spazi vuoti.

- Predefinito: `[]`
- Richiede un valore

#### `--no-header`

Non generare l’intestazione della tabella

- Predefinito: `false`
- Non accetta un valore


## `autoscaling:set`

```bash
magento-cloud autoscaling:set [-s|--service SERVICE] [-m|--metric METRIC] [--enabled ENABLED] [--threshold-up THRESHOLD-UP] [--duration-up DURATION-UP] [--cooldown-up COOLDOWN-UP] [--threshold-down THRESHOLD-DOWN] [--duration-down DURATION-DOWN] [--cooldown-down COOLDOWN-DOWN] [--instances-min INSTANCES-MIN] [--instances-max INSTANCES-MAX] [--dry-run] [-p|--project PROJECT] [-e|--environment ENVIRONMENT]
```

Impostare la configurazione di scalabilità automatica di app o processi di lavoro in un ambiente

```
Configure automatic scaling for apps or workers in an environment.

You can also configure resources statically by running: magento-cloud resources:set
```

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--service`, `-s`

Nome dell’app o del processo di lavoro per cui configurare la scalabilità automatica

- Richiede un valore

#### `--metric`, `-m`

Nome della metrica da utilizzare per attivare la scalabilità automatica

- Richiede un valore

#### `--enabled`

Abilita la scalabilità automatica in base alla metrica specificata

- Richiede un valore

#### `--threshold-up`

Soglia oltre la quale il servizio verrà incrementato

- Richiede un valore

#### `--duration-up`

Durata oltre la quale la metrica viene valutata rispetto alla soglia per il ridimensionamento

- Richiede un valore

#### `--cooldown-up`

Durata dell’attesa prima di tentare di aumentare ulteriormente la scalabilità dopo un evento di ridimensionamento

- Richiede un valore

#### `--threshold-down`

Soglia al di sotto della quale il servizio verrà ridotto

- Richiede un valore

#### `--duration-down`

Durata della valutazione della metrica rispetto alla soglia per la riduzione

- Richiede un valore

#### `--cooldown-down`

Durata dell’attesa prima di tentare di effettuare un’ulteriore riduzione dopo un evento di ridimensionamento

- Richiede un valore

#### `--instances-min`

Numero minimo di istanze che verranno ridotte a

- Richiede un valore

#### `--instances-max`

Numero massimo di istanze che verranno ridimensionate fino a

- Richiede un valore

#### `--dry-run`

Mostra le modifiche che verranno apportate, senza apportare alcuna modifica

- Predefinito: `false`
- Non accetta un valore

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore

#### `--environment`, `-e`

ID ambiente. Utilizza &quot;.&quot; per selezionare l’ambiente predefinito del progetto.

- Richiede un valore


## `blackfire:setup`

```bash
magento-cloud blackfire:setup [--server_id SERVER_ID] [--server_token SERVER_TOKEN] [-p|--project PROJECT] [-W|--no-wait] [--wait]
```

Configurare l’integrazione di Blackfire.io per il progetto

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--server_id`

ID server

- Richiede un valore

#### `--server_token`

Token del server

- Richiede un valore

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore

#### `--no-wait`, `-W`

Non attendere il completamento dell&#39;operazione

- Predefinito: `false`
- Non accetta un valore

#### `--wait`

Attendere il completamento dell&#39;operazione (impostazione predefinita)

- Predefinito: `false`
- Non accetta un valore


## `certificate:add`

```bash
magento-cloud certificate:add [--cert CERT] [--key KEY] [--chain CHAIN] [-p|--project PROJECT] [-W|--no-wait] [--wait]
```

Aggiungere un certificato SSL al progetto

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--cert`

Percorso del file di certificato

- Richiede un valore

#### `--key`

Percorso del file della chiave privata del certificato

- Richiede un valore

#### `--chain`

Percorso del file della catena di certificati

- Predefinito: `[]`
- Richiede un valore

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore

#### `--no-wait`, `-W`

Non attendere il completamento dell&#39;operazione

- Predefinito: `false`
- Non accetta un valore

#### `--wait`

Attendere il completamento dell&#39;operazione (impostazione predefinita)

- Predefinito: `false`
- Non accetta un valore


## `certificate:delete`

```bash
magento-cloud certificate:delete [-p|--project PROJECT] [-W|--no-wait] [--wait] [--] <id>
```

Eliminare un certificato dal progetto

### Argomenti

#### `id`

ID del certificato (o il suo inizio)

- Obbligatorio

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore

#### `--no-wait`, `-W`

Non attendere il completamento dell&#39;operazione

- Predefinito: `false`
- Non accetta un valore

#### `--wait`

Attendere il completamento dell&#39;operazione (impostazione predefinita)

- Predefinito: `false`
- Non accetta un valore


## `certificate:get`

```bash
magento-cloud certificate:get [-P|--property PROPERTY] [--date-fmt DATE-FMT] [-p|--project PROJECT] [--] <id>
```

Visualizzare un certificato

### Argomenti

#### `id`

ID del certificato (o il suo inizio)

- Obbligatorio

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--property`, `-P`

Proprietà del certificato da visualizzare

- Richiede un valore

#### `--date-fmt`

Il formato data (come stringa di formato data PHP)

- Predefinito: `c`
- Richiede un valore

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore


## `certificate:list`

```bash
magento-cloud certificates [--domain DOMAIN] [--exclude-domain EXCLUDE-DOMAIN] [--issuer ISSUER] [--only-auto] [--no-auto] [--ignore-expiry] [--only-expired] [--no-expired] [--pipe-domains] [--date-fmt DATE-FMT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT]
```

Elencare certificati di progetto

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--domain`

Filtra per nome di dominio (ricerca senza distinzione tra maiuscole e minuscole)

- Richiede un valore

#### `--exclude-domain`

Escludi certificati, corrispondenza per nome di dominio (ricerca senza distinzione maiuscole/minuscole)

- Richiede un valore

#### `--issuer`

Filtra per emittente

- Richiede un valore

#### `--only-auto`

Mostra solo certificati con provisioning automatico

- Predefinito: `false`
- Non accetta un valore

#### `--no-auto`

Mostra solo i certificati aggiunti manualmente

- Predefinito: `false`
- Non accetta un valore

#### `--ignore-expiry`

Mostra certificati scaduti e non scaduti

- Predefinito: `false`
- Non accetta un valore

#### `--only-expired`

Mostra solo certificati scaduti

- Predefinito: `false`
- Non accetta un valore

#### `--no-expired`

Mostra solo certificati non scaduti (impostazione predefinita)

- Predefinito: `false`
- Non accetta un valore

#### `--pipe-domains`

Restituisce solo un elenco di nomi di dominio coperti dai certificati

- Predefinito: `false`
- Non accetta un valore

#### `--date-fmt`

Il formato data (come stringa di formato data PHP)

- Predefinito: `c`
- Richiede un valore

#### `--format`

Il formato di output: tabella, csv, tsv o normale

- Predefinito: `table`
- Richiede un valore

#### `--columns`, `-c`

Colonne da visualizzare. Colonne disponibili: creato, domini, scadenza, ID, emittente. I caratteri % o * possono essere utilizzati come caratteri jolly. I valori possono essere divisi da virgole (ad esempio, &quot;a,b,c&quot;) e/o spazi vuoti.

- Predefinito: `[]`
- Richiede un valore

#### `--no-header`

Non generare l’intestazione della tabella

- Predefinito: `false`
- Non accetta un valore

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore


## `commit:get`

```bash
magento-cloud commit:get [-P|--property PROPERTY] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--date-fmt DATE-FMT] [--] [<commit>]
```

Mostra dettagli commit

### Argomenti

#### `commit`

Il commit SHA. Questo può anche accettare suffissi &quot;HEAD&quot; e accento circonflesso (^) o tilde (~) per commit principali.

- Predefinito: `HEAD`

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--property`, `-P`

Proprietà commit da visualizzare.

- Richiede un valore

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore

#### `--environment`, `-e`

ID ambiente. Utilizza &quot;.&quot; per selezionare l’ambiente predefinito del progetto.

- Richiede un valore

#### `--date-fmt`

Il formato data (come stringa di formato data PHP)

- Predefinito: `c`
- Richiede un valore


## `commit:list`

```bash
magento-cloud commits [--limit LIMIT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT] [--] [<commit>]
```

Elenca commit

### Argomenti

#### `commit`

Il commit Git iniziale SHA. Questo può anche accettare suffissi &quot;HEAD&quot; e accento circonflesso (^) o tilde (~) per commit principali.

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--limit`

Numero di commit da visualizzare.

- Predefinito: `10`
- Richiede un valore

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore

#### `--environment`, `-e`

ID ambiente. Utilizza &quot;.&quot; per selezionare l’ambiente predefinito del progetto.

- Richiede un valore

#### `--format`

Il formato di output: tabella, csv, tsv o normale

- Predefinito: `table`
- Richiede un valore

#### `--columns`, `-c`

Colonne da visualizzare. Colonne disponibili: author, date, sha, summary. I caratteri % o * possono essere utilizzati come caratteri jolly. I valori possono essere divisi da virgole (ad esempio, &quot;a,b,c&quot;) e/o spazi vuoti.

- Predefinito: `[]`
- Richiede un valore

#### `--no-header`

Non generare l’intestazione della tabella

- Predefinito: `false`
- Non accetta un valore

#### `--date-fmt`

Il formato data (come stringa di formato data PHP)

- Predefinito: `c`
- Richiede un valore


## `db:dump`

```bash
magento-cloud db:dump [--schema SCHEMA] [-f|--file FILE] [-d|--directory DIRECTORY] [-z|--gzip] [-t|--timestamp] [-o|--stdout] [--table TABLE] [--exclude-table EXCLUDE-TABLE] [--schema-only] [--charset CHARSET] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [-r|--relationship RELATIONSHIP]
```

Creare un dump locale del database remoto

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--schema`

Schema da scaricare. Ometti di utilizzare lo schema predefinito (in genere &quot;main&quot;).

- Richiede un valore

#### `--file`, `-f`

Un nome file personalizzato per l’immagine

- Richiede un valore

#### `--directory`, `-d`

Una directory personalizzata per il dump

- Richiede un valore

#### `--gzip`, `-z`

Comprimi l’immagine utilizzando gzip

- Predefinito: `false`
- Non accetta un valore

#### `--timestamp`, `-t`

Aggiungi una marca temporale al nome del file di dump

- Predefinito: `false`
- Non accetta un valore

#### `--stdout`, `-o`

Output in STDOUT anziché in un file

- Predefinito: `false`
- Non accetta un valore

#### `--table`

Tabelle da includere

- Predefinito: `[]`
- Richiede un valore

#### `--exclude-table`

Tabelle da escludere

- Predefinito: `[]`
- Richiede un valore

#### `--schema-only`

Esegui il dump solo degli schemi, nessun dato

- Predefinito: `false`
- Non accetta un valore

#### `--charset`

Codifica del set di caratteri per l’immagine

- Richiede un valore

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore

#### `--environment`, `-e`

ID ambiente. Utilizza &quot;.&quot; per selezionare l’ambiente predefinito del progetto.

- Richiede un valore

#### `--app`, `-A`

Nome dell&#39;applicazione remota

- Richiede un valore

#### `--relationship`, `-r`

Relazione di servizio da utilizzare

- Richiede un valore


## `db:sql`

```bash
magento-cloud sql [--raw] [--schema SCHEMA] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [-r|--relationship RELATIONSHIP] [--] [<query>]
```

Esegui SQL sul database remoto

### Argomenti

#### `query`

Istruzione SQL da eseguire

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--raw`

Genera output non tabulare

- Predefinito: `false`
- Non accetta un valore

#### `--schema`

Schema da utilizzare. Ometti di utilizzare lo schema predefinito (in genere &quot;main&quot;). Passa una stringa vuota per non utilizzare alcuno schema.

- Richiede un valore

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore

#### `--environment`, `-e`

ID ambiente. Utilizza &quot;.&quot; per selezionare l’ambiente predefinito del progetto.

- Richiede un valore

#### `--app`, `-A`

Nome dell&#39;applicazione remota

- Richiede un valore

#### `--relationship`, `-r`

Relazione di servizio da utilizzare

- Richiede un valore


## `domain:add`

```bash
magento-cloud domain:add [--cert CERT] [--key KEY] [--chain CHAIN] [--attach ATTACH] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] <name>
```

Aggiungi un nuovo dominio al progetto

### Argomenti

#### `name`

Il nome di dominio

- Obbligatorio

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--cert`

Percorso di un file di certificato personalizzato

- Richiede un valore

#### `--key`

Percorso della chiave privata per il certificato personalizzato

- Richiede un valore

#### `--chain`

Percorso del file catena per il certificato personalizzato

- Predefinito: `[]`
- Richiede un valore

#### `--attach`

Il dominio di produzione che questo sostituisce nelle route dell&#39;ambiente. Obbligatorio per i domini dell’ambiente non di produzione.

- Richiede un valore

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore

#### `--environment`, `-e`

ID ambiente. Utilizza &quot;.&quot; per selezionare l’ambiente predefinito del progetto.

- Richiede un valore

#### `--no-wait`, `-W`

Non attendere il completamento dell&#39;operazione

- Predefinito: `false`
- Non accetta un valore

#### `--wait`

Attendere il completamento dell&#39;operazione (impostazione predefinita)

- Predefinito: `false`
- Non accetta un valore


## `domain:delete`

```bash
magento-cloud domain:delete [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] <name>
```

Eliminare un dominio dal progetto

### Argomenti

#### `name`

Il nome di dominio

- Obbligatorio

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore

#### `--environment`, `-e`

ID ambiente. Utilizza &quot;.&quot; per selezionare l’ambiente predefinito del progetto.

- Richiede un valore

#### `--no-wait`, `-W`

Non attendere il completamento dell&#39;operazione

- Predefinito: `false`
- Non accetta un valore

#### `--wait`

Attendere il completamento dell&#39;operazione (impostazione predefinita)

- Predefinito: `false`
- Non accetta un valore


## `domain:get`

```bash
magento-cloud domain:get [-P|--property PROPERTY] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--] [<name>]
```

Visualizzare informazioni dettagliate per un dominio

### Argomenti

#### `name`

Il nome di dominio

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--property`, `-P`

Proprietà di dominio da visualizzare

- Richiede un valore

#### `--format`

Il formato di output: tabella, csv, tsv o normale

- Predefinito: `table`
- Richiede un valore

#### `--columns`, `-c`

Colonne da visualizzare. I caratteri % o * possono essere utilizzati come caratteri jolly. I valori possono essere divisi da virgole (ad esempio, &quot;a,b,c&quot;) e/o spazi vuoti.

- Predefinito: `[]`
- Richiede un valore

#### `--no-header`

Non generare l’intestazione della tabella

- Predefinito: `false`
- Non accetta un valore

#### `--date-fmt`

Il formato data (come stringa di formato data PHP)

- Predefinito: `c`
- Richiede un valore

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore

#### `--environment`, `-e`

ID ambiente. Utilizza &quot;.&quot; per selezionare l’ambiente predefinito del progetto.

- Richiede un valore


## `domain:list`

```bash
magento-cloud domains [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT] [-e|--environment ENVIRONMENT]
```

Ottieni un elenco di tutti i domini

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--format`

Il formato di output: tabella, csv, tsv o normale

- Predefinito: `table`
- Richiede un valore

#### `--columns`, `-c`

Colonne da visualizzare. Colonne disponibili: name*, ssl*, created_at*, registered_name, replace_for, type, updated_at (* = colonne predefinite). Il carattere &quot;+&quot; può essere utilizzato come segnaposto per le colonne predefinite. I caratteri % o * possono essere utilizzati come caratteri jolly. I valori possono essere divisi da virgole (ad esempio, &quot;a,b,c&quot;) e/o spazi vuoti.

- Predefinito: `[]`
- Richiede un valore

#### `--no-header`

Non generare l’intestazione della tabella

- Predefinito: `false`
- Non accetta un valore

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore

#### `--environment`, `-e`

ID ambiente. Utilizza &quot;.&quot; per selezionare l’ambiente predefinito del progetto.

- Richiede un valore


## `domain:update`

```bash
magento-cloud domain:update [--cert CERT] [--key KEY] [--chain CHAIN] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] <name>
```

Aggiornare un dominio

### Argomenti

#### `name`

Il nome di dominio

- Obbligatorio

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--cert`

Percorso di un file di certificato personalizzato

- Richiede un valore

#### `--key`

Percorso della chiave privata per il certificato personalizzato

- Richiede un valore

#### `--chain`

Percorso del file catena per il certificato personalizzato

- Predefinito: `[]`
- Richiede un valore

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore

#### `--environment`, `-e`

ID ambiente. Utilizza &quot;.&quot; per selezionare l’ambiente predefinito del progetto.

- Richiede un valore

#### `--no-wait`, `-W`

Non attendere il completamento dell&#39;operazione

- Predefinito: `false`
- Non accetta un valore

#### `--wait`

Attendere il completamento dell&#39;operazione (impostazione predefinita)

- Predefinito: `false`
- Non accetta un valore


## `environment:activate`

```bash
magento-cloud environment:activate [--parent PARENT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<environment>]...
```

Attivare un ambiente

### Argomenti

#### `environment`

Ambiente/i da attivare

- Predefinito: `[]`
- Array

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--parent`

Imposta un nuovo ambiente principale prima dell’attivazione

- Richiede un valore

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore

#### `--environment`, `-e`

ID ambiente. Utilizza &quot;.&quot; per selezionare l’ambiente predefinito del progetto.

- Richiede un valore

#### `--no-wait`, `-W`

Non attendere il completamento dell&#39;operazione

- Predefinito: `false`
- Non accetta un valore

#### `--wait`

Attendere il completamento dell&#39;operazione (impostazione predefinita)

- Predefinito: `false`
- Non accetta un valore


## `environment:branch`

```bash
magento-cloud branch [--title TITLE] [--type TYPE] [--no-clone-parent] [--no-checkout] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<id>] [<parent>]
```

Creazione di un ramo di un ambiente

### Argomenti

#### `id`

ID (nome del ramo) del nuovo ambiente


#### `parent`

Elemento padre del nuovo ambiente

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--title`

Titolo del nuovo ambiente

- Richiede un valore

#### `--type`

Tipo del nuovo ambiente

- Richiede un valore

#### `--no-clone-parent`

Non clonare i dati dell’ambiente principale

- Predefinito: `false`
- Non accetta un valore

#### `--no-checkout`

Non estrarre il ramo localmente

- Predefinito: `false`
- Non accetta un valore

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore

#### `--environment`, `-e`

ID ambiente. Utilizza &quot;.&quot; per selezionare l’ambiente predefinito del progetto.

- Richiede un valore

#### `--no-wait`, `-W`

Non attendere il completamento dell&#39;operazione

- Predefinito: `false`
- Non accetta un valore

#### `--wait`

Attendere il completamento dell&#39;operazione (impostazione predefinita)

- Predefinito: `false`
- Non accetta un valore


## `environment:checkout`

```bash
magento-cloud checkout [<id>]
```

Estrarre un ambiente

### Argomenti

#### `id`

ID dell&#39;ambiente da estrarre. Ad esempio: &quot;sprint2&quot;

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).


## `environment:delete`

```bash
magento-cloud environment:delete [--delete-branch] [--no-delete-branch] [--type TYPE] [-t|--only-type ONLY-TYPE] [--exclude EXCLUDE] [--exclude-type EXCLUDE-TYPE] [--inactive] [--status STATUS] [--only-status ONLY-STATUS] [--exclude-status EXCLUDE-STATUS] [--merged] [--allow-delete-parent] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<environment>]...
```

Eliminare uno o più ambienti

```
When a Magento Cloud environment is deleted, it will become "inactive": it will
exist only as a Git branch, containing code but no services, databases nor
files.

This command allows you to delete environments as well as their Git branches.
```

### Argomenti

#### `environment`

Ambienti da eliminare. I caratteri % o * possono essere utilizzati come caratteri jolly. I valori possono essere divisi da virgole (ad esempio, &quot;a,b,c&quot;) e/o spazi vuoti.

- Predefinito: `[]`
- Array

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--delete-branch`

Elimina rami Git per ambienti inattivi, senza conferma

- Predefinito: `false`
- Non accetta un valore

#### `--no-delete-branch`

Non eliminare i rami Git (ambienti inattivi)

- Predefinito: `false`
- Non accetta un valore

#### `--type`

Elimina tutti gli ambienti di un tipo (aggiungendo a qualsiasi altro tipo selezionato) I valori possono essere suddivisi da virgole (ad esempio, &quot;a,b,c&quot;) e/o spazi vuoti.

- Predefinito: `[]`
- Richiede un valore

#### `--only-type`, `-t`

Solo gli ambienti di eliminazione di un tipo specifico I valori possono essere divisi da virgole (ad esempio, &quot;a,b,c&quot;) e/o spazi vuoti.

- Predefinito: `[]`
- Richiede un valore

#### `--exclude`

Ambienti da non eliminare. I caratteri % o * possono essere utilizzati come caratteri jolly. I valori possono essere divisi da virgole (ad esempio, &quot;a,b,c&quot;) e/o spazi vuoti.

- Predefinito: `[]`
- Richiede un valore

#### `--exclude-type`

I tipi di ambiente di cui non eliminare i valori possono essere divisi da virgole (ad esempio, &quot;a,b,c&quot;) e/o spazi vuoti.

- Predefinito: `[]`
- Richiede un valore

#### `--inactive`

Elimina tutti gli ambienti inattivi (aggiungendoli agli altri selezionati)

- Predefinito: `false`
- Non accetta un valore

#### `--status`

Elimina tutti gli ambienti di uno stato (aggiungendo a tutti gli altri selezionati) I valori possono essere divisi da virgole (ad esempio, &quot;a,b,c&quot;) e/o spazi vuoti.

- Predefinito: `[]`
- Richiede un valore

#### `--only-status`

Solo gli ambienti di eliminazione con uno stato specifico I valori possono essere divisi da virgole (ad esempio, &quot;a,b,c&quot;) e/o spazi vuoti.

- Predefinito: `[]`
- Richiede un valore

#### `--exclude-status`

Gli stati dell’ambiente di cui non eliminare i valori possono essere suddivisi da virgole (ad esempio, &quot;a,b,c&quot;) e/o spazi vuoti.

- Predefinito: `[]`
- Richiede un valore

#### `--merged`

Elimina tutti gli ambienti uniti (aggiungendoli a quelli selezionati)

- Predefinito: `false`
- Non accetta un valore

#### `--allow-delete-parent`

Consenti eliminazione degli ambienti con elementi figlio

- Predefinito: `false`
- Non accetta un valore

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore

#### `--environment`, `-e`

ID ambiente. Utilizza &quot;.&quot; per selezionare l’ambiente predefinito del progetto.

- Richiede un valore

#### `--no-wait`, `-W`

Non attendere il completamento dell&#39;operazione

- Predefinito: `false`
- Non accetta un valore

#### `--wait`

Attendere il completamento dell&#39;operazione (impostazione predefinita)

- Predefinito: `false`
- Non accetta un valore


## `environment:deploy`

```bash
magento-cloud deploy [-s|--strategy STRATEGY] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait]
```

Distribuire le modifiche di un ambiente in staging

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--strategy`, `-s`

Strategia di distribuzione, avvio (impostazione predefinita, riavvio con arresto) o continuo (nessuna interruzione)

- Richiede un valore

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore

#### `--environment`, `-e`

ID ambiente. Utilizza &quot;.&quot; per selezionare l’ambiente predefinito del progetto.

- Richiede un valore

#### `--no-wait`, `-W`

Non attendere il completamento dell&#39;operazione

- Predefinito: `false`
- Non accetta un valore

#### `--wait`

Attendere il completamento dell&#39;operazione (impostazione predefinita)

- Predefinito: `false`
- Non accetta un valore


## `environment:deploy:type`

```bash
magento-cloud environment:deploy:type [--pipe] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<type>]
```

Mostrare o impostare il tipo di distribuzione dell’ambiente

```
Choose automatic (the default) if you want your changes to be deployed immediately as they are made.
Choose manual to have changes staged until you trigger a deployment (including changes to code, variables, domains and settings).
```

### Argomenti

#### `type`

Tipo di distribuzione dell’ambiente: automatica o manuale.

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--pipe`

Invia output del tipo di distribuzione a stdout

- Predefinito: `false`
- Non accetta un valore

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore

#### `--environment`, `-e`

ID ambiente. Utilizza &quot;.&quot; per selezionare l’ambiente predefinito del progetto.

- Richiede un valore

#### `--no-wait`, `-W`

Non attendere il completamento dell&#39;operazione

- Predefinito: `false`
- Non accetta un valore

#### `--wait`

Attendere il completamento dell&#39;operazione (impostazione predefinita)

- Predefinito: `false`
- Non accetta un valore


## `environment:http-access`

```bash
magento-cloud httpaccess [--access ACCESS] [--auth AUTH] [--enabled ENABLED] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait]
```

Aggiornare le impostazioni di accesso HTTP per un ambiente

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--access`

Limitazione di accesso nel formato &quot;autorizzazione:address&quot;. Utilizza 0 per cancellare tutti gli indirizzi.

- Predefinito: `[]`
- Richiede un valore

#### `--auth`

Credenziali di autenticazione HTTP Basic in formato &quot;nomeutente:password&quot;. Utilizzare 0 per cancellare tutte le credenziali.

- Predefinito: `[]`
- Richiede un valore

#### `--enabled`

Specifica se il controllo degli accessi deve essere abilitato: 1 per abilitare, 0 per disabilitare

- Richiede un valore

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore

#### `--environment`, `-e`

ID ambiente. Utilizza &quot;.&quot; per selezionare l’ambiente predefinito del progetto.

- Richiede un valore

#### `--no-wait`, `-W`

Non attendere il completamento dell&#39;operazione

- Predefinito: `false`
- Non accetta un valore

#### `--wait`

Attendere il completamento dell&#39;operazione (impostazione predefinita)

- Predefinito: `false`
- Non accetta un valore


## `environment:info`

```bash
magento-cloud environment:info [--refresh] [--date-fmt DATE-FMT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<property>] [<value>]
```

Lettura o impostazione delle proprietà di un ambiente

### Argomenti

#### `property`

Nome della proprietà


#### `value`

Imposta un nuovo valore per la proprietà

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--refresh`

Se aggiornare la cache

- Predefinito: `false`
- Non accetta un valore

#### `--date-fmt`

Il formato data (come stringa di formato data PHP)

- Predefinito: `c`
- Richiede un valore

#### `--format`

Il formato di output: tabella, csv, tsv o normale

- Predefinito: `table`
- Richiede un valore

#### `--columns`, `-c`

Colonne da visualizzare. I caratteri % o * possono essere utilizzati come caratteri jolly. I valori possono essere divisi da virgole (ad esempio, &quot;a,b,c&quot;) e/o spazi vuoti.

- Predefinito: `[]`
- Richiede un valore

#### `--no-header`

Non generare l’intestazione della tabella

- Predefinito: `false`
- Non accetta un valore

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore

#### `--environment`, `-e`

ID ambiente. Utilizza &quot;.&quot; per selezionare l’ambiente predefinito del progetto.

- Richiede un valore

#### `--no-wait`, `-W`

Non attendere il completamento dell&#39;operazione

- Predefinito: `false`
- Non accetta un valore

#### `--wait`

Attendere il completamento dell&#39;operazione (impostazione predefinita)

- Predefinito: `false`
- Non accetta un valore


## `environment:init`

```bash
magento-cloud environment:init [--profile PROFILE] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] <url>
```

Inizializzare un ambiente da un archivio Git pubblico

### Argomenti

#### `url`

URL di un archivio Git

- Obbligatorio

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--profile`

Nome del profilo

- Richiede un valore

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore

#### `--environment`, `-e`

ID ambiente. Utilizza &quot;.&quot; per selezionare l’ambiente predefinito del progetto.

- Richiede un valore

#### `--no-wait`, `-W`

Non attendere il completamento dell&#39;operazione

- Predefinito: `false`
- Non accetta un valore

#### `--wait`

Attendere il completamento dell&#39;operazione (impostazione predefinita)

- Predefinito: `false`
- Non accetta un valore


## `environment:list`

```bash
magento-cloud environments [-I|--no-inactive] [--status STATUS] [--pipe] [--refresh REFRESH] [--sort SORT] [--reverse] [--type TYPE] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT]
```

Ottieni un elenco di ambienti

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--no-inactive`, `-I`

Non mostrare ambienti inattivi

- Predefinito: `false`
- Non accetta un valore

#### `--status`

Filtra gli ambienti per stato (attivo, inattivo, sporco, in pausa, eliminato). I valori possono essere divisi da virgole (ad esempio, &quot;a,b,c&quot;) e/o spazi vuoti.

- Predefinito: `[]`
- Richiede un valore

#### `--pipe`

Genera un semplice elenco di ID ambiente.

- Predefinito: `false`
- Non accetta un valore

#### `--refresh`

Specifica se aggiornare l&#39;elenco.

- Predefinito: `1`
- Richiede un valore

#### `--sort`

Proprietà in base alla quale eseguire l&#39;ordinamento

- Predefinito: `title`
- Richiede un valore

#### `--reverse`

Ordinamento inverso (decrescente)

- Predefinito: `false`
- Non accetta un valore

#### `--type`

Filtra l’elenco per tipo/i di ambiente. I valori possono essere divisi da virgole (ad esempio, &quot;a,b,c&quot;) e/o spazi vuoti.

- Predefinito: `[]`
- Richiede un valore

#### `--format`

Il formato di output: tabella, csv, tsv o normale

- Predefinito: `table`
- Richiede un valore

#### `--columns`, `-c`

Colonne da visualizzare. Colonne disponibili: id*, title*, status*, type*, created, machine_name, updated (* = default columns). Il carattere &quot;+&quot; può essere utilizzato come segnaposto per le colonne predefinite. I caratteri % o * possono essere utilizzati come caratteri jolly. I valori possono essere divisi da virgole (ad esempio, &quot;a,b,c&quot;) e/o spazi vuoti.

- Predefinito: `[]`
- Richiede un valore

#### `--no-header`

Non generare l’intestazione della tabella

- Predefinito: `false`
- Non accetta un valore

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore


## `environment:logs`

```bash
magento-cloud log [--lines LINES] [--tail] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--worker WORKER] [-I|--instance INSTANCE] [--] [<type>]
```

Leggere i registri di un ambiente

### Argomenti

#### `type`

Tipo di registro, ad esempio &quot;accesso&quot; o &quot;errore&quot;

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--lines`

Numero di righe da visualizzare

- Predefinito: `100`
- Richiede un valore

#### `--tail`

Coda continua del registro

- Predefinito: `false`
- Non accetta un valore

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore

#### `--environment`, `-e`

ID ambiente. Utilizza &quot;.&quot; per selezionare l’ambiente predefinito del progetto.

- Richiede un valore

#### `--app`, `-A`

Nome dell&#39;applicazione remota

- Richiede un valore

#### `--worker`

Un nome lavoratore

- Richiede un valore

#### `--instance`, `-I`

Un ID istanza

- Richiede un valore


## `environment:merge`

```bash
magento-cloud merge [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<environment>]
```

Unire un ambiente

```
This command will initiate a Git merge of the specified environment into its parent environment.
```

### Argomenti

#### `environment`

Ambiente da unire

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore

#### `--environment`, `-e`

ID ambiente. Utilizza &quot;.&quot; per selezionare l’ambiente predefinito del progetto.

- Richiede un valore

#### `--no-wait`, `-W`

Non attendere il completamento dell&#39;operazione

- Predefinito: `false`
- Non accetta un valore

#### `--wait`

Attendere il completamento dell&#39;operazione (impostazione predefinita)

- Predefinito: `false`
- Non accetta un valore


## `environment:pause`

```bash
magento-cloud environment:pause [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait]
```

Sospendere un ambiente

```
Pausing an environment helps to reduce resource consumption and carbon emissions.

The environment will be unavailable until it is resumed. No data will be lost.
```

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore

#### `--environment`, `-e`

ID ambiente. Utilizza &quot;.&quot; per selezionare l’ambiente predefinito del progetto.

- Richiede un valore

#### `--no-wait`, `-W`

Non attendere il completamento dell&#39;operazione

- Predefinito: `false`
- Non accetta un valore

#### `--wait`

Attendere il completamento dell&#39;operazione (impostazione predefinita)

- Predefinito: `false`
- Non accetta un valore


## `environment:push`

```bash
magento-cloud push [--target TARGET] [-f|--force] [--force-with-lease] [-u|--set-upstream] [--activate] [--parent PARENT] [--type TYPE] [--no-clone-parent] [-W|--no-wait] [--wait] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--] [<source>]
```

Invio del codice a un ambiente

### Argomenti

#### `source`

Il riferimento sorgente Git, ad esempio un nome di ramo o un hash di commit.

- Predefinito: `HEAD`

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--target`

Nome del ramo di destinazione. Viene impostato automaticamente sul ramo corrente.

- Richiede un valore

#### `--force`, `-f`

Consenti aggiornamenti di avanzamento non rapido

- Predefinito: `false`
- Non accetta un valore

#### `--force-with-lease`

Consenti aggiornamenti di inoltro non rapido, se il ramo di tracciamento remoto è aggiornato

- Predefinito: `false`
- Non accetta un valore

#### `--set-upstream`, `-u`

Imposta l’ambiente di destinazione come ambiente a monte per il ramo di origine. Questo imposta anche il progetto di destinazione come remoto per l’archivio locale.

- Predefinito: `false`
- Non accetta un valore

#### `--activate`

Attiva l’ambiente. Gli ambienti in pausa verranno ripresi. In questo modo l’ambiente sarà attivo anche se non è stata inviata alcuna modifica.

- Predefinito: `false`
- Non accetta un valore

#### `--parent`

Imposta l&#39;ambiente padre (utilizzato solo con —activate)

- Richiede un valore

#### `--type`

Imposta il tipo di ambiente (utilizzato solo con —activate )

- Richiede un valore

#### `--no-clone-parent`

Non clonare i dati del ramo principale (utilizzato solo con —activate)

- Predefinito: `false`
- Non accetta un valore

#### `--no-wait`, `-W`

Non attendere il completamento dell&#39;operazione

- Predefinito: `false`
- Non accetta un valore

#### `--wait`

Attendere il completamento dell&#39;operazione (impostazione predefinita)

- Predefinito: `false`
- Non accetta un valore

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore

#### `--environment`, `-e`

ID ambiente. Utilizza &quot;.&quot; per selezionare l’ambiente predefinito del progetto.

- Richiede un valore


## `environment:redeploy`

```bash
magento-cloud redeploy [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait]
```

Ridistribuire un ambiente

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore

#### `--environment`, `-e`

ID ambiente. Utilizza &quot;.&quot; per selezionare l’ambiente predefinito del progetto.

- Richiede un valore

#### `--no-wait`, `-W`

Non attendere il completamento dell&#39;operazione

- Predefinito: `false`
- Non accetta un valore

#### `--wait`

Attendere il completamento dell&#39;operazione (impostazione predefinita)

- Predefinito: `false`
- Non accetta un valore


## `environment:relationships`

```bash
magento-cloud relationships [-P|--property PROPERTY] [--refresh] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--] [<environment>]
```

Visualizzare le relazioni di un ambiente

### Argomenti

#### `environment`

L&#39;ambiente

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--property`, `-P`

Proprietà di relazione da visualizzare

- Richiede un valore

#### `--refresh`

Se aggiornare le relazioni

- Predefinito: `false`
- Non accetta un valore

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore

#### `--environment`, `-e`

ID ambiente. Utilizza &quot;.&quot; per selezionare l’ambiente predefinito del progetto.

- Richiede un valore

#### `--app`, `-A`

Nome dell&#39;applicazione remota

- Richiede un valore


## `environment:resume`

```bash
magento-cloud environment:resume [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait]
```

Riprendere un ambiente in pausa

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore

#### `--environment`, `-e`

ID ambiente. Utilizza &quot;.&quot; per selezionare l’ambiente predefinito del progetto.

- Richiede un valore

#### `--no-wait`, `-W`

Non attendere il completamento dell&#39;operazione

- Predefinito: `false`
- Non accetta un valore

#### `--wait`

Attendere il completamento dell&#39;operazione (impostazione predefinita)

- Predefinito: `false`
- Non accetta un valore


## `environment:scp`

```bash
magento-cloud scp [-r|--recursive] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--worker WORKER] [-I|--instance INSTANCE] [--] [<files>]...
```

Copiare file in e da un ambiente utilizzando scp

### Argomenti

#### `files`

File da copiare. Utilizza il prefisso remote: per definire le posizioni remote.

- Predefinito: `[]`
- Array

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--recursive`, `-r`

Copia ricorsiva di intere directory

- Predefinito: `false`
- Non accetta un valore

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore

#### `--environment`, `-e`

ID ambiente. Utilizza &quot;.&quot; per selezionare l’ambiente predefinito del progetto.

- Richiede un valore

#### `--app`, `-A`

Nome dell&#39;applicazione remota

- Richiede un valore

#### `--worker`

Un nome lavoratore

- Richiede un valore

#### `--instance`, `-I`

Un ID istanza

- Richiede un valore


## `environment:ssh`

```bash
magento-cloud ssh [--pipe] [--all] [-o|--option OPTION] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--worker WORKER] [-I|--instance INSTANCE] [--] [<cmd>]...
```

SSH per l’ambiente corrente

### Argomenti

#### `cmd`

Comando da eseguire nell&#39;ambiente.

- Predefinito: `[]`
- Array

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--pipe`

Genera solo l’URL SSH.

- Predefinito: `false`
- Non accetta un valore

#### `--all`

Genera tutti gli URL SSH (per ogni app).

- Predefinito: `false`
- Non accetta un valore

#### `--option`, `-o`

Trasferisci un&#39;opzione aggiuntiva a SSH

- Predefinito: `[]`
- Richiede un valore

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore

#### `--environment`, `-e`

ID ambiente. Utilizza &quot;.&quot; per selezionare l’ambiente predefinito del progetto.

- Richiede un valore

#### `--app`, `-A`

Nome dell&#39;applicazione remota

- Richiede un valore

#### `--worker`

Un nome lavoratore

- Richiede un valore

#### `--instance`, `-I`

Un ID istanza

- Richiede un valore


## `environment:synchronize`

```bash
magento-cloud sync [--rebase] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<synchronize>]...
```

Sincronizzare il codice e/o i dati di un ambiente dal relativo elemento padre

```
This command synchronizes to a child environment from its parent environment.

Synchronizing "code" means there will be a Git merge from the parent to the
child.

Synchronizing "data" means that all files in all services (including
static files, databases, logs, search indices, etc.) will be copied from the
parent to the child.
```

### Argomenti

#### `synchronize`

Cosa sincronizzare: &quot;codice&quot;, &quot;dati&quot; o entrambi

- Predefinito: `[]`
- Array

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--rebase`

Sincronizzare il codice ribasandolo anziché unendo

- Predefinito: `false`
- Non accetta un valore

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore

#### `--environment`, `-e`

ID ambiente. Utilizza &quot;.&quot; per selezionare l’ambiente predefinito del progetto.

- Richiede un valore

#### `--no-wait`, `-W`

Non attendere il completamento dell&#39;operazione

- Predefinito: `false`
- Non accetta un valore

#### `--wait`

Attendere il completamento dell&#39;operazione (impostazione predefinita)

- Predefinito: `false`
- Non accetta un valore


## `environment:url`

```bash
magento-cloud url [-1|--primary] [--browser BROWSER] [--pipe] [-p|--project PROJECT] [-e|--environment ENVIRONMENT]
```

Ottenere gli URL pubblici di un ambiente

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--primary`, `-1`

Restituisce solo l&#39;URL per la route principale

- Predefinito: `false`
- Non accetta un valore

#### `--browser`

Browser da utilizzare per aprire l’URL. Impostate 0 su none.

- Richiede un valore

#### `--pipe`

Invia l’URL a stdout.

- Predefinito: `false`
- Non accetta un valore

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore

#### `--environment`, `-e`

ID ambiente. Utilizza &quot;.&quot; per selezionare l’ambiente predefinito del progetto.

- Richiede un valore


## `environment:xdebug`

```bash
magento-cloud xdebug [--port PORT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--worker WORKER] [-I|--instance INSTANCE]
```

Apri un tunnel per Xdebug nell’ambiente

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--port`

La porta locale

- Predefinito: `9000`
- Richiede un valore

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore

#### `--environment`, `-e`

ID ambiente. Utilizza &quot;.&quot; per selezionare l’ambiente predefinito del progetto.

- Richiede un valore

#### `--app`, `-A`

Nome dell&#39;applicazione remota

- Richiede un valore

#### `--worker`

Un nome lavoratore

- Richiede un valore

#### `--instance`, `-I`

Un ID istanza

- Richiede un valore


## `integration:activity:get`

```bash
magento-cloud integration:activity:get [-P|--property PROPERTY] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT] [--] [<integration>] [<activity>]
```

Visualizzare informazioni dettagliate su una singola attività di integrazione

### Argomenti

#### `integration`

Un ID integrazione. Lascia vuoto per scegliere da un elenco.


#### `activity`

L’ID attività. Impostazione predefinita dell&#39;attività di integrazione più recente.

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--property`, `-P`

Proprietà da visualizzare

- Richiede un valore

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore

#### `--environment`, `-e`

[Opzione obsoleta, non utilizzata]

- Richiede un valore

#### `--format`

Il formato di output: tabella, csv, tsv o normale

- Predefinito: `table`
- Richiede un valore

#### `--columns`, `-c`

Colonne da visualizzare. I caratteri % o * possono essere utilizzati come caratteri jolly. I valori possono essere divisi da virgole (ad esempio, &quot;a,b,c&quot;) e/o spazi vuoti.

- Predefinito: `[]`
- Richiede un valore

#### `--no-header`

Non generare l’intestazione della tabella

- Predefinito: `false`
- Non accetta un valore

#### `--date-fmt`

Il formato data (come stringa di formato data PHP)

- Predefinito: `c`
- Richiede un valore


## `integration:activity:list`

```bash
magento-cloud integration:activities [--type TYPE] [-x|--exclude-type EXCLUDE-TYPE] [--limit LIMIT] [--start START] [--state STATE] [--result RESULT] [-i|--incomplete] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--] [<id>]
```

Ottieni un elenco di attività per un’integrazione

### Argomenti

#### `id`

Un ID integrazione. Lascia vuoto per scegliere da un elenco.

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--type`

Filtra le attività per tipo. I valori possono essere divisi da virgole (ad esempio, &quot;a,b,c&quot;) e/o spazi vuoti.

- Predefinito: `[]`
- Richiede un valore

#### `--exclude-type`, `-x`

Escludi attività per tipo. I valori possono essere divisi da virgole (ad esempio, &quot;a,b,c&quot;) e/o spazi vuoti. I caratteri % o * possono essere utilizzati come caratteri jolly per escludere i tipi.

- Predefinito: `[]`
- Richiede un valore

#### `--limit`

Limita il numero di risultati visualizzati

- Predefinito: `10`
- Richiede un valore

#### `--start`

Verranno elencate solo le attività create prima di questa data

- Richiede un valore

#### `--state`

Filtra le attività per stato. I valori possono essere divisi da virgole (ad esempio, &quot;a,b,c&quot;) e/o spazi vuoti.

- Predefinito: `[]`
- Richiede un valore

#### `--result`

Filtra attività per risultato

- Richiede un valore

#### `--incomplete`, `-i`

Elencare solo le attività incomplete

- Predefinito: `false`
- Non accetta un valore

#### `--format`

Il formato di output: tabella, csv, tsv o normale

- Predefinito: `table`
- Richiede un valore

#### `--columns`, `-c`

Colonne da visualizzare. Colonne disponibili: id*, created*, description*, type*, state*, result*, completed, progress, time_build, time_deploy, time_execute, time_wait (* = colonne predefinite). Il carattere &quot;+&quot; può essere utilizzato come segnaposto per le colonne predefinite. I caratteri % o * possono essere utilizzati come caratteri jolly. I valori possono essere divisi da virgole (ad esempio, &quot;a,b,c&quot;) e/o spazi vuoti.

- Predefinito: `[]`
- Richiede un valore

#### `--no-header`

Non generare l’intestazione della tabella

- Predefinito: `false`
- Non accetta un valore

#### `--date-fmt`

Il formato data (come stringa di formato data PHP)

- Predefinito: `c`
- Richiede un valore

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore

#### `--environment`, `-e`

[Opzione obsoleta, non utilizzata]

- Richiede un valore


## `integration:activity:log`

```bash
magento-cloud integration:activity:log [-t|--timestamps] [--date-fmt DATE-FMT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--] [<integration>] [<activity>]
```

Visualizzare il registro per un’attività di integrazione

### Argomenti

#### `integration`

Un ID integrazione. Lascia vuoto per scegliere da un elenco.


#### `activity`

L’ID attività. Impostazione predefinita dell&#39;attività di integrazione più recente.

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--timestamps`, `-t`

Visualizza un timestamp accanto a ogni messaggio

- Predefinito: `false`
- Non accetta un valore

#### `--date-fmt`

Il formato data (come stringa di formato data PHP)

- Predefinito: `c`
- Richiede un valore

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore

#### `--environment`, `-e`

[Opzione obsoleta, non utilizzata]

- Richiede un valore


## `integration:add`

```bash
magento-cloud integration:add [--type TYPE] [--base-url BASE-URL] [--bitbucket-url BITBUCKET-URL] [--username USERNAME] [--token TOKEN] [--key KEY] [--secret SECRET] [--license-key LICENSE-KEY] [--server-project SERVER-PROJECT] [--repository REPOSITORY] [--build-merge-requests BUILD-MERGE-REQUESTS] [--build-pull-requests BUILD-PULL-REQUESTS] [--build-draft-pull-requests BUILD-DRAFT-PULL-REQUESTS] [--build-pull-requests-post-merge BUILD-PULL-REQUESTS-POST-MERGE] [--build-wip-merge-requests BUILD-WIP-MERGE-REQUESTS] [--merge-requests-clone-parent-data MERGE-REQUESTS-CLONE-PARENT-DATA] [--pull-requests-clone-parent-data PULL-REQUESTS-CLONE-PARENT-DATA] [--resync-pull-requests RESYNC-PULL-REQUESTS] [--fetch-branches FETCH-BRANCHES] [--prune-branches PRUNE-BRANCHES] [--resources-init RESOURCES-INIT] [--url URL] [--shared-key SHARED-KEY] [--file FILE] [--events EVENTS] [--states STATES] [--environments ENVIRONMENTS] [--excluded-environments EXCLUDED-ENVIRONMENTS] [--from-address FROM-ADDRESS] [--recipients RECIPIENTS] [--channel CHANNEL] [--routing-key ROUTING-KEY] [--category CATEGORY] [--index INDEX] [--sourcetype SOURCETYPE] [--protocol PROTOCOL] [--syslog-host SYSLOG-HOST] [--syslog-port SYSLOG-PORT] [--facility FACILITY] [--message-format MESSAGE-FORMAT] [--auth-mode AUTH-MODE] [--auth-token AUTH-TOKEN] [--verify-tls VERIFY-TLS] [--header HEADER] [-p|--project PROJECT] [-W|--no-wait] [--wait]
```

Aggiungere un’integrazione al progetto

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--type`

Il tipo di integrazione (&quot;bitbucket&quot;, &quot;bitbucket_server&quot;, &quot;github&quot;, &quot;gitlab&quot;, &quot;webhook&quot;, &quot;health.email&quot;, &quot;health.pagerduty&quot;, &quot;health.slack&quot;, &quot;health.webhook&quot;, &quot;httplog&quot;, &quot;script&quot;, &quot;newrelic&quot;, &quot;splunk&quot;, &quot;sumologic&quot;, &quot;syslog&quot;, &quot;otlplog&quot;)

- Richiede un valore

#### `--base-url`

URL di base dell&#39;installazione del server

- Richiede un valore

#### `--bitbucket-url`

URL di base dell&#39;installazione del server Bitbucket

- Richiede un valore

#### `--username`

Nome utente del server Bitbucket

- Richiede un valore

#### `--token`

Un token di autenticazione o di accesso per l’integrazione

- Richiede un valore

#### `--key`

Una chiave consumer OAuth Bitbucket

- Richiede un valore

#### `--secret`

Un segreto consumer di Bitbucket OAuth

- Richiede un valore

#### `--license-key`

Chiave di licenza per i registri di New Relic

- Richiede un valore

#### `--server-project`

Il progetto (ad esempio, &quot;namespace/repo&quot;)

- Richiede un valore

#### `--repository`

L’archivio di cui tenere traccia (ad esempio, &quot;proprietario/archivio&quot;)

- Richiede un valore

#### `--build-merge-requests`

GitLab: creare richieste di unione come ambienti

- Predefinito: `true`
- Richiede un valore

#### `--build-pull-requests`

Creare ogni richiesta di pull come ambiente

- Predefinito: `true`
- Richiede un valore

#### `--build-draft-pull-requests`

Creare bozze di richieste pull

- Predefinito: `true`
- Richiede un valore

#### `--build-pull-requests-post-merge`

Creare richieste di pull in base al loro stato post-unione

- Predefinito: `false`
- Richiede un valore

#### `--build-wip-merge-requests`

GitLab: generare richieste di unione WIP

- Predefinito: `true`
- Richiede un valore

#### `--merge-requests-clone-parent-data`

GitLab: dati clone per richieste di unione

- Predefinito: `true`
- Richiede un valore

#### `--pull-requests-clone-parent-data`

Clonare i dati dell’ambiente principale per le richieste pull

- Predefinito: `true`
- Richiede un valore

#### `--resync-pull-requests`

Risincronizzare i dati dell’ambiente di richiesta pull su ogni build

- Predefinito: `false`
- Richiede un valore

#### `--fetch-branches`

Recupera tutti i rami dal remoto (come ambienti inattivi)

- Predefinito: `true`
- Richiede un valore

#### `--prune-branches`

Elimina rami inesistenti nel remoto

- Predefinito: `true`
- Richiede un valore

#### `--resources-init`

Risorse da utilizzare per l&#39;inizializzazione di un nuovo servizio (&#39;minimum&#39;, &#39;default&#39;, &#39;manual&#39;, &#39;parent&#39;)

- Richiede un valore

#### `--url`

L’URL o l’endpoint API per l’integrazione

- Richiede un valore

#### `--shared-key`

Webhook: chiave segreta condivisa JWS

- Richiede un valore

#### `--file`

Nome di un file locale che contiene lo script da caricare

- Richiede un valore

#### `--events`

Elenco di eventi su cui agire, ad esempio environment.push

- Predefinito: `*`
- Richiede un valore

#### `--states`

Elenco di stati su cui intervenire, ad esempio in sospeso, in corso, completo

- Predefinito: `complete`
- Richiede un valore

#### `--environments`

ID ambiente da includere

- Predefinito: `*`
- Richiede un valore

#### `--excluded-environments`

ID ambiente da escludere

- Predefinito: `[]`
- Richiede un valore

#### `--from-address`

[Facoltativo] Indirizzo mittente personalizzato per le e-mail di avviso

- Richiede un valore

#### `--recipients`

Gli indirizzi e-mail dei destinatari

- Predefinito: `[]`
- Richiede un valore

#### `--channel`

Canale Slack

- Richiede un valore

#### `--routing-key`

Chiave di routing PagerDuty

- Richiede un valore

#### `--category`

La categoria Logica di riepilogo, utilizzata per il filtro

- Richiede un valore

#### `--index`

Indice Splunk

- Richiede un valore

#### `--sourcetype`

Tipo di origine dell&#39;evento Splunk

- Richiede un valore

#### `--protocol`

Protocollo di trasporto Syslog (&#39;tcp&#39;, &#39;udp&#39;, &#39;tls&#39;)

- Predefinito: `tls`
- Richiede un valore

#### `--syslog-host`

Host agente di inoltro/agente di raccolta Syslog

- Richiede un valore

#### `--syslog-port`

Porta di inoltro/raccolta Syslog

- Richiede un valore

#### `--facility`

Funzionalità Syslog

- Predefinito: `1`
- Richiede un valore

#### `--message-format`

Formato del messaggio Syslog (&#39;rfc3164&#39; o &#39;rfc5424&#39;)

- Predefinito: `rfc5424`
- Richiede un valore

#### `--auth-mode`

Modalità di autenticazione (&#39;prefix&#39; o &#39;structured_data&#39;)

- Predefinito: `prefix`
- Richiede un valore

#### `--auth-token`

Token di autenticazione

- Richiede un valore

#### `--verify-tls`

Indica se la verifica del certificato HTTPS deve essere abilitata (scelta consigliata)

- Predefinito: `true`
- Richiede un valore

#### `--header`

Intestazioni HTTP da utilizzare nelle richieste POST. Separa nomi e valori con due punti (:).

- Predefinito: `[]`
- Richiede un valore

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore

#### `--no-wait`, `-W`

Non attendere il completamento dell&#39;operazione

- Predefinito: `false`
- Non accetta un valore

#### `--wait`

Attendere il completamento dell&#39;operazione (impostazione predefinita)

- Predefinito: `false`
- Non accetta un valore


## `integration:delete`

```bash
magento-cloud integration:delete [-p|--project PROJECT] [-W|--no-wait] [--wait] [--] [<id>]
```

Eliminare un’integrazione da un progetto

### Argomenti

#### `id`

L’ID integrazione. Lascia vuoto per scegliere da un elenco.

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore

#### `--no-wait`, `-W`

Non attendere il completamento dell&#39;operazione

- Predefinito: `false`
- Non accetta un valore

#### `--wait`

Attendere il completamento dell&#39;operazione (impostazione predefinita)

- Predefinito: `false`
- Non accetta un valore


## `integration:get`

```bash
magento-cloud integration:get [-P|--property [PROPERTY]] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT] [--] [<id>]
```

Visualizzare i dettagli di un’integrazione

### Argomenti

#### `id`

Un ID integrazione. Lascia vuoto per scegliere da un elenco.

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--property`, `-P`

Proprietà di integrazione da visualizzare

- Accetta un valore

#### `--format`

Il formato di output: tabella, csv, tsv o normale

- Predefinito: `table`
- Richiede un valore

#### `--columns`, `-c`

Colonne da visualizzare. I caratteri % o * possono essere utilizzati come caratteri jolly. I valori possono essere divisi da virgole (ad esempio, &quot;a,b,c&quot;) e/o spazi vuoti.

- Predefinito: `[]`
- Richiede un valore

#### `--no-header`

Non generare l’intestazione della tabella

- Predefinito: `false`
- Non accetta un valore

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore


## `integration:list`

```bash
magento-cloud integrations [-t|--type TYPE] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT]
```

Visualizza un elenco di integrazioni di progetto

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--type`, `-t`

Filtra per tipo

- Richiede un valore

#### `--format`

Il formato di output: tabella, csv, tsv o normale

- Predefinito: `table`
- Richiede un valore

#### `--columns`, `-c`

Colonne da visualizzare. Colonne disponibili: id, riepilogo, tipo. I caratteri % o * possono essere utilizzati come caratteri jolly. I valori possono essere divisi da virgole (ad esempio, &quot;a,b,c&quot;) e/o spazi vuoti.

- Predefinito: `[]`
- Richiede un valore

#### `--no-header`

Non generare l’intestazione della tabella

- Predefinito: `false`
- Non accetta un valore

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore


## `integration:update`

```bash
magento-cloud integration:update [--type TYPE] [--base-url BASE-URL] [--bitbucket-url BITBUCKET-URL] [--username USERNAME] [--token TOKEN] [--key KEY] [--secret SECRET] [--license-key LICENSE-KEY] [--server-project SERVER-PROJECT] [--repository REPOSITORY] [--build-merge-requests BUILD-MERGE-REQUESTS] [--build-pull-requests BUILD-PULL-REQUESTS] [--build-draft-pull-requests BUILD-DRAFT-PULL-REQUESTS] [--build-pull-requests-post-merge BUILD-PULL-REQUESTS-POST-MERGE] [--build-wip-merge-requests BUILD-WIP-MERGE-REQUESTS] [--merge-requests-clone-parent-data MERGE-REQUESTS-CLONE-PARENT-DATA] [--pull-requests-clone-parent-data PULL-REQUESTS-CLONE-PARENT-DATA] [--resync-pull-requests RESYNC-PULL-REQUESTS] [--fetch-branches FETCH-BRANCHES] [--prune-branches PRUNE-BRANCHES] [--resources-init RESOURCES-INIT] [--url URL] [--shared-key SHARED-KEY] [--file FILE] [--events EVENTS] [--states STATES] [--environments ENVIRONMENTS] [--excluded-environments EXCLUDED-ENVIRONMENTS] [--from-address FROM-ADDRESS] [--recipients RECIPIENTS] [--channel CHANNEL] [--routing-key ROUTING-KEY] [--category CATEGORY] [--index INDEX] [--sourcetype SOURCETYPE] [--protocol PROTOCOL] [--syslog-host SYSLOG-HOST] [--syslog-port SYSLOG-PORT] [--facility FACILITY] [--message-format MESSAGE-FORMAT] [--auth-mode AUTH-MODE] [--auth-token AUTH-TOKEN] [--verify-tls VERIFY-TLS] [--header HEADER] [-p|--project PROJECT] [-W|--no-wait] [--wait] [--] [<id>]
```

Aggiornare un’integrazione

### Argomenti

#### `id`

ID dell’integrazione da aggiornare

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--type`

Il tipo di integrazione (&quot;bitbucket&quot;, &quot;bitbucket_server&quot;, &quot;github&quot;, &quot;gitlab&quot;, &quot;webhook&quot;, &quot;health.email&quot;, &quot;health.pagerduty&quot;, &quot;health.slack&quot;, &quot;health.webhook&quot;, &quot;httplog&quot;, &quot;script&quot;, &quot;newrelic&quot;, &quot;splunk&quot;, &quot;sumologic&quot;, &quot;syslog&quot;, &quot;otlplog&quot;)

- Richiede un valore

#### `--base-url`

URL di base dell&#39;installazione del server

- Richiede un valore

#### `--bitbucket-url`

URL di base dell&#39;installazione del server Bitbucket

- Richiede un valore

#### `--username`

Nome utente del server Bitbucket

- Richiede un valore

#### `--token`

Un token di autenticazione o di accesso per l’integrazione

- Richiede un valore

#### `--key`

Una chiave consumer OAuth Bitbucket

- Richiede un valore

#### `--secret`

Un segreto consumer di Bitbucket OAuth

- Richiede un valore

#### `--license-key`

Chiave di licenza per i registri di New Relic

- Richiede un valore

#### `--server-project`

Il progetto (ad esempio, &quot;namespace/repo&quot;)

- Richiede un valore

#### `--repository`

L’archivio di cui tenere traccia (ad esempio, &quot;proprietario/archivio&quot;)

- Richiede un valore

#### `--build-merge-requests`

GitLab: creare richieste di unione come ambienti

- Predefinito: `true`
- Richiede un valore

#### `--build-pull-requests`

Creare ogni richiesta di pull come ambiente

- Predefinito: `true`
- Richiede un valore

#### `--build-draft-pull-requests`

Creare bozze di richieste pull

- Predefinito: `true`
- Richiede un valore

#### `--build-pull-requests-post-merge`

Creare richieste di pull in base al loro stato post-unione

- Predefinito: `false`
- Richiede un valore

#### `--build-wip-merge-requests`

GitLab: generare richieste di unione WIP

- Predefinito: `true`
- Richiede un valore

#### `--merge-requests-clone-parent-data`

GitLab: dati clone per richieste di unione

- Predefinito: `true`
- Richiede un valore

#### `--pull-requests-clone-parent-data`

Clonare i dati dell’ambiente principale per le richieste pull

- Predefinito: `true`
- Richiede un valore

#### `--resync-pull-requests`

Risincronizzare i dati dell’ambiente di richiesta pull su ogni build

- Predefinito: `false`
- Richiede un valore

#### `--fetch-branches`

Recupera tutti i rami dal remoto (come ambienti inattivi)

- Predefinito: `true`
- Richiede un valore

#### `--prune-branches`

Elimina rami inesistenti nel remoto

- Predefinito: `true`
- Richiede un valore

#### `--resources-init`

Risorse da utilizzare per l&#39;inizializzazione di un nuovo servizio (&#39;minimum&#39;, &#39;default&#39;, &#39;manual&#39;, &#39;parent&#39;)

- Richiede un valore

#### `--url`

L’URL o l’endpoint API per l’integrazione

- Richiede un valore

#### `--shared-key`

Webhook: chiave segreta condivisa JWS

- Richiede un valore

#### `--file`

Nome di un file locale che contiene lo script da caricare

- Richiede un valore

#### `--events`

Elenco di eventi su cui agire, ad esempio environment.push

- Predefinito: `*`
- Richiede un valore

#### `--states`

Elenco di stati su cui intervenire, ad esempio in sospeso, in corso, completo

- Predefinito: `complete`
- Richiede un valore

#### `--environments`

ID ambiente da includere

- Predefinito: `*`
- Richiede un valore

#### `--excluded-environments`

ID ambiente da escludere

- Predefinito: `[]`
- Richiede un valore

#### `--from-address`

[Facoltativo] Indirizzo mittente personalizzato per le e-mail di avviso

- Richiede un valore

#### `--recipients`

Gli indirizzi e-mail dei destinatari

- Predefinito: `[]`
- Richiede un valore

#### `--channel`

Canale Slack

- Richiede un valore

#### `--routing-key`

Chiave di routing PagerDuty

- Richiede un valore

#### `--category`

La categoria Logica di riepilogo, utilizzata per il filtro

- Richiede un valore

#### `--index`

Indice Splunk

- Richiede un valore

#### `--sourcetype`

Tipo di origine dell&#39;evento Splunk

- Richiede un valore

#### `--protocol`

Protocollo di trasporto Syslog (&#39;tcp&#39;, &#39;udp&#39;, &#39;tls&#39;)

- Predefinito: `tls`
- Richiede un valore

#### `--syslog-host`

Host agente di inoltro/agente di raccolta Syslog

- Richiede un valore

#### `--syslog-port`

Porta di inoltro/raccolta Syslog

- Richiede un valore

#### `--facility`

Funzionalità Syslog

- Predefinito: `1`
- Richiede un valore

#### `--message-format`

Formato del messaggio Syslog (&#39;rfc3164&#39; o &#39;rfc5424&#39;)

- Predefinito: `rfc5424`
- Richiede un valore

#### `--auth-mode`

Modalità di autenticazione (&#39;prefix&#39; o &#39;structured_data&#39;)

- Predefinito: `prefix`
- Richiede un valore

#### `--auth-token`

Token di autenticazione

- Richiede un valore

#### `--verify-tls`

Indica se la verifica del certificato HTTPS deve essere abilitata (scelta consigliata)

- Predefinito: `true`
- Richiede un valore

#### `--header`

Intestazioni HTTP da utilizzare nelle richieste POST. Separa nomi e valori con due punti (:).

- Predefinito: `[]`
- Richiede un valore

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore

#### `--no-wait`, `-W`

Non attendere il completamento dell&#39;operazione

- Predefinito: `false`
- Non accetta un valore

#### `--wait`

Attendere il completamento dell&#39;operazione (impostazione predefinita)

- Predefinito: `false`
- Non accetta un valore


## `integration:validate`

```bash
magento-cloud integration:validate [-p|--project PROJECT] [--] [<id>]
```

Convalidare un’integrazione esistente

```
This command allows you to check whether an integration is valid.

An exit code of 0 means the integration is valid, while 4 means it is invalid.
Any other exit code indicates an unexpected error.

Integrations are validated automatically on creation and on update. However,
because they involve external resources, it is possible for a valid integration
to become invalid. For example, an access token may be revoked, or an external
repository may be deleted.
```

### Argomenti

#### `id`

Un ID integrazione. Lascia vuoto per scegliere da un elenco.

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore


## `local:build`

```bash
magento-cloud build [-a|--abslinks] [-s|--source SOURCE] [-d|--destination DESTINATION] [-c|--copy] [--clone] [--run-deploy-hooks] [--no-clean] [--no-archive] [--no-backup] [--no-cache] [--no-build-hooks] [--no-deps] [--working-copy] [--concurrency CONCURRENCY] [--lock] [--] [<app>]...
```

Crea il progetto corrente localmente

### Argomenti

#### `app`

Specifica le applicazioni da generare

- Predefinito: `[]`
- Array

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--abslinks`, `-a`

Utilizzare i collegamenti assoluti

- Predefinito: `false`
- Non accetta un valore

#### `--source`, `-s`

La directory di origine. Impostazione predefinita: directory principale del progetto corrente.

- Richiede un valore

#### `--destination`, `-d`

La destinazione, alla quale sarà collegata la directory principale del web di ogni app. Predefinito: _www

- Richiede un valore

#### `--copy`, `-c`

Copia in una directory di build, invece di eseguire il collegamento simbolico dal sorgente

- Predefinito: `false`
- Non accetta un valore

#### `--clone`

Utilizza Git per clonare il HEAD corrente nella directory di build

- Predefinito: `false`
- Non accetta un valore

#### `--run-deploy-hooks`

Eseguire gli hook di distribuzione e/o post_distribuzione

- Predefinito: `false`
- Non accetta un valore

#### `--no-clean`

Non rimuovere le build precedenti

- Predefinito: `false`
- Non accetta un valore

#### `--no-archive`

Non creare o utilizzare un archivio di build

- Predefinito: `false`
- Non accetta un valore

#### `--no-backup`

Non eseguire il backup della build precedente

- Predefinito: `false`
- Non accetta un valore

#### `--no-cache`

Disattiva caching

- Predefinito: `false`
- Non accetta un valore

#### `--no-build-hooks`

Non eseguire hook di post-generazione

- Predefinito: `false`
- Non accetta un valore

#### `--no-deps`

Non installare localmente le dipendenze della build

- Predefinito: `false`
- Non accetta un valore

#### `--working-copy`

Elimina: utilizza Git per clonare un archivio di ciascun modulo Drupal anziché semplicemente scaricare una versione

- Predefinito: `false`
- Non accetta un valore

#### `--concurrency`

Elimina: imposta il numero di progetti simultanei che verranno elaborati contemporaneamente

- Predefinito: `4`
- Richiede un valore

#### `--lock`

Drush: crea o aggiorna un file di blocco (disponibile solo con Drush versione 7+)

- Predefinito: `false`
- Non accetta un valore


## `local:dir`

```bash
magento-cloud dir [<subdir>]
```

Trova la directory principale del progetto locale

### Argomenti

#### `subdir`

La sottodirectory da trovare (&#39;local&#39;, &#39;web&#39; o &#39;shared&#39;)

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).


## `metrics:all`

```bash
magento-cloud metrics [-B|--bytes] [-r|--range RANGE] [-i|--interval INTERVAL] [--to TO] [-1|--latest] [-s|--service SERVICE] [--type TYPE] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT]
```

Mostra le metriche di CPU, disco e memoria per un ambiente

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--bytes`, `-B`

Mostra dimensioni in byte

- Predefinito: `false`
- Non accetta un valore

#### `--range`, `-r`

L’intervallo di tempo. Le metriche vengono caricate per questa durata fino all’ora di fine (—to). È possibile specificare le unità di misura: ore (h), minuti (m) o secondi (s). Minimo 5 m, massimo 8 h o più (a seconda del progetto), predefinito 10 m.

- Richiede un valore

#### `--interval`, `-i`

Intervallo di tempo. Impostazione predefinita: una divisione dell&#39;intervallo. È possibile specificare le unità di misura: ore (h), minuti (m) o secondi (s). Minimo 1 m.

- Richiede un valore

#### `--to`

Ora di fine. Impostazione predefinita.

- Richiede un valore

#### `--latest`, `-1`

Mostra solo l&#39;ultimo punto dati singolo

- Predefinito: `false`
- Non accetta un valore

#### `--service`, `-s`

Filtra in base al nome del servizio o dell&#39;applicazione È possibile utilizzare come carattere jolly i caratteri % o *.

- Predefinito: `[]`
- Richiede un valore

#### `--type`

Filtra per tipo di servizio (se —servizio non è fornito). La versione non è richiesta. I caratteri % o * possono essere utilizzati come caratteri jolly.

- Predefinito: `[]`
- Richiede un valore

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore

#### `--environment`, `-e`

ID ambiente. Utilizza &quot;.&quot; per selezionare l’ambiente predefinito del progetto.

- Richiede un valore

#### `--format`

Il formato di output: tabella, csv, tsv o normale

- Predefinito: `table`
- Richiede un valore

#### `--columns`, `-c`

Colonne da visualizzare. Colonne disponibili: timestamp*, service*, cpu_percent*, mem_percent*, disk_percent*, tmp_disk_percent*, cpu_limit, cpu_used, disk_limit, disk_used, inodes_limit, inodes_percent, inodes_used, mem_limit, mem_used, tmp_disk_limit, tmp_disk_used, tmp_inodes_limit, tmp_inodes_percent, tmp_inodes_used, type (* = default columns). Il carattere &quot;+&quot; può essere utilizzato come segnaposto per le colonne predefinite. I caratteri % o * possono essere utilizzati come caratteri jolly. I valori possono essere divisi da virgole (ad esempio, &quot;a,b,c&quot;) e/o spazi vuoti.

- Predefinito: `[]`
- Richiede un valore

#### `--no-header`

Non generare l’intestazione della tabella

- Predefinito: `false`
- Non accetta un valore

#### `--date-fmt`

Il formato data (come stringa di formato data PHP)

- Predefinito: `c`
- Richiede un valore


## `metrics:cpu`

```bash
magento-cloud cpu [-r|--range RANGE] [-i|--interval INTERVAL] [--to TO] [-1|--latest] [-s|--service SERVICE] [--type TYPE] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT]
```

Mostrare l’utilizzo di un ambiente da parte di CPU

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--range`, `-r`

L’intervallo di tempo. Le metriche vengono caricate per questa durata fino all’ora di fine (—to). È possibile specificare le unità di misura: ore (h), minuti (m) o secondi (s). Minimo 5 m, massimo 8 h o più (a seconda del progetto), predefinito 10 m.

- Richiede un valore

#### `--interval`, `-i`

Intervallo di tempo. Impostazione predefinita: una divisione dell&#39;intervallo. È possibile specificare le unità di misura: ore (h), minuti (m) o secondi (s). Minimo 1 m.

- Richiede un valore

#### `--to`

Ora di fine. Impostazione predefinita.

- Richiede un valore

#### `--latest`, `-1`

Mostra solo l&#39;ultimo punto dati singolo

- Predefinito: `false`
- Non accetta un valore

#### `--service`, `-s`

Filtra in base al nome del servizio o dell&#39;applicazione È possibile utilizzare come carattere jolly i caratteri % o *.

- Predefinito: `[]`
- Richiede un valore

#### `--type`

Filtra per tipo di servizio (se —servizio non è fornito). La versione non è richiesta. I caratteri % o * possono essere utilizzati come caratteri jolly.

- Predefinito: `[]`
- Richiede un valore

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore

#### `--environment`, `-e`

ID ambiente. Utilizza &quot;.&quot; per selezionare l’ambiente predefinito del progetto.

- Richiede un valore

#### `--format`

Il formato di output: tabella, csv, tsv o normale

- Predefinito: `table`
- Richiede un valore

#### `--columns`, `-c`

Colonne da visualizzare. Colonne disponibili: timestamp*, service*, used*, limit*, percent*, type (* = default columns). Il carattere &quot;+&quot; può essere utilizzato come segnaposto per le colonne predefinite. I caratteri % o * possono essere utilizzati come caratteri jolly. I valori possono essere divisi da virgole (ad esempio, &quot;a,b,c&quot;) e/o spazi vuoti.

- Predefinito: `[]`
- Richiede un valore

#### `--no-header`

Non generare l’intestazione della tabella

- Predefinito: `false`
- Non accetta un valore

#### `--date-fmt`

Il formato data (come stringa di formato data PHP)

- Predefinito: `c`
- Richiede un valore


## `metrics:disk-usage`

```bash
magento-cloud disk [-B|--bytes] [-r|--range RANGE] [-i|--interval INTERVAL] [--to TO] [-1|--latest] [-s|--service SERVICE] [--type TYPE] [--tmp] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT]
```

Mostra l’utilizzo del disco di un ambiente

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--bytes`, `-B`

Mostra dimensioni in byte

- Predefinito: `false`
- Non accetta un valore

#### `--range`, `-r`

L’intervallo di tempo. Le metriche vengono caricate per questa durata fino all’ora di fine (—to). È possibile specificare le unità di misura: ore (h), minuti (m) o secondi (s). Minimo 5 m, massimo 8 h o più (a seconda del progetto), predefinito 10 m.

- Richiede un valore

#### `--interval`, `-i`

Intervallo di tempo. Impostazione predefinita: una divisione dell&#39;intervallo. È possibile specificare le unità di misura: ore (h), minuti (m) o secondi (s). Minimo 1 m.

- Richiede un valore

#### `--to`

Ora di fine. Impostazione predefinita.

- Richiede un valore

#### `--latest`, `-1`

Mostra solo l&#39;ultimo punto dati singolo

- Predefinito: `false`
- Non accetta un valore

#### `--service`, `-s`

Filtra in base al nome del servizio o dell&#39;applicazione È possibile utilizzare come carattere jolly i caratteri % o *.

- Predefinito: `[]`
- Richiede un valore

#### `--type`

Filtra per tipo di servizio (se —servizio non è fornito). La versione non è richiesta. I caratteri % o * possono essere utilizzati come caratteri jolly.

- Predefinito: `[]`
- Richiede un valore

#### `--tmp`

Segnala l’utilizzo temporaneo del disco (mostra le colonne: timestamp, service, tmp_used, tmp_limit, tmp_percent, tmp_ipercent)

- Predefinito: `false`
- Non accetta un valore

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore

#### `--environment`, `-e`

ID ambiente. Utilizza &quot;.&quot; per selezionare l’ambiente predefinito del progetto.

- Richiede un valore

#### `--format`

Il formato di output: tabella, csv, tsv o normale

- Predefinito: `table`
- Richiede un valore

#### `--columns`, `-c`

Colonne da visualizzare. Colonne disponibili: timestamp*, service*, used*, limit*, percent*, ipercent*, tmp_percent*, ilimit, iused, tmp_ilimit, tmp_ipercent, tmp_iused, tmp_limit, tmp_used, type (* = default columns). Il carattere &quot;+&quot; può essere utilizzato come segnaposto per le colonne predefinite. I caratteri % o * possono essere utilizzati come caratteri jolly. I valori possono essere divisi da virgole (ad esempio, &quot;a,b,c&quot;) e/o spazi vuoti.

- Predefinito: `[]`
- Richiede un valore

#### `--no-header`

Non generare l’intestazione della tabella

- Predefinito: `false`
- Non accetta un valore

#### `--date-fmt`

Il formato data (come stringa di formato data PHP)

- Predefinito: `c`
- Richiede un valore


## `metrics:memory`

```bash
magento-cloud mem [-B|--bytes] [-r|--range RANGE] [-i|--interval INTERVAL] [--to TO] [-1|--latest] [-s|--service SERVICE] [--type TYPE] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT]
```

Mostra l’utilizzo della memoria di un ambiente

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--bytes`, `-B`

Mostra dimensioni in byte

- Predefinito: `false`
- Non accetta un valore

#### `--range`, `-r`

L’intervallo di tempo. Le metriche vengono caricate per questa durata fino all’ora di fine (—to). È possibile specificare le unità di misura: ore (h), minuti (m) o secondi (s). Minimo 5 m, massimo 8 h o più (a seconda del progetto), predefinito 10 m.

- Richiede un valore

#### `--interval`, `-i`

Intervallo di tempo. Impostazione predefinita: una divisione dell&#39;intervallo. È possibile specificare le unità di misura: ore (h), minuti (m) o secondi (s). Minimo 1 m.

- Richiede un valore

#### `--to`

Ora di fine. Impostazione predefinita.

- Richiede un valore

#### `--latest`, `-1`

Mostra solo l&#39;ultimo punto dati singolo

- Predefinito: `false`
- Non accetta un valore

#### `--service`, `-s`

Filtra in base al nome del servizio o dell&#39;applicazione È possibile utilizzare come carattere jolly i caratteri % o *.

- Predefinito: `[]`
- Richiede un valore

#### `--type`

Filtra per tipo di servizio (se —servizio non è fornito). La versione non è richiesta. I caratteri % o * possono essere utilizzati come caratteri jolly.

- Predefinito: `[]`
- Richiede un valore

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore

#### `--environment`, `-e`

ID ambiente. Utilizza &quot;.&quot; per selezionare l’ambiente predefinito del progetto.

- Richiede un valore

#### `--format`

Il formato di output: tabella, csv, tsv o normale

- Predefinito: `table`
- Richiede un valore

#### `--columns`, `-c`

Colonne da visualizzare. Colonne disponibili: timestamp*, service*, used*, limit*, percent*, type (* = default columns). Il carattere &quot;+&quot; può essere utilizzato come segnaposto per le colonne predefinite. I caratteri % o * possono essere utilizzati come caratteri jolly. I valori possono essere divisi da virgole (ad esempio, &quot;a,b,c&quot;) e/o spazi vuoti.

- Predefinito: `[]`
- Richiede un valore

#### `--no-header`

Non generare l’intestazione della tabella

- Predefinito: `false`
- Non accetta un valore

#### `--date-fmt`

Il formato data (come stringa di formato data PHP)

- Predefinito: `c`
- Richiede un valore


## `mount:download`

```bash
magento-cloud mount:download [-a|--all] [-m|--mount MOUNT] [--target TARGET] [--source-path] [--delete] [--exclude EXCLUDE] [--include INCLUDE] [--refresh] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--worker WORKER] [-I|--instance INSTANCE]
```

Scaricare i file da un mount utilizzando rsync

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--all`, `-a`

Scarica da tutti i supporti

- Predefinito: `false`
- Non accetta un valore

#### `--mount`, `-m`

Il mount (come percorso relativo all’app)

- Richiede un valore

#### `--target`

La directory in cui verranno scaricati i file. Se si utilizza —all, al percorso di montaggio verrà aggiunto

- Richiede un valore

#### `--source-path`

Utilizza il percorso di origine del mount (anziché il percorso di mount) come sottodirectory della destinazione, quando si utilizza —all

- Predefinito: `false`
- Non accetta un valore

#### `--delete`

Specifica se eliminare i file estranei nella directory di destinazione

- Predefinito: `false`
- Non accetta un valore

#### `--exclude`

File da escludere dal download (modello)

- Predefinito: `[]`
- Richiede un valore

#### `--include`

File da non escludere (pattern)

- Predefinito: `[]`
- Richiede un valore

#### `--refresh`

Se aggiornare la cache

- Predefinito: `false`
- Non accetta un valore

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore

#### `--environment`, `-e`

ID ambiente. Utilizza &quot;.&quot; per selezionare l’ambiente predefinito del progetto.

- Richiede un valore

#### `--app`, `-A`

Nome dell&#39;applicazione remota

- Richiede un valore

#### `--worker`

Un nome lavoratore

- Richiede un valore

#### `--instance`, `-I`

Un ID istanza

- Richiede un valore


## `mount:list`

```bash
magento-cloud mounts [--paths] [--refresh] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--worker WORKER] [-I|--instance INSTANCE]
```

Ottieni un elenco di montaggi

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--paths`

Output solo dei percorsi di montaggio (uno per riga)

- Predefinito: `false`
- Non accetta un valore

#### `--refresh`

Se aggiornare la cache

- Predefinito: `false`
- Non accetta un valore

#### `--format`

Il formato di output: tabella, csv, tsv o normale

- Predefinito: `table`
- Richiede un valore

#### `--columns`, `-c`

Colonne da visualizzare. Colonne disponibili: definizione, percorso. I caratteri % o * possono essere utilizzati come caratteri jolly. I valori possono essere divisi da virgole (ad esempio, &quot;a,b,c&quot;) e/o spazi vuoti.

- Predefinito: `[]`
- Richiede un valore

#### `--no-header`

Non generare l’intestazione della tabella

- Predefinito: `false`
- Non accetta un valore

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore

#### `--environment`, `-e`

ID ambiente. Utilizza &quot;.&quot; per selezionare l’ambiente predefinito del progetto.

- Richiede un valore

#### `--app`, `-A`

Nome dell&#39;applicazione remota

- Richiede un valore

#### `--worker`

Un nome lavoratore

- Richiede un valore

#### `--instance`, `-I`

Un ID istanza

- Richiede un valore


## `mount:upload`

```bash
magento-cloud mount:upload [--source SOURCE] [-m|--mount MOUNT] [--delete] [--exclude EXCLUDE] [--include INCLUDE] [--refresh] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--worker WORKER] [-I|--instance INSTANCE]
```

Caricare i file su un mount, utilizzando rsync

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--source`

Una directory contenente i file da caricare

- Richiede un valore

#### `--mount`, `-m`

Il mount (come percorso relativo all’app)

- Richiede un valore

#### `--delete`

Indica se eliminare i file estranei nel mount

- Predefinito: `false`
- Non accetta un valore

#### `--exclude`

File da escludere dal caricamento (pattern)

- Predefinito: `[]`
- Richiede un valore

#### `--include`

File da non escludere (pattern)

- Predefinito: `[]`
- Richiede un valore

#### `--refresh`

Se aggiornare la cache

- Predefinito: `false`
- Non accetta un valore

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore

#### `--environment`, `-e`

ID ambiente. Utilizza &quot;.&quot; per selezionare l’ambiente predefinito del progetto.

- Richiede un valore

#### `--app`, `-A`

Nome dell&#39;applicazione remota

- Richiede un valore

#### `--worker`

Un nome lavoratore

- Richiede un valore

#### `--instance`, `-I`

Un ID istanza

- Richiede un valore


## `operation:list`

```bash
magento-cloud ops [--full] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--worker WORKER] [--format FORMAT] [-c|--columns COLUMNS] [--no-header]
```

Elencare le operazioni di runtime in un ambiente

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--full`

Non limitare la lunghezza del comando da visualizzare. Il limite predefinito è 24 righe.

- Predefinito: `false`
- Non accetta un valore

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore

#### `--environment`, `-e`

ID ambiente. Utilizza &quot;.&quot; per selezionare l’ambiente predefinito del progetto.

- Richiede un valore

#### `--app`, `-A`

Nome dell&#39;applicazione remota

- Richiede un valore

#### `--worker`

Un nome lavoratore

- Richiede un valore

#### `--format`

Il formato di output: tabella, csv, tsv o normale

- Predefinito: `table`
- Richiede un valore

#### `--columns`, `-c`

Colonne da visualizzare. Colonne disponibili: service*, name*, start*, role, stop (* = colonne predefinite). Il carattere &quot;+&quot; può essere utilizzato come segnaposto per le colonne predefinite. I caratteri % o * possono essere utilizzati come caratteri jolly. I valori possono essere divisi da virgole (ad esempio, &quot;a,b,c&quot;) e/o spazi vuoti.

- Predefinito: `[]`
- Richiede un valore

#### `--no-header`

Non generare l’intestazione della tabella

- Predefinito: `false`
- Non accetta un valore


## `operation:run`

```bash
magento-cloud operation:run [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--worker WORKER] [-W|--no-wait] [--wait] [--] [<operation>]
```

Eseguire un’operazione nell’ambiente

### Argomenti

#### `operation`

Nome dell’operazione

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore

#### `--environment`, `-e`

ID ambiente. Utilizza &quot;.&quot; per selezionare l’ambiente predefinito del progetto.

- Richiede un valore

#### `--app`, `-A`

Nome dell&#39;applicazione remota

- Richiede un valore

#### `--worker`

Un nome lavoratore

- Richiede un valore

#### `--no-wait`, `-W`

Non attendere il completamento dell&#39;operazione

- Predefinito: `false`
- Non accetta un valore

#### `--wait`

Attendere il completamento dell&#39;operazione (impostazione predefinita)

- Predefinito: `false`
- Non accetta un valore


## `project:clear-build-cache`

```bash
magento-cloud project:clear-build-cache [-p|--project PROJECT]
```

Cancellare la cache di build di un progetto

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore


## `project:get`

```bash
magento-cloud get [-e|--environment ENVIRONMENT] [--depth DEPTH] [--build] [-p|--project PROJECT] [--] [<project>] [<directory>]
```

Clonare un progetto localmente

### Argomenti

#### `project`

ID progetto


#### `directory`

La directory in cui clonare. Impostazione predefinita del titolo del progetto

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--environment`, `-e`

ID ambiente da clonare. Impostazione predefinita del progetto o del primo ambiente disponibile

- Richiede un valore

#### `--depth`

Creare un clone superficiale: limita il numero di commit nella cronologia

- Richiede un valore

#### `--build`

Genera il progetto dopo la clonazione

- Predefinito: `false`
- Non accetta un valore

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore


## `project:info`

```bash
magento-cloud project:info [--refresh] [--date-fmt DATE-FMT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT] [-W|--no-wait] [--wait] [--] [<property>] [<value>]
```

Lettura o impostazione delle proprietà di un progetto

### Argomenti

#### `property`

Nome della proprietà


#### `value`

Imposta un nuovo valore per la proprietà

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--refresh`

Se aggiornare la cache

- Predefinito: `false`
- Non accetta un valore

#### `--date-fmt`

Il formato data (come stringa di formato data PHP)

- Predefinito: `c`
- Richiede un valore

#### `--format`

Il formato di output: tabella, csv, tsv o normale

- Predefinito: `table`
- Richiede un valore

#### `--columns`, `-c`

Colonne da visualizzare. I caratteri % o * possono essere utilizzati come caratteri jolly. I valori possono essere divisi da virgole (ad esempio, &quot;a,b,c&quot;) e/o spazi vuoti.

- Predefinito: `[]`
- Richiede un valore

#### `--no-header`

Non generare l’intestazione della tabella

- Predefinito: `false`
- Non accetta un valore

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore

#### `--no-wait`, `-W`

Non attendere il completamento dell&#39;operazione

- Predefinito: `false`
- Non accetta un valore

#### `--wait`

Attendere il completamento dell&#39;operazione (impostazione predefinita)

- Predefinito: `false`
- Non accetta un valore


## `project:list`

```bash
magento-cloud projects [--pipe] [--region REGION] [--title TITLE] [--my] [--refresh REFRESH] [--sort SORT] [--reverse] [--page PAGE] [-c|--count COUNT] [--format FORMAT] [--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT]
```

Ottieni un elenco di tutti i progetti attivi

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--pipe`

Genera un semplice elenco di ID progetto. Disattiva la paginazione.

- Predefinito: `false`
- Non accetta un valore

#### `--region`

Filtra per area geografica (corrispondenza esatta)

- Richiede un valore

#### `--title`

Filtra per titolo (ricerca senza distinzione maiuscole/minuscole)

- Richiede un valore

#### `--my`

Visualizza solo i progetti di tua proprietà

- Predefinito: `false`
- Non accetta un valore

#### `--refresh`

Se aggiornare l’elenco

- Predefinito: `1`
- Richiede un valore

#### `--sort`

Proprietà in base alla quale eseguire l&#39;ordinamento

- Predefinito: `title`
- Richiede un valore

#### `--reverse`

Ordinamento inverso (decrescente)

- Predefinito: `false`
- Non accetta un valore

#### `--page`

Numero di pagina. Questo consente l’impaginazione, nonostante la configurazione o il conteggio. Ignorato se è specificato —pipe.

- Richiede un valore

#### `--count`, `-c`

Il numero di progetti da visualizzare per pagina. Utilizza 0 per disabilitare l’impaginazione. Ignorato se si specifica —page.

- Richiede un valore

#### `--format`

Il formato di output: tabella, csv, tsv o normale

- Predefinito: `table`
- Richiede un valore

#### `--columns`

Colonne da visualizzare. Colonne disponibili: id*, title*, region*, created_at, organization_id, organization_label, organization_name, organization_type, status (* = colonne predefinite). Il carattere &quot;+&quot; può essere utilizzato come segnaposto per le colonne predefinite. I caratteri % o * possono essere utilizzati come caratteri jolly. I valori possono essere divisi da virgole (ad esempio, &quot;a,b,c&quot;) e/o spazi vuoti.

- Predefinito: `[]`
- Richiede un valore

#### `--no-header`

Non generare l’intestazione della tabella

- Predefinito: `false`
- Non accetta un valore

#### `--date-fmt`

Il formato data (come stringa di formato data PHP)

- Predefinito: `c`
- Richiede un valore


## `project:set-remote`

```bash
magento-cloud set-remote [<project>]
```

Imposta il progetto remoto per l’archivio Git corrente

### Argomenti

#### `project`

ID progetto

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).


## `repo:cat`

```bash
magento-cloud repo:cat [-c|--commit COMMIT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--] <path>
```

Lettura di un file nel repository del progetto

### Argomenti

#### `path`

Percorso del file

- Obbligatorio

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--commit`, `-c`

Il commit SHA. Questo può anche accettare suffissi &quot;HEAD&quot; e accento circonflesso (^) o tilde (~) per commit principali.

- Richiede un valore

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore

#### `--environment`, `-e`

ID ambiente. Utilizza &quot;.&quot; per selezionare l’ambiente predefinito del progetto.

- Richiede un valore


## `repo:ls`

```bash
magento-cloud repo:ls [-d|--directories] [-f|--files] [--git-style] [-c|--commit COMMIT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--] [<path>]
```

Elencare i file nell’archivio del progetto

### Argomenti

#### `path`

Percorso di una sottodirectory

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--directories`, `-d`

Mostra solo directory

- Predefinito: `false`
- Non accetta un valore

#### `--files`, `-f`

Mostra solo file

- Predefinito: `false`
- Non accetta un valore

#### `--git-style`

Output di stile simile a &quot;Git ls-tree&quot;

- Predefinito: `false`
- Non accetta un valore

#### `--commit`, `-c`

Il commit SHA. Questo può anche accettare suffissi &quot;HEAD&quot; e accento circonflesso (^) o tilde (~) per commit principali.

- Richiede un valore

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore

#### `--environment`, `-e`

ID ambiente. Utilizza &quot;.&quot; per selezionare l’ambiente predefinito del progetto.

- Richiede un valore


## `repo:read`

```bash
magento-cloud read [-c|--commit COMMIT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--] [<path>]
```

Lettura di una directory o di un file nel repository del progetto

### Argomenti

#### `path`

Percorso della directory o del file

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--commit`, `-c`

Il commit SHA. Questo può anche accettare suffissi &quot;HEAD&quot; e accento circonflesso (^) o tilde (~) per commit principali.

- Richiede un valore

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore

#### `--environment`, `-e`

ID ambiente. Utilizza &quot;.&quot; per selezionare l’ambiente predefinito del progetto.

- Richiede un valore


## `resources:build:get`

```bash
magento-cloud build-resources:get [-p|--project PROJECT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header]
```

Visualizzare le risorse di build di un progetto

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore

#### `--format`

Il formato di output: tabella, csv, tsv o normale

- Predefinito: `table`
- Richiede un valore

#### `--columns`, `-c`

Colonne da visualizzare. Colonne disponibili: CPU, memoria. I caratteri % o * possono essere utilizzati come caratteri jolly. I valori possono essere divisi da virgole (ad esempio, &quot;a,b,c&quot;) e/o spazi vuoti.

- Predefinito: `[]`
- Richiede un valore

#### `--no-header`

Non generare l’intestazione della tabella

- Predefinito: `false`
- Non accetta un valore


## `route:get`

```bash
magento-cloud route:get [--id ID] [-1|--primary] [-P|--property PROPERTY] [--refresh] [--date-fmt DATE-FMT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [-i|--identity-file IDENTITY-FILE] [--] [<route>]
```

Visualizzare informazioni dettagliate su un ciclo di lavorazione

### Argomenti

#### `route`

URL originale del percorso

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--id`

Un ID di route da selezionare

- Richiede un valore

#### `--primary`, `-1`

Seleziona il percorso principale

- Predefinito: `false`
- Non accetta un valore

#### `--property`, `-P`

Proprietà da visualizzare

- Richiede un valore

#### `--refresh`

Ignora la cache delle route

- Predefinito: `false`
- Non accetta un valore

#### `--date-fmt`

Il formato data (come stringa di formato data PHP)

- Predefinito: `c`
- Richiede un valore

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore

#### `--environment`, `-e`

ID ambiente. Utilizza &quot;.&quot; per selezionare l’ambiente predefinito del progetto.

- Richiede un valore

#### `--app`, `-A`

[Opzione obsoleta, non più utilizzata]

- Richiede un valore

#### `--identity-file`, `-i`

[Opzione obsoleta, non più utilizzata]

- Richiede un valore


## `route:list`

```bash
magento-cloud routes [--refresh] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--] [<environment>]
```

Elencare tutte le route per un ambiente

### Argomenti

#### `environment`

ID dell’ambiente

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--refresh`

Ignora la cache delle route

- Predefinito: `false`
- Non accetta un valore

#### `--format`

Il formato di output: tabella, csv, tsv o normale

- Predefinito: `table`
- Richiede un valore

#### `--columns`, `-c`

Colonne da visualizzare. Colonne disponibili: route*, type*, to*, url (* = colonne predefinite). Il carattere &quot;+&quot; può essere utilizzato come segnaposto per le colonne predefinite. I caratteri % o * possono essere utilizzati come caratteri jolly. I valori possono essere divisi da virgole (ad esempio, &quot;a,b,c&quot;) e/o spazi vuoti.

- Predefinito: `[]`
- Richiede un valore

#### `--no-header`

Non generare l’intestazione della tabella

- Predefinito: `false`
- Non accetta un valore

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore

#### `--environment`, `-e`

ID ambiente. Utilizza &quot;.&quot; per selezionare l’ambiente predefinito del progetto.

- Richiede un valore


## `self:install`

```bash
magento-cloud self:install [--shell-type SHELL-TYPE]
```

Installare o aggiornare i file di configurazione CLI

```
This command automatically installs shell configuration for the Magento Cloud CLI,
adding autocompletion support and handy aliases. Bash and ZSH are supported.
```

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--shell-type`

Tipo di shell per il completamento automatico (bash o zsh)

- Richiede un valore


## `self:update`

```bash
magento-cloud update [--no-major] [--unstable] [--manifest MANIFEST] [--current-version CURRENT-VERSION] [--timeout TIMEOUT]
```

Aggiornare CLI alla versione più recente

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--no-major`

Aggiorna solo tra versioni secondarie o patch

- Predefinito: `false`
- Non accetta un valore

#### `--unstable`

Aggiornamento a una nuova versione instabile, se disponibile

- Predefinito: `false`
- Non accetta un valore

#### `--manifest`

Ignora il percorso del file manifesto

- Richiede un valore

#### `--current-version`

Sostituisci la versione corrente

- Richiede un valore

#### `--timeout`

Timeout per il controllo della versione

- Predefinito: `30`
- Richiede un valore


## `service:list`

```bash
magento-cloud services [--refresh] [--pipe] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header]
```

Elencare servizi nel progetto

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--refresh`

Se aggiornare la cache

- Predefinito: `false`
- Non accetta un valore

#### `--pipe`

Genera un elenco di nomi di servizio

- Predefinito: `false`
- Non accetta un valore

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore

#### `--environment`, `-e`

ID ambiente. Utilizza &quot;.&quot; per selezionare l’ambiente predefinito del progetto.

- Richiede un valore

#### `--format`

Il formato di output: tabella, csv, tsv o normale

- Predefinito: `table`
- Richiede un valore

#### `--columns`, `-c`

Colonne da visualizzare. Colonne disponibili: disco, nome, dimensione, tipo. I caratteri % o * possono essere utilizzati come caratteri jolly. I valori possono essere divisi da virgole (ad esempio, &quot;a,b,c&quot;) e/o spazi vuoti.

- Predefinito: `[]`
- Richiede un valore

#### `--no-header`

Non generare l’intestazione della tabella

- Predefinito: `false`
- Non accetta un valore


## `service:mongo:dump`

```bash
magento-cloud mongodump [-c|--collection COLLECTION] [-z|--gzip] [-o|--stdout] [-r|--relationship RELATIONSHIP] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP]
```

Creare un dump di archivio binario di dati da MongoDB

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--collection`, `-c`

Raccolta da scaricare

- Richiede un valore

#### `--gzip`, `-z`

Comprimi l’immagine utilizzando gzip

- Predefinito: `false`
- Non accetta un valore

#### `--stdout`, `-o`

Output in STDOUT anziché in un file

- Predefinito: `false`
- Non accetta un valore

#### `--relationship`, `-r`

Relazione di servizio da utilizzare

- Richiede un valore

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore

#### `--environment`, `-e`

ID ambiente. Utilizza &quot;.&quot; per selezionare l’ambiente predefinito del progetto.

- Richiede un valore

#### `--app`, `-A`

Nome dell&#39;applicazione remota

- Richiede un valore


## `service:mongo:export`

```bash
magento-cloud mongoexport [-c|--collection COLLECTION] [--jsonArray] [--type TYPE] [-f|--fields FIELDS] [-r|--relationship RELATIONSHIP] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP]
```

Esporta dati da MongoDB

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--collection`, `-c`

Raccolta da esportare

- Richiede un valore

#### `--jsonArray`

Esportare i dati come un singolo array JSON

- Predefinito: `false`
- Non accetta un valore

#### `--type`

Tipo di esportazione, ad esempio &quot;csv&quot;

- Richiede un valore

#### `--fields`, `-f`

Campi da esportare

- Predefinito: `[]`
- Richiede un valore

#### `--relationship`, `-r`

Relazione di servizio da utilizzare

- Richiede un valore

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore

#### `--environment`, `-e`

ID ambiente. Utilizza &quot;.&quot; per selezionare l’ambiente predefinito del progetto.

- Richiede un valore

#### `--app`, `-A`

Nome dell&#39;applicazione remota

- Richiede un valore


## `service:mongo:restore`

```bash
magento-cloud mongorestore [-c|--collection COLLECTION] [-r|--relationship RELATIONSHIP] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP]
```

Ripristinare un’immagine di archivio binaria dei dati in MongoDB

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--collection`, `-c`

Raccolta da ripristinare

- Richiede un valore

#### `--relationship`, `-r`

Relazione di servizio da utilizzare

- Richiede un valore

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore

#### `--environment`, `-e`

ID ambiente. Utilizza &quot;.&quot; per selezionare l’ambiente predefinito del progetto.

- Richiede un valore

#### `--app`, `-A`

Nome dell&#39;applicazione remota

- Richiede un valore


## `service:mongo:shell`

```bash
magento-cloud mongo [--eval EVAL] [-r|--relationship RELATIONSHIP] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP]
```

Utilizzare la shell MongoDB

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--eval`

Trasmettere un frammento JavaScript alla shell

- Richiede un valore

#### `--relationship`, `-r`

Relazione di servizio da utilizzare

- Richiede un valore

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore

#### `--environment`, `-e`

ID ambiente. Utilizza &quot;.&quot; per selezionare l’ambiente predefinito del progetto.

- Richiede un valore

#### `--app`, `-A`

Nome dell&#39;applicazione remota

- Richiede un valore


## `service:redis-cli`

```bash
magento-cloud redis [-r|--relationship RELATIONSHIP] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--] [<args>]...
```

Accedere a Redis CLI

### Argomenti

#### `args`

Argomenti da aggiungere al comando redis-cli

- Predefinito: `[]`
- Array

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--relationship`, `-r`

Relazione di servizio da utilizzare

- Richiede un valore

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore

#### `--environment`, `-e`

ID ambiente. Utilizza &quot;.&quot; per selezionare l’ambiente predefinito del progetto.

- Richiede un valore

#### `--app`, `-A`

Nome dell&#39;applicazione remota

- Richiede un valore


## `service:valkey-cli`

```bash
magento-cloud valkey [-r|--relationship RELATIONSHIP] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--] [<args>]...
```

Accedere a Valkey CLI

### Argomenti

#### `args`

Argomenti da aggiungere al comando valkey-cli

- Predefinito: `[]`
- Array

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--relationship`, `-r`

Relazione di servizio da utilizzare

- Richiede un valore

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore

#### `--environment`, `-e`

ID ambiente. Utilizza &quot;.&quot; per selezionare l’ambiente predefinito del progetto.

- Richiede un valore

#### `--app`, `-A`

Nome dell&#39;applicazione remota

- Richiede un valore


## `snapshot:create`

```bash
magento-cloud backup [--live] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<environment>]
```

Creare un’istantanea di un ambiente

### Argomenti

#### `environment`

L&#39;ambiente

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--live`

Snapshot live: non arrestare l’ambiente. Se questa opzione è impostata, l’ambiente rimane in esecuzione e si apre alle connessioni durante lo snapshot. Ciò riduce i tempi di inattività, con il rischio di eseguire il backup dei dati in uno stato incoerente.

- Predefinito: `false`
- Non accetta un valore

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore

#### `--environment`, `-e`

ID ambiente. Utilizza &quot;.&quot; per selezionare l’ambiente predefinito del progetto.

- Richiede un valore

#### `--no-wait`, `-W`

Non attendere il completamento dell&#39;operazione

- Predefinito: `false`
- Non accetta un valore

#### `--wait`

Attendere il completamento dell&#39;operazione (impostazione predefinita)

- Predefinito: `false`
- Non accetta un valore


## `snapshot:delete`

```bash
magento-cloud snapshot:delete [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<id>]
```

Eliminare uno snapshot dell’ambiente

### Argomenti

#### `id`

ID dello snapshot. Richiesto in modalità non interattiva.

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore

#### `--environment`, `-e`

ID ambiente. Utilizza &quot;.&quot; per selezionare l’ambiente predefinito del progetto.

- Richiede un valore

#### `--no-wait`, `-W`

Non attendere il completamento dell&#39;operazione

- Predefinito: `false`
- Non accetta un valore

#### `--wait`

Attendere il completamento dell&#39;operazione (impostazione predefinita)

- Predefinito: `false`
- Non accetta un valore


## `snapshot:get`

```bash
magento-cloud snapshot:get [-P|--property PROPERTY] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--date-fmt DATE-FMT] [--] [<id>]
```

Visualizzare uno snapshot dell’ambiente

### Argomenti

#### `id`

ID dello snapshot. Viene impostato automaticamente sul valore più recente.

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--property`, `-P`

Proprietà da visualizzare.

- Richiede un valore

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore

#### `--environment`, `-e`

ID ambiente. Utilizza &quot;.&quot; per selezionare l’ambiente predefinito del progetto.

- Richiede un valore

#### `--date-fmt`

Il formato data (come stringa di formato data PHP)

- Predefinito: `c`
- Richiede un valore


## `snapshot:list`

```bash
magento-cloud snapshots [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT]
```

Elencare le istantanee disponibili di un ambiente

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--format`

Il formato di output: tabella, csv, tsv o normale

- Predefinito: `table`
- Richiede un valore

#### `--columns`, `-c`

Colonne da visualizzare. I caratteri % o * possono essere utilizzati come caratteri jolly. I valori possono essere divisi da virgole (ad esempio, &quot;a,b,c&quot;) e/o spazi vuoti.

- Predefinito: `[]`
- Richiede un valore

#### `--no-header`

Non generare l’intestazione della tabella

- Predefinito: `false`
- Non accetta un valore

#### `--date-fmt`

Il formato data (come stringa di formato data PHP)

- Predefinito: `c`
- Richiede un valore

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore

#### `--environment`, `-e`

ID ambiente. Utilizza &quot;.&quot; per selezionare l’ambiente predefinito del progetto.

- Richiede un valore


## `snapshot:restore`

```bash
magento-cloud snapshot:restore [--target TARGET] [--branch-from BRANCH-FROM] [--no-code] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<snapshot>]
```

Ripristinare uno snapshot dell’ambiente

### Argomenti

#### `snapshot`

ID dello snapshot. Impostazione predefinita più recente

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--target`

L’ambiente in cui eseguire il ripristino. Impostazione predefinita dell&#39;ambiente corrente dello snapshot

- Richiede un valore

#### `--branch-from`

Se —target non esiste ancora, specifica l&#39;elemento padre del nuovo ambiente

- Richiede un valore

#### `--no-code`

Non ripristinare codice, solo dati.

- Predefinito: `false`
- Non accetta un valore

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore

#### `--environment`, `-e`

ID ambiente. Utilizza &quot;.&quot; per selezionare l’ambiente predefinito del progetto.

- Richiede un valore

#### `--no-wait`, `-W`

Non attendere il completamento dell&#39;operazione

- Predefinito: `false`
- Non accetta un valore

#### `--wait`

Attendere il completamento dell&#39;operazione (impostazione predefinita)

- Predefinito: `false`
- Non accetta un valore


## `source-operation:list`

```bash
magento-cloud source-ops [--full] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header]
```

Elencare le operazioni di origine in un ambiente

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--full`

Non limitare la lunghezza del comando da visualizzare. Il limite predefinito è 24 righe.

- Predefinito: `false`
- Non accetta un valore

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore

#### `--environment`, `-e`

ID ambiente. Utilizza &quot;.&quot; per selezionare l’ambiente predefinito del progetto.

- Richiede un valore

#### `--format`

Il formato di output: tabella, csv, tsv o normale

- Predefinito: `table`
- Richiede un valore

#### `--columns`, `-c`

Colonne da visualizzare. Colonne disponibili: app, comando, operazione. I caratteri % o * possono essere utilizzati come caratteri jolly. I valori possono essere divisi da virgole (ad esempio, &quot;a,b,c&quot;) e/o spazi vuoti.

- Predefinito: `[]`
- Richiede un valore

#### `--no-header`

Non generare l’intestazione della tabella

- Predefinito: `false`
- Non accetta un valore


## `source-operation:run`

```bash
magento-cloud source-operation:run [--variable VARIABLE] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<operation>]
```

Eseguire un&#39;operazione di origine

### Argomenti

#### `operation`

Nome dell’operazione

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--variable`

Variabile da impostare durante l&#39;operazione, nel formato tipo:name=valore

- Predefinito: `[]`
- Richiede un valore

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore

#### `--environment`, `-e`

ID ambiente. Utilizza &quot;.&quot; per selezionare l’ambiente predefinito del progetto.

- Richiede un valore

#### `--no-wait`, `-W`

Non attendere il completamento dell&#39;operazione

- Predefinito: `false`
- Non accetta un valore

#### `--wait`

Attendere il completamento dell&#39;operazione (impostazione predefinita)

- Predefinito: `false`
- Non accetta un valore


## `ssh-cert:load`

```bash
magento-cloud ssh-cert:load [--refresh-only] [--new] [--new-key]
```

Generare un certificato SSH

```
This command checks if a valid SSH certificate is present, and generates a
new one if necessary.

Certificates allow you to make SSH connections without having previously
uploaded a public key. They are more secure than keys and they allow for
other features.

Normally the certificate is loaded automatically during login, or when
making an SSH connection. So this command is seldom needed.

If you want to set up certificates without login and without an SSH-related
command, for example if you are writing a script that uses an API token via
an environment variable, then you would probably want to run this command
explicitly. For unattended scripts, remember to turn off interaction via
--yes or the MAGENTO_CLOUD_CLI_NO_INTERACTION environment variable.
```

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--refresh-only`

Aggiorna il certificato solo se necessario (non scrivere la configurazione SSH)

- Predefinito: `false`
- Non accetta un valore

#### `--new`

Forza l’aggiornamento del certificato

- Predefinito: `false`
- Non accetta un valore

#### `--new-key`

Forza la generazione di una nuova coppia di chiavi

- Predefinito: `false`
- Non accetta un valore


## `ssh-key:add`

```bash
magento-cloud ssh-key:add [--name NAME] [--] [<path>]
```

Aggiungi una nuova chiave SSH

```
This command lets you add an SSH key to your account. It can generate a key using OpenSSH.

Notice:
SSH keys are no longer needed by default, as SSH certificates are supported.
Certificates offer more security than keys.

To load or check your SSH certificate, run: magento-cloud ssh-cert:load
```

### Argomenti

#### `path`

Percorso di una chiave pubblica SSH esistente

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--name`

Nome per identificare la chiave

- Richiede un valore


## `ssh-key:delete`

```bash
magento-cloud ssh-key:delete [<id>]
```

Eliminare una chiave SSH

```
This command lets you delete SSH keys from your account.

Notice:
SSH keys are no longer needed by default, as SSH certificates are supported.
Certificates offer more security than keys.

To load or check your SSH certificate, run: magento-cloud ssh-cert:load
```

### Argomenti

#### `id`

ID della chiave SSH da eliminare

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).


## `ssh-key:list`

```bash
magento-cloud ssh-keys [--format FORMAT] [-c|--columns COLUMNS] [--no-header]
```

Ottieni un elenco di chiavi SSH nel tuo account

```
This command lets you list SSH keys in your account.

Notice:
SSH keys are no longer needed by default, as SSH certificates are supported.
Certificates offer more security than keys.

To load or check your SSH certificate, run: magento-cloud ssh-cert:load
```

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--format`

Il formato di output: tabella, csv, tsv o normale

- Predefinito: `table`
- Richiede un valore

#### `--columns`, `-c`

Colonne da visualizzare. Colonne disponibili: id*, title*, path*, fingerprint (* = colonne predefinite). Il carattere &quot;+&quot; può essere utilizzato come segnaposto per le colonne predefinite. I caratteri % o * possono essere utilizzati come caratteri jolly. I valori possono essere divisi da virgole (ad esempio, &quot;a,b,c&quot;) e/o spazi vuoti.

- Predefinito: `[]`
- Richiede un valore

#### `--no-header`

Non generare l’intestazione della tabella

- Predefinito: `false`
- Non accetta un valore


## `subscription:info`

```bash
magento-cloud subscription:info [-s|--id ID] [--date-fmt DATE-FMT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT] [--] [<property>] [<value>]
```

Lettura o modifica delle proprietà di sottoscrizione

### Argomenti

#### `property`

Nome della proprietà


#### `value`

Imposta un nuovo valore per la proprietà

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--id`, `-s`

ID sottoscrizione

- Richiede un valore

#### `--date-fmt`

Il formato data (come stringa di formato data PHP)

- Predefinito: `c`
- Richiede un valore

#### `--format`

Il formato di output: tabella, csv, tsv o normale

- Predefinito: `table`
- Richiede un valore

#### `--columns`, `-c`

Colonne da visualizzare. I caratteri % o * possono essere utilizzati come caratteri jolly. I valori possono essere divisi da virgole (ad esempio, &quot;a,b,c&quot;) e/o spazi vuoti.

- Predefinito: `[]`
- Richiede un valore

#### `--no-header`

Non generare l’intestazione della tabella

- Predefinito: `false`
- Non accetta un valore

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore


## `tunnel:close`

```bash
magento-cloud tunnel:close [-a|--all] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP]
```

Chiudi tunnel SSH

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--all`, `-a`

Chiudi tutti i tunnel

- Predefinito: `false`
- Non accetta un valore

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore

#### `--environment`, `-e`

ID ambiente. Utilizza &quot;.&quot; per selezionare l’ambiente predefinito del progetto.

- Richiede un valore

#### `--app`, `-A`

Nome dell&#39;applicazione remota

- Richiede un valore


## `tunnel:info`

```bash
magento-cloud tunnel:info [-P|--property PROPERTY] [-c|--encode] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP]
```

Visualizza informazioni sulle relazioni per i tunnel SSH

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--property`, `-P`

Proprietà di relazione da visualizzare

- Richiede un valore

#### `--encode`, `-c`

Output come JSON con codifica base64

- Predefinito: `false`
- Non accetta un valore

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore

#### `--environment`, `-e`

ID ambiente. Utilizza &quot;.&quot; per selezionare l’ambiente predefinito del progetto.

- Richiede un valore

#### `--app`, `-A`

Nome dell&#39;applicazione remota

- Richiede un valore


## `tunnel:list`

```bash
magento-cloud tunnels [-a|--all] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--format FORMAT] [-c|--columns COLUMNS] [--no-header]
```

Elenca tunnel SSH

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--all`, `-a`

Visualizza tutti i tunnel

- Predefinito: `false`
- Non accetta un valore

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore

#### `--environment`, `-e`

ID ambiente. Utilizza &quot;.&quot; per selezionare l’ambiente predefinito del progetto.

- Richiede un valore

#### `--app`, `-A`

Nome dell&#39;applicazione remota

- Richiede un valore

#### `--format`

Il formato di output: tabella, csv, tsv o normale

- Predefinito: `table`
- Richiede un valore

#### `--columns`, `-c`

Colonne da visualizzare. Colonne disponibili: porta*, progetto*, ambiente*, app*, relazione*, URL (* = colonne predefinite). Il carattere &quot;+&quot; può essere utilizzato come segnaposto per le colonne predefinite. I caratteri % o * possono essere utilizzati come caratteri jolly. I valori possono essere divisi da virgole (ad esempio, &quot;a,b,c&quot;) e/o spazi vuoti.

- Predefinito: `[]`
- Richiede un valore

#### `--no-header`

Non generare l’intestazione della tabella

- Predefinito: `false`
- Non accetta un valore


## `tunnel:open`

```bash
magento-cloud tunnel:open [-g|--gateway-ports] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP]
```

Aprire i tunnel SSH alle relazioni di un’app

```
This command opens SSH tunnels to all of the relationships of an application.

Connections can then be made to the application's services as if they were
local, for example a local MySQL client can be used, or the Solr web
administration endpoint can be accessed through a local browser.

This command requires the posix and pcntl PHP extensions (as multiple
background CLI processes are created to keep the SSH tunnels open). The
tunnel:single command can be used on systems without these
extensions.
```

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--gateway-ports`, `-g`

Consenti agli host remoti di connettersi alle porte inoltrate locali

- Predefinito: `false`
- Non accetta un valore

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore

#### `--environment`, `-e`

ID ambiente. Utilizza &quot;.&quot; per selezionare l’ambiente predefinito del progetto.

- Richiede un valore

#### `--app`, `-A`

Nome dell&#39;applicazione remota

- Richiede un valore


## `tunnel:single`

```bash
magento-cloud tunnel:single [--port PORT] [-g|--gateway-ports] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [-r|--relationship RELATIONSHIP]
```

Aprire un singolo tunnel SSH a una relazione app

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--port`

La porta locale

- Richiede un valore

#### `--gateway-ports`, `-g`

Consenti agli host remoti di connettersi alle porte inoltrate locali

- Predefinito: `false`
- Non accetta un valore

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore

#### `--environment`, `-e`

ID ambiente. Utilizza &quot;.&quot; per selezionare l’ambiente predefinito del progetto.

- Richiede un valore

#### `--app`, `-A`

Nome dell&#39;applicazione remota

- Richiede un valore

#### `--relationship`, `-r`

Relazione di servizio da utilizzare

- Richiede un valore


## `user:add`

```bash
magento-cloud user:add [-r|--role ROLE] [--force-invite] [-p|--project PROJECT] [-W|--no-wait] [--wait] [--] [<email>]
```

Aggiungere un utente al progetto

### Argomenti

#### `email`

Indirizzo e-mail dell’utente

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--role`, `-r`

Ruolo del progetto dell&#39;utente (&#39;admin&#39; o &#39;viewer&#39;) o ruolo del tipo di ambiente (ad esempio &#39;staging:contributor&#39; o &#39;production:viewer&#39;). Per rimuovere un utente da un tipo di ambiente, imposta il ruolo come &quot;none&quot; (nessuno). I caratteri % o * possono essere utilizzati come carattere jolly per il tipo di ambiente, ad esempio &#39;%:viewer&#39; per assegnare all&#39;utente il ruolo &#39;visualizzatore&#39; su tutti i tipi. Il ruolo può essere abbreviato, ad esempio &#39;production:v&#39;.

- Predefinito: `[]`
- Richiede un valore

#### `--force-invite`

Invia un invito, anche se ne è già stato inviato uno

- Predefinito: `false`
- Non accetta un valore

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore

#### `--no-wait`, `-W`

Non attendere il completamento dell&#39;operazione

- Predefinito: `false`
- Non accetta un valore

#### `--wait`

Attendere il completamento dell&#39;operazione (impostazione predefinita)

- Predefinito: `false`
- Non accetta un valore


## `user:delete`

```bash
magento-cloud user:delete [-p|--project PROJECT] [-W|--no-wait] [--wait] [--] <email>
```

Eliminare un utente dal progetto

### Argomenti

#### `email`

Indirizzo e-mail dell’utente

- Obbligatorio

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore

#### `--no-wait`, `-W`

Non attendere il completamento dell&#39;operazione

- Predefinito: `false`
- Non accetta un valore

#### `--wait`

Attendere il completamento dell&#39;operazione (impostazione predefinita)

- Predefinito: `false`
- Non accetta un valore


## `user:get`

```bash
magento-cloud user:get [-l|--level LEVEL] [--pipe] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [-r|--role ROLE] [--] [<email>]
```

Visualizzare i ruoli di un utente

### Argomenti

#### `email`

Indirizzo e-mail dell’utente

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--level`, `-l`

Livello di ruolo (&quot;progetto&quot; o &quot;ambiente&quot;)

- Richiede un valore

#### `--pipe`

Trasmette il ruolo allo stdout (dopo aver apportato eventuali modifiche)

- Predefinito: `false`
- Non accetta un valore

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore

#### `--environment`, `-e`

ID ambiente. Utilizza &quot;.&quot; per selezionare l’ambiente predefinito del progetto.

- Richiede un valore

#### `--no-wait`, `-W`

Non attendere il completamento dell&#39;operazione

- Predefinito: `false`
- Non accetta un valore

#### `--wait`

Attendere il completamento dell&#39;operazione (impostazione predefinita)

- Predefinito: `false`
- Non accetta un valore

#### `--role`, `-r`

[Obsoleto: utilizzare l&#39;utente:update per modificare i ruoli di un utente]

- Richiede un valore


## `user:list`

```bash
magento-cloud users [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT]
```

Elenca utenti progetto

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--format`

Il formato di output: tabella, csv, tsv o normale

- Predefinito: `table`
- Richiede un valore

#### `--columns`, `-c`

Colonne da visualizzare. Colonne disponibili: email*, name*, role*, id*, grant_at, update_at (* = colonne predefinite). Il carattere &quot;+&quot; può essere utilizzato come segnaposto per le colonne predefinite. I caratteri % o * possono essere utilizzati come caratteri jolly. I valori possono essere divisi da virgole (ad esempio, &quot;a,b,c&quot;) e/o spazi vuoti.

- Predefinito: `[]`
- Richiede un valore

#### `--no-header`

Non generare l’intestazione della tabella

- Predefinito: `false`
- Non accetta un valore

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore


## `user:update`

```bash
magento-cloud user:update [-r|--role ROLE] [-p|--project PROJECT] [-W|--no-wait] [--wait] [--] [<email>]
```

Aggiornare i ruoli utente in un progetto

### Argomenti

#### `email`

Indirizzo e-mail dell’utente

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--role`, `-r`

Ruolo del progetto dell&#39;utente (&#39;admin&#39; o &#39;viewer&#39;) o ruolo del tipo di ambiente (ad esempio &#39;staging:contributor&#39; o &#39;production:viewer&#39;). Per rimuovere un utente da un tipo di ambiente, imposta il ruolo come &quot;none&quot; (nessuno). I caratteri % o * possono essere utilizzati come carattere jolly per il tipo di ambiente, ad esempio &#39;%:viewer&#39; per assegnare all&#39;utente il ruolo &#39;visualizzatore&#39; su tutti i tipi. Il ruolo può essere abbreviato, ad esempio &#39;production:v&#39;.

- Predefinito: `[]`
- Richiede un valore

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore

#### `--no-wait`, `-W`

Non attendere il completamento dell&#39;operazione

- Predefinito: `false`
- Non accetta un valore

#### `--wait`

Attendere il completamento dell&#39;operazione (impostazione predefinita)

- Predefinito: `false`
- Non accetta un valore


## `variable:create`

```bash
magento-cloud variable:create [-u|--update] [-l|--level LEVEL] [--name NAME] [--value VALUE] [--json JSON] [--sensitive SENSITIVE] [--prefix PREFIX] [--enabled ENABLED] [--inheritable INHERITABLE] [--visible-build VISIBLE-BUILD] [--visible-runtime VISIBLE-RUNTIME] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<name>]
```

Creare una variabile

### Argomenti

#### `name`

Nome della variabile

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--update`, `-u`

Aggiorna la variabile se esiste già

- Predefinito: `false`
- Non accetta un valore

#### `--level`, `-l`

Livello al quale impostare la variabile (&quot;progetto&quot; o &quot;ambiente&quot;)

- Richiede un valore

#### `--name`

Nome della variabile

- Richiede un valore

#### `--value`

Valore della variabile

- Richiede un valore

#### `--json`

Se il valore della variabile è in formato JSON

- Predefinito: `false`
- Richiede un valore

#### `--sensitive`

Se il valore della variabile è sensibile

- Predefinito: `false`
- Richiede un valore

#### `--prefix`

Prefisso del nome della variabile che può determinarne il tipo, ad esempio &#39;env&#39;. Applicabile solo se il nome non contiene già un prefisso. (ad esempio, &#39;none&#39; o &#39;env:&#39;)

- Predefinito: `none`
- Richiede un valore

#### `--enabled`

Specifica se la variabile deve essere abilitata nell’ambiente

- Predefinito: `true`
- Richiede un valore

#### `--inheritable`

Se la variabile è ereditabile dagli ambienti figlio

- Predefinito: `true`
- Richiede un valore

#### `--visible-build`

Indica se la variabile deve essere visibile al momento della compilazione

- Richiede un valore

#### `--visible-runtime`

Indica se la variabile deve essere visibile in fase di runtime

- Predefinito: `true`
- Richiede un valore

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore

#### `--environment`, `-e`

ID ambiente. Utilizza &quot;.&quot; per selezionare l’ambiente predefinito del progetto.

- Richiede un valore

#### `--no-wait`, `-W`

Non attendere il completamento dell&#39;operazione

- Predefinito: `false`
- Non accetta un valore

#### `--wait`

Attendere il completamento dell&#39;operazione (impostazione predefinita)

- Predefinito: `false`
- Non accetta un valore


## `variable:delete`

```bash
magento-cloud variable:delete [-l|--level LEVEL] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] <name>
```

Eliminare una variabile

### Argomenti

#### `name`

Nome della variabile

- Obbligatorio

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--level`, `-l`

Livello della variabile (&quot;project&quot;, &quot;environment&quot;, &quot;p&quot; o &quot;e&quot;)

- Richiede un valore

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore

#### `--environment`, `-e`

ID ambiente. Utilizza &quot;.&quot; per selezionare l’ambiente predefinito del progetto.

- Richiede un valore

#### `--no-wait`, `-W`

Non attendere il completamento dell&#39;operazione

- Predefinito: `false`
- Non accetta un valore

#### `--wait`

Attendere il completamento dell&#39;operazione (impostazione predefinita)

- Predefinito: `false`
- Non accetta un valore


## `variable:get`

```bash
magento-cloud vget [-P|--property PROPERTY] [-l|--level LEVEL] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--pipe] [--] [<name>]
```

Visualizzare una variabile

### Argomenti

#### `name`

Nome della variabile

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--property`, `-P`

Visualizzare una singola proprietà variabile

- Richiede un valore

#### `--level`, `-l`

Livello della variabile (&quot;project&quot;, &quot;environment&quot;, &quot;p&quot; o &quot;e&quot;)

- Richiede un valore

#### `--format`

Il formato di output: tabella, csv, tsv o normale

- Predefinito: `table`
- Richiede un valore

#### `--columns`, `-c`

Colonne da visualizzare. I caratteri % o * possono essere utilizzati come caratteri jolly. I valori possono essere divisi da virgole (ad esempio, &quot;a,b,c&quot;) e/o spazi vuoti.

- Predefinito: `[]`
- Richiede un valore

#### `--no-header`

Non generare l’intestazione della tabella

- Predefinito: `false`
- Non accetta un valore

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore

#### `--environment`, `-e`

ID ambiente. Utilizza &quot;.&quot; per selezionare l’ambiente predefinito del progetto.

- Richiede un valore

#### `--pipe`

[Opzione obsoleta] Restituisce solo il valore della variabile

- Predefinito: `false`
- Non accetta un valore


## `variable:list`

```bash
magento-cloud variables [-l|--level LEVEL] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT] [-e|--environment ENVIRONMENT]
```

Variabili elenco

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--level`, `-l`

Livello della variabile (&quot;project&quot;, &quot;environment&quot;, &quot;p&quot; o &quot;e&quot;)

- Richiede un valore

#### `--format`

Il formato di output: tabella, csv, tsv o normale

- Predefinito: `table`
- Richiede un valore

#### `--columns`, `-c`

Colonne da visualizzare. Colonne disponibili: is_enabled, level, name, value. I caratteri % o * possono essere utilizzati come caratteri jolly. I valori possono essere divisi da virgole (ad esempio, &quot;a,b,c&quot;) e/o spazi vuoti.

- Predefinito: `[]`
- Richiede un valore

#### `--no-header`

Non generare l’intestazione della tabella

- Predefinito: `false`
- Non accetta un valore

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore

#### `--environment`, `-e`

ID ambiente. Utilizza &quot;.&quot; per selezionare l’ambiente predefinito del progetto.

- Richiede un valore


## `variable:update`

```bash
magento-cloud variable:update [--allow-no-change] [-l|--level LEVEL] [--value VALUE] [--json JSON] [--sensitive SENSITIVE] [--enabled ENABLED] [--inheritable INHERITABLE] [--visible-build VISIBLE-BUILD] [--visible-runtime VISIBLE-RUNTIME] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] <name>
```

Aggiornare una variabile

### Argomenti

#### `name`

Nome della variabile

- Obbligatorio

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--allow-no-change`

Restituzione riuscita (codice di uscita pari a zero) se non sono state fornite modifiche

- Predefinito: `false`
- Non accetta un valore

#### `--level`, `-l`

Livello della variabile (&quot;project&quot;, &quot;environment&quot;, &quot;p&quot; o &quot;e&quot;)

- Richiede un valore

#### `--value`

Valore della variabile

- Richiede un valore

#### `--json`

Se il valore della variabile è in formato JSON

- Predefinito: `false`
- Richiede un valore

#### `--sensitive`

Se il valore della variabile è sensibile

- Predefinito: `false`
- Richiede un valore

#### `--enabled`

Specifica se la variabile deve essere abilitata nell’ambiente

- Predefinito: `true`
- Richiede un valore

#### `--inheritable`

Se la variabile è ereditabile dagli ambienti figlio

- Predefinito: `true`
- Richiede un valore

#### `--visible-build`

Indica se la variabile deve essere visibile al momento della compilazione

- Richiede un valore

#### `--visible-runtime`

Indica se la variabile deve essere visibile in fase di runtime

- Predefinito: `true`
- Richiede un valore

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore

#### `--environment`, `-e`

ID ambiente. Utilizza &quot;.&quot; per selezionare l’ambiente predefinito del progetto.

- Richiede un valore

#### `--no-wait`, `-W`

Non attendere il completamento dell&#39;operazione

- Predefinito: `false`
- Non accetta un valore

#### `--wait`

Attendere il completamento dell&#39;operazione (impostazione predefinita)

- Predefinito: `false`
- Non accetta un valore


## `worker:list`

```bash
magento-cloud workers [--refresh] [--pipe] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header]
```

Ottieni un elenco di tutti i processi di lavoro distribuiti

### Opzioni

Per le opzioni globali, vedi [Opzioni globali](#global-options).

#### `--refresh`

Se aggiornare la cache

- Predefinito: `false`
- Non accetta un valore

#### `--pipe`

Generare un elenco di nomi di lavoratori

- Predefinito: `false`
- Non accetta un valore

#### `--project`, `-p`

ID o URL del progetto

- Richiede un valore

#### `--environment`, `-e`

ID ambiente. Utilizza &quot;.&quot; per selezionare l’ambiente predefinito del progetto.

- Richiede un valore

#### `--format`

Il formato di output: tabella, csv, tsv o normale

- Predefinito: `table`
- Richiede un valore

#### `--columns`, `-c`

Colonne da visualizzare. Colonne disponibili: comandi, nome, tipo. I caratteri % o * possono essere utilizzati come caratteri jolly. I valori possono essere divisi da virgole (ad esempio, &quot;a,b,c&quot;) e/o spazi vuoti.

- Predefinito: `[]`
- Richiede un valore

#### `--no-header`

Non generare l’intestazione della tabella

- Predefinito: `false`
- Non accetta un valore
