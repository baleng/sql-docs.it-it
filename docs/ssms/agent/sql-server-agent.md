---
title: SQL Server Agent | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL Server Agent, about SQL Server Agent
- automatic administration steps
ms.assetid: 8d1dc600-aabb-416f-b3af-fbc9fccfd0ec
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 0c9be76ca64a4df24cca399308244c5bc4c28e0d
ms.lasthandoff: 04/11/2017

---
# <a name="sql-server-agent"></a>SQL Server Agent
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent è un servizio di Microsoft Windows per l'esecuzione di attività amministrative pianificate, denominate *processi* in [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)].  
  
**Contenuto dell'argomento**  
  
-   [Vantaggi di SQL Server Agent](#Benefits)  
  
-   [Componenti di SQL Server Agent](#Components)  
  
-   [Sicurezza per l'amministrazione di SQL Server Agent](#Security)  
  
## <a name="Benefits"></a>Vantaggi di SQL Server Agent  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent viene utilizzato [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] . I processi sono costituiti da uno o più passaggi, ciascuno dei quali contiene un'attività, ad esempio il backup di un database.  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent è in grado di eseguire un processo incluso in una pianificazione, in risposta a un evento specifico, oppure su richiesta. Se, ad esempio, l'esigenza è quella di eseguire il backup di tutti i server aziendali ogni sera in orario non lavorativo, è possibile automatizzare questa attività, Pianificare l'esecuzione del backup dal lunedì al venerdì dopo le 22.00. In caso di problemi durante l'operazione, SQL Server Agent potrà registrare l'evento e inviarne notifica all'utente.  
  
> [!NOTE]  
> Per impostazione predefinita, all'installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] il servizio [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] Agent viene disabilitato, a meno che l'utente non scelga esplicitamente l'avvio automatico del servizio.  
  
## <a name="Components"></a>Componenti di SQL Server Agent  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent utilizza i componenti seguenti per definire le attività da eseguire, quando eseguirle e come fornire informazioni in merito alla riuscita o meno delle attività.  
  
### <a name="jobs"></a>processi  
Un *processo* è una serie specificata di azioni eseguite da [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent. I processi consentono la definizione di un'attività amministrativa eseguibile una o più volte e il monitoraggio della riuscita o non riuscita di ogni esecuzione. Un processo può essere eseguito su un server locale oppure su più server remoti.  
  
> [!IMPORTANT]  
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent che sono in esecuzione al momento di un evento di failover su un'istanza del cluster di failover [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] non riprendono dopo il failover su un altro nodo del cluster di failover. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] I processi di Agent che sono in esecuzione quando un nodo Hyper-V viene messo in pausa non riprendono se la pausa provoca un failover in un altro nodo. I processi che iniziano ma che non riescono a essere completati a causa di un evento di failover vengono registrati come avviati, ma non mostrano voci di log aggiuntive per il completamento o l'errore. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent in questi scenari sembrano non avere mai termine.  
  
È possibile eseguire i processi in diversi modi:  
  
-   In base a una o più pianificazioni.  
  
-   In risposta a uno o più avvisi.  
  
-   Tramite l'esecuzione della stored procedure sp_start_job.  
  
Ogni azione di un processo viene definita *passaggio del processo*. Un passaggio del processo, ad esempio, può essere costituito dall'esecuzione di un'istruzione [!INCLUDE[tsql](../../includes/tsql_md.md)] , di un pacchetto di [!INCLUDE[ssIS](../../includes/ssis_md.md)] o di un comando in un server Analysis Services. I passaggi del processo vengono gestiti come parte di un processo.  
  
Ogni passaggio del processo viene eseguito in un contesto di sicurezza specifico. Nel caso dei passaggi di processo che utilizzano [!INCLUDE[tsql](../../includes/tsql_md.md)], specificare l'istruzione EXECUTE AS per impostare il contesto di sicurezza corrispondente. Per gli altri tipi di passaggi di processo, utilizzare un account proxy per impostare il contesto di sicurezza corrispondente.  
  
### <a name="schedules"></a>Pianificazioni  
Una *pianificazione* specifica quando viene eseguito un processo. È possibile eseguire più processi sulla stessa pianificazione e applicare più di una pianificazione allo stesso processo. Una pianificazione consente di definire le condizioni seguenti relativi al momento in cui un processo viene eseguito:  
  
-   All'avvio di [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent.  
  
-   Quando l'utilizzo della CPU del computer corrisponde al livello di inattività.  
  
-   Una sola volta in corrispondenza di una data e un'ora specifiche.  
  
-   Su base periodica.  
  
Per altre informazioni, vedere [Creare e collegare le pianificazioni ai processi](../../ssms/agent/create-and-attach-schedules-to-jobs.md).  
  
### <a name="alerts"></a>Avvisi  
Un *avviso* è una risposta automatica a un evento specifico. Ad esempio, un evento può essere generato dall'avvio di un processo o dal raggiungimento della soglia specifica delle risorse di sistema. Le condizioni per la generazione di un avviso vengono definite dall'utente.  
  
Un avviso può rispondere a una delle condizioni seguenti:  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] eventi  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] condizioni delle prestazioni  
  
-   Eventi WMI (Microsoft Windows Management Instrumentation) nel computer in cui viene eseguito SQL Server Agent  
  
Un avviso può eseguire le azioni seguenti:  
  
-   Invio di una notifica a uno o più operatori  
  
-   Esecuzione di un processo  
  
Per altre informazioni, vedere [Avvisi](../../ssms/agent/alerts.md).  
  
### <a name="operators"></a>Operatori  
Un *operatore* definisce le informazioni di contatto relative al responsabile della manutenzione di una o più istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. In alcune organizzazioni le mansioni di operatore vengono assegnate a un unico dipendente. In organizzazioni con più server, tali mansioni possono essere ripartite tra più dipendenti. Un operatore non include informazioni di sicurezza e non definisce alcuna entità di sicurezza.  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] è in grado di segnalare gli avvisi agli operatori tramite:  
  
-   Posta elettronica  
  
-   Cercapersone (tramite posta elettronica)  
  
-   **net send**  
  
> [!NOTE]  
> Per inviare notifiche usando **Net Send**, è necessario che il servizio Windows Messenger sia avviato nel computer in cui si trova [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent.  
  
> [!IMPORTANT]  
> Le opzioni Cercapersone e **Net Send** verranno rimosse da [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent in una versione futura di [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Evitare pertanto di utilizzarle in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui sono state implementate.  
  
Per inviare notifiche agli operatori usando la posta elettronica o i cercapersone, è necessario configurare [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent per l'uso di Posta elettronica database. Per altre informazioni, vedere [Posta elettronica database](http://msdn.microsoft.com/en-us/9e4563dd-4799-4b32-a78a-048ea44a44c1).  
  
È possibile definire un operatore come alias assegnato a un gruppo di utenti. In questo modo la notifica può raggiungere contemporaneamente tutti i membri dell'alias. Per altre informazioni, vedere [Operatori](../../ssms/agent/operators.md).  
  
## <a name="Security"></a>Sicurezza per l'amministrazione di SQL Server Agent  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent utilizza i ruoli predefiniti del database **SQLAgentUserRole**, **SQLAgentReaderRole**e **SQLAgentOperatorRole** nel database **msdb** per controllare l'accesso a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent per gli utenti che non sono membri del ruolo predefinito del server **sysadmin** . Sottosistemi e proxy consentono agli amministratori del database di garantire l'esecuzione di tutti i passaggi di processo con le autorizzazioni minime necessarie all'esecuzione della relativa attività.  
  
### <a name="roles"></a>Ruoli  
I membri dei ruoli predefiniti del database **SQLAgentUserRole**, **SQLAgentReaderRole**e **SQLAgentOperatorRole** in **msdb**e i membri del ruolo predefinito del server **sysadmin** hanno accesso a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent. Un utente che non appartiene a nessuno di questi ruoli non può utilizzare [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent. Per altre informazioni sui ruoli usati da [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent, vedere [Implementazione della sicurezza di SQL Server Agent](../../ssms/agent/implement-sql-server-agent-security.md).  
  
### <a name="subsystems"></a>Sottosistemi  
Un sottosistema è un oggetto predefinito che rappresenta funzionalità disponibili per un passaggio di processo. Ogni proxy ha accesso a uno o più sottosistemi. I sottosistemi offrono sicurezza in quanto delimitano l'accesso alle funzionalità disponibili per un proxy. Ogni passaggio di processo viene eseguito nel contesto di un proxy, ad eccezione dei passaggi di processo [!INCLUDE[tsql](../../includes/tsql_md.md)] . [!INCLUDE[tsql](../../includes/tsql_md.md)] utilizzano il comando EXECUTE AS per impostare il contesto di sicurezza.  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] vengono definiti i sottosistemi inclusi nella tabella seguente:  
  
|Nome sottosistema|Description|  
|--------------|-----------|  
|Script Microsoft ActiveX|Esegue un passaggio di processo con script ActiveX.<br /><br />**Avviso** Il sottosistema di scripting ActiveX verrà rimosso da [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent in una versione futura di [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata.|  
|Sistema operativo (**CmdExec**)|Esegue un programma eseguibile.|  
|PowerShell|Esegue un passaggio di processo con script di PowerShell.|  
|Server di distribuzione repliche|Esegue un passaggio di processo tramite cui viene attivata l'utilità Agente distribuzione repliche.|  
|Merge repliche|Esegue un passaggio di processo tramite cui viene attivata l'utilità Agente merge repliche.|  
|Lettura coda repliche|Esegue un passaggio di processo tramite cui viene attivata l'utilità Agente di lettura coda repliche.|  
|Snapshot repliche|Esegue un passaggio di processo tramite cui viene attivata l'utilità Agente snapshot repliche.|  
|Lettura log repliche|Esegue un passaggio di processo tramite cui viene attivata l'utilità Agente lettura log repliche.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion_md.md)] Command|Esegue un comando di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion_md.md)] .|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion_md.md)] Query|Esegue una query di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion_md.md)] .|  
|[!INCLUDE[ssIS](../../includes/ssis_md.md)] esecuzione del pacchetto|Esegue un pacchetto [!INCLUDE[ssIS](../../includes/ssis_md.md)] .|  
  
> [!NOTE]  
> Poiché i passaggi di processo [!INCLUDE[tsql](../../includes/tsql_md.md)] non utilizzano proxy, non è disponibile alcun sottosistema di [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] per i passaggi di processo [!INCLUDE[tsql](../../includes/tsql_md.md)] .  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent applica restrizioni di sottosistema anche quando l'entità di sicurezza per il proxy disporrebbe dell'autorizzazione necessaria per eseguire l'attività nel passaggio di processo. Ad esempio, un proxy per un utente membro del ruolo predefinito del server sysadmin non può eseguire un passaggio di processo [!INCLUDE[ssIS](../../includes/ssis_md.md)] a meno che non abbia accesso al sottosistema di [!INCLUDE[ssIS](../../includes/ssis_md.md)] , anche se l'utente può eseguire pacchetti [!INCLUDE[ssIS](../../includes/ssis_md.md)] .  
  
### <a name="proxies"></a>Proxy  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent utilizza i proxy per la gestione dei contesti di sicurezza. È possibile utilizzare un proxy in più passaggi di processo. I membri del ruolo predefinito del server **sysadmin** sono autorizzati alla creazione di proxy.  
  
Ogni proxy corrisponde a una credenziale di sicurezza e può essere associato a un set di sottosistemi e a un set di account di accesso. È possibile utilizzare il proxy solo per i passaggi di processo che utilizzano un sottosistema associato al proxy stesso. Per creare un passaggio di processo che utilizza un proxy specifico, il proprietario del processo deve utilizzare un account di accesso associato a tale proxy oppure essere un membro di un ruolo con accesso senza limitazioni ai proxy. I membri del ruolo predefinito del server **sysadmin** hanno privilegi di accesso senza limitazioni ai proxy. I membri del ruolo **SQLAgentUserRole**, **SQLAgentReaderRole**o **SQLAgentOperatorRole** possono utilizzare solo i proxy ai quali sono specificamente autorizzati ad accedere. È necessario concedere l'accesso a proxy specifici a ogni utente membro di uno di questi ruoli predefiniti del database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent, in modo che possa creare passaggi di processo che utilizzano tali proxy.  
  
## <a name="related-tasks"></a>Attività correlate  
Per configurare [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent per automatizzare l'amministrazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] procedere come descritto di seguito:  
  
1.  Individuare le attività amministrative o gli eventi server che si verificano regolarmente e che possono essere gestiti a livello di programmazione. È possibile automatizzare un'attività se implica una sequenza prevedibile di passaggi e si verifica a un'ora specifica o in risposta a un evento specifico.  
  
2.  Definire un set di processi, pianificazioni, avvisi e operatori tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)], script [!INCLUDE[tsql](../../includes/tsql_md.md)] o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Management Objects (SMO). Per altre informazioni, vedere [Crea processi](../../ssms/agent/create-jobs.md).  
  
3.  Eseguire i processi [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent definiti.  
  
> [!NOTE]  
> Per un'istanza predefinita di [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], il nome del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] è SQLSERVERAGENT. Nel caso di istanze denominate il nome del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent è SQLAgent$*instancename*.  
  
Se si eseguono più istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], è possibile utilizzare l'amministrazione multiserver per automatizzare attività comuni a tutte le istanze. Per altre informazioni, vedere [Amministrazione automatizzata in un'organizzazione](../../ssms/agent/automated-administration-across-an-enterprise.md).  
  
Per un'introduzione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] , utilizzare le attività riportate di seguito.  
  
|Description|Argomento|  
|-----------|-----|  
|Viene descritto come configurare SQL Server Agent.|[Configurazione di SQL Server Agent](../../ssms/agent/configure-sql-server-agent.md)|  
|Viene descritto come avviare, arrestare e sospendere il servizio SQL Server Agent.|[Avvio, arresto o sospensione del servizio SQL Server Agent](../../ssms/agent/start-stop-or-pause-the-sql-server-agent-service.md)|  
|Descrive le considerazioni di cui tener conto per specificare un account per il servizio SQL Server Agent.|[Selezionare un account per il servizio SQL Server Agent](../../ssms/agent/select-an-account-for-the-sql-server-agent-service.md)|  
|Descrive come utilizzare il log degli errori di SQL Server Agent.|[Log degli errori di SQL Server Agent](../../ssms/agent/sql-server-agent-error-log.md)|  
|Viene descritto come utilizzare gli oggetti prestazioni.|[Utilizzo degli oggetti prestazioni](../../ssms/agent/use-performance-objects.md)|  
|Viene descritta la Creazione guidata piano di manutenzione, un'utilità che è possibile utilizzare per creare processi, avvisi e operatori allo scopo di automatizzare l'amministrazione di un'istanza di SQL Server.|[Utilizzare la Creazione guidata piano di manutenzione](http://msdn.microsoft.com/en-us/db65c726-9892-480c-873b-3af29afcee44)|  
|Viene descritto come utilizzare SQL Server Agent per automatizzare le attività amministrative.|[Automatizzazione delle attività amministrative &amp;#40;SQL Server Agent&amp;#41;](../../ssms/agent/automated-administration-tasks-sql-server-agent.md)|  
  
## <a name="see-also"></a>Vedere anche  
[Configurazione superficie di attacco](http://msdn.microsoft.com/en-us/f741169c-1453-4ad2-830b-bf2be27d712f)  
  
