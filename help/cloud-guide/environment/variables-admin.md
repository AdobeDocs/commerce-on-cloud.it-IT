---
title: Variabili ADMIN
description: Consulta un elenco delle variabili di ambiente utilizzate per l’installazione di Adobe Commerce sull’infrastruttura cloud.
feature: Cloud, Configuration, Install, Roles/Permissions
role: Developer
exl-id: d2746185-bc59-4d30-a088-73df1bd2c0b2
source-git-commit: 4e751f02b92f954cd41d5523237da295a068661a
workflow-type: tm+mt
source-wordcount: '758'
ht-degree: 0%

---

# Variabili amministratore

Gli utenti con accesso amministrativo al progetto Adobe Commerce on Cloud Infrastructure possono utilizzare le seguenti variabili di ambiente del progetto per ignorare le impostazioni di configurazione dell’account utente amministratore per accedere all’interfaccia utente amministratore.

## Credenziali amministratore

Durante l’installazione di Commerce, è possibile sovrascrivere le credenziali utente amministratore con le variabili ADMIN riportate nella tabella seguente.

Se si desidera modificare i valori dopo l&#39;installazione, connettersi all&#39;ambiente utilizzando SSH e utilizzare il comando Adobe Commerce CLI [`admin:user`](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/tutorials/admin.html?lang=it) per creare o modificare le credenziali utente amministratore.

| Variabile | Predefinito | Descrizione |
| -------------- | --------------------------- | ----------- |
| `ADMIN_USERNAME` | Indirizzo e-mail proprietario licenza | Un nome utente per l’utente amministratore con la possibilità di creare altri utenti, inclusi gli utenti amministratori. |
| `ADMIN_EMAIL` |                             | Indirizzo e-mail dell’utente amministratore. Questo indirizzo viene utilizzato per inviare le notifiche di reimpostazione della password. |
| `ADMIN_PASSWORD` |                             | Password per l&#39;utente amministratore. Al momento della creazione del progetto, viene generata una password casuale e viene inviata un’e-mail al Proprietario della licenza. Durante la creazione del progetto, il Proprietario della licenza avrebbe dovuto modificare la password. Contattare il proprietario della licenza per ottenere la password aggiornata. |
| `ADMIN_LOCALE` | `en_US` | Impostazioni locali predefinite utilizzate dall&#39;amministratore. |

## URL amministratore

Utilizza la seguente variabile di ambiente per proteggere l’accesso all’interfaccia utente di amministrazione. Se specificato, questo valore sostituisce l&#39;URL predefinito durante l&#39;installazione. In [!DNL Adobe Commerce] sull&#39;infrastruttura cloud, è necessario impostare o modificare l&#39;URL amministratore utilizzando la variabile `ADMIN_URL` in ([!DNL Cloud Console] o [!DNL Cloud CLI]). La modifica dell&#39;impostazione da [!DNL Admin] è applicabile solo alle installazioni locali.

`ADMIN_URL`: l&#39;URL relativo per accedere all&#39;interfaccia utente di amministrazione. URL predefinito: `/admin`.

### Modificare l’URL dell’amministratore

Per impostazione predefinita, l&#39;URL [Commerce Admin](https://experienceleague.adobe.com/docs/commerce-admin/start/admin/admin.html?lang=it) è impostato su *&lt;nome_dominio>/admin*. Per motivi di sicurezza, Adobe consiglia di impostarlo su un URL amministratore univoco e personalizzato, difficilmente intuibile.

**In [!DNL Adobe Commerce] nell&#39;infrastruttura cloud**, è necessario modificare l&#39;URL amministratore utilizzando la variabile di ambiente `ADMIN_URL` in ([!DNL Cloud Console] o [!DNL Cloud CLI]). La modifica dell&#39;impostazione da [!DNL Admin] è applicabile solo alle installazioni locali. Per le installazioni locali, segui [utilizza un URL amministratore personalizzato](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/site-store/store-urls.html?lang=it#use-a-custom-admin-url).

