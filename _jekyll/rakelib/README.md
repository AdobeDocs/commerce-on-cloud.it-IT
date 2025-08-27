---
source-git-commit: f75dbbc9726ff21a648b1bb3d8f06cb45a5d6b08
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%

---
# Crea file libreria

Questa directory contiene le definizioni delle attività di rake organizzate per funzionalità. Rake carica automaticamente tutti i file `.rake` in questa directory.

## Organizzazione file

### `adobe-docs-tasks.rake`

Contiene i requisiti comuni, le funzionalità condivise e le attività senza spazio dei nomi per le attività di rake dell’archivio della documentazione di Adobe Commerce su Experience League:

- `whatsnew` - Genera dati per riepilogo notizie (impostazione predefinita: dall&#39;ultimo aggiornamento)
- `render` - Rendering dei file con modelli e gestione include

### `includes.rake`

Contiene le attività di gestione di inclusione organizzate nello spazio dei nomi `:includes`:

- `includes:maintain_relationships` - Individuazione e gestione delle relazioni di inclusione nei file Markdown
- `includes:maintain_timestamps` - Aggiungi/aggiorna timestamp in base alle modifiche del file di inclusione
- `includes:maintain_all` - Esegui entrambe le operazioni in sequenza
- `includes:unused` - Trovare i file di inclusione inutilizzati

### `images.rake`

Contiene le attività di gestione delle immagini organizzate nello spazio dei nomi `:images`:

- `images:optimize` - Ottimizzazione delle immagini nei file non salvati modificati
- `images:unused` - Trova immagini inutilizzate nel progetto

## Come funziona

Rake individua e carica automaticamente tutti i file `.rake` nella directory `rakelib/`. Questo consente di:

1. **Organizza le attività per funzionalità** - Raggruppa le attività correlate
2. **Mantenere pulito il file di configurazione principale** - Concentrarsi sulle attività principali del progetto
3. **Aggiungi facilmente nuovi gruppi di attività** - Crea nuovi file `.rake`
4. **Mantieni separazione dei problemi** - Ogni file gestisce un dominio specifico

## Aggiunta di nuovi gruppi di attività

Per aggiungere un nuovo gruppo di attività correlate:

1. Crea un nuovo file `.rake` in questa directory
2. Utilizza uno spazio dei nomi descrittivo (ad esempio, `namespace :images` per le attività relative alle immagini)
3. Definisci le attività all’interno dello spazio dei nomi
4. Rake li carica automaticamente

## Esempio di struttura

```ruby
namespace :your_namespace do
  desc 'Description of what this task does'
  task :task_name do
    # Task implementation
  end
end
```

## Utilizzo

Le attività sono disponibili subito dopo la creazione:

```bash
rake your_namespace:task_name
```

## Vantaggi

- **Modularità**: ogni file si concentra su un&#39;area specifica
- **Manutenzione**: è più semplice trovare e modificare gruppi di attività specifici
- **Scalabilità**: è possibile aggiungere molti gruppi di attività senza riempire il file di configurazione principale
- **Sviluppo team**: sviluppatori diversi possono lavorare su gruppi di attività diversi
