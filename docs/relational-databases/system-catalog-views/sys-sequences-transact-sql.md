---
title: sequences (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.sequences_TSQL
- sys.sequences
- sequences
- sequences_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sequence number object, sys. sequences catalog view
- sys.sequences catalog view
ms.assetid: 0e1b0e32-1cce-40f7-83c8-860ec660138a
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: a3cffdd8b6040e1740e61043433cc95ca3319f5b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/01/2018
ms.locfileid: "47832039"
---
# <a name="syssequences-transact-sql"></a>sys.sequences (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Contiene una riga per ogni oggetto sequenza di un database.  
  
|Nome colonna|Tipo di dati|Description|  
|-----------------|---------------|-----------------|  
|\<colonne ereditate >||Eredita tutte le colonne da [Sys. Objects](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md).|  
|**start_value**|**sql_variant non NULL**|Valore iniziale per l'oggetto sequenza. Se l'oggetto sequenza viene riavviato tramite ALTER SEQUENCE verrà riavviato con questo valore. Quando l'oggetto sequenza cicli si procede al **minimum_value** oppure **maximum_value**, non il **start_value**.|  
|**increment**|**sql_variant non NULL**|Valore utilizzato per incrementare l'oggetto sequenza dopo ogni valore generato.|  
|**minimum_value**|**sql_variant NULL**|Valore minimo che può essere generato dall'oggetto sequenza. Una volta raggiunto questo valore, l'oggetto sequenza restituirà un errore durante il tentativo di generazione di più valori o di riavvio se viene specificata l'opzione CYCLE. Se non è stato specificato alcun valore MINVALUE, questa colonna restituisce il valore minimo supportato dal tipo di dati del generatore di sequenze.|  
|**maximum_value**|**sql_variant NULL**|Valore massimo che può essere generato dall'oggetto sequenza. Una volta raggiunto questo valore, l'oggetto sequenza restituirà un errore durante il tentativo di generazione di più valori o di riavvio se viene specificata l'opzione CYCLE. Se non è stato specificato alcun valore MAXVALUE, questa colonna restituisce il valore massimo supportato dal tipo di dati dell'oggetto sequenza.|  
|**is_cycling**|**bit non NULL**|Restituisce 0 se è stato specificato NO CYCLE per l'oggetto sequenza e 1 se è stato specificato CYCLE.|  
|**is_cached**|**bit non NULL**|Restituisce 0 se è stato specificato NO CACHE per l'oggetto sequenza e 1 se è stato specificato CACHE.|  
|**cache_size**|**int NULL**|Restituisce la dimensione della cache specificata per l'oggetto sequenza. Questa colonna contiene NULL se la sequenza è stata creata con l'opzione CACHE o se è stato specificato CACHE senza specificare la dimensione della cache. Se il valore specificato dalla dimensione della cache è maggiore del numero massimo di valori che può essere restituito dall'oggetto sequenza, viene ancora visualizzata la dimensione non ottenibile della cache.|  
|**system_type_id**|**tinyint non NULL**|ID del tipo di sistema per il tipo di dati dell'oggetto sequenza.|  
|**user_type_id**|**int non NULL**|ID del tipo di dati per l'oggetto sequenza, come definito dall'utente.|  
|**Precisione**|**tinyint non NULL**|Precisione massima del tipo di dati.|  
|**Scalabilità**|**tinyint non NULL**|Scala massima del tipo. La scala viene restituita insieme alla precisione per fornire agli utenti metadati completi. La scala è sempre 0 per gli oggetti sequenza perché sono consentiti solo i tipi integer.|  
|**Current_value**|**sql_variant non NULL**|Valore finale obbligato, Vale a dire, il valore restituito dall'esecuzione della funzione NEXT VALUE FOR o l'ultimo valore dall'esecuzione più recente di **sp_sequence_get_range** procedure. Restituisce il valore START WITH se la sequenza non è mai stata utilizzata.|  
|**is_exhausted**|**bit non NULL**|0 indica che è possibile generare più valori dalla sequenza. 1 indica che l'oggetto sequenza ha raggiunto il parametro MAXVALUE e che la sequenza non è impostata su CYCLE. La funzione NEXT VALUE FOR restituisce un errore finché la sequenza non viene riavviata tramite ALTER SEQUENCE.|  
  
## <a name="permissions"></a>Permissions  
 In [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e nelle versioni successive, la visibilità dei metadati nelle viste del catalogo è limitata alle entità a protezione diretta di cui l'utente è proprietario o per le quali dispone di autorizzazioni. Per altre informazioni, vedere [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Numeri di sequenza](../../relational-databases/sequence-numbers/sequence-numbers.md)   
 [CREATE SEQUENCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-sequence-transact-sql.md)   
 [ALTER SEQUENCE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-sequence-transact-sql.md)   
 [DROP SEQUENCE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-sequence-transact-sql.md)   
 [NEXT VALUE FOR &#40;Transact-SQL&#41;](../../t-sql/functions/next-value-for-transact-sql.md)   
 [sp_sequence_get_range &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-sequence-get-range-transact-sql.md)  
  
  
