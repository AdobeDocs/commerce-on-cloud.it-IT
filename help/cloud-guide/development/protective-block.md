---
title: Blocco protettivo
description: Scopri la funzione di blocco protettivo di Adobe Commerce sull’infrastruttura cloud e come funziona per proteggere il tuo sito da vulnerabilità di sicurezza note.
feature: Cloud, Configuration, Security
topic: Security
exl-id: 4a470e75-0b42-4ab7-b3dc-9f50b63bea14
TQID: https://experienceleague.adobe.com/E0lyCu6cFEaHR0KoauRFmQi9QThzoGDmNetnzYv3hVg
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: ba9e5be9-7de1-4f71-a5d2-baead0e425ee
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
source-git-commit: fd3ef8201c368f889344452e334976070a6c7157
workflow-type: tm+mt
source-wordcount: 311
ht-degree: 0%

---

# Blocco protettivo

Adobe Commerce sull’infrastruttura cloud dispone di una funzione di blocco protettiva che, in determinate circostanze, limita l’accesso ai siti web con vulnerabilità di sicurezza. Questo metodo di blocco parziale impedisce lo sfruttamento delle vulnerabilità di sicurezza note. Il software obsoleto spesso contiene exploit, quindi è importante proteggerlo da questi exploit bloccando parzialmente l&#39;accesso a questi siti.

## Come funziona il blocco protettivo

Adobe Commerce gestisce un database di firme di vulnerabilità di sicurezza note nel software open-source, comunemente implementate nell’infrastruttura cloud. Il controllo di sicurezza analizza solo le vulnerabilità note nei progetti open-source; non può esaminare le personalizzazioni scritte.

Esecuzione analisi sicurezza:

- Quando invii un nuovo codice a Git
- Quando vengono aggiunte nuove vulnerabilità al database

Se nell’applicazione viene rilevata una vulnerabilità critica, questa rifiuta il push Git.

Esistono due tipi di blocchi che vengono eseguiti:

1. **Blocco completo**—per siti Web di sviluppo. Il messaggio di errore che accompagna `git push` fornisce informazioni dettagliate sulla vulnerabilità.

1. **Blocco parziale**—per i siti Web di produzione, che consente al sito di rimanere principalmente online. A seconda della natura della vulnerabilità, parti di una richiesta, come una stringa di query, cookie o eventuali intestazioni aggiuntive, potrebbero essere rimosse dalle richieste GET. Tutte le altre richieste possono essere bloccate completamente, ad esempio l’accesso, l’invio di moduli o l’estrazione di prodotti.

Lo sblocco viene automatizzato dopo la risoluzione del rischio di sicurezza. Il blocco viene rimosso subito dopo l’applicazione di un aggiornamento della sicurezza che rimuove la vulnerabilità.

## Rinuncia al blocco di protezione

Il blocco protettivo serve a proteggerti da vulnerabilità note nel software che distribuisci Adobe Commerce sull’infrastruttura cloud.

Tuttavia, è possibile rinunciare al blocco di protezione aggiungendo quanto segue a [`.magento.app.yaml`](../application/configure-app-yaml.md):

```yaml
   preflight:
      enabled: false
```

Puoi rinunciare esplicitamente a un controllo specifico, ad esempio:

```yaml
   preflight:
      enabled: true
      ignore_rules: [ "drupal:SA-CORE-2014-005" ]
```
