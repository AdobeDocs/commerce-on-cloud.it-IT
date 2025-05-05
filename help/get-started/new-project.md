---
title: Provisioning di Commerce su Cloud
description: Scopri come preparare un consulente tecnico per i clienti Adobe per il provisioning del progetto Adobe Commerce su infrastruttura cloud.
recommendations: noDisplay, catalog
role: Admin
source-git-commit: 0d9d3d64cd0ad4792824992af354653f61e4388d
workflow-type: tm+mt
source-wordcount: '751'
ht-degree: 0%

---

# Prerequisiti per il provisioning di Commerce on Cloud

Iniziamo e inizializziamo il tuo progetto Commerce sull’infrastruttura cloud.

Adobe Prima di eseguire il provisioning del Commerce negli ambienti di progetto cloud, è consigliabile prendere in considerazione le strategie seguenti e preparare le risposte per la prima consultazione con il team dell’account Adobe. Utilizza le sezioni seguenti come elenco di controllo per aiutarti a preparare la conversazione con un consulente tecnico del cliente per il provisioning di un progetto cloud:

## Definizione del dominio

**Domanda 1**: _Quali domini intendi utilizzare per il lancio del sito?_

Prepara l’integrazione dei servizi Fastly e Inginx definendo i domini e i sottodomini di livello superiore per gli ambienti di staging e produzione Pro. Dopo la configurazione iniziale, è possibile aggiungere domini solo inviando un ticket di supporto Adobe Commerce; si consiglia quindi di disporre delle informazioni sul dominio.

Esempi per i domini Produzione e Staging:

- `www.your-store.com`
- `your-store.com`
- `mcprod.your-store.com`
- `mcstaging.your-store.com`

Per ulteriori informazioni su più domini o su domini univoci, consulta [Configurare più siti Web o store](../cloud-guide/store/multiple-sites.md) nella guida _Commerce on Cloud Infrastructure_.

Se disponi di un account Fastly esistente che collega gli stessi domini APEX e secondari utilizzati sul tuo sito Adobe Commerce, consulta [Più account Fastly e domini assegnati](https://experienceleague.adobe.com/it/docs/commerce-on-cloud/user-guide/cdn/fastly#multiple-fastly-accounts-and-assigned-domains){target="_blank"}.

## Dominio e-mail transazionale

**Domanda 2**: _Quale dominio o quali domini intendi utilizzare per le e-mail transazionali?_

Adobe Commerce on Cloud utilizza il servizio proxy SMTP (Simple Mail Transfer Protocol) di SendGrid, che fornisce servizi di autenticazione e-mail in uscita e di monitoraggio della reputazione. SendGrid invia e-mail transazionali per conto dell’utente, pertanto sono necessarie informazioni sul dominio.

Esempio di dominio SendGrid: `example@your-store.com`

Per ulteriori informazioni sulle e-mail transazionali e le impostazioni di dominio, consulta [Servizio di posta SendGrid](../cloud-guide/project/sendgrid.md) nella guida _Commerce on Cloud Infrastructure_.

## Allocazione di storage

**Domanda 3**: _Quanto spazio di archiviazione contrattuale intendi allocare per il caricamento di file e per il database?_

Adobe Commerce su infrastruttura cloud utilizza l’archiviazione per la struttura dei file, l’indicizzazione delle ricerche e il database. È possibile suddividere lo storage in base alle esigenze, a partire da 10 GB per ciascuna partizione.

La quantità di spazio di archiviazione contrattuale per il progetto cloud rappresenta lo spazio di archiviazione totale per ogni ambiente. Ad esempio, se si acquistano 50 GB di spazio di storage, si dispone di 50 GB di storage per ogni ambiente. Sono disponibili 50 GB di storage separato rispettivamente per la produzione, la gestione temporanea e ogni ambiente di integrazione.

Puoi aumentare la capacità di archiviazione contrattuale in qualsiasi momento. Per gli ambienti Pro Production e Staging, è necessario inviare un ticket di supporto Adobe Commerce per modificare l’allocazione dello spazio su disco. Un aumento delle dimensioni degli ambienti di produzione e staging di Pro può verificarsi solo a determinati intervalli. In base all&#39;utilizzo attuale dello spazio su disco, il team di supporto potrebbe consigliare di aumentare l&#39;allocazione dello spazio su disco di almeno 10 GB. Una volta allocato, l&#39;aumento dello spazio di archiviazione per Pro Staging and Production può **non** essere ripristinato.

Consulta [Gestire lo spazio su disco](../cloud-guide/storage/manage-disk-space.md) nella guida _Commerce on Cloud Infrastructure_.

## Area geografica del servizio cloud

**Domanda 4**: _In quale regione del servizio cloud è più conveniente essere vicini?_

Scegli Amazon Web Services (AWS) o Microsoft Azure as your Infrastructure as a Service (IaaS) foundation per i progetti Adobe Commerce on Cloud Infrastructure Pro. Ogni provider di servizi opera in più aree geografiche e fornisce più aree di disponibilità. Seleziona un’area adatta alla tua posizione e riduci il potenziale di latenza e costi più elevati.

Vedi [una mappa delle aree geografiche cloud di Adobe Commerce](../cloud-guide/overview.md).

## Servizio di connessione

**Domanda 5**: _È necessario un servizio PrivateLink? In caso affermativo, in quale area si trova la connessione PrivateLink?_

Adobe Commerce su infrastruttura cloud supporta l’integrazione con il servizio AWS PrivateLink o Azure Private Link. Anche se questo servizio è facoltativo, PrivateLink viene utilizzato per stabilire comunicazioni private sicure tra ambienti di infrastruttura cloud con servizi e applicazioni ospitati su sistemi esterni.

È importante prendere in considerazione la strategia del servizio cloud (AWS o Azure) in modo che l’istanza di Adobe Commerce sia accessibile nella stessa area geografica. Consulta il servizio [PrivateLink](../cloud-guide/development/privatelink-service.md) nella guida _Commerce on Cloud Infrastructure_ per ulteriori chiarimenti sull&#39;accessibilità regionale.

## Lancio del sito di destinazione

**Domanda 6**: _Qual è la data di lancio prevista?_

Il lancio di un sito richiede una configurazione e un test iterativi per garantire il successo del lancio. L’impostazione di una data di destinazione consente a te e al tuo account team Adobe di prepararsi per le attività finali precedenti all’avvio, che includono una chiamata per coordinare i passaggi finali.

Per esaminare l&#39;intero processo e scaricare una copia dell&#39;elenco di controllo di Launch, consulta la [panoramica del sito di Launch](../cloud-guide/launch/overview.md) nella guida _Commerce on Cloud Infrastructure_.

>[!TIP]
>
> Dai un’occhiata al portale Cloud e accedi al tuo nuovo progetto cloud.
>
>**Passaggio successivo**: [Onboarding in Commerce](onboarding.md)
