---
title: sp_addsynctriggers (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sp_addsynctriggers_TSQL
- sp_addsynctriggers
helpviewer_keywords:
- sp_addsynctriggers
ms.assetid: e37d0c3b-19bf-4719-9535-96ba361372b3
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c69681e396065f1881ff9ea81468ef85c8b26da4
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/01/2018
ms.locfileid: "47799719"
---
# <a name="spaddsynctriggers-transact-sql"></a>sp_addsynctriggers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Crea nel Sottoscrittore trigger utilizzati con tutti i tipi di sottoscrizioni aggiornabili, ovvero ad aggiornamento immediato, ad aggiornamento in coda e ad aggiornamento immediato sostituito dall'aggiornamento in coda in caso di errore. Questa stored procedure viene eseguita nel database di sottoscrizione del Sottoscrittore.  
  
> [!IMPORTANT]  
>  Il [sp_script_synctran_commands](../../relational-databases/system-stored-procedures/sp-script-synctran-commands-transact-sql.md) procedura deve essere utilizzata al posto di **sp_addsynctrigger**. [sp_script_synctran_commands](../../relational-databases/system-stored-procedures/sp-script-synctran-commands-transact-sql.md) genera uno script che contiene il **sp_addsynctrigger** chiamate.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_addsynctriggers [ @sub_table = ] 'sub_table'  
        , [ @sub_table_owner = ] 'sub_table_owner'  
        , [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
        , [ @publication = ] 'publication'   
        , [ @ins_proc = ] 'ins_proc'   
        , [ @upd_proc = ] 'upd_proc'   
        , [ @del_proc = ] 'del_proc'   
        , [ @cftproc = ] 'cftproc'  
        , [ @proc_owner = ] 'proc_owner'  
    [ , [ @identity_col = ] 'identity_col' ]  
    [ , [ @ts_col = ] 'timestamp_col' ]  
    [ , [ @filter_clause = ] 'filter_clause' ]   
        , [ @primary_key_bitmap = ] 'primary_key_bitmap'  
    [ , [ @identity_support = ] identity_support ]  
    [ , [ @independent_agent = ] independent_agent ]  
        , [ @distributor = ] 'distributor'   
    [ , [ @pubversion = ] pubversion  
```  
  
## <a name="arguments"></a>Argomenti  
 [  **@sub_table=**] **'***sub_table***'**  
 Nome della tabella del Sottoscrittore. *sub_table* viene **sysname**, non prevede alcun valore predefinito.  
  
 [  **@sub_table_owner=**] **'***sub_table_owner***'**  
 Nome del proprietario della tabella del Sottoscrittore. *sub_table_owner* viene **sysname**, non prevede alcun valore predefinito.  
  
 [  **@publisher=**] **'***publisher***'**  
 Nome del server di pubblicazione. *server di pubblicazione* viene **sysname**, non prevede alcun valore predefinito.  
  
 [ **@publisher_db=**] **'***publisher_db***'**  
 Nome del database del server di pubblicazione. *publisher_db* viene **sysname**, non prevede alcun valore predefinito. Se è NULL, viene utilizzato il database corrente.  
  
 [  **@publication=**] **'***pubblicazione***'**  
 Nome della pubblicazione. *pubblicazione* viene **sysname**, non prevede alcun valore predefinito.  
  
 [  **@ins_proc=**] **'***ins_proc***'**  
 Nome della stored procedure che supporta gli inserimenti tramite la sincronizzazione delle transazioni nel server di pubblicazione. *ins_proc* viene **sysname**, non prevede alcun valore predefinito.  
  
 [  **@upd_proc=**] **'***upd_proc***'**  
 Nome della stored procedure che supporta gli aggiornamenti tramite la sincronizzazione delle transazioni nel server di pubblicazione. *ins_proc* viene **sysname**, non prevede alcun valore predefinito.  
  
 [  **@del_proc=**] **'***del_proc***'**  
 Nome della stored procedure che supporta le eliminazioni tramite la sincronizzazione delle transazioni nel server di pubblicazione. *ins_proc* viene **sysname**, non prevede alcun valore predefinito.  
  
 [  **@cftproc =** ] **'***cftproc***'**  
 Nome della procedura a generazione automatica utilizzata dalle pubblicazioni che consentono l'aggiornamento in coda. *cftproc* viene **sysname**, non prevede alcun valore predefinito. Nel caso di pubblicazioni che consentono l'aggiornamento immediato, questo valore è NULL. Questo parametro viene applicato alle pubblicazioni che consentono l'aggiornamento in coda (aggiornamento in coda e aggiornamento immediato sostituito dall'aggiornamento in coda in caso di errore).  
  
 [  **@proc_owner =** ] **'***proc_owner***'**  
 Specifica l'account utente utilizzato nel server di pubblicazione per la creazione di tutte le stored procedure a generazione automatica per l'aggiornamento della pubblicazione (aggiornamento in coda e/o immediato). *proc_owner* viene **sysname** non prevede alcun valore predefinito.  
  
 [  **@identity_col=**] **'***identity_col***'**  
 Nome della colonna Identity nel server di pubblicazione. *identity_col* viene **sysname**, con un valore predefinito è NULL.  
  
 [  **@ts_col=**] **'***timestamp_col***'**  
 È il nome del **timestamp** colonna nel server di pubblicazione. *timestamp_col* viene **sysname**, con un valore predefinito è NULL.  
  
 [  **@filter_clause=**] **'***filter_clause***'**  
 Clausola di restrizione (WHERE) che definisce un filtro orizzontale. Quando si specifica la clausola di restrizione, omettere la parola chiave WHERE. *filter_clause*viene **nvarchar (4000)**, con un valore predefinito è NULL.  
  
 [  **@primary_key_bitmap =**] **'***primary_key_bitmap***'**  
 Mappa di bit delle colonne chiave primaria nella tabella. *primary_key_bitmap* viene **varbinary(4000**, non prevede alcun valore predefinito.  
  
 [  **@identity_support =** ] *identity_support*  
 Abilita e disabilita la gestione automatica degli intervalli di valori Identity quando viene utilizzato l'aggiornamento in coda. *identity_support* è un **bit**, il valore predefinito è **0**. **0** indica che non siano presenti identità intervalli di valori, il supporto **1** consente degli intervalli di valori identity automatico.  
  
 [  **@independent_agent =** ] *independent_agent*  
 Specifica se è disponibile un solo agente di distribuzione (agente indipendente) per la pubblicazione oppure un agente di distribuzione per ogni coppia database di pubblicazione/database di sottoscrizione (agente condiviso). Questo valore è determinato dal valore della proprietà independent_agent della pubblicazione definito nel server di pubblicazione. *independent_agent* è di tipo bit e il valore predefinito **0**. Se **0**, l'agente è un agente condiviso. Se **1**, l'agente è un agente indipendente.  
  
 [  **@distributor =** ] **'***distributore***'**  
 Nome del server di distribuzione. *server di distribuzione* viene **sysname**, non prevede alcun valore predefinito.  
  
 [ **@pubversion**=] *pubversion*  
 Indica la versione del server di pubblicazione. *pubversion* viene **int**, con un valore predefinito è 1. **1** significa che è la versione di server di pubblicazione [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] Service Pack 2 o precedente. **2** significa che il server di pubblicazione [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] Service Pack 3 (SP3) o versione successiva. *pubversion* deve essere impostata esplicitamente su **2** quando la versione del server di pubblicazione è [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] SP3 o versione successiva.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 **sp_addsynctriggers** viene usato dall'agente di distribuzione come parte dell'inizializzazione della sottoscrizione. In genere, non viene eseguita dagli utenti, ma può risultare utile se l'utente deve configurare una sottoscrizione nosync in modo manuale.  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server oppure **db_owner** ruolo predefinito del database possono eseguire **sp_addsynctriggers**.  
  
## <a name="see-also"></a>Vedere anche  
 [Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)   
 [sp_script_synctran_commands &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-script-synctran-commands-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
