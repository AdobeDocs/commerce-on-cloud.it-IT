---
title: Configura servizio ActiveMQ
description: Scopri come abilitare il servizio ActiveMQ Artemis per gestire le code di messaggi per Adobe Commerce sull’infrastruttura cloud.
feature: Cloud, Services
source-git-commit: ef22de6873b49f0fb9adfa9fc343a8d738a543e9
workflow-type: tm+mt
source-wordcount: '606'
ht-degree: 0%

---

# Configura il servizio [!DNL ActiveMQ]

[MQF](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/message-queues/message-queue-framework.html) è un sistema di Adobe Commerce che consente a un [modulo](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/glossary#module) di pubblicare messaggi nelle code. Definisce inoltre i consumatori che ricevono i messaggi in modo asincrono.

MQF può utilizzare [ActiveMQ Artemis](https://activemq.apache.org/components/artemis/) come gestore di messaggistica, che fornisce una piattaforma scalabile per l&#39;invio e la ricezione di messaggi. Include inoltre un meccanismo per l’archiviazione dei messaggi non consegnati. [!DNL ActiveMQ Artemis] supporta il protocollo STOMP (Streaming Text Oriented Messaging Protocol) per i messaggi.

[!DNL ActiveMQ Artemis] è disponibile come alternativa a RabbitMQ per la gestione delle code di messaggi. È particolarmente utile quando si necessita di funzionalità specifiche di ActiveMQ o si desidera utilizzare il protocollo STOMP.

>[!IMPORTANT]
>
>Se preferisci utilizzare un servizio di broker di messaggi esistente, come [!DNL ActiveMQ], invece di affidarti ad Adobe Commerce sull&#39;infrastruttura cloud per crearlo, utilizza la variabile di ambiente [`QUEUE_CONFIGURATION`](../environment/variables-deploy.md#queue_configuration) per connettersi al tuo sito.

{{service-instruction}}

**Per abilitare ActiveMQ Artemis**:

1. Aggiungere il nome, il tipo e il valore del disco richiesti (in MB) al file `.magento/services.yaml` insieme alla versione di ActiveMQ installata.

   ```yaml
   activemq-artemis:
       type: activemq-artemis:<version>
       disk: 1024
   ```

1. Configurare le relazioni nel file `.magento.app.yaml`.

   ```yaml
   relationships:
       activemq-artemis: "activemq-artemis:activemq-artemis"
   ```

1. Aggiungi, esegui il commit e invia le modifiche al codice.

   ```bash
   git add .magento/services.yaml .magento.app.yaml
   ```

   ```bash
   git commit -m "Enable ActiveMQ Artemis service"
   ```

   ```bash
   git push origin <branch-name>
   ```

1. [Verificare le relazioni del servizio](services-yaml.md#service-relationships).

{{service-change-tip}}

## Connetti ad ActiveMQ per il debug

A scopo di debug, è possibile connettersi direttamente a un’istanza del servizio in uno dei seguenti modi:

- Connettersi dall’ambiente di sviluppo locale
- Connettersi dall’applicazione
- Connessione dall&#39;applicazione PHP

### Connettersi dall’ambiente di sviluppo locale

1. Accedere a `magento-cloud` CLI e al progetto:

   ```bash
   magento-cloud login
   ```

1. Controllare l&#39;ambiente con ActiveMQ Artemis installato e configurato.

   ```bash
   magento-cloud environment:checkout <environment-id>
   ```

1. Utilizza SSH per connettersi all’ambiente Cloud:

   ```bash
   magento-cloud ssh
   ```

1. Recupera i dettagli della connessione ActiveMQ e le credenziali di accesso dalla variabile [$MAGENTO_CLOUD_RELATIONSHIPS](../application/properties.md#relationships):

   ```bash
   echo $MAGENTO_CLOUD_RELATIONSHIPS | base64 -d | json_pp
   ```

   o

   ```bash
   php -r 'print_r(json_decode(base64_decode($_ENV["MAGENTO_CLOUD_RELATIONSHIPS"])));'
   ```

   Nella risposta, trovare le informazioni di ActiveMQ. Il nome della relazione dipende dalla configurazione effettuata nel file `.magento.app.yaml`. Ad esempio, se hai utilizzato `activemq-artemis` come nome di relazione:

   ```json
   {
      "activemq-artemis" : [
         {
            "password" : "guest",
            "ip" : "246.0.129.2",
            "scheme" : "stomp",
            "port" : 61616,
            "host" : "activemq-artemis.internal",
            "username" : "guest"
         }
      ]
   }
   ```

1. Abilita l&#39;inoltro porta locale ad ActiveMQ (se il progetto si trova in un&#39;area diversa, ad esempio l&#39;area US-3, EU-5 o AP-3, sostituire ``us-3``/``eu-5``/``ap-3`` con ``us``)

   ```bash
   ssh -L <port-number>:activemq-artemis.internal:<port-number> <project-ID>-<branch-ID>@ssh.us.magentosite.cloud
   ```

   Un esempio per accedere alla console Web ActiveMQ Artemis in `http://localhost:8161` è:

   ```bash
   ssh -L 8161:activemq-artemis.internal:8161 <project-ID>-<branch-ID>@ssh.us.magentosite.cloud
   ```

   >[!NOTE]
   >
   >ActiveMQ Artemis utilizza la porta 61616 per la messaggistica STOMP e la porta 8161 per la console web.

1. Mentre la sessione è aperta, è possibile accedere alla console Web ActiveMQ Artemis all&#39;indirizzo `http://localhost:8161` utilizzando il nome utente e la password della variabile MAGENTO_CLOUD_RELATIONSHIPS.

### Connettersi dall’applicazione

Per connettersi ad ActiveMQ in esecuzione in un&#39;applicazione, installare una libreria client STOMP nell&#39;applicazione PHP.

### Connessione dall&#39;applicazione PHP

Per connettersi ad ActiveMQ utilizzando l&#39;applicazione PHP, aggiungere una libreria PHP STOMP alla struttura di origine. Adobe Commerce utilizza il protocollo STOMP per la comunicazione ActiveMQ e la configurazione viene impostata automaticamente durante la distribuzione quando ActiveMQ Artemis viene rilevato come servizio configurato.

## Supporto protocollo

ActiveMQ Artemis in Adobe Commerce su infrastrutture cloud utilizza il protocollo STOMP (Streaming Text Oriented Messaging Protocol):

- **STOMP**: protocollo di messaggistica utilizzato per le operazioni in coda (porta 61616)
- **Console web**: interfaccia di gestione accessibile tramite HTTP (porta 8161)

## Differenze rispetto a RabbitMQ

Sebbene sia [!DNL ActiveMQ Artemis] che [!DNL RabbitMQ] fungano da broker di messaggi per Adobe Commerce, esistono alcune differenze:

- **Protocollo**: ActiveMQ Artemis utilizza il protocollo STOMP, mentre RabbitMQ utilizza AMQP
- **Configurazione**: quando è configurato ActiveMQ Artemis, Adobe Commerce utilizza automaticamente il protocollo STOMP
- **Priorità**: se sono configurati sia ActiveMQ che RabbitMQ, ActiveMQ ha la precedenza per le operazioni basate su STOMP, mentre le operazioni AMQP utilizzano RabbitMQ
- **Console Web**: ActiveMQ fornisce una console di gestione basata sul Web per il monitoraggio di code e messaggi

## Configurazione coda

Quando ActiveMQ Artemis è configurato come servizio, Adobe Commerce configura automaticamente il sistema di coda per utilizzare il protocollo STOMP. La configurazione viene scritta nel file `app/etc/env.php` durante la distribuzione:

```php
'queue' => [
    'stomp' => [
        'host' => 'activemq-artemis.internal',
        'port' => '61616',
        'user' => 'guest',
        'password' => 'guest'
    ],
    'default_connection' => 'stomp'
]
```

Se necessario, è possibile eseguire l&#39;override di questa configurazione utilizzando la variabile di ambiente [`QUEUE_CONFIGURATION`](../environment/variables-deploy.md#queue_configuration).

