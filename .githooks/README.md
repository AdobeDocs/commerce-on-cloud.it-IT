---
source-git-commit: 3d3df68ab5e1781974348190b30372c0b8169d1d
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 0%

---
# Hook di pre-commit per l’ottimizzazione delle immagini

Questa directory contiene hook di pre-commit che ottimizzano automaticamente le immagini prima che vengano salvate nell’archivio.

## Funzionamento degli hook

- **Rileva automaticamente** file di immagine di staging (`.png`, `.jpeg`, `.jpg`, `.gif`, `.svg`)
- **Eseguire`image_optim`** per comprimere e ottimizzare le immagini raster (`.png`, `.jpeg`, `.jpg`, `.gif`)
- **Riposiziona nell&#39;area intermedia le immagini ottimizzate** automaticamente
- **Assicurarsi che tutte le immagini raster vincolate** siano ottimizzate correttamente
- **Controlla i file SVG in staging** rispetto a un limite di dimensioni e interrompi il commit se da qualsiasi file in `help/` viene fatto riferimento a un SVG di dimensioni eccessive (altrimenti, solo avvertenza)

## Vantaggi

- Dimensioni ridotte dell’archivio
- Caricamenti di pagina più rapidi per la documentazione
- Qualità delle immagini coerente per tutti i collaboratori
- Non è richiesta alcuna ottimizzazione manuale

## Prerequisiti

- Rubino 3.0 o superiore
- Bundler
- Git

## Configurazione

### Configurazione automatica (scelta consigliata)

```bash
.githooks/setup-hooks.sh
```

### Impostazione manuale

```bash
git config core.hooksPath .githooks
chmod +x .githooks/*
```

### Completare la configurazione del progetto

1. Clona l’archivio:

   ```bash
   git clone <repository-url>
   cd commerce-admin.en
   ```

2. Abilita hook di pre-commit:

   ```bash
   .githooks/setup-hooks.sh
   ```

3. Installare le dipendenze di Jekyll:

   ```bash
   cd _jekyll
   bundle install
   ```

## Verifica degli hook

1. Aggiungere un file di immagine al repository
2. Posiziona nell&#39;area intermedia: `git add <image-file>`
3. Prova a eseguire il commit: `git commit -m 'test'`
4. L’hook deve ottimizzare automaticamente l’immagine

### Output previsto

```bash
Found 1 staged image(s). Running optimization...

Checking images ...
path/to/your/image.png    100.00%
Pre-commit image checks complete!
```

### Test di unità

La logica di rilevamento dei collegamenti SVG dell&#39;hook (che determina se da `help/` viene fatto riferimento a un SVG di dimensioni eccessive) è coperta da unit test che richiedono solo il bundle Ruby `minitest` — nessun gems o l&#39;installazione di `_jekyll`:

```bash
ruby .githooks/test/svg_link_checker_test.rb
```

## Linee guida per le immagini

- **PNG**: da utilizzare per le schermate e gli elementi dell&#39;interfaccia utente (verranno ottimizzati automaticamente)
- **JPEG**: utilizza per le foto (verrà ottimizzato automaticamente)
- **GIF**: utilizza per le animazioni (verrà ottimizzato automaticamente)
- **SVG**: utilizzare per icone e grafica semplice (non ottimizzata, ma verificata in base a un limite di dimensioni; il commit non riesce solo se il SVG di dimensioni eccessive è collegato da `help/`)

Gli hook di pre-commit ottimizzeranno automaticamente `.png`, `.jpeg`/`.jpg` e `.gif` immagini durante il commit e controlleranno gli SVG in staging rispetto a un limite di dimensioni (140 KB).

Se un SVG in staging supera il limite e viene utilizzato come riferimento da un file in `help/`, il commit viene interrotto. Se in `help/` non viene fatto riferimento al SVG di dimensioni eccessive, l&#39;hook stampa solo un avviso e il commit procede. Converti invece file SVG di grandi dimensioni in PNG:

```bash
cd _jekyll
bundle exec rake images:svg_to_png path=../help/assets/image.svg
```

Il percorso è relativo a `_jekyll`, pertanto alle immagini in `help/` viene fatto riferimento come `../help/...`.

## Ottimizzazione manuale

Per l&#39;ottimizzazione manuale dell&#39;immagine:

```bash
cd _jekyll
bundle exec rake images:optimize path=../path/to/images
```

## Configurazione

