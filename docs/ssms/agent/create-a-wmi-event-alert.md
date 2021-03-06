---
title: Creare un avviso per evento WMI | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- WMI event alerts [SQL Server Management Studio]
ms.assetid: b8c46db6-408b-484e-98f0-a8af3e7ec763
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: aed644bec059dadff338711634c6ec7d252498cd
ms.sourcegitcommit: 50b60ea99551b688caf0aa2d897029b95e5c01f3
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/15/2018
ms.locfileid: "51701850"
---
# <a name="create-a-wmi-event-alert"></a>Creare un avviso per evento WMI
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> In [Istanza gestita di database SQL di Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) sono attualmente supportate la maggior parte delle funzionalità di SQL Server Agent, ma non tutte. Per informazioni dettagliate, vedere [Differenze T-SQL tra Istanza gestita del database SQL di Azure e SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

In questo argomento viene descritto come creare un avviso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent che viene generato quando si verifica un evento specifico di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] monitorato dal provider WMI per eventi del server in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
Per informazioni sull'uso del provider WMI per il monitoraggio degli eventi del [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , vedere [Classi e proprietà del provider WMI per eventi del server](../../relational-databases/wmi-provider-server-events/wmi-provider-for-server-events-concepts.md). Per informazioni sulle autorizzazioni necessarie per ricevere notifiche di avviso per eventi WMI, vedere [Selezionare un account per il servizio SQL Server Agent](../../ssms/agent/select-an-account-for-the-sql-server-agent-service.md). Per altre informazioni su WQL, vedere [Utilizzo di WQL con il provider WMI per eventi del server](../../relational-databases/wmi-provider-server-events/using-wql-with-the-wmi-provider-for-server-events.md).  
  
**Contenuto dell'argomento**  
  
-   **Prima di iniziare:**  
  
    [Limitazioni e restrizioni](#Restrictions)  
  
    [Security](#Security)  
  
-   **Per creare un avviso per evento WMI utilizzando:**  
  
    [SQL Server Management Studio](#SSMSProcedure)  
  
    [Transact-SQL](#TsqlProcedure)  
  
## <a name="BeforeYouBegin"></a>Prima di iniziare  
  
### <a name="Restrictions"></a>Limitazioni e restrizioni  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] include un semplice strumento grafico per la gestione del sistema di avvisi ed è lo strumento consigliato per la configurazione di un'infrastruttura di avvisi.  
  
-   Gli eventi generati con la stored procedure **xp_logevent** si verificano nel database master. Pertanto, **xp_logevent** genera un avviso solo se **@database_name** per l'avviso è **'master'** o NULL.  
  
-   Sono supportati solo gli spazi dei nomi WMI sul computer in cui è in esecuzione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
### <a name="Security"></a>Security  
  
#### <a name="Permissions"></a>Permissions  
Per impostazione predefinita, solo i membri del ruolo predefinito del server **sysadmin** possono eseguire **sp_add_alert**.  
  
## <a name="SSMSProcedure"></a>Utilizzo di SQL Server Management Studio  
  
#### <a name="to-create-a-wmi-event-alert"></a>Per creare un avviso per evento WMI  
  
1.  In **Esplora oggetti** fare clic sul segno più per espandere il server in cui si desidera creare un avviso di evento WMI.  
  
2.  Fare clic sul segno più per espandere **SQL Server Agent**.  
  
3.  Fare clic con il pulsante destro del mouse su **Avvisi** e selezionare **Nuovo avviso**.  
  
4.  Nella casella **Nome** della finestra di dialogo **Nuovo avviso** immettere un nome per l'avviso.  
  
5.  Selezionare la casella di controllo **Abilita** per abilitare l'esecuzione dell'avviso. Per impostazione predefinita, l'opzione **Abilita** è selezionata.  
  
6.  Nell'elenco **Tipo** selezionare **Avviso per evento WMI**.  
  
7.  Nella casella **Spazio dei nomi**in **Definizione di avviso di evento WMI** specificare lo spazio dei nomi WMI da usare per l'istruzione WQL (WMI Query Language) che identifica l'evento WMI che attiva l'avviso.  
  
8.  Nella casella **Query** specificare l'istruzione WQL che identifica l'evento al quale risponde l'avviso.  
  
9. Fare clic su **OK**.  
  
## <a name="TsqlProcedure"></a>Utilizzo di Transact-SQL  
  
#### <a name="to-create-a-wmi-event-alert"></a>Per creare un avviso per evento WMI  
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde_md.md)].  
  
2.  Sulla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra delle query e fare clic su **Esegui**.  
  
    ```  
    -- creates a WMI event alert that retrieves all event properties for any ALTER_TABLE event that occurs on table AdventureWorks2012.Sales.SalesOrderDetail  
    -- This example assumes that the message 54001 already exists.  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_add_alert  
        @name = N'Test Alert 2',  
        @message_id = 54001  
        @notification_message = N'Error 54001 has occurred on the Sales.SalesOrderDetail table on the AdventureWorks2012 database.',  
        @wmi_namespace = '\\.\root\Microsoft\SqlServer\ServerEvents\,  
        @wmi_query = N'SELECT * FROM ALTER_TABLE   
    WHERE DatabaseName = 'AdventureWorks2012' AND SchemaName = 'Sales'   
        AND ObjectType='Table' AND ObjectName = 'SalesOrderDetail'';  
    GO  
    ```  
  
Per altre informazioni, vedere [sp_add_alert](https://msdn.microsoft.com/d9b41853-e22d-4813-a79f-57efb4511f09).  
  
