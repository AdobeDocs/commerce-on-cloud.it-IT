---
title: Variables, proprietà
description: Utilizzare la proprietà variables per personalizzare le opzioni di configurazione dell'archivio per l'applicazione  [!DNL Commerce] .
feature: Cloud, Configuration
exl-id: 9909d4a1-d9c8-492b-a5cc-cfbf17b5b7a8
TQID: https://experienceleague.adobe.com/bNdcqNxAAE1E1Qe2C-y1LWpFX-8Kzuwc9rJYEnbRz0U
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: d863fc70609dcc66d21eb95e709db80e29114714
workflow-type: tm+mt
source-wordcount: 85
ht-degree: 0%

---

# Variables, proprietà

È possibile utilizzare variabili di ambiente basate su applicazioni per personalizzare le configurazioni degli archivi. Queste variabili utilizzano una sintassi specifica. Vedi [Ignora impostazioni di configurazione](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/paths/override-config-settings.html?lang=it) nella _Guida alla configurazione_.

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

