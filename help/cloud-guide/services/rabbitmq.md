---
title: Configurazione del servizio RabbitMQ
description: Scopri come abilitare il servizio RabbitMQ per gestire le code di messaggi per Adobe Commerce sull’infrastruttura cloud.
feature: Cloud, Services
exl-id: 64af1dfa-e3f0-4404-a352-659ca47c1121
source-git-commit: 2df119f1c09b92e45ae30544e5c2ee0e0d21834c
workflow-type: tm+mt
source-wordcount: '417'
ht-degree: 0%

---

# Configura il servizio [!DNL RabbitMQ]

[MQF](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/message-queues/message-queue-framework.html) è un sistema di Adobe Commerce che consente a un [modulo](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/glossary#module) di pubblicare messaggi nelle code. Definisce inoltre i consumatori che ricevono i messaggi in modo asincrono.

MQF utilizza [RabbitMQ](https://www.rabbitmq.com/) come broker di messaggistica, che fornisce una piattaforma scalabile per l&#39;invio e la ricezione di messaggi. Include inoltre un meccanismo per l’archiviazione dei messaggi non consegnati. [!DNL RabbitMQ] è basato sulla specifica AMQP 0.9.1.

>[!NOTE]
>
>Adobe Commerce su infrastruttura cloud supporta anche [ActiveMQ Artemis](activemq.md) come servizio di coda messaggi alternativo tramite il protocollo STOMP.

>[!IMPORTANT]
>
>Se preferisci utilizzare un servizio basato su AMQP esistente, come [!DNL RabbitMQ], invece di affidarti ad Adobe Commerce sull&#39;infrastruttura cloud per crearlo, utilizza la variabile di ambiente [`QUEUE_CONFIGURATION`](../environment/variables-deploy.md#queue_configuration) per connetterlo al tuo sito.

{{service-instruction}}

**Per abilitare RabbitMQ**:

1. Aggiungere il nome, il tipo e il valore del disco richiesti (in MB) al file `.magento/services.yaml` insieme alla versione di RabbitMQ installata.

   ```yaml
   rabbitmq:
       type: rabbitmq:<version>
       disk: 1024
   ```

1. Configurare le relazioni nel file `.magento.app.yaml`.

   ```yaml
   relationships:
       rabbitmq: "rabbitmq:rabbitmq"
   ```

1. Aggiungi, esegui il commit e invia le modifiche al codice.

   ```bash
   git add .magento/services.yaml .magento.app.yaml
   ```

   ```bash
   git commit -m "Enable RabbitMQ service"
   ```

   ```bash
   git push origin <branch-name>
   ```

1. [Verificare le relazioni del servizio](services-yaml.md#service-relationships).

{{service-change-tip}}

## Connessione a RabbitMQ per il debug

A scopo di debug, è utile connettersi direttamente a un’istanza del servizio in uno dei seguenti modi:

- Connettersi dall’ambiente di sviluppo locale
- Connettersi dall’applicazione
- Connessione dall&#39;applicazione PHP

### Connettersi dall’ambiente di sviluppo locale

1. Accedere a `magento-cloud` CLI e al progetto:

   ```bash
   magento-cloud login
   ```

1. Consulta l’ambiente con RabbitMQ installato e configurato.

   ```bash
   magento-cloud environment:checkout <environment-id>
   ```

1. Utilizza SSH per connettersi all’ambiente Cloud:

   ```bash
   magento-cloud ssh
   ```

1. Recupera i dettagli della connessione RabbitMQ e le credenziali di accesso dalla variabile [$MAGENTO_CLOUD_RELATIONSHIPS](../application/properties.md#relationships):

   ```bash
   echo $MAGENTO_CLOUD_RELATIONSHIPS | base64 -d | json_pp
   ```

   o

   ```bash
   php -r 'print_r(json_decode(base64_decode($_ENV["MAGENTO_CLOUD_RELATIONSHIPS"])));'
   ```

   Nella risposta, trova le informazioni RabbitMQ, ad esempio:

   ```json
   {
      "rabbitmq" : [
         {
            "password" : "guest",
            "ip" : "246.0.129.2",
            "scheme" : "amqp",
            "port" : 5672,
            "host" : "rabbitmq.internal",
            "username" : "guest"
         }
      ]
   }
   ```

1. Abilita l&#39;inoltro porta locale a RabbitMQ (se il progetto si trova in un&#39;area diversa, ad esempio l&#39;area US-3, EU-5 o AP-3, sostituire ``us-3``/``eu-5``/``ap-3`` con ``us``)

   ```bash
   ssh -L <port-number>:rabbitmq.internal:<port-number> <project-ID>-<branch-ID>@ssh.us.magentosite.cloud
   ```

   Un esempio per accedere all&#39;interfaccia Web di gestione RabbitMQ in `http://localhost:15672` è:

   ```bash
   ssh -L 15672:rabbitmq.internal:15672 <project-ID>-<branch-ID>@ssh.us.magentosite.cloud
   ```

1. Mentre la sessione è aperta, è possibile avviare un client RabbitMQ scelto dalla workstation locale, configurato per connettersi a `localhost:<portnumber>` utilizzando le informazioni relative al numero di porta, al nome utente e alla password della variabile MAGENTO_CLOUD_RELATIONSHIPS.

### Connettersi dall’applicazione

Per connettersi a RabbitMQ in esecuzione in un&#39;applicazione, installare un client, ad esempio [amqp-utils](https://github.com/dougbarth/amqp-utils), come dipendenza del progetto nel file `.magento.app.yaml`.

Ad esempio:

```yaml
dependencies:
    ruby:
        amqp-utils: "0.5.1"
```

Quando si accede al contenitore PHP, si immette qualsiasi comando `amqp-` disponibile per la gestione delle code.

### Connessione dall&#39;applicazione PHP

Per connettersi a RabbitMQ utilizzando l&#39;applicazione PHP, aggiungere una libreria PHP alla struttura di origine.
