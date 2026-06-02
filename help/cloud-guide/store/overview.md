---
title: Panoramica delle opzioni di archiviazione e della gestione della configurazione
description: Personalizza il tuo store Adobe Commerce sull’infrastruttura cloud.
feature: Cloud, Configuration, Services
exl-id: e653172f-7370-4761-b2ce-3a420b33b948
TQID: https://experienceleague.adobe.com/iseYcfjh61-4ArUf9rKBGKFVuOz1dbS1xVq-FYiCxsw
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: c1579802-ddd4-4214-8a91-97b2066abe11
source-git-commit: fd3ef8201c368f889344452e334976070a6c7157
workflow-type: tm+mt
source-wordcount: 193
ht-degree: 0%

---

# Panoramica delle opzioni di archiviazione e della gestione della configurazione

Esistono diversi modi per personalizzare lo store, ad esempio aggiungere un tema personalizzato, installare un’estensione o applicare una configurazione specifica negli ambienti dell’infrastruttura cloud. Puoi configurare le impostazioni per servizi specifici direttamente negli ambienti di staging e produzione. È possibile impostare più siti Web e store. La configurazione Store consente di configurare queste opzioni nella workstation locale e di implementare impostazioni specifiche in ambienti diversi.

Per accedere alla vetrina, utilizzare il comando `magento-cloud url` e rispondere alle richieste. Oppure puoi trovare l&#39;URL in [!DNL Cloud Console] in **Sito di accesso**.

## Configurare le opzioni store

Le opzioni del Negozio includono:

* [Modulo business-to-business (B2B)](b2b-module.md)
* [Temi personalizzati](custom-theme.md)
* [Estensioni](extensions.md)
* [Più siti](multiple-sites.md)
* [Servizi di pagamento](paypal.md)

## Configurare servizi e integrazioni

Sono presenti [file di configurazione](../environment/overview.md) specifici che gestiscono determinati comportamenti di distribuzione in ambienti remoti. È possibile esaminare questi argomenti separatamente:

* [Distribuzione dell’applicazione](../application/configure-app-yaml.md)
* [Azioni di build e implementazione dell’ambiente](../environment/configure-env-yaml.md)
* [Route richieste in ingresso](../routes/routes-yaml.md)
* [Servizi supportati](../services/services-yaml.md)

## Gestione della configurazione

Dopo aver configurato le opzioni di archiviazione, i servizi e le integrazioni, utilizza la gestione della configurazione per distribuire queste configurazioni in tutti gli ambienti in modo coerente e con tempi di inattività minimi. Consulta [Gestione configurazione](store-settings.md).
