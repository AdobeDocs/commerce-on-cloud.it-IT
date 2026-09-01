---
source-git-commit: 79ac13115bd3f275651a5477f2939c8f00a5a985
workflow-type: tm+mt
source-wordcount: '704'
ht-degree: 0%

---
# Supporto dei servizi Pro e disponibilità dei clienti

## Supporto dei servizi Pro

Per richiedere e completare un aggiornamento del servizio Pro in Staging o Produzione, effettuare le seguenti operazioni:

1. **Per installare o aggiornare [servizi](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/configure/service/services-yaml) solo negli ambienti `Staging` e `Production`**, invia un [ticket di supporto Adobe Commerce](https://experienceleague.adobe.com/en/docs/support-resources/adobe-support-tools-guide/adobe-commerce-support/adobe-commerce-help-center-user-guide#submit-ticket).

   Nel ticket, specifica le modifiche del servizio richieste, includi i file aggiornati `.magento.app.yaml` e `.magento/services.yaml` e annota la versione PHP di destinazione.

   La versione PHP, gli aggiornamenti del Compositore, le estensioni e le impostazioni di ambiente sono modifiche self-service. Adobe potrebbe dover aggiornare l’agente New Relic per garantire la compatibilità della versione PHP. Vedi [Impostazioni PHP](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/configure/app/php-settings) in _Configurazione applicazione_.

   >[!IMPORTANT]
   >
   >Quando selezioni il campo **[!UICONTROL Environment]** nel modulo del ticket, utilizza la denominazione dell&#39;ambiente di Adobe. Ad esempio, seleziona Staging anche se chiami l&#39;ambiente **Dev** internamente. È possibile indicare il proprio nome interno nella descrizione, ma il campo [!UICONTROL Environment] deve utilizzare la nomenclatura di Adobe.

1. **Confermare la pianificazione dell&#39;aggiornamento** tramite il processo in due parti di Adobe: confermare prima la data e l&#39;ora richieste, quindi inviarle al team dell&#39;infrastruttura per la conferma finale.

   I cambiamenti di produzione (solo Pro) richiedono un preavviso di almeno due giorni lavorativi, esclusi i fine settimana. Ad esempio, il team di Cloud Infrastructure deve riconoscere un aggiornamento del lunedì entro il mercoledì precedente. Prevedere un lead time aggiuntivo durante il picco della domanda. Per evitare ritardi, rispondi alla richiesta iniziale almeno 48 ore prima della finestra. L’aggiornamento non viene considerato pianificato fino a quando non ricevi una conferma finale.

   >[!NOTE]
   >
   >Fornisci finestre di manutenzione in UTC. Gli aggiornamenti di staging non vengono pianificati in anticipo e vengono in genere completati lo stesso giorno della richiesta.
   >
   >Dopo un aggiornamento di RabbitMQ, ridistribuire l’ambiente per reinizializzare le code dei messaggi.

1. **Convalidare l&#39;aggiornamento** in un ambiente di staging o integrazione prima di pianificarlo in produzione.

   I problemi causati dai moduli di terze parti, dal codice personalizzato o dalla compatibilità delle dipendenze spesso emergono durante la ridistribuzione che segue un aggiornamento del servizio. Per convalidare più aggiornamenti di servizio uno alla volta, un ordine ragionevole è Valkey o Redis, quindi RabbitMQ, OpenSearch, quindi MariaDB. Questa non è una sequenza obbligatoria. Gli aggiornamenti del database hanno il massimo impatto operativo e meritano la massima cautela.

   Adobe non garantisce in anticipo la durata esatta di una finestra di manutenzione di produzione, poiché la tempistica dipende dall’ambiente e dai servizi coinvolti. Utilizza il tempo impiegato dall’aggiornamento di staging come stima pratica durante la pianificazione della finestra Produzione.

1. **Ridistribuisci l&#39;ambiente** dopo che Adobe ha completato l&#39;aggiornamento del servizio in modo che la modifica abbia effetto, anche se la versione dell&#39;applicazione Adobe Commerce non cambia.

   Se l&#39;aggiornamento include OpenSearch, pianificare anche una reindicizzazione completa. Adobe non può garantire tempi di inattività pari a zero per un aggiornamento del servizio, pertanto pianifica una finestra di manutenzione che consenta di ridistribuire il tempo, reindicizzare se necessario e convalidare la vetrina e l’amministratore prima di riaprire il sito.

## Disponibilità del cliente durante gli aggiornamenti

**Un rappresentante del team o del partner di implementazione deve essere disponibile online per la durata della finestra di aggiornamento produzione pianificata.** La pianificazione durante un periodo di traffico ridotto non impedisce l’esecuzione dell’aggiornamento. Adobe gestisce l’aggiornamento dell’infrastruttura cloud, ma non può convalidare il comportamento dell’applicazione, le integrazioni, il codice personalizzato o i flussi di lavoro aziendali.

Il rappresentante disponibile deve poter:

- **Monitora** le transazioni di storefront e le transazioni aziendali critiche durante e dopo l&#39;aggiornamento.
- **Rispondi** alle domande del supporto Adobe o del team di Cloud Infrastructure.
- **Verificare** che integrazioni, estensioni, personalizzazioni, processi cron, code e altre funzioni specifiche del cliente funzionino come previsto.
- **Convalida** flussi di lavoro business-critical, ad esempio estrazione, visualizzazioni catalogo, ricerca, accesso ed elaborazione degli ordini.
- **Segnala** comportamenti imprevisti immediatamente, mentre il contesto di aggiornamento e i registri sono ancora disponibili.

>[!TIP]
>
>Per i progetti Pro, gli aggiornamenti dei servizi in produzione richiedono anche una pianificazione anticipata e un processo di conferma in due parti con il supporto Adobe. Consulta il supporto per [Pro Services](#pro-services-support).

### Modalità di manutenzione

**La modalità di manutenzione non sostituisce la disponibilità del cliente.** La modalità di manutenzione blocca l’accesso alla vetrina, ma non convalida i servizi dell’applicazione, le integrazioni, le code, i processi cron, il pagamento o altre funzioni specifiche del cliente.

Se il lavoro pianificato richiede la modalità di manutenzione, coordinane l’utilizzo con il supporto Adobe e segui le istruzioni per l’aggiornamento. In seguito, verifica che la vetrina e i flussi di lavoro critici funzionino normalmente prima di considerare il lavoro completato.
