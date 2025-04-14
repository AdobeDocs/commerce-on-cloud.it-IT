---
title: Messaggi di errore per il pacchetto ECE-Tools
description: Visualizza un elenco di codici di errore e messaggi che possono verificarsi durante i processi di creazione, distribuzione e post-distribuzione dell’infrastruttura cloud di Adobe Commerce.
recommendations: noDisplay
role: Developer
exl-id: e240c268-b171-44e9-9fa4-f0e91b0d9899
source-git-commit: 350cfea06f036f0787b330e6e40c5af46a30f5ad
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%

---

# Messaggi di errore per gli strumenti ECE

Questo riferimento ai messaggi di errore fornisce informazioni per la risoluzione dei problemi che possono verificarsi durante i processi di creazione, distribuzione e post-distribuzione di Adobe Commerce su infrastrutture cloud.

Tutti i messaggi di errore critici e di avvertenza che si verificano durante la distribuzione vengono scritti sia nei file `var/log/cloud.log` che in quelli `/var/log/cloud.error.log`. Il file di registro degli errori del cloud contiene solo errori della distribuzione più recente. Un file vuoto indica una distribuzione riuscita senza errori.

Nel file `cloud.error.log`, ogni voce è formattata come stringa JSON per facilitarne l&#39;analisi:

```json
{"errorCode":1006,"stage":"build","step":"validate-config","suggestion":"No stores/website/locales found in config.php\n  To speed up the deploy process do the following:\n  1. Using SSH, log in to your Magento Cloud account\n  2. Run \"php ./vendor/bin/ece-tools config:dump\"\n  3. Using SCP, copy the app/etc/config.php file to your local repository\n  4. Add, commit, and push your changes to the app/etc/config.php file","title":"The configured state is not ideal","type":"warning"}
```

I messaggi di errore sono suddivisi in categorie in base a una delle fasi di distribuzione: compilazione, distribuzione e post-distribuzione. Ogni sezione fornisce un elenco degli errori associati con le seguenti informazioni per ogni errore:

- **Codice errore**: identificatore assegnato da Adobe Commerce per il messaggio di errore
- **Fase**: indica se l&#39;errore si è verificato durante la fase di compilazione, distribuzione o post-distribuzione
- **Passaggio**: indica il passaggio nello scenario di distribuzione che può restituire l&#39;errore. Se la colonna _Passaggio_ è vuota, si tratta di un errore generale che può essere restituito da più passaggi o durante le operazioni di pre-elaborazione. Per ulteriori informazioni sui passaggi di compilazione, distribuzione e post-distribuzione, vedere [Distribuzione basata su scenari](../deploy/scenario-based.md).
- **Suggerimento**: fornisce indicazioni per risolvere i problemi e risolvere l&#39;errore
- **Titolo (descrizione errore)**: descrizione che riepiloga la causa dell&#39;errore
- **Tipo**: indica se l&#39;errore è un errore critico o un avviso

{{$include /help/_includes/automated/ece-tools-error-codes.md}}
