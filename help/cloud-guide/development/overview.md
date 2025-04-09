---
title: Panoramica sullo sviluppo
description: Preparati allo sviluppo locale con un progetto Adobe Systems Commerce on infrastruttura cloud.
role: Developer
feature: Cloud, Install
topic: Development
last-substantial-update: 2024-02-06T00:00:00Z
exl-id: 14fb0b41-1c3a-4abc-8726-cea16ab00ba8
source-git-commit: 1cea1cdebf3aba2a1b43f305a61ca6b55e3b9d08
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 0%

---

# Panoramica sullo sviluppo

Gli ambienti remoti dell&#39;infrastruttura cloud Adobe Commerce sono **di sola lettura**, inclusi tutti gli ambienti Starter e tutti gli ambienti di integrazione, staging e produzione Pro. In un ambiente di sviluppo locale, puoi scrivere e testare il codice prima di inviarlo a un ambiente di integrazione per ulteriori test e distribuirlo a Staging e Produzione.

Prima di preparare l&#39;area di lavoro locale, verificare di disporre delle [credenziali](../../get-started/prepare-workspace.md). Lo sviluppo locale richiede l&#39;installazione di PHP e Composer, a meno che non si decida di utilizzare [Cloud Docker per Commerce](#docker-environment).

## Pacchetti richiesti

Adobe Commerce su infrastruttura cloud utilizza Composer per gestire le dipendenze e gli aggiornamenti per i progetti. Per lo sviluppo locale, è necessario installare le versioni PHP e Composer compatibili con il progetto Cloud. Se ad esempio si utilizza il modello cloud [!DNL Commerce] 2.4.8, è possibile notare che il file di configurazione [`.magento.app.yaml`](https://github.com/magento/magento-cloud/blob/2.4.8/.magento.app.yaml) utilizza **PHP 8.4** e **Composer 2.8.4**.

Composer installa i librerie e le dipendenze richiesti per il `vendor` progetto nella directory. I seguenti file Composer richiesti si trovano nella directory principale del progetto:

- `composer.json`- Utilizzare il `composer.json` file per gestire le installazioni e gli aggiornamenti del prodotto.
- `composer.lock`- Il `composer.lock` file memorizza un insieme di dipendenze di versione esatte che soddisfano i vincoli di versione di ogni requisito per ogni pacchetto nell&#39;albero delle dipendenze del progetto.

**Comandi comuni:**

| Comando | Descrizione |
|--------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------|
| `composer update` | Aggiornamenti alle versioni più recenti delle dipendenze riportate nel file `composer.json`. Il file `composer.lock` verrà aggiornato. |
| `composer install` | Legge il file `composer.lock` per scaricare le dipendenze. È consigliabile mantenere una copia aggiornata di `composer.lock` nell&#39;archivio dei progetti. |

{style="table-layout:auto"}

Dopo aver aggiunto, confermato e inviato il codice aggiornato, il processo di distribuzione esegue automaticamente il comando `composer install` durante la [fase di compilazione](../deploy/process.md#build-phase-build-phase).

### Metapackage cloud

Adobe Systems Commerce su infrastruttura cloud utilizza un metapacchetto che richiede `magento/product-enterprise-edition`. Per ottenere gli aggiornamenti più recenti per l&#39;ultima versione di Commerce, utilizzare la seguente sintassi vincolo:

```text
>=current_version <next_version
```

Ad esempio, per utilizzare la versione più recente di Adobe Systems Commerce 2.4.9, impostata `2.4.8` come versione &quot;corrente&quot; e `2.4.9` come versione &quot;successiva&quot; nel `composer.json` file:

```text
"magento/magento-cloud-metapackage": ">=2.4.8 <2.4.9"
```

I pacchetti principali di questo metapacchetto sono i seguenti:

- **vendor/magento/ece-tools**: il `ece-tools` pacchetto è compatibile con Adobe Systems Commerce versione 2.1.4 e successive per fornire un set completo di funzionalità che è possibile utilizzare per gestire il Adobe Systems Commerce su infrastruttura cloud progetto. Contiene script e comandi di Adobe Commerce on cloud infrastructure progettati per facilitare la gestione del codice e la creazione e distribuzione automatica dei progetti. Vedere la panoramica del pacchetto [`ece-tools`](../dev-tools/package-overview.md).
- **vendor/magento/product-enterprise-edition**: questo metapackage richiede componenti dell&#39;applicazione, inclusi moduli, framework, temi e altro ancora.
- **vendor/fastly2/magento2**: questo modulo gestisce la rete CDN e i servizi Fastly per gli ambienti di staging e produzione Pro e di produzione Starter. Vedi [Servizi Fastly](/help/cloud-guide/cdn/fastly.md#fastly-cdn-module-for-magento-2).
- **vendor/magento/module-paypal-on-boarding**—Questo modulo fornisce il pagamento tramite checkout del gateway PayPal tramite la connessione al tuo conto PayPal. Consulta [Strumento di registrazione PayPal](../store/paypal.md).

>[!TIP]
>
>Per un elenco delle dipendenze e delle licenze di terze parti, consulta [Pacchetti cloud per Adobe Commerce](/help/cloud-guide/release-notes/cloud-packages.md) nelle _Note sulla versione di Commerce_.

## Ambiente Docker

È possibile utilizzare il strumento Docker Cloud per Commerce per emulare Adobe Systems Commerce in infrastruttura cloud ambienti di produzione e sviluppo per lo sviluppo locale. Cloud Docker for Commerce non richiede PHP e Composer da installare localmente.

- [Sviluppo locale con Cloud Docker](https://developer.adobe.com/commerce/cloud-tools/docker/setup/) nel sito Adobe Systems Developer
- [Architettura Docker e comandi comuni](../dev-tools/cloud-docker.md)
- [Note sulla versione di Cloud Docker](../release-notes/cloud-docker.md)

>[!TIP]
>
>Per informazioni sull&#39;utilizzo dei servizi di hosting basati su Git con Adobe Commerce sull&#39;infrastruttura cloud, consulta [Integrazioni](../integrations/overview.md).
