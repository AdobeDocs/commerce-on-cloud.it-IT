---
title: Informazioni sull’app
description: Scopri come funziona Adobe Commerce Traffic Insights, come guidarlo con i filtri, come vengono misurati i dati, e le relative limitazioni e prestazioni.
feature: Cloud, Observability
role: Admin
source-git-commit: 09318645dd341a74d72237f4d4162d1d26d03651
workflow-type: tm+mt
source-wordcount: '949'
ht-degree: 0%

---

# Informazioni sull’app

L&#39;app [!DNL Adobe Commerce Traffic Insights] visualizza i registri di accesso CDN (Fastly Content Delivery Network) non elaborati in un&#39;immagine del traffico Edge di uno store. I grafici sono raggruppati nelle seguenti schede:

- **Larghezza di banda**: distribuzione nel tempo della larghezza di banda del traffico tra domini, tipi di contenuto e di risorse e progetti Cloud.
- **Prestazioni cache a pagina intera**: efficienza della memorizzazione nella cache delle pagine HTML di vetrina dinamiche per le pagine PDP (Product Detail Pages), PLP (Product Listing Pages) e CMS (Content Management System).
- **Analisi attività e richieste bot** — Traffico suddiviso per agenti bot noti, geolocalizzazione, IP/subnet, URL e segnali Fastly Next-Gen Web Application Firewall (WAF).

Una quarta scheda della **documentazione** in-app contiene note concettuali e il [playbook di investigazione](investigation-playbook.md).

## A chi serve questa guida?

- **Operatori del sito e SRE (Site Reliability Engineering)** che analizzano l&#39;overage della larghezza di banda CDN, i picchi di traffico o il carico dell&#39;origine.
- **Sviluppatori** ottimizzazione della copertura della Full Page Cache (FPC) e delle percentuali di hit o implementazione delle regole VCL (Fastly Varnish Configuration Language).
- **Amministratori e ingegneri della sicurezza** che identificano e attenuano i bot indesiderati, i raschiatori e il traffico automatizzato dannoso.

Si presume la familiarità con [!DNL Adobe Commerce on Cloud Infrastructure], i concetti Fastly CDN e la navigazione di base di New Relic.

## Come funziona

Seleziona un account e un intervallo di tempo dai controlli della piattaforma nella parte superiore della pagina. Un **ID progetto** facoltativo può restringere ulteriormente i grafici a specifici progetti Cloud. In un account principale o in una configurazione di partnership, la possibilità di visualizzare un account nel menu a discesa non significa che sia possibile eseguire una query. Se un grafico segnala un errore di autorizzazione, passa a un account a cui hai accesso New Relic Query Language (NRQL).