Dopo l’installazione, Adobe consiglia di modificare la variabile a livello di ambiente per l’URL amministratore. Configurare questa impostazione per motivi di sicurezza prima di creare diramazioni dall&#39;ambiente `master` clonato. Tutti i rami creati dal ramo `master` ereditano le variabili a livello di ambiente e i relativi valori, a meno che l&#39;ereditarietà non venga impostata su false.

Utilizzare [!DNL Cloud Console] o [!DNL Cloud CLI] per impostare o aggiornare `ADMIN_URL`.

#### Opzione A: modificare l&#39;URL amministratore utilizzando [!DNL Cloud Console]

##### Ambiente di integrazione

Dalla [console cloud](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/project/overview.html?lang=it), aggiungi una nuova variabile con:

- **Nome:** `ADMIN_URL`
- **Valore:** Il nuovo URL amministratore (ad esempio, `magento_A8v10`)

- Per i passaggi dettagliati, consulta [aggiungere variabili di ambiente](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/project/overview.html?lang=it#configure-environment) o [variabili di ambiente](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/env/stage/variables-admin.html?lang=it) nella documentazione per gli sviluppatori.

##### Imposta l&#39;URL amministratore in [!DNL Cloud Console]

1. Accedi alla [console cloud](https://console.adobecommerce.com/).
2. Selezionare un progetto dall&#39;elenco **[!UICONTROL All projects]**.
3. Nella panoramica del progetto, seleziona l’ambiente e fai clic sull’icona di configurazione.
4. Selezionare la scheda **[!UICONTROL Variables]**.
5. Fare clic su **[!UICONTROL Create Variable]** (o modificare la variabile `ADMIN_URL` esistente, se presente).
6. Immetti quanto segue:
   - **Nome variabile:** `ADMIN_URL`
   - **Valore:** Il nuovo percorso amministratore (ad esempio, `magento_A8v10`).

   Per impostazione predefinita, sono selezionati **[!UICONTROL Available during runtime]** e **[!UICONTROL Make inheritable]**. Per evitare che gli ambienti figlio ereditino questo valore, cancellare **[!UICONTROL Make inheritable]** per questa variabile.
7. Fare clic su **[!UICONTROL Create variable]** (o **[!UICONTROL Save]**) e attendere il completamento della distribuzione. Il pulsante è visibile solo se i campi obbligatori contengono valori.

##### Quando Gestione temporanea e Produzione non sono disponibili in [!DNL Cloud Console]

[Invia un ticket di supporto](https://experienceleague.adobe.com/it/docs/support-resources/adobe-support-tools-guide/adobe-commerce-support/adobe-commerce-help-center-user-guide#submit-ticket) richiedendo di aggiungere la variabile `ADMIN_URL` per l&#39;ambiente di staging o produzione. Se l&#39;ambiente di gestione temporanea e l&#39;ambiente di produzione sono accessibili da [!DNL Cloud Console], aggiungere la variabile come descritto in [Ambiente di integrazione](#integration-environment).

#### Opzione B: modificare l&#39;URL amministratore utilizzando [!DNL Cloud CLI]

Utilizzare il comando `magento-cloud variable:update` per aggiornare la variabile. Il comando `variable:set` è obsoleto e non è disponibile.

L&#39;esempio seguente aggiorna l&#39;ambiente `master` `ADMIN_URL` in `newAdmin_A8v10` e impedisce agli ambienti figlio di ereditare il valore:

```bash
magento-cloud variable:update ADMIN_URL --value newAdmin_A8v10 -e master --inheritable false
```

- **Ridistribuzione:** La modifica della variabile `ADMIN_URL` in [!DNL Cloud CLI] attiva una ridistribuzione dell&#39;ambiente.
- **Ereditarietà:** Le variabili sono ereditabili per impostazione predefinita. Per evitare che il valore venga ereditato dagli ambienti figlio, utilizzare l&#39;opzione `--inheritable false` come illustrato. Per ulteriori dettagli, vedi [visibilità livello variabile](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/env/variable-levels.html?lang=it#visibility).

>[!NOTE]
>
>Il valore `ADMIN_URL` accetta lettere (a-z, A-Z), numeri (0-9) e il carattere di sottolineatura (_). Gli spazi o altri caratteri non sono accettati.
