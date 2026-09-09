---
title: Playbook investigativo
description: Scopri come analizzare il sovraccarico di larghezza di banda della rete CDN, cercare bot e carico di crawler, e il traffico dannoso utilizzando Adobe Commerce Traffic Insights e quando aumentare la gravità della situazione.
feature: Cloud, Observability
role: Admin
source-git-commit: 09318645dd341a74d72237f4d4162d1d26d03651
workflow-type: tm+mt
source-wordcount: '1774'
ht-degree: 0%

---

# Playbook di investigazione

L&#39;app [!DNL Adobe Commerce Traffic Insights] è progettata per consentire di analizzare i seguenti problemi:

- Larghezza di banda eccedente
- Carico crawler
- Traffico dannoso

In alternativa, puoi richiedere [Sicurezza avanzata: gestione dei bot nativi, limitazione dei valori DDoS e dei tassi di livello 7](#advanced-security-native-bot-management-layer-7-ddos--rate-limiting), percorso di escalation nativo di Adobe quando la mitigazione manuale non è sufficiente. Ogni passaggio fa riferimento al widget che mette in evidenza il sintomo, in modo da poter passare da una metrica a un’azione concreta.

>[!WARNING]
>
>I suggerimenti riportati in questa pagina sono solo linee guida. Convalida sempre eventuali regole di blocco in base al traffico prima di distribuirle.

## Superamento larghezza di banda CDN

Prima di considerare le interruzioni della larghezza di banda, è necessario comprendere come viene fatturata la larghezza di banda. Il traffico per **tutti** i servizi Fastly inclusi nell&#39;account [!DNL Adobe Commerce on Cloud Infrastructure], inclusi tutti gli ambienti di staging **e** di produzione, viene conteggiato per l&#39;utilizzo comune rispetto alla quota annuale nel contratto. Iniziare da **Larghezza di banda > Larghezza di banda totale**, quindi attribuire il volume con **Larghezza di banda per tipo di contenuto** e **Larghezza di banda per dettagli dominio**.

### Contenuto multimediale

Alcuni negozi forniscono legittimamente una grande parte della larghezza di banda come media a causa del loro catalogo. Se **La larghezza di banda per tipo di contenuto** mostra una quantità significativa di larghezza di banda dei contenuti multimediali, considera le seguenti attenuazioni:

- Prova con [conversione con perdita di dati](https://experienceleague.adobe.com/it/docs/commerce-on-cloud/user-guide/cdn/fastly-image-optimization#force-lossy-conversion) per distribuire immagini più piccole e di qualità inferiore.
- Indaga su [Fastly Deep Image Optimization](https://experienceleague.adobe.com/it/docs/commerce-on-cloud/user-guide/cdn/fastly-image-optimization#deep-image-optimization) per generare immagini ridimensionate sul lato Content Delivery Network (CDN).

### File di grandi dimensioni

Alcuni siti contengono file di grandi dimensioni o risposte specifiche e pesanti, ad esempio integrazioni o esportazioni di Enterprise Resource Planning (ERP). Utilizza **URL per larghezza di banda** per esaminare le colonne **BW** e **Dimensione media** per trovare questi file di grandi dimensioni. È possibile utilizzare **Segmento di percorso lvl 1 per larghezza di banda** per una visualizzazione di livello superiore.

### 404 s pesanti

Una pagina di Adobe Commerce **404 non trovata** è in genere una pagina pesante in stile tema (~1,5 MB) e **non memorizzabile in cache**, pertanto la ripetizione di 404 pagine può generare traffico anomalo. Anche una risorsa minima mancante come `favicon.ico` può trasformarsi in una pagina `404` pesante invece di un file piccolo. Utilizza le colonne **404** e **404 BW** in **Larghezza di banda per dettagli dominio**, **URL per larghezza di banda**, **IP principali per larghezza di banda** e **Statistiche per subnet IP** per trovare client, IP e URL che generano in modo coerente il volume 404. Quindi riduci o limita tale accesso, ad esempio, restituisci invece un `403` leggero.

### Basso rapporto di hit FPC

[!DNL Adobe] consiglia di abilitare Fastly [shielding](https://www.fastly.com/documentation/guides/concepts/shielding/) in modo che un aggregatore di cache CDN principale serva l&#39;origine, consentendo a un numero inferiore di richieste di raggiungerla dai punti di presenza locali ([POPs](https://www.fastly.com/documentation/guides/getting-started/concepts/using-fastlys-global-pop-network/)) più vicini al client. Consulta [verifica della configurazione](https://experienceleague.adobe.com/it/docs/commerce-on-cloud/user-guide/cdn/setup-fastly/fastly-custom-cache-configuration#configure-back-ends-and-origin-shielding).

Il traffico POP-to-client e shield-to-POP vengono conteggiati separatamente e, mentre la risposta del client è compressa, il traffico da shield-to-POP [&#x200B; non viene compresso](https://www.fastly.com/documentation/guides/concepts/compression/#compression-at-the-edge) per mantenere il supporto di Edge Side Includes ([ESI](https://www.fastly.com/documentation/reference/vcl/statements/esi/)). Ciò significa che un basso rapporto di hit della Full Page Cache (FPC) porta a una larghezza di banda molto più elevata sulle pagine dinamiche. Confermare il sintomo con **Proporzione di hit FPC**, **Statistiche FPC per dominio** e **Larghezza di banda del segmento di rete CDN**.

Una bassa percentuale di hit è spesso determinata da un grande volume di crawler di motori di ricerca (vedi [Bot e crawler di ricerca](#search-bots-and-crawlers)). Un&#39;altra mitigazione è quella di [distribuire una cache non aggiornata ai crawler](https://www.fastly.com/documentation/reference/vcl/variables/cache-object/stale-exists/) quando disponibile. Se la causa è un&#39;invalidazione ampia e frequente della cache, utilizza **Invalidazione cache per tag** e **Invalidazione FPC per URL principali** per trovare i tag/URL abbandonati.

## Cerca bot e crawler

Per misurare l&#39;impatto sul crawler, inizia tra **Bot noti per larghezza di banda** e **Bot noti per dettagli sull&#39;impatto** per vedere quali bot sono più attivi, quindi [filtra](https://docs.newrelic.com/docs/query-your-data/explore-query-data/dashboards/filter-new-relic-one-dashboards-facets/#example-use) per un bot specifico per studiare solo le sue richieste.

### Troppe richieste

La causa più comune di un bot di ricerca che invia troppe richieste si verifica durante l&#39;analisi delle pagine che contengono `<meta name="robots" content="index,follow">`. I bot possono seguire i collegamenti di navigazione superiori e su più livelli in un ciclo quasi infinito. Per risolvere il problema, considera le seguenti opzioni:

>[!WARNING]
>
> Consulta un esperto di ottimizzazione SEO (Search Engine Optimization) prima di limitare l’attività del crawler. La riqualificazione può influire negativamente sulla SEO.

- Aggiungi `nofollow` ai collegamenti di navigazione superiore e a livello, ad esempio `<a rel="nofollow" href="https://example.com/sales.html">Sales</a>`.
- Cambia il metatag della pagina in `index,nofollow`, come [impostazione di configurazione &#x200B;](https://experienceleague.adobe.com/it/docs/commerce-admin/marketing/seo/seo-overview#configure-robotstxt) comune o per tipo di pagina con estensioni personalizzate. Mantenere accurato `sitemap.xml` in modo che i bot abbiano sempre un elenco aggiornato delle pagine da indicizzare.
- Aggiorna `robots.txt` per bloccare percorsi e le risorse a cui i bot non devono accedere.
- La direttiva `crawl-delay` non fa parte del protocollo ufficiale di esclusione dei robot, ma funziona per alcuni bot, come Bingbot, Slurp, SEMrushBot e alcuni altri. Googlebot ignora questa direttiva.
- Aggiungere regole di limite di tasso. Nel modulo Fastly è presente una protezione nativa del crawler [abusiva](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/RATE-LIMITING.md#abusive-crawler-protection). Per un controllo più preciso, uno snippet [VCL](https://experienceleague.adobe.com/it/docs/commerce-on-cloud/user-guide/cdn/custom-vcl-snippets/fastly-vcl-custom-snippets) può restituire `429` (Troppe richieste) o `405` (Metodo non consentito) per un regex agente utente con un limite di velocità individuale. Consulta la documentazione del crawler per informazioni sul metodo preferito e sul codice di risposta. Consulta le [indicazioni VCL di Fastly](https://www.fastly.com/documentation/reference/vcl/functions/rate-limiting/ratelimit-check-rate/).
- I crawler basati sull’intelligenza artificiale e sul modello di linguaggio di grandi dimensioni (LLM) rappresentano un caso speciale sempre più diffuso. Non sempre si identificano in modo coerente, pertanto le regole dell’agente utente VCL possono restare indietro. Il componente aggiuntivo [Advanced Security](https://experienceleague.adobe.com/it/docs/commerce-on-cloud/user-guide/cdn/advanced-security) di Adobe dispone di [gestione nativa dei bot](#advanced-security-native-bot-management-layer-7-ddos--rate-limiting) in grado di distinguere i crawler e i recuperi di IA verificati da quelli sospetti al limite, operazione che non è possibile eseguire da sola con VCL.

### Blocco dei crawler indesiderati

Se alcuni motori di ricerca generano un traffico significativo e non sono importanti per l’azienda, possono essere bloccati completamente:

- Alcuni bot seguono `robots.txt` modifiche 1-2 giorni dopo, dopo aver riletto e aggiornato le regole di analisi.
- Se un crawler ignora `robots.txt`, bloccarlo con uno snippet VCL personalizzato ([example](https://experienceleague.adobe.com/it/docs/commerce-knowledge-base/kb/how-to/block-malicious-traffic-for-magento-commerce-on-fastly-level#block-traffic-by-user-agent)). Alcuni crawler documentano esplicitamente questo come il metodo preferito o l&#39;unico metodo di controllo della frequenza.

## Script e raschietti dannosi

Utilizza l’app Traffic Insights per identificare le direzioni comuni dell’attacco, filtrando per aree mirate in base alle esigenze. Se le richieste contrassegnate con il flag di rosso provengono principalmente da determinati IP, subnet o geolocalizzazioni (**Numero di IP principali per richieste**, **Numero di statistiche per subnet IP**, **Numero di statistiche per paese**), è consigliabile bloccarle con VCL Fastly personalizzato.

Ogni progetto di infrastruttura cloud dispone già di una linea di base di protezione automatica, indipendentemente da qualsiasi configurazione eseguita. Il WAF (Web Application Firewall) incluso blocca immediatamente l&#39;iniezione SQL e i segnali noto-dannosi-IP (backdoor, attack tooling, CMDEXE, Log4J-JNDI, traversal, XSS) e limita la velocità di altri IP non dannosi una volta che attraversano 50 richieste/minuto, 350 richieste/10 minuti o 1.800 richieste/ora. Questa linea di base è ciò che **le richieste di risposta di WAF** e le colonne del segnale di WAF nelle tabelle dell&#39;app indicano. Un picco in queste colonne non significa necessariamente che non sei protetto.

- Fai attenzione alle credenziali, all’acquisizione dell’account, alla creazione di account falsi, al test delle carte, alla raschiatura dei contenuti e all’accumulo di inventario/carrello. Questi pattern di abuso basati su bot vengono visualizzati nella scheda **Analisi delle attività e delle richieste dei bot**. Gli endpoint di accesso, account, estrazione o catalogo con traffico elevato e a bassa diversità rappresentano la firma da cercare in **IP principali per numero di richieste** e **Dettagli sull&#39;impatto dei bot noti**.
- Proteggere gli endpoint API di estrazione e pagamento dagli attacchi di bot con [Google reCAPTCHA](https://experienceleague.adobe.com/it/docs/commerce-admin/systems/security/captcha/security-google-recaptcha).
- Utilizza la protezione del percorso [limite di velocità nativo del modulo Fastly](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/RATE-LIMITING.md#path-protection).
- Controlla [Segnali WAF di nuova generazione](https://www.fastly.com/documentation/guides/next-gen-waf/signals/using-system-signals/) nel campo `Sigsci_Tags` separato da virgole e combina le corrispondenze dei segnali rilevanti in una regola di blocco mirata. Il valore di una richiesta sospetta può essere `BOT-ANALYSIS,DATACENTER,SIGSCI-IP,SITE-FLAGGED-IP,SUSPECTED-BAD-BOT`. WAF etichetta un IP con `SITE-FLAGGED-IP` fino a una soglia prima che inizi a bloccarsi automaticamente. I widget **Segnali di attacco e anomalie WAF**, **Segnali bot WAF** e **Richieste da risposta WAF** e le colonne WAF nelle tabelle IP, subnet e country presentano queste caratteristiche.
- Per gli approcci comuni, consulta l’articolo di Adobe sul [blocco del traffico dannoso per Adobe Commerce al livello Fastly](https://experienceleague.adobe.com/it/docs/commerce-knowledge-base/kb/how-to/block-malicious-traffic-for-magento-commerce-on-fastly-level).
- Per scenari complessi in cui il blocco manuale non è un&#39;opzione valida, ad esempio campagne bot sostenute, attacchi distribuiti su molti IP/API o attacchi DDoS (Distributed Denial of Service) di livello 7, considera prima il componente aggiuntivo [Advanced Security](https://experienceleague.adobe.com/it/docs/commerce-on-cloud/user-guide/cdn/advanced-security) di Adobe (vedi [gestione bot nativa](#advanced-security-native-bot-management-layer-7-ddos--rate-limiting)). Funziona sullo stesso Fastly Edge che serve la vetrina. Se hai bisogno di funzionalità esterne al suo ambito, un servizio di mitigazione dei bot gestito da terze parti con integrazione Fastly nativa, come [Datadome](https://docs.datadome.co/docs/module-fastly) o [HUMAN Bot Defender](https://www.fastly.com/documentation/guides/integrations/non-fastly-services/human-bot-defender/) (precedentemente PerimeterX) è l&#39;alternativa suggerita. Tutte queste opzioni aggiungono costi aggiuntivi.

## Sicurezza avanzata: gestione nativa dei bot, funzionalità DDoS di Layer 7 e limitazione della velocità

Le sezioni precedenti spiegano cosa è possibile fare con i dati dell’app Traffic Insights e con Fastly VCL manuale. Per scenari in cui ciò non è sufficiente, come campagne bot sostenute o in evoluzione, DDoS di livello 7 (livello applicazione) o abusi distribuiti in modo limitato su molti endpoint API e IP, Adobe offre [Sicurezza avanzata](https://experienceleague.adobe.com/it/docs/commerce-on-cloud/user-guide/cdn/advanced-security).

Advanced Security è un componente aggiuntivo a pagamento per [!DNL Adobe Commerce on Cloud Infrastructure] che aggiunge la gestione dei bot perimetrali (tra cui il rilevamento di crawler di intelligenza artificiale e fetcher), la protezione DDoS di Layer 7 e la limitazione avanzata della velocità sulla stessa piattaforma Fastly che serve già la vetrina. Consulta [Sicurezza avanzata](https://experienceleague.adobe.com/it/docs/commerce-on-cloud/user-guide/cdn/advanced-security) per informazioni sulle funzionalità complete, sulle limitazioni correnti e su come richiederle.

Una volta acquistata e abilitata, utilizza l’app Traffic Insights per verificare che Advanced Security funzioni. Le sue decisioni vengono segnalate attraverso gli stessi campi `Sigsci_Tags` e `Agent_response` dietro **Segnali di attacco e anomalie WAF**, **Segnali bot WAF** e **Richieste da risposta WAF**. Confronta tali widget prima e dopo averlo abilitato per confermarne l’attività sul traffico.
