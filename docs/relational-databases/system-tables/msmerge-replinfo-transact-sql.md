---
title: MSmerge_replinfo (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- MSmerge_replinfo_TSQL
- MSmerge_replinfo
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_replinfo system table
ms.assetid: b0924094-c0cc-49c1-869a-65be0d0465a0
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7257ce7d12fe4797c09836de2de45829500afd6b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/01/2018
ms.locfileid: "47790659"
---
# <a name="msmergereplinfo-transact-sql"></a>MSmerge_replinfo (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Il **MSmerge_replinfo** tabella contiene una riga per ogni sottoscrizione. In questa tabella viene tenuta traccia delle informazioni relative alle sottoscrizioni. Questa tabella è archiviata nei database di pubblicazione e di sottoscrizione.  
  
|Nome colonna|Tipo di dati|Description|  
|-----------------|---------------|-----------------|  
|**repid**|**uniqueidentifier**|ID univoco della replica.|  
|**use_interactive_resolver**|**bit**|Specifica se nella fase di riconciliazione dei conflitti viene utilizzato il sistema di risoluzione interattivo.<br /><br /> **0** = non non utilizzare il sistema di risoluzione interattivo.<br /><br /> **1** = Usa il sistema di risoluzione interattivo.|  
|**validation_level**|**int**|Tipo di convalida da eseguire sulla sottoscrizione. I possibili valori sono i seguenti:<br /><br /> **0** = Nessuna convalida.<br /><br /> **1** = convalida solo mediante conteggio delle righe.<br /><br /> **2** = convalida mediante conteggio delle righe e checksum.<br /><br /> **3** = conteggio delle righe e convalida mediante checksum binario.|  
|**resync_gen**|**bigint**|Numero di generazione utilizzato per la risincronizzazione della sottoscrizione. Un valore pari **-1** indica che la sottoscrizione non è contrassegnata per la risincronizzazione.|  
|**login_name**|**sysname**|Nome dell'utente che ha creato la sottoscrizione.|  
|**Nome host**|**sysname**|Valore utilizzato dal filtro di riga con parametri durante la generazione della partizione per la sottoscrizione.|  
|**merge_jobid**|**binary(16)**|ID del processo di merge della sottoscrizione.|  
|**sync_info**|**int**|Solo per uso interno.|  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle di replica &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Viste della replica &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
