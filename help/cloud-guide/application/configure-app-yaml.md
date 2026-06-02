---
title: Configurare la distribuzione dell'applicazione
description: Scopri come configurare le proprietà nel file di configurazione dell'applicazione che controllano il modo in cui l'applicazione  [!DNL Commerce]  genera e distribuisce nell'ambiente Cloud.
feature: Cloud, Configuration, Build, Deploy
exl-id: 47dcb13f-8873-495d-956f-08a5e04844d9
TQID: https://experienceleague.adobe.com/LCTu-HeJCO1pp9trlZ7h74CxSQtyBr5SDmYP9DgCtkU
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: fd3ef8201c368f889344452e334976070a6c7157
workflow-type: tm+mt
source-wordcount: 190
ht-degree: 0%

---

# Configurare la distribuzione dell&#39;applicazione

Il file `.magento.app.yaml` controlla il modo in cui l&#39;applicazione genera e distribuisce. Sebbene Adobe Commerce su infrastruttura cloud supporti più applicazioni per progetto, in genere un progetto ha una singola applicazione con il file `.magento.app.yaml` nella directory principale dell&#39;archivio.

`.magento.app.yaml` ha molti valori predefiniti. Vedere [un file `.magento.app.yaml` di esempio](https://github.com/magento/magento-cloud/blob/master/.magento.app.yaml). Rivedi sempre `.magento.app.yaml` per la versione installata. Questo file può differire tra le diverse versioni di Adobe Commerce nelle infrastrutture cloud.

Utilizzare il file `.magento.app.yaml` per definire i seguenti valori di configurazione:

- [Proprietà](properties.md) - Consente di definire i valori delle proprietà per l&#39;istanza dell&#39;applicazione.
- [Proprietà variabili](variables-property.md) - Esaminare le variabili di ambiente necessarie per la versione dell&#39;applicazione [!DNL Commerce].
- [Impostazioni PHP](php-settings.md)—Configurare le opzioni PHP di runtime.
- [Imposta cache per file statici](set-cache.md) - Imposta TTL cache per file multimediali e statici.

>[!NOTE]
>
>Il file `.magento.app.yaml` è gestito localmente o nell&#39;archivio Git. La configurazione viene letta solo ai fini del processo di distribuzione e compilazione e viene rimossa al termine della distribuzione, pertanto non sarà possibile trovarla sul server.
