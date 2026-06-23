---
title: Lavoratori
description: Scopri come configurare la proprietà worker nel file di configurazione dell'applicazione  [!DNL Commerce] .
feature: Cloud, Configuration
exl-id: 62d9dfaf-6265-4016-8d68-26362cf6a63a
TQID: https://experienceleague.adobe.com/sLfoGU5aolWVm6p-jHMC6VkF-DgNGdt7Wk40oALTj0o
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: d863fc70609dcc66d21eb95e709db80e29114714
workflow-type: tm+mt
source-wordcount: 357
ht-degree: 0%

---

# Proprietà Workers

È possibile definire un processo di lavoro da eseguire indipendentemente dall&#39;istanza Web senza un&#39;istanza Nginx in esecuzione. Tuttavia, il processo di lavoro utilizza la stessa archiviazione di rete utilizzata dall&#39;applicazione [!DNL Commerce]. Non è necessario configurare un server Web sull&#39;istanza di lavoro (utilizzando Node.js o Go) perché il router non può indirizzare le richieste pubbliche al worker. Questo rende l’istanza di lavoro ideale per le attività in background o in esecuzione continua che rischiano di bloccare una distribuzione.

## Configurare un lavoratore

I processi di lavoro sono disponibili per l&#39;utilizzo solo con gli ambienti di staging e produzione Pro. Gli ambienti di integrazione Pro e Starter possono scegliere di utilizzare la variabile [CRON_CONSUMER_RUNNER](../environment/variables-deploy.md#cron_consumers_runner).

Per configurare un lavoratore in Produzione o Staging, [Inviare un ticket di supporto Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) e includere le seguenti informazioni:

- ID Progetto
- ID ambiente
- Nome lavoratore
- Comandi Start

È possibile configurare un processo per ogni lavoratore. Una configurazione di lavoro di base e comune nel file `.magento.app.yaml` potrebbe essere simile alla seguente:

```yaml
workers:
    queue:
        commands:
            start: |
                php ./bin/magento queue:consumers:start commerce.eventing.event.publish
```

In questo esempio viene definito un singolo processo di lavoro denominato `queue`, con un livello di allocazione delle risorse ridotto (dimensione S) ed eseguito il comando `php ./bin/magento` all&#39;avvio. Il processo di lavoro `queue` viene quindi eseguito su ogni nodo come processo di lavoro. Se il comando viene chiuso, viene riavviato automaticamente.

## Comandi e sostituzioni

La chiave `commands.start` è necessaria per avviare i comandi con l&#39;applicazione di lavoro. Puoi utilizzare qualsiasi comando shell valido, anche se è ideale utilizzare la lingua dell’applicazione. Se il comando specificato dal tasto `start` termina, viene riavviato automaticamente.

>[!IMPORTANT]
>
>Gli hook di `deploy` e `post_deploy` e i comandi di `crons` vengono eseguiti solo sul contenitore Web, non nelle istanze di lavoro.

### Ereditarietà

Le definizioni per le proprietà `size`, `relationships`, `access`, `disk` e `mount` e `variables` vengono ereditate da un processo di lavoro, a meno che non vengano esplicitamente ignorate.

Le seguenti proprietà sono quelle più comunemente utilizzate per sostituire [le impostazioni di primo livello](properties.md):

- `size`: allocazione di un numero inferiore di risorse a un singolo processo in background
- `variables`: indica all&#39;applicazione di eseguire diversamente

### Tempistica e accodamento

Anche se ogni lavoratore si trova dietro un altro, la seguente configurazione produce una separazione coerente di due secondi tra i timestamp nel file `var/time.txt`, indipendentemente dalla sospensione di otto secondi all&#39;interno del codice PHP:

```yaml
workers:
    time1:
        commands:
            start: 'php -r "sleep(8); echo time() . PHP_EOL;" >> var/time.txt& sleep 2'
```

