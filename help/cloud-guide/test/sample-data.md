---
title: Dati di esempio
description: Scopri come installare dati di esempio con Adobe Commerce sull’infrastruttura cloud.
exl-id: 59e23cfa-d364-4e70-8a86-644c339778cc
TQID: https://experienceleague.adobe.com/hEowDeOnXfkdlB-GCNRylKYrJLtXITR11-zsveyIA0Y
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: fd3ef8201c368f889344452e334976070a6c7157
workflow-type: tm+mt
source-wordcount: 205
ht-degree: 0%

---

# Dati di esempio

Se hai bisogno di alcuni dati di esempio durante lo sviluppo del tuo archivio, puoi installare dati di esempio. Questi dati simulano un archivio Adobe Commerce attivo con clienti, prodotti e altri dati. Questi dati di esempio funzionano al meglio con una nuova installazione di Adobe Commerce su modello di infrastruttura cloud.

Come best practice, installa dati di esempio in ambienti di sviluppo e integrazione. Se utilizzi dati di esempio in Staging o Produzione, devi [rimuovere](#reset-or-uninstall-sample-data) le informazioni e i prodotti prima di andare &quot;live&quot;.

## Installare i dati di esempio

Per installare i dati di esempio:

1. Sulla workstation locale, passa alla directory del progetto.

1. Nella directory principale, immetti il seguente comando per aggiungere dati di esempio:

   ```bash
   ./bin/magento sampledata:deploy
   ```

1. Attendi l’aggiornamento dei componenti.

1. Eseguire il commit e il push delle modifiche:

   ```bash
   git add -A && git commit -m "Install sample data"
   ```

   ```bash
   git push origin <branch-name>
   ```

1. Attendi la distribuzione del progetto.

1. Verifica che l’installazione sia stata eseguita correttamente accedendo alla pagina della vetrina nell’ambiente di integrazione. È possibile individuare il collegamento URL alla vetrina tramite [!DNL Cloud Console].

1. Crea un’istantanea dell’ambiente:

   ```bash
   magento-cloud snapshot:create -e <environment-ID>
   ```

Puoi iniziare a testare il tuo sviluppo con i dati live.

## Reimpostare o disinstallare i dati di esempio

È possibile reimpostare o rimuovere i dati di esempio seguendo la stessa procedura utilizzata per installarli:

- Elimina dati di esempio: `./bin/magento sampledata:remove`
- Reimposta dati di esempio: `./bin/magento sampledata:reset`
