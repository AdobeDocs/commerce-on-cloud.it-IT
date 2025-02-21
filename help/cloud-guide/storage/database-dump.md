---
title: Eseguire il backup del database
description: Scopri come utilizzare gli strumenti ECE per creare un backup del database per un progetto di infrastruttura cloud di Adobe Commerce.
feature: Cloud, Iaas, Storage
exl-id: 351f7691-3153-4b8a-83af-8b8895b93d98
source-git-commit: 3a3b0cd6e28f3e6ed3521a86f7c7c8868be0cf83
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 0%

---

# Eseguire il backup del database

È possibile creare una copia del database utilizzando il comando `ece-tools db-dump` senza acquisire tutti i dati dell&#39;ambiente da servizi e installazioni. Per impostazione predefinita, questo comando crea backup nella directory `app/var/` per tutte le connessioni al database specificate nella configurazione dell&#39;ambiente. L&#39;operazione di dump del database passa alla modalità di manutenzione dell&#39;applicazione, interrompe i processi della coda del consumatore e disattiva i processi cron prima dell&#39;inizio del dump.

Considera le seguenti linee guida per l’immagine del database:

- Per gli ambienti di produzione, Adobe consiglia di completare le operazioni di dump del database nelle ore di minore utilizzo, per ridurre al minimo le interruzioni del servizio che si verificano quando il sito è in modalità manutenzione.
- Se si verifica un errore durante l&#39;operazione di dump, il comando elimina il file di dump per risparmiare spazio su disco. Esaminare i registri per i dettagli (`var/log/cloud.log`).
- Per gli ambienti Pro Production, questo comando esegue il dump solo da _uno_ dei tre nodi ad alta disponibilità, pertanto i dati di produzione scritti in un nodo diverso durante il dump potrebbero non essere copiati. Il comando genera un file `var/dbdump.lock` per impedire l&#39;esecuzione del comando su più nodi.
- Per un backup di tutti i servizi dell&#39;ambiente, Adobe consiglia di creare un [backup](snapshots.md).

È possibile scegliere di eseguire il backup di più database aggiungendo i nomi dei database al comando. L&#39;esempio seguente esegue il backup di due database: `main` e `sales`:

```bash
php vendor/bin/ece-tools db-dump main sales
```

Usa il comando `php vendor/bin/ece-tools db-dump --help` per altre opzioni:

- `--dump-directory=<dir>` - Scegliere una directory di destinazione per il dump del database. **Non scegliere directory Web pubbliche come `pub/media` o`pub/static`**.
- `--remove-definers` - Rimuovere le istruzioni DEFINER dal dump del database.

**Per creare un&#39;immagine del database nell&#39;ambiente di staging o di produzione**:

1. [Utilizzare SSH per accedere o creare un tunnel per connettersi all&#39;ambiente remoto](../development/secure-connections.md) che contiene il database da copiare.

1. Elencare le relazioni dell’ambiente e prendere nota delle informazioni di accesso al database.

   ```bash
   echo $MAGENTO_CLOUD_RELATIONSHIPS | base64 -d | json_pp
   ```

   o

   ```bash
   php -r 'print_r(json_decode(base64_decode($_ENV["MAGENTO_CLOUD_RELATIONSHIPS"]))->database);'
   ```

1. Crea un backup del database. Per scegliere una directory di destinazione per il dump del database, utilizzare l&#39;opzione `--dump-directory`.

   >[!WARNING]
   >
   >Se si specifica una directory di destinazione, non scegliere directory Web pubbliche come `pub/media` o `pub/static`.

   ```bash
   php vendor/bin/ece-tools db-dump -- main
   ```

   Risposta di esempio:

   ```
   The db-dump operation switches the site to maintenance mode, stops all active cron jobs and consumer queue processes, and disables cron jobs before starting the dump process.
   Your site will not receive any traffic until the operation completes.
   Do you wish to proceed with this process? (y/N)? y
   2020-01-28 16:38:08] INFO: Starting backup.
   [2020-01-28 16:38:08] NOTICE: Enabling Maintenance mode
   [2020-01-28 16:38:10] INFO: Trying to kill running cron jobs and consumers processes
   [2020-01-28 16:38:10] INFO: Running Magento cron and consumers processes were not found.
   [2020-01-28 16:38:10] INFO: Waiting for lock on db dump.
   [2020-01-28 16:38:10] INFO: Start creation DB dump for main database...
   [2020-01-28 16:38:10] INFO: Finished DB dump for main database, it can be found here: /app/qxmtlseakof6y/var/dump-main-1580229490.sql.gz
   [2020-01-28 16:38:10] INFO: Backup completed.
   [2020-01-28 16:38:11] NOTICE: Maintenance mode is disabled.
   ```

1. Il comando `db-dump` crea un file di archivio `dump-<timestamp>.sql.gz` nella directory del progetto remoto.

>[!TIP]
>
>Se desideri inviare questi dati a un ambiente specifico, consulta [Migrare i dati e i file statici](../deploy/staging-production.md#migrate-static-files).
