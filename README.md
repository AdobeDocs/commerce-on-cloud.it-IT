---
source-git-commit: b151aac666510594751937e80dc3d9db4ede41b7
workflow-type: tm+mt
source-wordcount: '815'
ht-degree: 1%

---
# Adobe Commerce su infrastruttura cloud

Questo sito contiene la documentazione più recente per gli sviluppatori di Commerce on Cloud Infrastructure.

- [Guida di Commerce sull&#39;infrastruttura cloud](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/overview)
- [Introduzione a Commerce](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/start/overview) sull&#39;infrastruttura cloud

## Codice di condotta di Adobe Open Source

Questo progetto ha adottato il [Codice di condotta di Adobe Open Source](code-of-conduct.md). Per ulteriori informazioni, consulta l’articolo [Contribuzione](contributing.md).

## Informazioni sui contributi ai contenuti di Adobe

Consulta la [Guida per i collaboratori per la documentazione di Adobe](https://experienceleague.adobe.com/en/docs/contributor/contributor-guide/introduction).

Il modo in cui contribuisci dipende da chi sei e dal tipo di modifiche con cui desideri contribuire:

### Modifiche minori

Se stai apportando aggiornamenti minori, visita l&#39;articolo e fai clic sull&#39;area di feedback visualizzata in fondo all&#39;articolo, fai clic su **Opzioni di feedback dettagliate**, quindi fai clic su **Suggerisci una modifica** per passare al file Markdown di origine su GitHub. Utilizza l’interfaccia utente di GitHub per apportare modifiche.

Le correzioni minori o i chiarimenti inviati per la documentazione e gli esempi di codice in questo archivio sono coperti dalle condizioni d’uso di Adobe.

### Modifiche sostanziali o nuovi articoli da parte dei membri della community

Se fai parte della community Adobe e desideri creare un nuovo articolo o inviare modifiche importanti, utilizza la scheda Issues (Problemi) nell’archivio Git per inviare una segnalazione e avviare una conversazione con il team addetto alla documentazione. Dopo aver accettato un piano, dovrai collaborare con un dipendente per coordinare la pubblicazione dei nuovi contenuti attraverso una combinazione di interventi negli archivi pubblici e privati.

### Modifiche sostanziali da parte dei dipendenti Adobe

Se sei un autore tecnico, un responsabile di programma o uno sviluppatore del team di prodotto per una soluzione Adobe Experience Cloud ed è tuo compito creare o contribuire ad articoli tecnici, devi utilizzare l&#39;archivio privato all&#39;indirizzo `https://git.corp.adobe.com/AdobeDocs`.

## Strumenti e configurazione

I collaboratori della community possono utilizzare l’interfaccia utente di GitHub per apportare modifiche di base o eseguire il fork dell’archivio per apportare contributi principali.

Per informazioni dettagliate, consulta la [Guida per i collaboratori per la documentazione di Adobe](https://experienceleague.adobe.com/en/docs/contributor/contributor-guide/introduction).

## Come utilizzare markdown per formattare l’argomento

Tutti gli articoli in questo archivio utilizzano il markdown GitHub. Se non conosci Markdown, consulta:

- [Nozioni di base su Markdown](https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)
- [Foglio di riferimento per il markdown stampabile](https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)

## Modelli

Per alcuni argomenti, usiamo file di dati e modelli per generare contenuti pubblicati. I casi di utilizzo per questo approccio includono:

- Pubblicazione di grandi set di contenuti generati a livello di programmazione
- Un&#39;unica fonte di verità per i clienti su più sistemi che richiedono formati di file leggibili da un computer, come YAML, per l&#39;integrazione (ad esempio, strumenti CLI cloud, configurazioni di servizio)

Di seguito sono riportati alcuni esempi di contenuti basati su modelli:

- [Riferimento CLI cloud](help/templated/cloud-cli-ref.md)
- [Pacchetti cloud](help/templated/cloud-packages.md)
- [Riferimento utensili ECE](help/templated/ece-tools.md)
- [Estensioni PHP per cloud](help/templated/php-extensions-cloud.md)

### Generare contenuti basati su modelli

In generale, la maggior parte degli autori deve solo aggiungere una versione alle tabelle dei requisiti di sistema e di disponibilità del prodotto. La manutenzione per tutti gli altri contenuti basati su modelli è automatizzata o gestita da un membro del team dedicato. Queste istruzioni sono destinate alla maggior parte degli autori.

>**NOTA:**
>
>- La generazione di contenuti basati su modelli richiede l’utilizzo della riga di comando in un terminale.
>- Per eseguire lo script di rendering, è necessario che Ruby sia installato. Vedere [_jekyll/.ruby-version] (_jekyll/.ruby-version) per la versione richiesta.

Per una descrizione della struttura di file per il contenuto con modelli, consulta:

- `_jekyll` - Contiene gli argomenti con modelli e le risorse richieste
- `_jekyll/_data` - Contiene i formati di file leggibili dal computer utilizzati per il rendering dei modelli
- `_jekyll/templated` - Contiene file modello basati su HTML che utilizzano il linguaggio di modelli Liquid
- `help/_includes/templated` - Contiene l&#39;output generato per il contenuto con modelli nel formato di file `.md` in modo che possa essere pubblicato negli argomenti di Experience League. Lo script di rendering scrive automaticamente l&#39;output generato in questa directory

Per aggiornare il contenuto basato su modelli:

1. Nell&#39;editor di testo aprire un file di dati nella directory `_jekyll/_data`. Ad esempio:

   - [Riferimento CLI cloud](help/templated/cloud-cli-ref.md): `_jekyll/_data/cloud-cli-ref.yaml`
   - [Pacchetti cloud](help/templated/cloud-packages.md): `_jekyll/_data/cloud-packages.yaml`
   - [Riferimento strumenti ECE](help/templated/ece-tools.md): `_jekyll/_data/ece-tools.yaml`

2. Utilizzare la struttura YAML esistente per creare le voci.

3. Passare alla directory `_jekyll`.

   ```bash
   cd _jekyll
   ```

4. Genera contenuti con modelli e scrive l&#39;output nella directory `help/_includes/templated`.

   ```bash
   bundle exec rake render
   ```

   >**NOTA:** è necessario eseguire lo script dalla directory `_jekyll`. Se questa è la prima volta che esegui lo script, devi prima installare le dipendenze Ruby con il comando `bundle install`. Le attività di rastremazione vengono fornite dal gem `adobe-comdox-exl-rake-tasks` per una migliore manutenzione negli archivi della documentazione di Adobe Commerce.

5. Tornare alla directory `root`.

   ```bash
   cd ..
   ```

6. Verificare che i `help/_includes/templated` file previsti siano stati modificati.

   ```bash
   git status
   ```

   Dovresti visualizzare un output simile al seguente:

   ```bash
   modified:   _data/cloud-cli-ref.yaml
   modified:   help/_includes/templated/cloud-cli-ref.md
   ```

7. Invio delle modifiche.

   ```bash
   git add .
   git commit -m "descriptive message of the intended commit"
   git push
   ```

Per ulteriori informazioni su [File di dati](https://jekyllrb.com/docs/datafiles), [Filtri liquidi](https://jekyllrb.com/docs/liquid/filters/) e altre funzionalità, vedere la documentazione di Jekyll.

## Attività di rastremazione disponibili

Questo archivio utilizza le attività di rastremazione fornite dal gem `adobe-comdox-exl-rake-tasks`. Per visualizzare tutte le attività disponibili, eseguire le operazioni seguenti:

```bash
cd _jekyll
bundle exec rake --tasks
```

## Hook di pre-commit per l’ottimizzazione delle immagini

Questo archivio include hook di pre-commit automatizzati che ottimizzano le immagini prima del commit. **Tutti i collaboratori devono abilitare questi hook** per garantire un&#39;ottimizzazione delle immagini coerente e dimensioni ridotte dell&#39;archivio.

### Configurazione rapida

Dopo aver clonato l’archivio, esegui:

```bash
.githooks/setup-hooks.sh
```

### Funzionamento degli hook

- Rileva automaticamente i file immagine di staging (PNG, JPG, JPEG, GIF, SVG)
- Esegui `image_optim` per comprimere e ottimizzare le immagini
- Riposiziona automaticamente nell&#39;area intermedia le immagini ottimizzate
- Assicurati che tutte le immagini salvate siano ottimizzate correttamente

### Vantaggi

- Dimensioni ridotte dell’archivio
- Caricamenti di pagina più rapidi per la documentazione
- Qualità delle immagini coerente per tutti i collaboratori
- Non è richiesta alcuna ottimizzazione manuale

Per istruzioni dettagliate sulla configurazione, la risoluzione dei problemi e la configurazione, vedere [`.githooks/README.md`](.githooks/README.md).
