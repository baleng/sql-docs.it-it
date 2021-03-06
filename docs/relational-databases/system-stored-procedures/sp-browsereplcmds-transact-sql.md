---
title: sp_browsereplcmds (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sp_browsereplcmds_TSQL
- sp_browsereplcmds
helpviewer_keywords:
- sp_browsereplcmds
ms.assetid: 30abcb41-1d18-4f43-a692-4c80914c0450
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3e3884ba1d35a488319ee9ba32e584450b300eda
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/01/2018
ms.locfileid: "47670479"
---
# <a name="spbrowsereplcmds-transact-sql"></a>sp_browsereplcmds (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce un set di risultati in una versione leggibile dei comandi replicati archiviati nel database di distribuzione e viene utilizzata come strumento di diagnostica. La stored procedure viene eseguita nel database di distribuzione del server di distribuzione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_browsereplcmds [ [ @xact_seqno_start = ] 'xact_seqno_start' ]  
    [ , [ @xact_seqno_end = ] 'xact_seqno_end' ]   
    [ , [ @originator_id = ] 'originator_id' ]  
    [ , [ @publisher_database_id = ] 'publisher_database_id' ]  
    [ , [ @article_id = ] 'article_id' ]  
    [ , [ @command_id= ] command_id ]  
    [ , [ @agent_id = ] agent_id ]  
    [ , [ @compatibility_level = ] compatibility_level ]  
```  
  
## <a name="arguments"></a>Argomenti  
 [  **@xact_seqno_start =**] **'***xact_seqno_start***'**  
 Indica il numero minimo di sequenza esatto da restituire. *xact_seqno_start* viene **nchar(22)**, con un valore predefinito è 0x00000000000000000000.  
  
 [  **@xact_seqno_end =**] **'***xact_seqno_end***'**  
 Indica il numero massimo di sequenza esatto da restituire. *xact_seqno_end* viene **nchar(22)**, con un valore predefinito è 0xFFFFFFFFFFFFFFFFFFFF.  
  
 [  **@originator_id =**] **'***originator_id***'**  
 Specifica se i comandi con l'oggetto specificato *originator_id* vengono restituiti. *originator_id* viene **int**, con un valore predefinito è NULL.  
  
 [  **@publisher_database_id =**] **'***publisher_database_id***'**  
 Specifica se i comandi con l'oggetto specificato *publisher_database_id* vengono restituiti. *publisher_database_id* viene **int**, con un valore predefinito è NULL.  
  
 [  **@article_id =**] **'***article_id***'**  
 Specifica se i comandi con l'oggetto specificato *article_id* vengono restituiti. *article_id* viene **int**, con un valore predefinito è NULL.  
  
 [  **@command_id =**] *command_id*  
 È il percorso del comando nel [MSrepl_commands &#40;Transact-SQL&#41; ](../../relational-databases/system-tables/msrepl-commands-transact-sql.md) da decodificare. *command_id* viene **int**, con un valore predefinito è NULL. Se specificato, tutti gli altri parametri devono essere specificati anche, e *xact_seqno_start*deve essere identico al *xact_seqno_end*.  
  
 [  **@agent_id =**] *agent_id*  
 Indica che vengono restituiti solo i comandi per un agente di replica specifico. *agent_id* viene **int**, con un valore predefinito NULL.  
  
 [  **@compatibility_level =**] *compatibility_level*  
 È la versione di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in cui le *compatibility_level* viene **int**, con valore predefinito è 9000000.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="result-sets"></a>Set di risultati  
  
|Nome colonna|Tipo di dati|Description|  
|-----------------|---------------|-----------------|  
|**xact_seqno**|**varbinary(16)**|Numero di sequenza del comando.|  
|**originator_srvname**|**sysname**|Server in cui ha origine la transazione.|  
|**originator_db**|**sysname**|Database in cui ha origine la transazione.|  
|**article_id**|**int**|ID dell'articolo.|  
|**type**|**int**|Tipo di comando.|  
|**che**|**bit**|Indica se si tratta di un comando parziale.|  
|**hashKey**|**int**|Solo per uso interno.|  
|**originator_publication_id**|**int**|ID della pubblicazione in cui ha origine la transazione.|  
|**originator_db_version**|**int**|Versione del database in cui ha origine la transazione.|  
|**originator_lsn**|**varbinary(16)**|Identifica il numero di sequenza del file di log (LSN) per il comando nella pubblicazione di origine. Utilizzato nella replica transazionale peer-to-peer.|  
|**comando**|**nvarchar(1024)**|Comando [!INCLUDE[tsql](../../includes/tsql-md.md)].|  
|**command_id**|**int**|ID del comando nel [MSrepl_commands](../../relational-databases/system-tables/msrepl-commands-transact-sql.md).|  
  
 È possibile suddividere i comandi lunghi in più righe nei set di risultati.  
  
## <a name="remarks"></a>Note  
 **sp_browsereplcmds** viene utilizzata nella replica transazionale.  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** fissa ruolo del server o i membri del **db_owner** oppure **replmonitor** ruoli predefiniti del database nel database di distribuzione possono eseguire **sp_browsereplcmds**.  
  
## <a name="see-also"></a>Vedere anche  
 [sp_replcmds &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md)   
 [sp_replshowcmds &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replshowcmds-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
