---
title: sys.dm_pdw_exec_requests (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 390225cc-23e8-4051-a5f6-221e33e4c0b4
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: c2a1978aeea7ec69ea45bc088bbdff432de3c9f4
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/01/2018
ms.locfileid: "47621869"
---
# <a name="sysdmpdwexecrequests-transact-sql"></a>sys.dm_pdw_exec_requests (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Contiene informazioni su tutte le richieste attualmente o recentemente attivo in [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]. Elenca una riga per ogni richiesta o alla query.  
  
|Nome colonna|Tipo di dati|Description|Intervallo|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|Chiave per questa visualizzazione. Id numerico univoco associato alla richiesta.|Deve essere univoco tra tutte le richieste nel sistema.|  
|session_id|**nvarchar(32)**|Id numerico univoco associato alla sessione in cui è stata eseguita la query. Visualizzare [DM pdw_exec_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md).||  
|status|**nvarchar(32)**|Stato corrente della richiesta.|'In esecuzione', 'Sospeso', 'Completed', 'Annullata', "Non riuscito".|  
|submit_time|**datetime**|Ora in cui è stata inviata la richiesta per l'esecuzione.|Valido **datetime** inferiore o uguale a start_time e ora corrente.|  
|start_time|**datetime**|Ora di inizio dell'esecuzione della richiesta.|NULL per le richieste in coda. in caso contrario, validi **datetime** minore o uguale all'ora corrente.|  
|end_compile_time|**datetime**|Ora in cui il motore completato la compilazione della richiesta.|NULL per le richieste che non sono stati compilati ancora; in caso contrario, un valore valido **datetime** minore start_time e minore o uguale all'ora corrente.|
|end_time|**datetime**|Ora in cui l'esecuzione della richiesta completato, non è riuscita o è stata annullata.|Null per le richieste in coda o attive. in caso contrario, un valore valido **datetime** minore o uguale all'ora corrente.|  
|total_elapsed_time|**int**|Tempo trascorso nell'esecuzione poiché è stata avviata la richiesta, in millisecondi.|Compreso tra 0 e la differenza tra start_time ed end_time.<br /><br /> Se total_elapsed_time supera il valore massimo per un numero intero, total_elapsed_time continuerà a essere il valore massimo. Questa condizione verrà generato l'avviso "il valore massimo è stato superato."<br /><br /> Il valore massimo in millisecondi è equivalente a 24,8 giorni.|  
|Etichetta|**nvarchar(255)**|Stringa di etichetta facoltativa associata alcune istruzioni di query SELECT.|Qualsiasi stringa che contiene 'a-z', 'A-Z','0-9', '_'.|  
|error_id|**nvarchar(36)**|Id univoco dell'errore associato alla richiesta, se presente.|Visualizzare [sys.dm_pdw_errors &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-errors-transact-sql.md); se si è verificato alcun errore impostato su NULL.|  
|database_id|**int**|Identificatore del database utilizzato dal contesto esplicito (ad esempio, usare DB_X).|Vedere id nel [Sys. Databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md).|  
|comando|**nvarchar(4000)**|Contiene il testo completo della richiesta di stato inviato dall'utente.|Qualsiasi testo di query o di richiesta valido. Le query che durano più di 4000 byte vengono troncate.|  
|resource_class|**nvarchar(20)**|La classe di risorse per questa richiesta. Vedere correlati **concurrency_slots_used** nelle [sys.dm_pdw_resource_waits &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-resource-waits-transact-sql.md).|SmallRC<br /><br /> MediumRC<br /><br /> LargeRC<br /><br /> XLargeRC|  
  
 Per informazioni sul numero massimo di righe mantenuto da questa vista, vedere "Minimo e massimo valori" nel [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'autorizzazione VIEW SERVER STATE.  
  
## <a name="security"></a>Sicurezza  
 DM pdw_exec_requests non filtra i risultati della query in base alle autorizzazioni specifiche del database. Gli account di accesso con autorizzazione VIEW SERVER STATE possono ottenere risultati i risultati della query per tutti i database  
  
> [!WARNING]  
>  Un utente malintenzionato può usare DM pdw_exec_requests per recuperare informazioni su oggetti di database specifici, concedendo semplicemente l'autorizzazione VIEW SERVER STATE e in mancanza di un'autorizzazione specifico del database.  
  
## <a name="see-also"></a>Vedere anche  
 [SQL Data Warehouse e Parallel Data Warehouse viste a gestione dinamica &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
