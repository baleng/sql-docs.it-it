---
title: Coppie di File di monitoraggio e risoluzione dei problemi di Merge per dati e differenziali | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: a8b0bacc-4d2c-42e4-84bf-1a97e0bd385b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1f5febee69483b5f1a2e8aa5b7b48fdde0a7ada2
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/02/2018
ms.locfileid: "48075281"
---
# <a name="monitoring-and-troubleshooting-merge-for-data-and-delta-file-pairs"></a>Monitoraggio e risoluzione di problemi relativi all'unione di coppie di file di dati e differenziali
  OLTP in memoria utilizza i criteri di unione per unire automaticamente coppie di file di dati e differenziali adiacenti. Non è possibile disabilitare l'attività di unione.  
  
 È possibile monitorare le coppie di file di dati e differenziali come segue:  
  
-   Confrontare le dimensioni di archiviazione in memoria con le dimensioni di archiviazione complessive. Se le dimensioni di archiviazione sono eccessivamente grandi, è probabile che l'unione non venga attivata. Per informazioni  
  
-   Esaminare lo spazio usato nel file di dati e differenziali mediante [DM db_xtp_checkpoint_files &#40;Transact-SQL&#41; ](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-xtp-checkpoint-files-transact-sql) per vedere se merge non viene attivato quando dovrebbe.  
  
## <a name="performing-a-manual-merge"></a>Esecuzione di un'unione manuale  
 È possibile usare [Sys. sp_xtp_merge_checkpoint_files &#40;Transact-SQL&#41; ](/sql/relational-databases/system-stored-procedures/sys-sp-xtp-merge-checkpoint-files-transact-sql) per eseguire un merge manuale.  
  
 Utilizzare la seguente query per recuperare le informazioni sui file di dati e differenziali.  
  
```tsql  
select checkpoint_file_id, file_type_desc, internal_storage_slot, file_size_in_bytes, file_size_used_in_bytes,   
inserted_row_count, deleted_row_count, lower_bound_tsn, upper_bound_tsn   
from sys.dm_db_xtp_checkpoint_files  
where state = 1  
order by file_type_desc, upper_bound_tsn  
```  
  
 Si supponga di aver trovato tre file di dati che non sono stati uniti. Utilizzando il valore `lower_bound_tsn` del primo file di dati e `upper_bound_tsn` dell'ultimo file di dati, è possibile eseguire il comando seguente:  
  
```tsql  
exec sys.sp_xtp_merge_checkpoint_files 'H_DB',  12345, 67890  
```  
  
 Si supponga che le tre coppie di file di dati e differenziali contengano ciascuna 15.836 righe e 5.279 righe eliminate. Dopo l'unione, il nuovo file di dati contiene 31.872 righe e 0 righe eliminate. Le dimensioni del nuovo file di dati possono essere molto maggiori rispetto a quelle inizialmente allocate di 128 MB. Ciò avviene perché l'unione manuale esegue l'override dei criteri di unione e forza l'unione dei file richiesti.  
  
 Il blog [stato di transizione del file di Checkpoint nel database con tabelle ottimizzate per la memoria](http://blogs.technet.com/b/dataplatforminsider/archive/2014/01/23/state-transition-of-checkpoint-files-in-databases-with-memory-optimized-tables.aspx) descrive la transizione di stato di coppie di file di dati e differenziali dall'inizio alla garbage collection.  
  
## <a name="see-also"></a>Vedere anche  
 [Creazione e gestione dell'archiviazione per gli oggetti con ottimizzazione per la memoria](../relational-databases/in-memory-oltp/creating-and-managing-storage-for-memory-optimized-objects.md)  
  
  
