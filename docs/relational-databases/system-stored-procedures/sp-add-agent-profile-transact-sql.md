---
title: sp_add_agent_profile (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sp_add_agent_profile
- sp_add_agent_profile_TSQL
helpviewer_keywords:
- sp_add_agent_profile
ms.assetid: 5c246a33-2c21-4a77-9c2a-a2c9f0c5dda1
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: b5c6b2c03ff9956a58bf7da8426c87b692d5f879
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/01/2018
ms.locfileid: "47670435"
---
# <a name="spaddagentprofile-transact-sql"></a>sp_add_agent_profile (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Crea un nuovo profilo per un agente di replica. Questa stored procedure viene eseguita in qualsiasi database del server di distribuzione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_add_agent_profile [ [ @profile_id= ] profile_id OUTPUT ]  
        , [ @profile_name= ] 'profile_name'   
        , [ @agent_type= ] 'agent_type' ]   
    [ , [ @profile_type= ] profile_type ]  
    [ , [ @description= ] 'description' ]  
    [ , [ @default= ] default ]  
```  
  
## <a name="arguments"></a>Argomenti  
 [ **@profile_id=** ] *profile_id*  
 ID associato al nuovo profilo inserito. *profile_id* viene **int** ed è un parametro OUTPUT facoltativo. Se viene specificato, il valore è impostato sull'ID del nuovo profilo.  
  
 [  **@profile_name=** ] **'***profile_name***'**  
 Nome del profilo. *profile_name* viene **sysname**, non prevede alcun valore predefinito.  
  
 [  **@agent_type=** ] **'***agent_type***'**  
 Tipo di agente di replica. *agent_type* viene **int**e non prevede alcun valore predefinito, i possibili valori sono i seguenti.  
  
|valore|Description|  
|-----------|-----------------|  
|**1**|agente snapshot|  
|**2**|Agente di lettura log|  
|**3**|Agente di distribuzione|  
|**4**|Agente di merge|  
|**9**|Agente di lettura coda|  
  
 [  **@profile_type=** ] *profile_type*  
 È il tipo di profilo. *profile_type* viene **int**, il valore predefinito è **1**.  
  
 **0** indica un profilo del sistema. **1** indica un profilo personalizzato. Solo i profili personalizzati possono essere creati utilizzando questa stored procedure. pertanto è l'unico valore valido **1**. Solo [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Crea profili del sistema.  
  
 [  **@description=** ] **'***descrizione***'**  
 Descrizione del profilo. *Descrizione* viene **nvarchar(3000)**, non prevede alcun valore predefinito.  
  
 [  **@default=** ] *predefinito*  
 Indica se il profilo è il valore predefinito per *agent_type * *.* *impostazione predefinita* viene **bit**, il valore predefinito è **0**. **1** indica che il profilo da aggiungere diventerà il nuovo profilo predefinito per l'agente specificato da *agent_type*.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 **sp_add_agent_profile** viene utilizzata nella replica snapshot, la replica transazionale e di tipo merge.  
  
 I profili agenti personalizzati vengono aggiunti con valori predefiniti dei parametri degli agenti. Uso [sp_change_agent_parameter &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-change-agent-parameter-transact-sql.md) per modificare questi valori predefiniti oppure [sp_add_agent_parameter &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-add-agent-parameter-transact-sql.md) per aggiungere altri parametri.  
  
 Quando **sp_add_agent_profile** viene eseguita, viene aggiunta una riga per il nuovo profilo personalizzato nel [MSagent_profiles &#40;Transact-SQL&#41; ](../../relational-databases/system-tables/msagent-profiles-transact-sql.md) tabella e i parametri predefiniti associati per questo oggetto profilo vengono aggiunti per il [MSagent_parameters &#40;Transact-SQL&#41; ](../../relational-databases/system-tables/msagent-parameters-transact-sql.md) tabella.  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server possono eseguire **sp_add_agent_profile**.  
  
## <a name="see-also"></a>Vedere anche  
 [Usare i profili agenti di replica](../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)   
 [Profili degli agenti di replica](../../relational-databases/replication/agents/replication-agent-profiles.md)   
 [la procedura sp_add_agent_parameter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-agent-parameter-transact-sql.md)   
 [sp_change_agent_parameter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-change-agent-parameter-transact-sql.md)   
 [sp_change_agent_profile &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-change-agent-profile-transact-sql.md)   
 [sp_drop_agent_parameter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-drop-agent-parameter-transact-sql.md)   
 [sp_drop_agent_profile &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-drop-agent-profile-transact-sql.md)   
 [sp_help_agent_parameter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-agent-parameter-transact-sql.md)   
 [sp_help_agent_profile &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-agent-profile-transact-sql.md)  
  
  
