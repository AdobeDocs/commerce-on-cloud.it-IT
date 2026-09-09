---
title: Adobe Commerce Traffic Insights
description: Scopri lo strumento Adobe Commerce Traffic Insights e come può aiutarti a comprendere il traffico sul tuo progetto Adobe Commerce on Cloud Infrastructure.
feature: Cloud, Observability
role: Admin
source-git-commit: 119c9415abd22221e3ae785445d537f0609eba14
workflow-type: tm+mt
source-wordcount: '443'
ht-degree: 0%

---

# Approfondimenti traffico

Adobe Commerce Traffic Insights è un&#39;app New Relic One che visualizza il traffico CDN veloce di [!DNL Adobe Commerce on Cloud Infrastructure]. Legge le righe del log degli accessi Fastly CDN già inviate in New Relic come eventi `Log` ed esegue il rendering di un set curato di grafici, con ambito in un account New Relic selezionato e nell&#39;intervallo di tempo della piattaforma. Questo consente di visualizzare manualmente il traffico Edge di un negozio senza scrivere NRQL, il linguaggio di query di New Relic.

## Cosa ti aiuta a indagare

Traffic Insights è progettato per aiutarti a risolvere tre problemi comuni:

- **Superamento larghezza di banda CDN** — Traffico superiore all&#39;indennità di contratto. Attribuire il volume a supporti pesanti, file di grandi dimensioni, pagine 404 non memorizzabili nella cache o cache inefficiente, fino a un dominio, un tipo di contenuto, un URL o un progetto specifico.
- **Caricamento di bot e crawler di ricerca**: un motore di ricerca o un crawler di IA che genera una quota sproporzionata di richieste, compromettendo l&#39;efficienza della cache e il carico di origine. Scopri quali bot denominati sono più attivi ed esattamente cosa recuperano.
- **Script dannosi e raschiatori**: scarti, inserimento di credenziali, test delle carte, creazione di account falsi o abuso di livello 7. Riproduci i segnali Fastly Next-Gen di WAF e gli IP, le subnet e i paesi che generano traffico sospetto.

In ogni caso l&#39;app identifica *chi, cosa e dove* del traffico. Agendo su tali informazioni tramite le regole VCL Fastly, l&#39;ottimizzazione delle immagini, il tuning della cache, la limitazione della velocità o il componente aggiuntivo [Advanced Security](../../cdn/advanced-security.md) di Adobe nella configurazione di Commerce e Fastly. Il playbook [Investigazione](investigation-playbook.md) copre ciascuno di questi problemi.

## Accesso all’app

- **Collegamento diretto:** [Adobe Commerce Traffic Insights](https://one.newrelic.com/a9a0c3b8-3844-4ca1-8bad-c6742747be47).
- **Dalla schermata iniziale di New Relic One** (one.newrelic.com): una volta che l&#39;account è abbonato all&#39;app, viene visualizzato come riquadro, **Adobe Commerce Traffic Insights** nella home page.
- **Dalla barra di ricerca superiore (Ricerca rapida)** — cercare `Adobe Commerce Traffic Insights` e selezionarlo dai risultati.
- **Per fissarlo per un accesso più rapido** - usa il controllo a stella o a puntina sull&#39;intestazione della sezione o della pagina dell&#39;app per aggiungerlo ai preferiti o alla navigazione a sinistra. La posizione esatta del controllo dipende dalla versione dell&#39;interfaccia utente di New Relic in uso per l&#39;account.

## In questa guida

- **[Informazioni sull&#39;app](understanding-the-app.md)** - Informazioni su Traffic Insights, come guidarla con i filtri, come vengono misurati i numeri e cosa i dati possono e non possono dirti.
- **[Playbook di investigazione](investigation-playbook.md)** - Approcci consigliati ai tre problemi che l&#39;app è stata creata per risolvere: sovraccarico di larghezza di banda, carico di crawler e traffico dannoso. Ognuno di questi fa riferimento al grafico che lo conferma e specifica il percorso di escalation nativo [Advanced Security](../../cdn/advanced-security.md) di Adobe per i casi in cui la mitigazione manuale non è sufficiente.