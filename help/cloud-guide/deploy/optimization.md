---
title: Ottimizzare l’implementazione cloud
description: Scopri come ottimizzare il processo di implementazione di Adobe Commerce nei progetti di infrastruttura cloud, riducendo i tempi di inattività, l’implementazione di contenuti statici, l’implementazione basata su scenari e le procedure guidate intelligenti.
feature: Cloud, Deploy, SCD
source-git-commit: 1e789247c12009908eabb6039d951acbdfcc9263
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 0%

---

# Ottimizzare l’implementazione

Le prestazioni del sito possono risentire del processo di distribuzione. Il periodo di tempo in cui un sito è in modalità di manutenzione durante la distribuzione in un sito di produzione dipende da molti fattori, come la configurazione dell’ambiente e la quantità di contenuto contenuto in un sito. La prima best practice per l&#39;ottimizzazione della distribuzione cloud è [eseguire l&#39;aggiornamento per utilizzare `ece-tools`](../dev-tools/install-package.md) per usufruire delle funzionalità del pacchetto, ad esempio i comandi per creare un backup del database e verificare la configurazione dell&#39;ambiente.

I seguenti argomenti possono essere utili per comprendere meglio come ottimizzare il processo di distribuzione:

- [Processo di distribuzione cloud](process.md)
Il processo di implementazione di Cloud è suddiviso in tre fasi e puoi sfruttare a tuo vantaggio i punti di forza e i punti deboli di ogni fase.

- [Distribuzione senza tempi di inattività](reduce-downtime.md)
Scopri cosa accade durante l’implementazione e come ridurre la quantità di tempi di inattività che si verificano durante l’aggiornamento all’ambiente di produzione.

- [Distribuzione di contenuto statico](static-content.md)
Il modo migliore per ottimizzare la distribuzione Cloud consiste nel controllare come e quando generare contenuti statici.

- [Procedure guidate avanzate](smart-wizards.md)
Il pacchetto `ece-tools` fornisce i comandi della procedura guidata avanzata per valutare rapidamente la configurazione del progetto.

- [Tracciare le distribuzioni con New Relic](../monitor/track-deployments.md)
Utilizza il servizio New Relic per monitorare gli eventi di distribuzione e analizzare l’impatto della distribuzione sulle prestazioni complessive.
