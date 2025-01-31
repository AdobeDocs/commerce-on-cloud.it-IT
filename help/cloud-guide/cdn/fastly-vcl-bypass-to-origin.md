---
title: VCL personalizzato per ignorare la Fastly Cache
description: Risolvere i problemi relativi al traffico delle richieste verso il server di origine creando uno snippet VCL personalizzato per ignorare la cache Fastly.
feature: Cloud, Configuration, Cache
source-git-commit: 1e789247c12009908eabb6039d951acbdfcc9263
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 0%

---

# VCL personalizzato per ignorare la Fastly Cache

Puoi creare uno snippet VCL personalizzato per ignorare la cache Fastly e risolvere eventuali problemi di traffico delle richieste al server di origine. Ad esempio, puoi creare uno snippet per determinare se i problemi del sito sono causati dalla memorizzazione in cache o per risolvere i problemi relativi alle intestazioni.

Puoi configurare il frammento di codice in modo da evitare il caching Fastly per le richieste provenienti da un indirizzo IP o un URL specifico.

>[!NOTE]
>
>Prima di unire la configurazione VCL personalizzata in un ambiente di produzione, assicurati di testare il codice nell’ambiente di staging.

**Prerequisiti:**

{{$include /help/_includes/vcl-snippet-prerequisites.md}}

**Per ignorare la cache Fastly in base all&#39;indirizzo IP o all&#39;URL**:

{{admin-login-step}}

1. Fai clic su **Archivi** > Impostazioni > **Configurazione** > **Avanzate** > **Sistema**.

1. Espandi **Cache a pagina intera** > **Configurazione rapida** > **Snippet VCL personalizzati**.

1. Fare clic su **Crea snippet personalizzato**.

1. Aggiungi i valori dello snippet VCL:

   - **Nome** - `bypass_fastly`

   - **Tipo** - `recv`

   - **Priorità** - `5`

   - **VCL** contenuto frammento —

     L’esempio che segue bypassa Fastly per un indirizzo IP specifico:

     ```conf
     if (client.ip == "<Your IPv4 IP address>" || client.ip == "<Your IPv6 IP address>") {
       return(pass);
     }
     ```

     L’esempio che segue bypassa Fastly per un pattern URL specifico:

     ```conf
     if (req.url ~ "/media/feeds/GoogleShoppingHiVisNew.xml") {  return (pass);}
     ```

     Per ottenere una corrispondenza URL esatta, utilizzare l&#39;operatore `==` anziché l&#39;operatore `~`. Per informazioni dettagliate, vedere [Fastly VCL reference].

1. Fai clic su **Crea**.

   ![Crea snippet VCL con bypass veloce](/help/assets/cdn/fastly-create-bypass-snippet.png)

1. Dopo il ricaricamento della pagina, fai clic su **Carica VCL in Fastly** nella sezione *Fastly Configuration*.

1. Al termine del caricamento, aggiorna la cache in base alla notifica nella parte superiore della pagina.

   Convalida in breve la versione VCL aggiornata durante il processo di caricamento. Se la convalida non riesce, modifica il frammento VCL personalizzato per risolvere eventuali problemi. Quindi, carica nuovamente il file VCL.

Dopo aver aggiunto lo snippet VCL, è possibile utilizzare i comandi cURL per inviare le richieste al server di origine dall&#39;indirizzo IP o dall&#39;URL specificato, come illustrato nell&#39;esempio seguente:

```bash
curl -svo /dev/null www.example.com/index.html
```

Quindi, esamina la risposta per la risoluzione dei problemi relativi al contenuto non memorizzato in cache.

{{automate-vcl-snippet-deployment}}

{{$include /help/_includes/vcl-snippet-modify.md}}

{{$include /help/_includes/vcl-snippet-delete.md}}

<!--External link definitions-->

[Riferimento VCL Fastly]: https://docs.fastly.com/vcl/
