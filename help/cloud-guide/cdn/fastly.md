---
title: Panoramica dei servizi Fastly
description: Scopri in che modo i servizi Fastly inclusi nell’infrastruttura cloud di Adobe Commerce consentono di ottimizzare e proteggere le operazioni di distribuzione dei contenuti per i siti Adobe Commerce.
feature: Cloud, Configuration, Iaas, Paas, Cache, Security, Services
exl-id: 429b6762-0b01-438b-a962-35376306895b
source-git-commit: 0300930577959631a2331997ebb104381136f240
workflow-type: tm+mt
source-wordcount: '1535'
ht-degree: 0%

---

# Panoramica dei servizi Fastly

>[!WARNING]
>
>Per mantenere la conformità PCI per i siti Adobe Commerce distribuiti sulla piattaforma Cloud, configura Fastly nel tuo ramo principale Starter, negli ambienti di produzione Pro e negli ambienti di staging Pro. Se utilizzi Adobe Commerce in una distribuzione headless, ti consigliamo vivamente di utilizzare Fastly per memorizzare nella cache le risposte GraphQL. Vedi [Memorizzazione in cache con Fastly](https://developer.adobe.com/commerce/webapi/graphql/usage/caching/#caching-with-fastly) nella *Guida per gli sviluppatori di GraphQL*.

Fastly fornisce i seguenti servizi per ottimizzare e proteggere le operazioni di distribuzione dei contenuti per i progetti Adobe Commerce su infrastrutture cloud. Questi servizi sono inclusi in Adobe Commerce sull’infrastruttura cloud senza costi aggiuntivi.

- **Content Delivery Network (CDN)**: servizio basato su vernice che memorizza nella cache pagine del sito, risorse, CSS e altro ancora nei centri dati back-end configurati. Quando i clienti accedono al sito e agli store, le richieste raggiungono Fastly per caricare più rapidamente le pagine memorizzate nella cache. Il servizio CDN offre le seguenti funzionalità:

- **Gestione della cache**: memorizza nella cache le pagine del sito, le risorse, i file CSS e altro ancora nei centri dati back-end configurati per ridurre il carico e i costi della larghezza di banda

   - Utilizza [Fastly snippet VCL personalizzati](fastly-vcl-custom-snippets.md) (conforme a Varnish 2.1) per modificare il modo in cui il caching risponde alle richieste

   - Configura il supporto del servizio [GeoIP](fastly-custom-cache-configuration.md#configure-geoip-handling)

   - [Forza richieste non crittografate su TLS](fastly-custom-cache-configuration.md#force-tls)

   - [Personalizza le impostazioni Fastly Timeout](fastly-custom-cache-configuration.md#extend-fastly-timeout) per evitare risposte 503 nelle richieste di operazioni in blocco

   - Crea [pagine di risposta di errore personalizzate](fastly-custom-response.md)

- **Sicurezza** - Dopo aver attivato i servizi Fastly per i siti Adobe Commerce, sono disponibili ulteriori funzionalità di sicurezza per proteggere i siti e la rete:

   - [Firewall applicazione Web](fastly-waf-service.md) (WAF): servizio firewall applicazione Web gestito che fornisce protezione conforme a PCI per bloccare il traffico dannoso prima che possa danneggiare l&#39;Adobe Commerce di produzione sui siti e sulla rete dell&#39;infrastruttura cloud. Il servizio WAF è disponibile solo negli ambienti di produzione Pro e Starter.

   - [Protezione Distributed Denial of Service (DDoS)](#ddos-protection): protezione DDoS incorporata contro attacchi di livello 3 e 4 comuni come Ping of Death, Smurf e altri attacchi di tipo flood basati su ICMP. La protezione incorporata non include la protezione contro gli attacchi Layer 7. Vedere [Protezione DDoS](#ddos-protection).

   - [Certificati SSL/TLS](fastly-configuration.md#provision-ssltls-certificates) - Il servizio Fastly richiede un certificato SSL/TLS per gestire il traffico protetto tramite HTTPS.

     Adobe Commerce fornisce un certificato SSL/TLS crittografato con convalida del dominio per ogni ambiente di staging e produzione. Adobe Commerce completa la convalida del dominio e il provisioning dei certificati durante il processo di configurazione Fastly.

- **Mascheramento origine**: funzionalità di sicurezza che garantisce tutti i flussi di traffico attraverso Fastly e blocca l&#39;accesso diretto ai server di origine. Consulta la sezione [Mascheramento origine](#origin-cloaking) di seguito.

- **[Ottimizzazione immagine](fastly-image-optimization.md)**: consente di scaricare il carico di elaborazione e ridimensionamento delle immagini sul servizio Fastly in modo da consentire ai server di elaborare gli ordini e le conversioni in modo più efficiente.

- **[Registri Fastly CDN e WAF](../monitor/new-relic-service.md#new-relic-log-management)**. Per i progetti Adobe Commerce su infrastrutture cloud Pro, puoi utilizzare il servizio Registri di New Relic per rivedere e analizzare i dati di registro Fastly CDN e WAF.

## Cloaking dell&#39;origine {#origin-cloaking}

Il cloaking dell’origine è una funzione di sicurezza che impedisce al traffico non Fastly di raggiungere l’origine Adobe Commerce sull’infrastruttura cloud. Tutte le richieste devono seguire questo percorso imposto:

**Fastly > Load Balancer > Istanze applicazione Adobe Commerce**

L’utilizzo di questo percorso garantisce che tutto il traffico venga ispezionato da Fastly Web Application Firewall (WAF) e dal WAF interno sul load balancer. Il cloaking dell&#39;origine protegge i siti dai tentativi di accesso diretto e riduce il rischio di attacchi DDoS.

### Stato abilitazione

Il cloaking dell’origine è stato completamente abilitato su tutti i progetti di infrastruttura cloud di Adobe Commerce dal 2021.\
I progetti con provisioning dopo il 2021 includono questa configurazione per impostazione predefinita.\
**Non è richiesta alcuna azione** per richiedere l&#39;abilitazione del cloaking dell&#39;origine.

#### Quale origine blocchi di cloaking

Il cloaking dell’origine blocca qualsiasi accesso diretto all’infrastruttura di origine, ad esempio:

```
mywebsite.com.c.abcdefghijkl.ent.magento.cloud
mcstaging2.mywebsite.com.c.abcdefghijkl.dev.ent.magento.cloud
mcstagingX.mywebsite.com.c.abcdefghijkl.X.dev.ent.magento.cloud
```

Le richieste tramite il dominio pubblico continuano a funzionare normalmente, incluso il traffico API REST. Esempi:

```
mywebsite.com/rest/default/V1/integration/admin/token
mywebsite.com/rest/default/V1/orders/
mywebsite.com/rest/default/V1/products/
mywebsite.com/rest/default/V1/inventory/source-items
```

#### Impatto sul comportamento del servizio

- **Gli indirizzi IP in uscita non cambiano.**
- **Le API REST non sono interessate.** Fastly non memorizza nella cache le chiamate API.
- **Le distribuzioni e i tempi di inattività non sono interessati.**
- Se un progetto ha più ambienti di gestione temporanea, il cloaking **origine si applica a tutti**.

## Modulo CDN Fastly per Magento 2

I servizi Fastly per Adobe Commerce sull&#39;infrastruttura cloud utilizzano il modulo CDN [Fastly per Magento 2] installato nei seguenti ambienti: Pro Staging and Production, Starter Production (`master` branch).

Al momento del provisioning iniziale o dell’aggiornamento del progetto Adobe Commerce, Adobe installa la versione più recente del modulo Fastly CDN negli ambienti di staging e produzione. Quando il modulo Fastly viene aggiornato, riceverai notifiche nell’Amministratore per i tuoi ambienti. Adobe consiglia di aggiornare gli ambienti per utilizzare la versione più recente. Vedi [Aggiorna Fastly](fastly-configuration.md#upgrade-the-fastly-module).

## Account servizio Fastly e credenziali

Adobe Commerce sui progetti di infrastruttura cloud non dispone di un account Fastly dedicato. Il servizio Fastly viene gestito in un account centralizzato registrato in Adobe e il dashboard di gestione è accessibile solo al team di supporto Cloud.

Al contrario, ogni ambiente di staging e produzione dispone di credenziali Fastly univoche (token API e ID servizio) per configurare e gestire i servizi Fastly dall’amministratore di Commerce. L’API Fastly è disponibile per eseguire la gestione avanzata del servizio Fastly, che richiederà le credenziali per inviare tali richieste.

Durante il provisioning del progetto, Adobe aggiunge il progetto all’account Fastly Service per Adobe Commerce sull’infrastruttura cloud e le credenziali Fastly alla configurazione per gli ambienti di staging e produzione. Vedi [Ottieni credenziali rapide](fastly-configuration.md#get-fastly-credentials).

### Modifica token API Fastly

Invia un ticket di supporto Adobe Commerce per rilasciare una nuova credenziale token API Fastly [se la convalida non riesce/è scaduta](https://experienceleague.adobe.com/it/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/error-when-validating-fastly-credentials) o se ritieni che sia stata compromessa.

Quando ricevi il nuovo token, aggiorna l’ambiente di staging o produzione per utilizzare il nuovo token.

**Per modificare le credenziali del token API Fastly**:

1. [Invia un ticket di supporto Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html?lang=it#submit-ticket) richiedendo nuove credenziali API Fastly.

   Includi l’ID del progetto Adobe Commerce su infrastruttura cloud e gli ambienti che richiedono una nuova credenziale.

1. Dopo aver ricevuto il nuovo token API, aggiorna il valore del token API nella [configurazione delle credenziali Fastly](fastly-configuration.md#test-the-fastly-credentials) nell&#39;amministratore o dalle [[!DNL Cloud Console] variabili di ambiente](../project/overview.md#configure-environment).

1. [Verifica le nuove credenziali](fastly-configuration.md#test-the-fastly-credentials).

1. Dopo aver aggiornato le credenziali, invia un ticket di supporto Adobe Commerce per eliminare il vecchio token API.

### Più account Fastly e domini assegnati

Fastly consente di assegnare un dominio APEX e i sottodomini associati a un unico servizio e account Fastly. Se disponi di un account Fastly che collega gli stessi domini e sottodomini APEX utilizzati per il sito Adobe Commerce, puoi scegliere tra le seguenti opzioni:

- Rimuovi il file APEX e i sottodomini dall’account esistente prima di richiedere le credenziali Fastly Service per gli ambienti di progetto dell’infrastruttura cloud di Adobe Commerce. Vedi [Utilizzo dei domini] nella documentazione Fastly.

  Utilizza questa opzione per collegare il dominio apex e tutti i sottodomini all’account Fastly service per Adobe Commerce sull’infrastruttura cloud.

- Invia un ticket di supporto Adobe Commerce per richiedere la delega del dominio in modo che apex e sottodomini possano essere collegati a account diversi.

  Utilizza questa opzione se disponi di un dominio apex con più sottodomini per siti Adobe Commerce e non Adobe Commerce e desideri collegare questi sottodomini a diversi account Fastly.

#### Richiedi delega dominio

*Scenario 1:*

Il dominio apex (`testweb.com` e `www.testweb.com`) è collegato a un account Fastly esistente. È presente un progetto Adobe Commerce su infrastruttura cloud configurato con i seguenti sottodomini: `mcstaging.testweb.com` e `mcprod.testweb.com`. Non spostare il dominio apex sull’account Fastly Service per Adobe Commerce sull’infrastruttura cloud.

Invia un [ticket di supporto Fastly] richiedendo che i sottodomini siano delegati dall&#39;account Fastly esistente all&#39;account Fastly per Adobe Commerce sull&#39;infrastruttura cloud. Includi l’ID del progetto Adobe Commerce nel ticket.

Una volta completata la delega, i sottodomini del progetto possono essere aggiunti all’account Fastly service per Adobe Commerce sull’infrastruttura cloud. Vedi [Ottieni credenziali rapide](fastly-configuration.md#get-fastly-credentials).

*Scenario 2:*

Il dominio apex (`testweb.com` e `www.testweb.com`) è collegato all&#39;account Adobe Commerce on cloud infrastructure Fastly Service. Si desidera gestire i servizi Fastly per i sottodomini `service.testweb.com` e `product-updates.testweb.com` da un account Fastly diverso.

Invia un ticket di supporto Adobe Commerce richiedendo che i sottodomini siano delegati dall’account Adobe Commerce on cloud infrastructure Fastly service all’account Fastly. Includi l’ID servizio per l’account Fastly nel ticket.

## Protezione DoS

La protezione DDOS è integrata nel servizio Fastly CDN. Una volta abilitati i servizi Fastly per i siti Adobe Commerce, Fastly filtra tutto il traffico web e quello dell’amministratore per rilevare e bloccare potenziali attacchi.

- Per gli attacchi che hanno come target il livello 3 o 4, il servizio Fastly filtra il traffico in base alla porta e al protocollo, esaminando solo le richieste HTTP o HTTPS. Gli attacchi ICMP, UDP e altri attacchi avviati dalla rete vengono ignorati all&#39;estremità della nostra rete. Ciò include attacchi di riflessione e amplificazione, che utilizzano servizi UDP come SSDP o NTP. Fornendo questo livello di protezione, blocchiamo efficacemente diversi attacchi comuni come il Ping of Death, gli attacchi Smurf e altre inondazioni basate su ICMP.

  Gestisce in modo rapido gli attacchi a livello TCP a livello di cache. Questa strategia fornisce la scala e il contesto necessari per ogni client per gestire un attacco di tipo SYN flood e le sue numerose varianti, tra cui stack TCP, attacchi di risorse e attacchi TLS all&#39;interno dei sistemi Fastly.

>[!NOTE]
>
>La protezione contro gli attacchi Layer 7 non è coperta dal servizio Fastly CDN integrato con Adobe Commerce. Per suggerimenti sulla protezione dagli attacchi di livello 7, vedere [Verifica degli attacchi DDoS](https://experienceleague.adobe.com/it/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/checking-for-ddos-attack-from-cli) e [Come bloccare gli attacchi dannosi](https://experienceleague.adobe.com/it/docs/commerce-knowledge-base/kb/how-to/block-malicious-traffic-for-magento-commerce-on-fastly-level) nella *Knowledge Base di Adobe Commerce*.

<!--Link definitions-->

[Caching with Fastly]: https://developer.adobe.com/commerce/webapi/graphql/usage/caching/#caching-with-fastly

[Checking for DDoS attacks]: https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/checking-for-ddos-attack-from-cli.html?lang=it

[Modulo CDN Fastly per Magento 2]: https://github.com/fastly/fastly-magento2

[Ticket di supporto rapido]: https://docs.fastly.com/products/support-description-and-sla#support-requests

[How to block malicious traffic]: https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/block-malicious-traffic-for-magento-commerce-on-fastly-level.html?lang=it

[Utilizzo dei domini]: https://docs.fastly.com/en/guides/working-with-domains
