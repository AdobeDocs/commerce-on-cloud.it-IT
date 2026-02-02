---
source-git-commit: ee2ed3a78939af36572f0baa6672b2e9f9a2557f
workflow-type: tm+mt
source-wordcount: '417'
ht-degree: 0%

---
# Hook di pre-commit per l’ottimizzazione delle immagini

Questa directory contiene hook di pre-commit che ottimizzano automaticamente le immagini prima che vengano salvate nell’archivio.

## Funzionamento degli hook

- **Rileva automaticamente** file di immagine di staging (PNG, JPG, JPEG, GIF)
- **Esegui`image_optim`** per comprimere e ottimizzare le immagini
- **Riposiziona nell&#39;area intermedia le immagini ottimizzate** automaticamente
- **Assicurarsi che tutte le immagini salvate** siano ottimizzate correttamente

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
Optimizing: path/to/your/image.png
Re-staged optimized image: path/to/your/image.png
Image optimization complete!
```

## Linee guida per le immagini

- **PNG**: da utilizzare per le schermate e gli elementi dell&#39;interfaccia utente (verranno ottimizzati automaticamente)
- **JPEG**: utilizza per le foto (verrà ottimizzato automaticamente)
- **GIF**: utilizza per le animazioni (verrà ottimizzato automaticamente)
- **SVG**: da utilizzare per icone ed elementi grafici semplici (non elaborati da hook, commit così com&#39;è)

Gli hook di pre-commit ottimizzano automaticamente le immagini PNG, JPEG e GIF durante il commit.

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
- **SVG**: non elaborato (escluso dal rilevamento per mantenere grafica vettoriale e animazioni)

## Risoluzione dei problemi

### Hook non in esecuzione

- Verifica configurazione hook: `git config core.hooksPath`
- Verificare che il file hook sia eseguibile: `chmod +x .githooks/pre-commit`
- Verificare di essere nell&#39;archivio corretto con la directory `_jekyll`

### Errori di ottimizzazione

- Verificare che `bundle install` sia stato eseguito nella directory `_jekyll`
- Verifica che la Gem `adobe-comdox-exl-rake-tasks` sia installata (fornisce `image_optim`)
- Rivedi il file di configurazione `.image_optim.yml`

### Problemi relativi alle prestazioni

- Regola conteggio thread in `_jekyll/.image_optim.yml`
- Imposta variabile di ambiente `DEBUG=1` per informazioni dettagliate sull&#39;errore

## Come funziona

1. **Trigger pre-commit**: quando si esegue `git commit`, l&#39;hook viene eseguito automaticamente
2. **Rilevamento immagini**: analizza i file di staging per le estensioni di immagini
3. **Ottimizzazione**: esegue `image_optim` su ogni immagine pubblicata in staging
4. **Nuova gestione temporanea**: aggiunge automaticamente le immagini ottimizzate all&#39;area di gestione temporanea
5. **Il commit procede**: se l&#39;ottimizzazione viene eseguita correttamente, il commit continua normalmente

## Formati immagine supportati

- **PNG** (`.png`) - Compressione senza perdita di dati e perdita di dati
- **JPEG** (`.jpg`, `.jpeg`) - Compressione con perdita di dati con pulizia metadati
- **GIF** (`.gif`) - Animazione e ottimizzazione statica
- **SVG** (`.svg`) - Non elaborato dagli hook (conferma così com&#39;è per mantenere la qualità)

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
