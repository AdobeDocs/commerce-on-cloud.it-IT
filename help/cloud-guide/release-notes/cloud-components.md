---
title: Componenti cloud per Commerce
description: Consulta un elenco degli ultimi miglioramenti apportati al pacchetto Componenti cloud.
recommendations: noDisplay, catalog
exl-id: 34aec593-e2ea-4060-a6b9-6f4cb95a11c0
source-git-commit: 33f89e5c9af7c172ad0592b61343e285b456fc1a
workflow-type: tm+mt
source-wordcount: '618'
ht-degree: 0%

---

# Componenti cloud per Commerce

Il pacchetto [Componenti cloud](https://github.com/magento/magento-cloud-components) fornisce funzionalità Adobe Commerce di base estese per i siti distribuiti nell&#39;infrastruttura cloud. Questo pacchetto è una dipendenza per il pacchetto ECE-Strumenti. Queste note sulla versione descrivono gli ultimi miglioramenti apportati a questo pacchetto, che è un componente di [Cloud Tools Suite per Commerce](cloud-tools-suite.md).

Il pacchetto `magento/magento-cloud-components` utilizza la seguente sequenza di versioni: `<major>.<minor>.<patch>`

Le note sulla versione includono:

- ![nuova icona](../../assets/new.svg) Nuove funzioni
- ![icona correzione](../../assets/fix.svg) Correzioni e miglioramenti

<!--Add release notes below-->

## v1.1.1 {#latest}


Data di rilascio: 6 febbraio 2025

- ![nuova icona](../../assets/new.svg) **PHP 8.4**—Aggiunto supporto per PHP 8.4.<!-- MCLOUD-13148	 - -->
- ![icona di correzione](../../assets/fix.svg) **Correzione per il riscaldamento della cache**—È stato risolto un problema relativo agli URL delle categorie durante il riscaldamento della cache.<!-- MCLOUD-12454 - -->


## v1.1.0

Data di rilascio: 7 ottobre 2024

- ![icona correzione](../../assets/fix.svg) **Codice refactoring**—Rimosso il supporto delle versioni precedenti di PHP 7.4, 7.3, 7.2 e delle librerie correlate.<!-- MCLOUD-9278 - -->
- ![icona di correzione](../../assets/fix.svg) **Versione di Monolog aggiornata**—Aggiunto supporto per Monolog 3.6.<!-- MCLOUD-12855 - -->

## v1.0.14

Data di rilascio: 8 aprile 2024

- ![nuova icona](../../assets/new.svg) **PHP**—Aggiunto supporto per PHP 8.3.

## v1.0.13

Data di rilascio: 10 marzo 2023

- ![nuova icona](../../assets/new.svg) **Supporto avanzato per PHP 8.2**—Sono stati risolti alcuni problemi di compatibilità con alcune versioni di PHP 8.2.x per supportare Commerce 2.4.6.

## v1.0.12

Data di rilascio: 13 settembre 2022

- ![icona correzione](../../assets/fix.svg) **Errori durante il riscaldamento**—È stato risolto un problema che tentava di [riscaldamento](../environment/variables-post-deploy.md#warm_up_pages) quando la visibilità della pagina era impostata su [**Non visibile singolarmente**](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-attributes-product#simple-product-csv-file-structure) nell&#39;amministratore, causando `ERROR: Warming up failed: <link to page>` errori nel registro di distribuzione.<!-- MCLOUD-9134 -->

## v1.0.11

Data di rilascio: 4 agosto 2022

- ![icona correzione](../../assets/fix.svg) **Aggiunto supporto per la compatibilità con Symfony 5.4**—Correzioni per la compatibilità con Symfony 5.4.<!-- AC-3550 -->

## v1.0.10

Data di rilascio: 10 marzo 2022

- ![nuova icona](../../assets/new.svg) **Supporto PHP 8.1**—Aggiunta del supporto per PHP 8.1 e rimozione del supporto per PHP 7.1.

## v1.0.9

Data di rilascio: 25 ottobre 2021

- ![icona correzione](../../assets/fix.svg) **Aggiorna monologo**—È stata aggiornata la versione minima richiesta per il pacchetto `monolog` in `^2.3`.<!-- ACMP-1263 -->

## v1.0.8

Data di rilascio: 29 luglio 2021

- ![icona di correzione](../../assets/fix.svg) **Barre finali rimosse dagli URL generati automaticamente**. Le barre finali sono state rimosse dagli URL delle pagine delle categorie generati durante il riscaldamento della cache.<!--MCLOUD-7192-->

## v1.0.7

Data di rilascio: 9 settembre 2020

- ![nuova icona](../../assets/new.svg) **Miglioramenti alla registrazione**—Riduci le dimensioni del file `cache.log` per migliorare le prestazioni.<!--MCLOUD-6859-->

- ![icona correzione](../../assets/fix.svg) È stato corretto un errore di tipo nei valori di configurazione della cache che causava un errore nel comando CLI `php bin/magento cache:evict`.

## v1.0.6

Data di rilascio: 5 agosto 2020

- ![nuova icona](../../assets/new.svg) **Migliora le prestazioni di Redis**. È stato aggiunto il comando `./bin/magento cache:evict` per rimuovere le chiavi Redis scadute, che riduce l&#39;utilizzo della memoria Redis per migliorare le prestazioni.<!--MCLOUD-6023-->

- ![icona di correzione](../../assets/fix.svg) Supporto rimosso per *New Relic Logs in Context* per risolvere un problema di prestazioni.<!--MCLOUD-6422-->

## v1.0.5

Data di rilascio: 25 giugno 2020

- ![icona di correzione](../../assets/fix.svg) È stato risolto un problema introdotto nella versione 1.0.4 di magento/magento-cloud-components che causava il mancato funzionamento dell&#39;operazione di svuotamento della cache durante la fase di distribuzione, interrompendo il processo di distribuzione.

## v1.0.4

Data di rilascio: 25 giugno 2020

- ![nuova icona](../../assets/new.svg) **I registri New Relic implementati nel contesto**. I registri applicazioni generati da Adobe Commerce vengono ora visualizzati in tracce in New Relic per migliorare le funzionalità di risoluzione dei problemi.<!--MCLOUD-6029-->

- ![nuova icona](../../assets/new.svg) **Registrazione migliorata**—Aggiunta della registrazione per tenere traccia degli eventi di invalidazione e reindicizzazione completa della cache.<!--MCLOUD-6157-->

## v1.0.3

Data di rilascio: 27 febbraio 2020

- ![icona di correzione](../../assets/fix.svg) È stato risolto un problema di compatibilità per supportare le versioni di `ece-tools` 2002.0.x che utilizzano versioni PHP precedenti.

## v1.0.2

Data di rilascio: 6 febbraio 2020

- ![nuova icona](../../assets/new.svg) Ha esteso la funzionalità della variabile di ambiente `WARM_UP_PAGES` per supportare il precaricamento della cache per pagine di prodotto specifiche. Per una descrizione dettagliata della funzionalità, vedere l&#39;argomento [variabili post-distribuzione](../environment/variables-post-deploy.md#warm_up_pages).<!--MAGECLOUD-4444-->

- ![icona di correzione](../../assets/fix.svg) È stato risolto un problema che causava un errore dell&#39;hook post-distribuzione a causa di un URL archivio non valido quando si utilizzava la funzionalità `WARM_UP_PAGES` per popolare la cache. Questo problema si è verificato solo quando le riscritture URL sono state disabilitate.<!-- MAGECLOUD-4094 -->

## v1.0.1

Data di rilascio: 23 luglio 2019

- ![icona di correzione](../../assets/fix.svg) È stato risolto un problema che interessava la funzionalità [**WARM_UP_PAGES**](../environment/variables-post-deploy.md#warm_up_pages) che utilizza un URL di archivio predefinito. Ora, se il comando `config:show:default-url` non è in grado di recuperare un URL di base, viene utilizzato l&#39;URL dalla variabile MAGENTO_CLOUD_ROUTES.<!-- MAGECLOUD-3866 -->

## v1.0.0

Data di rilascio: 12 giugno 2019

Questa è la prima versione del pacchetto [`magento/magento-cloud-components`](https://github.com/magento/magento-cloud-components), che è una nuova dipendenza per il pacchetto `ece-tools` versione 2002.0.20 e successive.

- ![nuova icona](../../assets/new.svg) È stata aggiunta la possibilità di utilizzare i pattern regex per configurare la variabile di ambiente **WARM_UP_PAGES** in modo da memorizzare nella cache singole pagine, più domini e più pagine. Vedi [Variabili post-distribuzione](../environment/variables-post-deploy.md#warm_up_pages).<!--MAGECLOUD-3258-->
