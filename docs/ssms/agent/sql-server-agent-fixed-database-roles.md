---
title: Ruoli di database predefiniti di SQL Server Agent | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- roles [SQL Server], SQL Server Agent
- SQL Server Agent, roles
- SQLAgentUserRole database role
- SQLAgentReaderRole database role
- multiple roles
- security [SQL Server Agent], fixed database roles
- fixed database roles [SQL Server]
- SQLAgentOperatorRole database role
ms.assetid: 719ce56b-d6b2-414a-88a8-f43b725ebc79
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 7a2e658020afaa9910c0bd988efc6f0c528e499e
ms.sourcegitcommit: 50b60ea99551b688caf0aa2d897029b95e5c01f3
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/15/2018
ms.locfileid: "51697879"
---
# <a name="sql-server-agent-fixed-database-roles"></a>Ruoli di database predefiniti di SQL Server Agent
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> In [Istanza gestita di database SQL di Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) sono attualmente supportate la maggior parte delle funzionalità di SQL Server Agent, ma non tutte. Per informazioni dettagliate, vedere [Differenze T-SQL tra Istanza gestita del database SQL di Azure e SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Gli amministratori hanno a disposizione i seguenti ruoli predefiniti del database **msdb** , che consentono di controllare in modo più capillare l'accesso a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Sono previsti i seguenti ruoli, elencati a partire da quello che ha meno privilegi:  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
Quando gli utenti che non sono membri di questi ruoli sono connessi a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], il nodo di **SQL Server Agent** non è visibile in Esplora oggetti. Per poter usare **Agent, un utente deve essere membro di uno di questi ruoli di database predefiniti o membro del ruolo di server predefinito** sysadmin [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="permissions-of-sql-server-agent-fixed-database-roles"></a>Autorizzazioni dei ruoli di database predefiniti SQL Server Agent  
Le autorizzazioni dei ruoli di database [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent sono concentriche le une rispetto alle altre: i ruoli con privilegi di livello più alto ereditano le autorizzazioni dei ruoli con privilegi di livello più basso in oggetti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent (compresi avvisi, operatori, processi, pianificazioni e proxy). Se ad esempio ai membri del ruolo **SQLAgentUserRole** con privilegi di livello basso è stato concesso l'accesso a proxy_A, i membri di entrambi i ruoli **SQLAgentReaderRole** e **SQLAgentOperatorRole** hanno automaticamente accesso a questo proxy anche se l'accesso al proxy_A non è stato esplicitamente concesso. Ciò può avere implicazioni a livello di sicurezza e nelle sezioni seguenti verranno esaminate queste implicazioni ruolo per ruolo.  
  
### <a name="sqlagentuserrole-permissions"></a>Autorizzazioni per SQLAgentUserRole  
**SQLAgentUserRole** è il ruolo di database predefinito di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent con privilegi di livello più basso. Dispone di autorizzazioni solo su operatori, processi locali e pianificazioni di processi. I membri del ruolo **SQLAgentUserRole** hanno autorizzazioni solo sui processi locali e le pianificazioni di processo di cui sono proprietari. Essi non possono utilizzare processi multiserver (processi per server master e di destinazione) e non possono modificare la proprietà dei processi per ottenere l'accesso a processi di cui non sono già proprietari. I membri del ruolo**SQLAgentUserRole** possono visualizzare l'elenco dei proxy disponibili solo nella finestra di dialogo **Proprietà passaggio processo** di [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Ai membri del ruolo **SQLAgentUserRole** è visibile solo il nodo **Processi** in Esplora oggetti di [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
> [!IMPORTANT]  
> Si consiglia di considerare le implicazioni di sicurezza prima di concedere l'accesso proxy ai membri di **Agentdatabaseroles** **di**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. I ruoli **SQLAgentReaderRole** e **SQLAgentOperatorRole** sono automaticamente membri del ruolo **SQLAgentUserRole**. Ciò significa che i membri dei ruoli **SQLAgentReaderRole** e **SQLAgentOperatorRole** hanno accesso a tutti i proxy [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent che sono stati concessi al ruolo **SQLAgentUserRole** e possono usare questi proxy.  
  
Nella tabella seguente vengono riepilogate le autorizzazioni per il ruolo **SQLAgentUserRole** su oggetti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
|Azione|Operatori|Processi locali<br /><br />(solo processi di proprietà)|Pianificazioni di processi<br /><br />(solo pianificazioni di proprietà)|Proxy|  
|----------|-------------|-----------------------------------|-------------------------------------------|-----------|  
|Creazione/modifica/eliminazione|no|Sì<br /><br />Non è possibile modificare la proprietà del processo.|Sì|no|  
|Visualizzazione di un elenco (enumerazione)|Sì<br /><br />È possibile ottenere un elenco degli operatori disponibili da usare in **sp_notify_operator** e nella finestra di dialogo **Proprietà processo** di Management Studio.|Sì|Sì|Sì<br /><br />L'elenco dei proxy è disponibile solo nella finestra di dialogo **Proprietà passaggio processo** di Management Studio.|  
|Abilitazione/disabilitazione|no|Sì|Sì|Non applicabile|  
|Visualizzazione di proprietà|no|Sì|Sì|no|  
|Esecuzione/arresto/avvio|Non applicabile|Sì|Non applicabile|Non applicabile|  
|Visualizzazione cronologia processo|Non applicabile|Sì|Non applicabile|Non applicabile|  
|Eliminazione cronologia processo|Non applicabile|no<br /><br />Ai membri del ruolo **SQLAgentUserRole** deve essere concessa esplicitamente un'autorizzazione EXECUTE su **sp_purge_jobhistory** per l'eliminazione della cronologia processo di cui sono proprietari. I membri di tale ruolo non possono eliminare la cronologia di altri processi.|Non applicabile|Non applicabile|  
|Collegamento/scollegamento|Non applicabile|Non applicabile|Sì|Non applicabile|  
  
### <a name="sqlagentreaderrole-permissions"></a>Autorizzazioni per SQLAgentReaderRole  
Il ruolo**SQLAgentReaderRole** include tutte le autorizzazioni per **SQLAgentUserRole** e le autorizzazioni per visualizzare l'elenco dei processi multiserver disponibili, le loro proprietà e la loro cronologia. I membri di questo ruolo possono visualizzare non solo i processi e le pianificazioni di processo di cui sono proprietari ma anche l'elenco di tutti i processi, le pianificazioni di processo e le relative proprietà. I membri del ruolo**SQLAgentReaderRole** non possono modificare la proprietà dei processi per ottenere accesso a processi di cui non sono già proprietari. In Esplora oggetti di [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] i membri del ruolo **SQLAgentReaderRole** possono vedere solo il nodo **Processi**.  
  
> [!IMPORTANT]  
> Si consiglia di considerare le implicazioni di sicurezza prima di concedere l'accesso proxy ai membri di **Agentdatabaseroles** **di**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. I membri del ruolo **SQLAgentReaderRole** sono automaticamente membri del ruolo **SQLAgentUserRole**. Ciò significa che i membri del ruolo **SQLAgentReaderRole** hanno accesso a tutti i proxy di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent che sono stati concessi al ruolo **SQLAgentUserRole** e possono usare questi proxy.  
  
Nella tabella seguente vengono riepilogate le autorizzazioni per il ruolo **SQLAgentReaderRole** su oggetti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
|Azione|Operatori|Processi locali|Processi multiserver|Pianificazioni di processi|Proxy|  
|----------|-------------|--------------|--------------------|-----------------|-----------|  
|Creazione/modifica/eliminazione|no|Sì  (solo processi di proprietà)<br /><br />Non è possibile modificare la proprietà del processo.|no|Sì (solo pianificazioni di proprietà)|no|  
|Visualizzazione di un elenco (enumerazione)|Sì<br /><br />È possibile ottenere un elenco degli operatori disponibili da usare in **sp_notify_operator** e nella finestra di dialogo **Proprietà processo** di Management Studio.|Sì|Sì|Sì|Sì<br /><br />L'elenco dei proxy è disponibile solo nella finestra di dialogo **Proprietà passaggio processo** di Management Studio.|  
|Abilitazione/disabilitazione|no|Sì (solo processi di proprietà)|no|Sì (solo pianificazioni di proprietà)|Non applicabile|  
|Visualizzazione di proprietà|no|Sì|Sì|Sì|no|  
|Modifica di proprietà|no|Sì (solo processi di proprietà)|no|Sì (solo pianificazioni di proprietà)|no|  
|Esecuzione/arresto/avvio|Non applicabile|Sì (solo processi di proprietà)|no|Non applicabile|Non applicabile|  
|Visualizzazione cronologia processo|Non applicabile|Sì|Sì|Non applicabile|Non applicabile|  
|Eliminazione cronologia processo|Non applicabile|no<br /><br />Ai membri del ruolo **SQLAgentReaderRole** deve essere concessa esplicitamente un'autorizzazione EXECUTE su **sp_purge_jobhistory** per l'eliminazione della cronologia processo di cui sono proprietari. I membri di tale ruolo non possono eliminare la cronologia di altri processi.|no|Non applicabile|Non applicabile|  
|Collegamento/scollegamento|Non applicabile|Non applicabile|Non applicabile|Sì (solo pianificazioni di proprietà)|Non applicabile|  
  
### <a name="sqlagentoperatorrole-permissions"></a>Autorizzazioni per SQLAgentOperatorRole  
**SQLAgentOperatorRole** è il ruolo di database predefinito di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent con privilegi di livello più alto. E include tutte le autorizzazioni dei ruoli **SQLAgentUserRole** e **SQLAgentReaderRole**. I membri di questo ruolo possono inoltre visualizzare proprietà di operatori e proxy e possono enumerare i proxy e gli avvisi disponibili sul server.  
  
I membri del ruolo**SQLAgentOperatorRole** hanno autorizzazioni aggiuntive su pianificazioni e processi locali. Possono eseguire, arrestare o avviare tutti i processi locali e possono eliminare la cronologia processo di qualsiasi processo locale del server. Possono inoltre attivare o disabilitare tutte le pianificazioni e i processi locali del server. Per abilitare o disabilitare processi locali o pianificazioni, i membri di questo ruolo devono usare le stored procedure **sp_update_job** e **sp_update_schedule**. I membri del ruolo **@enabled** possono specificare solo i parametri che definiscono il nome o l'ID del processo o della pianificazione e il parametro **SQLAgentOperatorRole**. Se si specifica un qualsiasi altro parametro, l'esecuzione di queste stored procedure non viene portata a termine. I membri del ruolo**SQLAgentOperatorRole** non possono modificare la proprietà dei processi per ottenere l'accesso a processi di cui non sono già proprietari.  
  
I nodi **Processi**, **Avvisi**, **Operatori**e **Proxy** inclusi in Esplora oggetti di [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] sono visibili a membri del ruolo **SQLAgentOperatorRole**. Solo il nodo **Log degli errori** non è visibile ai membri di questo ruolo.  
  
> [!IMPORTANT]  
> Si consiglia di considerare le implicazioni di sicurezza prima di concedere l'accesso proxy ai membri di **Agentdatabaseroles** **di**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. I membri del ruolo **SQLAgentOperatorRole** sono automaticamente membri dei ruoli **SQLAgentUserRole** e **SQLAgentReaderRole**. Ciò significa che i membri del ruolo **SQLAgentOperatorRole** hanno accesso a tutti i proxy di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent che sono stati concessi al ruolo **SQLAgentUserRole** o **SQLAgentReaderRole** e possono usare questi proxy.  
  
Nella tabella seguente vengono riepilogate le autorizzazioni per il ruolo **SQLAgentOperatorRole** su oggetti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
|Azione|Avvisi|Operatori|Processi locali|Processi multiserver|Pianificazioni di processi|Proxy|  
|----------|----------|-------------|--------------|--------------------|-----------------|-----------|  
|Creazione/modifica/eliminazione|no|no|Sì  (solo processi di proprietà)<br /><br />Non è possibile modificare la proprietà del processo.|no|Sì (solo pianificazioni di proprietà)|no|  
|Visualizzazione di un elenco (enumerazione)|Sì|Sì<br /><br />È possibile ottenere un elenco degli operatori disponibili da usare in **sp_notify_operator** e nella finestra di dialogo **Proprietà processo** di Management Studio.|Sì|Sì|Sì|Sì|  
|Abilitazione/disabilitazione|no|no|Sì<br /><br />**SQLAgentOperatorRole** possono abilitare o disabilitare processi locali di cui non sono proprietari usando la stored procedure **sp_update_job** e specificando valori per i parametri **@enabled** e **@job_id** (o **@job_name**). Se un membro di questo ruolo specifica un qualsiasi altro parametro per questa stored procedure, la sua esecuzione non viene portata a termine.|no|Sì<br /><br />**SQLAgentOperatorRole** possono abilitare o disabilitare pianificazioni di cui non sono proprietari usando la stored procedure **sp_update_schedule** e specificando valori per i parametri **@enabled** e **@schedule_id** (o **@name**). Se un membro di questo ruolo specifica un qualsiasi altro parametro per questa stored procedure, la sua esecuzione non viene portata a termine.|Non applicabile|  
|Visualizzazione di proprietà|Sì|Sì|Sì|Sì|Sì|Sì|  
|Modifica di proprietà|no|no|Sì (solo processi di proprietà)|no|Sì (solo pianificazioni di proprietà)|no|  
|Esecuzione/arresto/avvio|Non applicabile|Non applicabile|Sì|no|Non applicabile|Non applicabile|  
|Visualizzazione cronologia processo|Non applicabile|Non applicabile|Sì|Sì|Non applicabile|Non applicabile|  
|Eliminazione cronologia processo|Non applicabile|Non applicabile|Sì|no|Non applicabile|Non applicabile|  
|Collegamento/scollegamento|Non applicabile|Non applicabile|Non applicabile|Non applicabile|Sì (solo pianificazioni di proprietà)|Non applicabile|  
  
## <a name="assigning-users-multiple-roles"></a>Assegnazione di più ruoli a utenti  
I membri del ruolo predefinito del server **sysadmin** dispongono di accesso a tutte le funzionalità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Se un utente non è membro del ruolo **sysadmin** ma è membro di più di un ruolo predefinito di database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, è importante tenere presente il modello ad autorizzazioni concentriche di questi ruoli. Poiché i ruoli con privilegi di livello più alto comprendono sempre tutte le autorizzazioni dei ruoli con privilegi di livello più basso, a un utente che è membro di più di un ruolo vengono concesse automaticamente le autorizzazioni associate al ruolo con privilegi di livello più alto di cui questo utente è membro.  
  
## <a name="see-also"></a>Vedere anche  
[Implementazione della sicurezza di SQL Server Agent](../../ssms/agent/implement-sql-server-agent-security.md)  
[sp_update_job (Transact-SQL)](https://msdn.microsoft.com/cbdfea38-9e42-47f3-8fc8-5978b82e2623)  
[sp_update_schedule (Transact-SQL)](https://msdn.microsoft.com/97b3119b-e43e-447a-bbfb-0b5499e2fefe)  
[sp_notify_operator (Transact-SQL)](https://msdn.microsoft.com/c440f5c9-9884-4196-b07c-55d87afb17c3)  
[sp_purge_jobhistory (Transact-SQL)](https://msdn.microsoft.com/237f9bad-636d-4262-9bfb-66c034a43e88)  
  