Continui ad applicare i filtri per trasformare una panoramica generale in un’indagine mirata. Fare clic su un valore in una colonna facet, ad esempio un bot, un IP, una subnet, un paese o un tipo di contenuto, per aggiungere un [filtro globale](https://docs.newrelic.com/docs/query-your-data/explore-query-data/dashboards/filter-new-relic-one-dashboards-facets/#example-use). I filtri attivi vengono visualizzati nella parte superiore della griglia e si applicano su ogni widget in ogni scheda contemporaneamente. Per ampliare l&#39;ambito, rimuovere un filtro.

**Procedura dettagliata** - Considera uno scenario in cui la *larghezza di banda totale* tende al di sopra della tolleranza del contratto e vuoi sapere chi la gestisce:

1. Apri la scheda **Analisi attività e richieste bot** e leggi **Struttura larghezza di banda** per vedere quanta parte del traffico è automatizzata rispetto a organica.
1. Se i bot sembrano avere più traffico, apri **Bot noti per larghezza di banda** e fai clic sul bot più pesante denominato, ad esempio un raschiatore. Questo aggiunge un nuovo filtro, il che significa che ora ogni widget ha un ambito in quel bot.
1. Leggi **Dettagli sull&#39;impatto dei bot noti** per la frequenza di richieste, la combinazione di stati e la frequenza di hit FPC.
1. Per vedere da dove proviene il bot, controlla **Larghezza di banda per paese**. Per vedere cosa sta recuperando il bot, consulta **URL per larghezza di banda**.
1. Se il traffico si concentra in una rete, fare clic su **Statistiche per subnet IP** per confermare che un attore ruota tra gli indirizzi in un singolo blocco.
1. Ora disponi di chi, cosa e dove necessario per scrivere una mitigazione mirata. Passare al playbook [Analisi](investigation-playbook.md) per informazioni su come procedere.

Lo stesso metodo di filtro funziona da qualsiasi facet iniziale: un paese sospetto, un singolo IP, un tipo di contenuto o un segmento di percorso URL.

## Come vengono misurati i dati

Comprendere alcune scelte di misurazione rende i numeri più facili da considerare attendibili e interpretare.

- **Larghezza di banda (BW)** indica il numero totale di byte serviti dalla rete CDN per le richieste corrispondenti, contando **sia le intestazioni di risposta che il corpo**. È la metrica del costo principale che viene conteggiata a fronte dell&#39;indennità di contratto.
- **Richieste (richieste)** è il numero di richieste distinte, tuttavia, con Fastly [shielding](https://www.fastly.com/documentation/guides/concepts/shielding/) abilitato, una singola richiesta viene registrata **due volte**, una volta per ciascuno dei seguenti elementi:
  - Scudo interno [Punto di presenza (POP)](https://www.fastly.com/documentation/guides/getting-started/concepts/using-fastlys-global-pop-network/)
  - EDGE POP
    Questo accade a meno che la risposta non provenga direttamente dalla cache POP locale o che lo scudo stesso funga da POP per la posizione del mittente. Per evitare il doppio conteggio di questi `HIT,MISS` e `MISS,MISS` casi, le query dell&#39;app si aggregano con [`uniqueCount`](https://docs.newrelic.com/docs/nrql/nrql-syntax-clauses-functions/#func-uniqueCount) nel campo `request_id`. Restituisce una **approssimazione** vicina con un margine di errore previsto di **~5%**, non un conteggio esatto.
- **I segmenti di rete CDN** sono compressi in modo diverso. La risposta recapitata al client è compressa, ma il traffico da shield a POP [non è compresso](https://www.fastly.com/documentation/guides/concepts/compression/#compression-at-the-edge) per mantenere il supporto di [Edge Side Includes (ESI)](https://www.fastly.com/documentation/reference/vcl/statements/esi/). Un basso rapporto di hit della cache aumenta quindi il segmento interno più di quello rivolto al client, poiché il contenuto non memorizzato nella cache deve essere ripetutamente trascinato attraverso lo schermo a dimensione piena e non compressa. Questa compressione spiega perché il widget Larghezza di banda del segmento di rete **CDN** e la proporzione di hit FPC sono due visualizzazioni dello stesso costo sottostante.

## Limitazioni dei dati e prestazioni

- **Conservazione per 30 giorni** - I registri CDN Fastly vengono conservati in New Relic per **30 giorni** in base al piano di abbonamento. Qualsiasi finestra scelta deve rientrare negli ultimi 30 giorni. Per la larghezza di banda **total** a lungo termine, utilizza l&#39;integrazione diretta Fastly nel pannello [!DNL Adobe Commerce admin], **Dashboard > Fastly > Bandwidth > Total**, ma considera che segnala per-service-ID, pertanto i dati devono essere raccolti per ambiente e aggregati per confrontare con la quota contrattuale.
- Limite di query di **60 secondi** - Il limite di esecuzione di [60 secondi di ogni tabella per NRQL](https://docs.newrelic.com/docs/nrql/using-nrql/rate-limits-nrql-queries/#query-duration). Per gli account con traffico molto elevato, si può verificare il timeout di un widget durante la scansione di troppi record di registro. In questo caso, ridurre l&#39;intervallo di tempo e ricaricare i grafici. Puoi espanderlo di nuovo per le schede più leggere.
