---
title: Ottimizzare l’implementazione cloud
description: Scopri come ottimizzare il processo di implementazione di Adobe Commerce nei progetti di infrastruttura cloud, riducendo i tempi di inattività, l’implementazione di contenuti statici, l’implementazione basata su scenari e le procedure guidate intelligenti.
feature: Cloud, Deploy, SCD
exl-id: 4315e2f4-06af-4a5c-9db9-e7b2f63660df
TQID: https://experienceleague.adobe.com/bd9n9CFrpyn1UZG6SX8qkoZGBOFd2N7z9Hoa1hQ8rew
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
source-git-commit: fd3ef8201c368f889344452e334976070a6c7157
workflow-type: tm+mt
source-wordcount: 230
ht-degree: 0%

---

# Ottimizzare l’implementazione

Le prestazioni del sito possono risentire del processo di distribuzione. Il periodo di tempo in cui un sito è in modalità di manutenzione durante la distribuzione in un sito di produzione dipende da molti fattori, come la configurazione dell’ambiente e la quantità di contenuto contenuto in un sito. La prima best practice per l&#39;ottimizzazione della distribuzione cloud è [eseguire l&#39;aggiornamento per utilizzare `ece-tools`](../dev-tools/install-package.md) per usufruire delle funzionalità del pacchetto, ad esempio i comandi per creare un backup del database e verificare la configurazione dell&#39;ambiente.

I seguenti argomenti possono essere utili per comprendere meglio come ottimizzare il processo di distribuzione:

- [Processo di distribuzione cloud](process.md)
Il processo di implementazione di Cloud è suddiviso in tre fasi e puoi sfruttare a tuo vantaggio i punti di forza e i punti deboli di ogni fase.

- [Nessuna distribuzione di downtime](reduce-downtime.md)
Scopri cosa accade durante l’implementazione e come ridurre la quantità di tempi di inattività che si verificano durante l’aggiornamento all’ambiente di produzione.

- [Distribuzione di contenuto statico](static-content.md)
Il modo migliore per ottimizzare la distribuzione Cloud consiste nel controllare come e quando generare contenuti statici.

- [Creazioni guidate avanzate](smart-wizards.md)
Il pacchetto `ece-tools` fornisce i comandi della procedura guidata avanzata per valutare rapidamente la configurazione del progetto.

- [Tracciare le distribuzioni con New Relic](../monitor/track-deployments.md)
Utilizza il servizio New Relic per monitorare gli eventi di distribuzione e analizzare l’impatto della distribuzione sulle prestazioni complessive.
