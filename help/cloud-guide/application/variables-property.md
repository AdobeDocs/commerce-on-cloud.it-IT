---
title: Variables, proprietà
description: Utilizzare la proprietà variables per personalizzare le opzioni di configurazione dell'archivio per l'applicazione  [!DNL Commerce] .
feature: Cloud, Configuration
source-git-commit: 1e789247c12009908eabb6039d951acbdfcc9263
workflow-type: tm+mt
source-wordcount: '72'
ht-degree: 0%

---

# Variables, proprietà

È possibile utilizzare variabili di ambiente basate su applicazioni per personalizzare le configurazioni degli archivi. Queste variabili utilizzano una sintassi specifica. Vedi [Ignora impostazioni di configurazione](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/paths/override-config-settings.html) nella _Guida alla configurazione_.

Le seguenti variabili di ambiente incluse nel file `.magento.app.yaml` sono necessarie per versioni specifiche dell&#39;applicazione [!DNL Commerce].

Richiesto per Adobe Commerce da 2.2.x a 2.3.x:

```yaml
variables:
    env:
        CONFIG__DEFAULT__PAYPAL_ONBOARDING__MIDDLEMAN_DOMAIN: 'payment-broker.magento.com'
        CONFIG__STORES__DEFAULT__PAYMENT__BRAINTREE__CHANNEL: 'Magento_Enterprise_Cloud_BT'
        CONFIG__STORES__DEFAULT__PAYPAL__NOTATION_CODE: 'Magento_Enterprise_Cloud'
```

Per Adobe Commerce 2.4.x, imposta le seguenti variabili:

```yaml
variables:
    env:
        CONFIG__DEFAULT__PAYPAL_ONBOARDING__MIDDLEMAN_DOMAIN: 'payment-broker.magento.com'
        CONFIG__STORES__DEFAULT__PAYPAL__NOTATION_CODE: 'Magento_Enterprise_Cloud'
```