Gli hook utilizzano il file di configurazione `_jekyll/.image_optim.yml` per personalizzare le impostazioni di ottimizzazione:

- **PNG**: usa `advpng`, `optipng` e `pngquant`
- **JPEG**: usa `jhead`, `jpegoptim` e `jpegtran`
- **GIF**: Usa `gifsicle`
- **SVG**: non ottimizzato (escluso da `image_optim` per mantenere grafica vettoriale e animazioni), ma controllato rispetto a un limite di dimensioni di 140 KB

## Risoluzione dei problemi

### Hook non in esecuzione

- Verifica configurazione hook: `git config core.hooksPath`
- Verificare che il file hook sia eseguibile: `chmod +x .githooks/pre-commit`
- Verificare di essere nell&#39;archivio corretto con la directory `_jekyll`

### Errori di ottimizzazione

- Verificare che `bundle install` sia stato eseguito nella directory `_jekyll`
- Verifica che il gem `adobe-comdox-exl-rake-tasks` sia installato (fornisce le attività di rake `images:optimize`, `images:check_size` e `images:svg_to_png` eseguite dall&#39;hook)
- Rivedi il file di configurazione `.image_optim.yml`

### SVG supera il limite di dimensioni

- Il commit viene interrotto se un SVG posizionato nell&#39;area intermedia supera i 140 KB e vi si fa riferimento da un file in `help/` (in caso contrario, l&#39;hook avvisa solo e il commit procede)
- Converti SVG in PNG: `cd _jekyll && bundle exec rake images:svg_to_png path=../help/assets/image.svg` (il percorso è relativo a `_jekyll`, pertanto alle immagini in `help/` viene fatto riferimento come `../help/...`)
- Posiziona quindi il file PNG al posto di SVG e conferma nuovamente

### Problemi relativi alle prestazioni

- Regola conteggio thread in `_jekyll/.image_optim.yml`
- Imposta variabile di ambiente `DEBUG=1` per informazioni dettagliate sull&#39;errore

## Come funziona

1. **Trigger pre-commit**: quando si esegue `git commit`, l&#39;hook viene eseguito automaticamente
2. **Rilevamento immagini**: analizza i file di staging per le estensioni di immagini
3. **Ottimizzazione**: esegue `image_optim` su ogni PNG, JPEG o GIF gestito
4. **Nuova gestione temporanea**: aggiunge automaticamente le immagini ottimizzate all&#39;area di gestione temporanea
5. **Controllo dimensioni SVG**: verifica ogni SVG in staging rispetto al limite di dimensioni di 140 KB
6. **Processo di commit**: se l&#39;ottimizzazione ha esito positivo e da `help/` non viene fatto riferimento a un SVG di dimensioni eccessive, il commit continua normalmente; in caso contrario il commit viene interrotto (un SVG di dimensioni eccessive a cui non si fa riferimento da `help/` attiva solo un avviso)

## Formati immagine supportati

- **PNG** (`.png`) - Compressione senza perdita di dati e perdita di dati
- **JPEG** (`.jpg`, `.jpeg`) - Compressione con perdita di dati con pulizia metadati
- **GIF** (`.gif`) - Animazione e ottimizzazione statica
- **SVG** (`.svg`) - Non ottimizzato (commit così com&#39;è per mantenere la qualità), ma controllato rispetto a un limite di dimensione di 140 KB; il commit viene interrotto se il limite viene superato e viene fatto riferimento a SVG da `help/` (in caso contrario, l&#39;hook visualizza solo gli avvisi)

## Best practice

1. **Verifica l&#39;hook**: prova a eseguire prima il commit di una piccola immagine per assicurarti che funzioni
2. **Rivedi modifiche**: controlla le differenze Git per visualizzare i risultati dell&#39;ottimizzazione
3. **Monitoraggio delle prestazioni**: l&#39;ottimizzazione di immagini di grandi dimensioni potrebbe richiedere tempo
4. **Controllo versione**: gli hook sono archiviati in questa directory `.githooks/`

## Supporto

Per i problemi relativi agli hook di pre-commit:

1. Controlla l’output dell’hook per individuare messaggi di errore
2. Verifica che la configurazione di `image_optim` funzioni
3. Eseguire prima il test con le attività di rastremazione manuali
4. Rivedi i registri hook e la configurazione
5. Verificare la configurazione dell&#39;hook: `git config core.hooksPath`
