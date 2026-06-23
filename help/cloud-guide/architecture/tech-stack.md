---
title: Stack tecnologico
description: Scopri lo stack di tecnologia che costituisce l’infrastruttura Commerce on Cloud.
feature: Cloud, Iaas, Paas
exl-id: 3fac1ab7-6440-4bf9-8169-9fadf51d70dd
TQID: https://experienceleague.adobe.com/2-uZdx1Oi-3LQUK-L7rC4kZWYcYobEhnVcUDNwOHpFs
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b5f00040-57a0-4a6d-a39e-383b1936c2c9id: ba9e5be9-7de1-4f71-a5d2-baead0e425eeid: c1256247-af4b-46d8-9dca-0c654ecfa157id: d1e21356-0064-4f48-9089-16e3f0dbd2a6id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
subfeature_v2: id: df5e974b-6742-4873-a687-a6bedaafdaa2id: f2261633-201d-46c5-8a66-999e70527a83
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1id: d095671a-1355-40aa-8b5f-06c33c68080b
source-git-commit: d863fc70609dcc66d21eb95e709db80e29114714
workflow-type: tm+mt
source-wordcount: 405
ht-degree: 0%

---

# Stack tecnologico

Considera Adobe Commerce sull’infrastruttura cloud come cinque livelli funzionali, come mostrato di seguito:

![Stack cloud](../../assets/CloudStack.png)

1. [**Infrastruttura cloud**](pro-architecture.md): scegli Amazon Web Services (AWS) o Microsoft Azure come base IaaS (Infrastructure as a Service) per i progetti Adobe Commerce su infrastruttura cloud Pro.

   Adobe analizza regolarmente l&#39;utilizzo delle risorse di elaborazione virtuale (vCPU) e alloca automaticamente le risorse per ottimizzare l&#39;utilizzo a lungo termine e ridurre il rischio di superare il limite di giorni massimo annuo per vCPU. Se si prevede un aumento del traffico del sito per periodi di tempo specifici, è necessario continuare ad aprire un ticket di supporto per [richiedere un upsize temporaneo](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/how-to-request-temporary-magento-upsize.html).

1. [**Platform as a Service**](cloud-architecture.md): ogni progetto Adobe Commerce su infrastruttura cloud fornisce un ambiente di integrazione Platform as a Service (PaaS) per lo sviluppo, il test e l&#39;integrazione di servizi.
1. [**Adobe Commerce**](../project/overview.md): Adobe Commerce sull&#39;infrastruttura cloud fornisce un&#39;infrastruttura preconfigurata che include PHP, MySQL (MariaDB), Redis, servizi della coda messaggi ([!DNL RabbitMQ] o [!DNL ActiveMQ]) e tecnologie supportate per motori di ricerca.
1. [**Strumenti per le prestazioni**](../monitor/new-relic-service.md): gli strumenti per le prestazioni di New Relic consentono di eseguire il debug, monitorare e gestire le applicazioni e l&#39;infrastruttura raccogliendo, analizzando e visualizzando dati dal proprio Adobe Commerce sui progetti di infrastruttura cloud.
1. [**Rete CDN (Content Delivery Network), Firewall applicazione Web ([!DNL WAF]) e Ottimizzazione immagine (IO)**](../cdn/fastly.md):

   * [Fastly CDN](../cdn/fastly.md#ddos-protection) - Fornisce servizi CDN protetti con protezione integrata da attacchi Distributed Denial of Service (DDoS) come [!DNL Ping of Death], attacchi [!DNL Smurf] e altri attacchi di tipo Flood basati su Internet Control Message Protocol (ICMP).
   * [Firewall applicazione Web (WAF)](../cdn/fastly-waf-service.md): i servizi WAF garantiscono la conformità PCI per gli storefront Adobe Commerce negli ambienti di produzione e i criteri WAF che proteggono le applicazioni Web Adobe Commerce da attacchi di iniezione, input dannosi, vulnerabilità cross-site scripting, exfiltrazione dei dati, violazioni del protocollo HTTP e altre [[!DNL OWASP] dieci minacce alla sicurezza](https://owasp.org/www-project-top-ten/).
   * [Ottimizzazione immagine (IO)](../cdn/fastly-image-optimization.md): consente di manipolare e ottimizzare le immagini in tempo reale per velocizzarne la consegna e semplificare la manutenzione dei set di origini delle immagini per le applicazioni Web reattive. L&#39;I/O veloce consente di ridurre il carico di elaborazione e di ridimensionamento delle immagini, consentendo ai server di elaborare gli ordini e le conversioni in modo efficiente.

Le applicazioni monolitiche richiedono un uso intensivo delle risorse, sono difficili da scalare e da gestire rapidamente. Con l’infrastruttura Cloud, i clienti Commerce hanno un accesso senza precedenti ai microservizi basati su SaaS che sono ricchi, intelligenti e performanti. Consulta [Software e servizi supportati](cloud-architecture.md#supported-software-and-services).

Utilizza la [Guida introduttiva di Commerce](../../get-started/overview.md) per configurare il nuovo programma Cloud e iniziare a gestire l&#39;applicazione [!DNL Commerce] in un ambiente nativo per il cloud.

