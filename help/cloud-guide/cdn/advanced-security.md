---
title: Sicurezza avanzata di Adobe Commerce
description: Scopri in che modo la sicurezza avanzata aggiunge la gestione dei bot, la limitazione avanzata della velocità e la protezione DDoS di Livello 7 ad Adobe Commerce su infrastruttura cloud.
feature: Cloud, Configuration, Security
source-git-commit: 8a7c1c297092fdf2b75d22ce99c360c85eac0495
workflow-type: tm+mt
source-wordcount: '1986'
ht-degree: 0%

---

# [!DNL Adobe Commerce Advanced Security]

[!DNL Adobe Commerce Advanced Security] è un prodotto che funziona con [!DNL Adobe Commerce on Cloud Infrastructure] per mantenere il tuo negozio online veloce, disponibile e sicuro. In questo modo è possibile proteggere i ricavi, ridurre i tempi di inattività e mantenere la fiducia dei clienti durante i picchi di traffico e gli attacchi automatizzati.

[!DNL Adobe Commerce on Cloud Infrastructure] include la protezione integrata [Layer 3 e 4 DDoS](./fastly.md#ddos-protection) e un [Firewall applicazione Web (WAF)](./fastly-waf-service.md). Nel [modello di responsabilità condivisa](https://experienceleague.adobe.com/en/docs/commerce-operations/security-and-compliance/shared-responsibility), il rilevamento dei dati DDoS di Layer 7, la protezione dei bot e il blocco proattivo degli indirizzi IP sono responsabilità degli esercenti, che [!DNL Adobe Commerce Advanced Security] è progettato per gestire.

[!DNL Advanced Security] estende la protezione della vetrina attraverso funzionalità di sicurezza edge basate su Fastly, che offrono la gestione dei bot, la limitazione avanzata della velocità e la protezione DDoS Layer 7 come parte di una piattaforma edge unificata che combina scalabilità, prestazioni e sicurezza ai margini della rete.

>[!NOTE]
>
>[!DNL Advanced Security] è disponibile solo per [!DNL Adobe Commerce on Cloud Infrastructure] progetti PaaS.

## Funzionalità di base

[!DNL Adobe Commerce Advanced Security] include le seguenti protezioni aggiuntive:

- **[Gestione bot](https://docs.fastly.com/products/bot-management)**—Identifica e attenua le attività bot indesiderate nelle applicazioni web. Il servizio di gestione dei bot distingue tra bot legittimi (crawler di motori di ricerca, bot per social media) e quelli dannosi, fornendo una classificazione in tempo reale ai margini della rete con opzioni per bloccare, consentire, sfidare o limitare il traffico.

- **[Protezione DDoS](https://docs.fastly.com/products/fastly-ddos-protection)**: fornisce protezione DDoS di livello 7 (livello applicazione) oltre la protezione Layer 3 e 4 esistente inclusa in tutti i [!DNL Adobe Commerce on Cloud Infrastructure] progetti. Il servizio di protezione DDoS assorbe gli attacchi volumetrici su larga scala e garantisce la disponibilità continua delle applicazioni durante gli eventi Distributed Denial of Service (DDoS), proteggendo i ricavi durante i periodi di traffico di picco.

- **[Limitazione avanzata velocità](https://www.fastly.com/documentation/guides/next-gen-waf/rules/working-with-advanced-rate-limiting-rules/)**—Fornisce regole di limitazione della velocità configurabili che proteggono da abusi URL specifici, endpoint API e risorse dell&#39;applicazione. Il servizio Advanced Rate Limiting va oltre il [limite di velocità di base](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/RATE-LIMITING.md) disponibile tramite il modulo Fastly CDN per indirizzare specifici modelli di traffico e vettori di attacco, riducendo la tensione dell&#39;infrastruttura e i costi cloud.

>[!NOTE]
>
>[!DNL Advanced Security] configurazioni richiedono attualmente l&#39;invio di un ticket di supporto. La configurazione self-service tramite l’interfaccia di amministrazione è pianificata per una versione futura. Per ulteriori informazioni, consultare [Richiesta [!DNL Advanced Security]](#request-advanced-security).

## Copertura delle minacce

[!DNL Advanced Security] protegge le vetrine da una serie di minacce automatizzate e a livello di applicazione.

![Posizionamento di sicurezza avanzato nello stack di sicurezza di Adobe Commerce](../../assets/advanced-security.svg)

### Abuso basato su bot

- **Inserimento di credenziali** - Tentativi automatici di accesso utilizzando credenziali rubate da violazioni di dati.
- **Acquisizione dell&#39;account**: bot che tentano di ottenere l&#39;accesso non autorizzato agli account dei clienti.
- **Abuso nella creazione di account**: creazione automatica di account falsi a scopo di frode o abuso.
- **Test della carta**: bot che sottopongono a test i numeri di carta di credito rubati rispetto al processore pagamenti.
- **Raschiatura dei contenuti**: estrazione automatizzata dei dati di prodotto, dei prezzi o dei contenuti dalla vetrina.
- **Magazzino**—Bot che tengono i prodotti nei carrelli per evitare acquisti legittimi.

### Gestione dei bot basati su IA

- **Rilevamento crawler di IA**: identifica e gestisce i crawler di IA che eseguono il raschiamento del contenuto per addestrare modelli di linguaggio di grandi dimensioni senza consenso.
- **Controllo fetcher AI**—Controlla i fetcher AI utilizzati nei risultati in tempo reale delle Ricerche IA.
- **Criteri bot di IA configurabili**: distingue tra bot di IA verificati e sospetti con tipi di segnale configurabili per l&#39;applicazione dei criteri.

### Attacchi a livello di applicazione

- **Attacchi DDoS di livello 7**: attacchi distribuiti destinati al livello dell&#39;applicazione che ignorano le protezioni integrate di livello 3 e 4. [!DNL Advanced Security] assorbe questi attacchi volumetrici al perimetro prima che raggiungano i server di origine.
- **Abuso di URL e API** - Attacchi che hanno come target URL o endpoint API specifici distribuiti su un gran numero di indirizzi IP, in cui il blocco di singoli IP non è efficace.
- **Attacchi non compatibili con la cache** - Richieste con parametri di query manipolati progettati per ignorare il caching CDN e sopraffare il server di origine.

### Funzionalità aggiuntive

- **Sfide dinamiche**: assegna automaticamente la sfida ottimale al traffico sospetto. Sfrutta i Private Access Tokens (PAT) per convalidare facilmente una parte delle richieste senza influire sull’esperienza utente.
- **Tecnologia dell&#39;inganno** - Indirizza i tentativi di acquisizione dell&#39;account restituendo informazioni false agli aggressori, mitigando il loro attacco e interrompendo la loro capacità di operare su larga scala.

## Scelta della protezione giusta

Segui questa guida per determinare se [!DNL Advanced Security] è la soluzione giusta per le tue esigenze di protezione della vetrina o se le protezioni esistenti o le soluzioni alternative sono più appropriate.

### Quando utilizzare [!DNL Advanced Security]

Gli scenari seguenti sono più adatti con [!DNL Advanced Security]:

| Scenario | Come [!DNL Advanced Security] aiuta |
|---|---|
| Nel sito si verificano attacchi basati su bot, ad esempio l’inserimento di credenziali, lo scarto di contenuti o l’accumulo di inventario | La gestione dei bot identifica e attenua le minacce automatizzate ai margini prima che raggiungano l’applicazione |
| È necessaria la protezione Layer 7 DDoS oltre la copertura Layer 3 e 4 incorporata | La protezione DDoS assorbe gli attacchi a livello di applicazione che ignorano le protezioni a livello di rete |
| Gli URL o gli endpoint API specifici sono interessati da un traffico distribuito di volumi elevati che non può essere bloccato da IP | Advanced Rate Limiting fornisce controlli granulari per endpoint e pattern di traffico specifici |
| Desideri gestire i crawler di intelligenza artificiale e i recuperatori che accedono al contenuto della vetrina | La gestione dei bot include regole configurabili per il rilevamento e l’applicazione di bot basati sull’intelligenza artificiale |
| È necessaria una soluzione di sicurezza Edge supportata da Adobe integrata con la rete CDN Fastly esistente | [!DNL Advanced Security] viene eseguito sulla stessa piattaforma Fastly Edge che serve già la tua vetrina |

### Quando utilizzare le protezioni esistenti

Con le protezioni esistenti è meglio affrontare i seguenti scenari:

| Scenario | Approccio consigliato |
|---|---|
| Un singolo IP o un piccolo set di IP identificabili sta inondando il tuo sito di richieste | Blocca gli IP utilizzando l’API di amministrazione di Commerce o Fastly. Utilizza la protezione integrata [Layer 3/4 DDoS](./fastly.md#ddos-protection) e i frammenti di elenco Bloccati [IP esistenti](./fastly-vcl-blocking.md) VCL. |
| È necessario bloccare SQL injection, cross-site scripting (XSS) o altre minacce OWASP Top Ten | Il servizio [WAF](./fastly-waf-service.md) incluso blocca automaticamente queste minacce. |
| I pattern di attacco DDoS possono essere controllati con regole di blocco VCL di base | Usa i [snippet VCL personalizzati esistenti](./fastly-vcl-custom-snippets.md) già disponibili con Adobe Commerce. |

### Quando utilizzare protezioni alternative

I seguenti scenari sono meglio gestiti con protezioni alternative che possono integrare [!DNL Advanced Security]:

| Scenario | Approccio consigliato |
|---|---|
| È necessario un punteggio di frode a livello di transazione o la prevenzione delle frodi nei pagamenti | Utilizzare una piattaforma dedicata per la prevenzione delle frodi. [!DNL Advanced Security] protegge a livello di rete Edge e non valuta le singole transazioni di pagamento. |
| Hai bisogno di gestione delle identità e degli accessi (IAM) | Implementare una soluzione IAM dedicata. L’autenticazione degli utenti e la gestione delle sessioni rimangono responsabilità del cliente. |
| Sono necessari test di sicurezza delle applicazioni statici o dinamici (SAST/DAST) | Utilizzare strumenti di test dedicati per la sicurezza delle applicazioni. Non viene fornita l’analisi delle vulnerabilità a livello di codice. |
| Hai bisogno di una sicurezza API completa oltre il limite di frequenza (ad esempio convalida dello schema o funzioni gateway API) | Prendi in considerazione una piattaforma di sicurezza API dedicata. |
| Necessità di strumenti di conformità normativa, ad esempio scansione PCI o reporting SOC | Utilizzare strumenti dedicati per la gestione della conformità. |

>[!TIP]
>
>Se al momento si utilizza un provider di protezione bot di terze parti, il consolidamento in [!DNL Advanced Security] può ridurre la complessità operativa ed eliminare la copertura di sicurezza incoerente tra i provider. Contatta il team del tuo account Adobe per valutare [!DNL Advanced Security] per il tuo progetto.

## Posizionamento dello stack di sicurezza

[!DNL Advanced Security] si inserisce nell&#39;architettura di sicurezza Adobe Commerce più ampia come livello aggiuntivo di protezione basata su Edge. Funziona insieme e non sostituisce le protezioni DDoS di WAF e Layer 3/4 già incluse in [!DNL Adobe Commerce on Cloud Infrastructure]. Le sezioni seguenti spiegano in che modo si relazionano con le protezioni esistenti e le responsabilità che rimangono al cliente.

### Protezione inclusa

[!DNL Adobe Commerce on Cloud Infrastructure] include le seguenti funzionalità di sicurezza:

- **[Firewall applicazione Web (WAF)](./fastly-waf-service.md)**: protezione gestita contro SQL injection, Cross-Site Scripting (XSS) e altre dieci minacce principali di Open Web Application Security Project (OWASP). Disponibile solo negli ambienti di produzione.
- **[Protezione DDoS di livello 3 e 4](./fastly.md#ddos-protection)**: protezione incorporata contro attacchi a livello di rete, ad esempio attacchi SYN, inondazioni UDP, attacchi basati su ICMP e attacchi a livello di TCP. Abilitato automaticamente con Fastly CDN.
- **[Certificati SSL/TLS](./fastly-configuration.md#provision-ssltls-certificates)**: certificati di crittografia convalidati dal dominio per il traffico HTTPS sicuro.
- **[Mascheramento origine](./fastly.md#origin-cloaking)**: assicura tutte le route di traffico attraverso Fastly, bloccando l&#39;accesso diretto ai server di origine.
- **[Frammenti di sicurezza basati su VCL](./fastly-vcl-custom-snippets.md)**—Regole VCL (Custom Varnish Configuration Language) per il blocco IP, la inserire nell&#39;elenco Consentiti di e il filtro delle richieste.

### [!DNL Advanced Security]

[!DNL Advanced Security] fornisce una protezione maggiore rispetto alle protezioni incorporate incluse in [!DNL Adobe Commerce on Cloud Infrastructure], ma a un costo aggiuntivo:

- **Gestione bot**: rilevamento e mitigazione dei bot basati su Edge con gestione dei bot basati sull&#39;intelligenza artificiale.
- **Protezione DDoS di livello 7**: assorbimento e difesa DDoS di livello applicazione.
- **Advanced Rate Limiting**—Controlli della velocità granulare per gli URL e gli endpoint API.
- **Dynamic Challenges and Deception Technology**—Assegnazione automatizzata delle sfide e mitigazione dell&#39;acquisizione dell&#39;account.

### Responsabilità del cliente

- **Prevenzione delle frodi**: punteggio di frode a livello di transazione e rilevamento delle frodi nei pagamenti.
- **Gestione delle identità e degli accessi**: autenticazione del cliente, autorizzazione e gestione delle sessioni.
- **Test di sicurezza dell&#39;applicazione**: SAST/DAST e analisi delle vulnerabilità.
- **Configurazioni di sicurezza personalizzate**: regole basate su VCL, inserisce nell&#39;elenco Consentiti di IP e inserisce nell&#39;elenco Bloccati di.
- **Strumenti di conformità**: scansione PCI, reporting sulla conformità SOC e strumenti di controllo normativi.
- **Protezione avanzata a livello di applicazione**: autenticazione API basata su token, normalizzazione dei parametri di query e progettazione della strategia di caching.

Per una panoramica completa delle responsabilità di Adobe e della sicurezza del cliente, vedere il [modello di responsabilità condivisa](https://experienceleague.adobe.com/en/docs/commerce-operations/security-and-compliance/shared-responsibility).

## Modelli di attacco e protezioni comuni

La tabella seguente mappa i pattern di attacco comuni al livello di protezione appropriato all’interno dello stack di sicurezza di Adobe Commerce.

| Pattern di attacco | Tipo | Protezione |
|---|---|---|
| IP singolo o set di IP identificabili che inviano un numero elevato di richieste | DDoS + bot | Blocca gli IP tramite l’API di amministrazione di Commerce o Fastly. La protezione DDoS Layer 3/4 integrata filtra questo traffico ai margini della rete. |
| Gli attacchi a URL o API specifici si diffondono su un numero elevato di IP | DDoS + bot | **[!DNL Advanced Security]**: la limitazione avanzata della frequenza limita il volume di richieste per URL. Gestione bot identifica e blocca il traffico da bot distribuito. |
| Attacchi automatizzati sugli endpoint REST API senza autenticazione corretta | Bot + DDoS | Verifica che gli endpoint API utilizzino l’autenticazione basata su token. Ruota le credenziali se il token è compromesso. **[!DNL Advanced Security]**: la limitazione avanzata della frequenza può proteggere gli endpoint esposti. |
| Attacchi di busting della cache mediante parametri di query manipolati | Bot + DDoS | Escludi i parametri di query non essenziali dalle chiavi della cache. Normalizza e limita i parametri di query a livello di applicazione. **[!DNL Advanced Security]**: Gestione bot rileva e blocca il traffico automatizzato di busting della cache. |
| Tentativi SQL injection o cross-site scripting (XSS) | WAF | Il servizio [WAF](./fastly-waf-service.md) incluso blocca automaticamente queste minacce utilizzando le regole di sicurezza gestite. |

### Comportamento di blocco di WAF

Il seguente comportamento di WAF si applica a tutti i [!DNL Adobe Commerce on Cloud Infrastructure] progetti, indipendentemente dal fatto che [!DNL Advanced Security] sia abilitato o meno. Il servizio WAF incluso utilizza il seguente comportamento di blocco per i segnali di attacco comuni:

- **Le richieste SQL injection** vengono bloccate immediatamente, anche per una singola richiesta corrispondente.
- Le richieste identificate con i seguenti segnali di minaccia provenienti da un IP dannoso noto vengono bloccate immediatamente: Backdoor, Attack Tooling, CMDEXE, Log4J JNDI, Traversal e XSS.
- Le richieste provenienti da IP non dannosi che presentano i segnali di minaccia di cui sopra vengono bloccate quando superano le soglie seguenti:

| Interval | Soglia | Verifica la frequenza |
|---|---|---|
| 1 minuto | 50 richieste | Ogni 20 secondi |
| 10 minuti | 350 richieste | Ogni 3 minuti |
| 1 ora | 1.800 richieste | Ogni 20 minuti |

## Richiedi [!DNL Advanced Security]

Per richiedere [!DNL Advanced Security]:

>[!NOTE]
>
>[!DNL Advanced Security] è disponibile a un costo aggiuntivo e richiede un abbonamento attivo [!DNL Adobe Commerce on Cloud Infrastructure] (PaaS).

1. Contatta il team del tuo account Adobe o il rappresentante commerciale Adobe per discutere di [!DNL Advanced Security] per il tuo progetto.

1. Dopo aver acquistato [!DNL Advanced Security], [invia un ticket di supporto Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) richiedendo l&#39;abilitazione di [!DNL Advanced Security]. Includi l&#39;ID progetto [!DNL Adobe Commerce on Cloud Infrastructure] e gli ambienti che richiedono l&#39;abilitazione (ad esempio, Produzione e Staging).

1. Adobe attiva [!DNL Advanced Security] nel servizio Fastly e configura i criteri di protezione iniziali. L’abilitazione di solito viene completata entro pochi giorni lavorativi dall’invio del biglietto.

1. Si riceve la conferma che [!DNL Advanced Security] è attivo, insieme ai dettagli sulle protezioni abilitate per gli ambienti.

>[!NOTE]
>
>Le modifiche alla configurazione apportate a [!DNL Advanced Security] richiedono attualmente [l&#39;invio di un ticket di supporto](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket). La configurazione self-service tramite l’interfaccia di amministrazione è pianificata per una versione futura.

## Limitazioni

[!DNL Advanced Security] fornisce la protezione della vetrina edge-layer. Le seguenti funzionalità non sono disponibili e sono meglio gestite con soluzioni complementari:

- **Il punteggio di frode a livello di transazione**—[!DNL Advanced Security] non valuta le singole transazioni di pagamento per il rischio di frode. Utilizza una piattaforma dedicata di prevenzione delle frodi per il punteggio a livello di transazione.
- **Gestione degli accessi e delle identità (IAM)**—[!DNL Advanced Security] non gestisce l&#39;autenticazione utente, l&#39;autorizzazione o la gestione delle sessioni. Queste rimangono responsabilità del cliente.
- **Il test di sicurezza delle applicazioni statiche e dinamiche (SAST/DAST)**—[!DNL Advanced Security] non include il test di penetrazione o l&#39;analisi delle vulnerabilità a livello di codice.
- **Sicurezza API**: mentre la limitazione avanzata della velocità consente di proteggere gli endpoint API da abusi, non vengono fornite funzionalità di sicurezza API complete quali la convalida dello schema e la gestione del gateway API.
- **Prevenzione completa delle frodi**—[!DNL Advanced Security] si concentra sulla protezione della vetrina edge-layer e non è una piattaforma completa di gestione delle frodi.
- **Strumenti di conformità**—[!DNL Advanced Security] non fornisce funzionalità di analisi PCI, rapporti di conformità SOC o audit normativi.
