---
title: Sys.database_event_sessions (Database SQL di Azure) | Documenti Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: 
ms.prod_service: sql-database
ms.reviewer: 
ms.service: sql-database
ms.component: system-catalog-views
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 02c2cd71-d35e-4d4c-b844-92b240f768f4
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3f27efef3db486246e1a7efe162c427a94f30243
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/17/2017
---
# <a name="sysdatabaseeventsessions-azure-sql-database"></a>Sys.database_event_sessions (Database SQL di Azure)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Elenca tutte le definizioni di sessione di eventi presenti nel database corrente, in [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
> [!NOTE]  
>  La vista del catalogo simile denominata `sys.server_event_sessions` si applica solo a [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
||  
|-|  
|**Si applica a**: [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]e a tutte le versioni successive.|  
  
|Nome colonna|Tipo di dati|Description|  
|-----------------|---------------|-----------------|  
|event_session_id|**int**|ID univoco della sessione dell'evento. Non ammette i valori Null.|  
|name|**sysname**|Nome definito dall'utente per identificare la sessione eventi. nome è univoco. Non ammette i valori Null.|  
|event_retention_mode|**nchar (1)**|Determina la modalità di gestione della perdita di eventi. L'impostazione predefinita è S. Non sono ammessi valori Null. I valori validi sono i seguenti:<br /><br /> S. Mapping su event_retention_mode_desc = ALLOW_SINGLE_EVENT_LOSS<br /><br /> M. Mapping su event_retention_mode_desc = ALLOW_MULTIPLE_EVENT_LOSS<br /><br /> N. Mapping su event_retention_mode_desc = NO_EVENT_LOSS|  
|event_retention_mode_desc|**sysname**|Descrive la modalità di gestione della perdita di eventi. L'impostazione predefinita è ALLOW_SINGLE_EVENT_LOSS. Non ammette i valori Null. I valori validi sono i seguenti:<br /><br /> ALLOW_SINGLE_EVENT_LOSS. Gli eventi possono essere persi dalla sessione. Gli eventi singoli vengono eliminati solo quando tutti i buffer dell'evento sono completi. La perdita di eventi singoli quando i buffer sono completi lascia spazio a caratteristiche di prestazioni accettabili di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], minimizzando la perdita nel flusso dell'evento elaborato.<br /><br /> ALLOW_MULTIPLE_EVENT_LOSS. I buffer di eventi completi possono essere persi dalla sessione. Il numero di eventi persi dipende dalla dimensione della memoria allocata alla sessione, dalla partizione della memoria e dalla dimensione degli eventi nel buffer. Questa opzione minimizza l'impatto sulle prestazioni nel server quando i buffer degli eventi vengono completati rapidamente. Tuttavia, molti eventi della sessione possono essere perduti..<br /><br /> NO_EVENT_LOSS. Non è consentita alcuna perdita di eventi. Questa opzione assicura che tutti gli eventi generati siano mantenuti. L'utilizzo di questa opzione forza tutte le attività che attivano eventi ad aspettare fino a che lo spazio è disponibile in un buffer degli eventi. Ciò può determinare una riduzione rilevabile del livello delle prestazioni quando la sessione dell'evento è attiva.|  
|max_dispatch_latency|**int**|Quantità di tempo, espresso in millisecondi, durante il quale gli eventi verranno trattenuti in memoria prima di essere resi disponibili alle destinazioni della sessione. I valori validi sono compresi tra 1 e 2147483648 e -1. Un valore -1 indica che la latenza di recapito è infinita. Ammette i valori Null.|  
|max_memory|**int**|La quantità di memoria allocata alla sessione per la memorizzazione degli eventi nel buffer. Il valore predefinito è 4 MB. Ammette i valori Null.|  
|max_event_size|**int**|La quantità di memoria riservata per eventi che non si adattano ai buffer di sessione dell'evento. Se max_event_size supera la dimensione del buffer calcolata, due buffer aggiuntivi di max_event_size sono allocati alla sessione dell'evento. Ammette i valori Null.|  
|memory_partition_mode|**nchar (1)**|Percorso della memoria dove i buffer dell'evento vengono creati. La modalità della partizione predefinita è G. Non ammette valori Null. MEMORY_PARTITION_MODE è uno di:<br /><br /> G - NONE<br /><br /> C - PER_CPU<br /><br /> N - PER_NODE|  
|memory_partition_mode_desc|**sysname**|Il valore predefinito è NONE. Non ammette i valori Null. I valori validi sono i seguenti:<br /><br /> NONE. All'interno di un'istanza di SQL Server viene creato un unico set di buffer.<br /><br /> PER_CPU. Viene creato un set di buffer per CPU.<br /><br /> PER_NODE. Viene creato un set di buffer per ogni nodo NUMA (non-uniform memory access).|  
|track_causality|**bit**|Abilita o disabilita il rilevamento della causalità. Se è impostato su 1 (ON), il rilevamento viene abilitato e gli eventi correlati su connessioni server diverse possono essere correlati. L'impostazione predefinita è 0 (OFF). Non ammette i valori Null.|  
|startup_state|**bit**|Valore che determina se la sessione viene avviata automaticamente all'avvio del server. Il valore predefinito è 0. Non ammette i valori Null. È uno dei seguenti valori:<br /><br /> 0 (OFF). La sessione non inizia all'avvio del server.<br /><br /> 1 (ON). La sessione dell'evento inizia all'avvio del server.|  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'autorizzazione VIEW SERVER STATE per il server.  
  
  