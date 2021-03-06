---
title: Eseguire un failover manuale pianificato di un gruppo di disponibilità (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.availabilitygroup.manualfailover.f1
helpviewer_keywords:
- Availability Groups [SQL Server], failover
- failover [SQL Server], AlwaysOn Availability Groups
ms.assetid: 419f655d-3f9a-4e7d-90b9-f0bab47b3178
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 386e07bd1be4eaac4c75541665fc6951e2a24fd3
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/02/2018
ms.locfileid: "48155343"
---
# <a name="perform-a-planned-manual-failover-of-an-availability-group-sql-server"></a>Eseguire un failover manuale pianificato di un gruppo di disponibilità (SQL Server)
  Questo argomento descrive come eseguire un failover manuale senza perdite di dati (*failover manuale pianificato*) in un gruppo di disponibilità AlwaysOn tramite [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)] o PowerShell in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]. Per un gruppo di disponibilità il failover si verifica al livello di una replica di disponibilità. Con un failover manuale pianificato, come con qualsiasi failover [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] , la replica secondaria passa al ruolo primario e, contemporaneamente, la replica primaria precedente passa al ruolo secondario.  
  
 Un failover manuale pianificato, supportato solo quando la replica primaria e la replica secondaria di destinazione sono in esecuzione in modalità con commit sincrono e sono attualmente sincronizzate, mantiene tutti i dati nei database secondari uniti in join al gruppo di disponibilità nella replica secondaria di destinazione. Quando la replica primaria precedente passa al ruolo secondario, i relativi database diventeranno database secondari e viene iniziata la sincronizzazione con i nuovi database primari. Dopo la transizione di tutti i database allo stato SYNCHRONIZED, la nuova replica secondaria diventa idonea a fungere da destinazione di un futuro failover manuale pianificato.  
  
> [!NOTE]  
>  Se la replica primaria e le repliche secondarie sono configurate per la modalità di failover automatico, dopo la sincronizzazione, la replica secondaria può anche fungere da destinazione per un failover automatico. Per altre informazioni, vedere [Modalità di disponibilità &#40;gruppi di disponibilità AlwaysOn&#41;](availability-modes-always-on-availability-groups.md).  
  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Restrictions"></a> Limitazioni e restrizioni  
  
-   Un comando del failover viene restituito non appena la replica secondaria di destinazione ha accettato il comando. Tuttavia, il recupero del database si verifica in modo asincrono dopo che il gruppo di disponibilità ha completato il failover.  
  
-   La coerenza tra i database all'interno del gruppo di disponibilità non viene mantenuta nel failover.  
  
    > [!NOTE]  
    >  Le transazioni tra database e quelle distribuite non sono supportate in [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]. Per altre informazioni, vedere [Transazioni tra database non supportate per il mirroring del database o i gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](transactions-always-on-availability-and-database-mirroring.md).  
  
###  <a name="Prerequisites"></a> Prerequisiti e restrizioni  
  
-   La replica secondaria di destinazione e la replica primaria devono essere entrambe in esecuzione in modalità di disponibilità con commit sincrono.  
  
-   La replica secondaria di destinazione deve essere attualmente sincronizzata con la replica primaria. È necessario che tutti i database secondari su tale replica secondaria siano uniti in join al gruppo di disponibilità e sincronizzati con i database primari corrispondenti (ossia lo stato dei database secondari locali deve essere SYNCHRONIZED).  
  
    > [!TIP]  
    >  Per determinare la conformità del failover di una replica secondaria, eseguire una query sulla colonna **is_failover_ready** nella DMV [sys.dm_hadr_database_cluster_states](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-cluster-states-transact-sql) o esaminare la colonna **Conformità failover** del [dashboard del gruppo AlwaysOn](use-the-always-on-dashboard-sql-server-management-studio.md).  
  
-   Questa attività è supportata solo nella replica secondaria di destinazione. È necessario essere connessi all'istanza del server che ospita la replica secondaria di destinazione.  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Permissions  
 È necessaria l'autorizzazione ALTER AVAILABILITY GROUP nel gruppo di disponibilità, l'autorizzazione CONTROL AVAILABILITY GROUP, l'autorizzazione ALTER ANY AVAILABILITY GROUP o l'autorizzazione CONTROL SERVER.  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
 **Per eseguire manualmente il failover di un gruppo di disponibilità**  
  
1.  In Esplora oggetti connettersi a un'istanza del server che ospita una replica secondaria del gruppo di disponibilità di cui eseguire il failover ed espandere l'albero del server.  
  
2.  Espandere il nodo **Disponibilità elevata AlwaysOn** e il nodo **Gruppi di disponibilità** .  
  
3.  Fare clic con il pulsante destro del mouse sul gruppo di disponibilità di cui eseguire il failover e selezionare il comando **Failover**.  
  
4.  Verrà avviata la Creazione guidata Gruppo di disponibilità di failover. Per altre informazioni, vedere [Usare la procedura guidata Failover gruppo di disponibilità &#40;SQL Server Management Studio&#41;](use-the-fail-over-availability-group-wizard-sql-server-management-studio.md).  
  
##  <a name="TsqlProcedure"></a> Uso di Transact-SQL  
 **Per eseguire manualmente il failover di un gruppo di disponibilità**  
  
1.  Connettersi all'istanza del server che ospita la replica secondaria di destinazione.  
  
2.  Utilizzare l'istruzione [ALTER AVAILABILITY GROUP](/sql/t-sql/statements/alter-availability-group-transact-sql) , come indicato di seguito:  
  
     ALTER AVAILABILITY GROUP *nome_gruppo* FAILOVER  
  
     dove *nome_gruppo* è il nome del gruppo di disponibilità.  
  
     Nell'esempio seguente viene eseguito il failover manuale del gruppo di disponibilità *MyAg* alla replica secondaria connessa.  
  
    ```  
    ALTER AVAILABILITY GROUP MyAg FAILOVER;  
    ```  
  
##  <a name="PowerShellProcedure"></a> Utilizzo di PowerShell  
 **Per eseguire manualmente il failover di un gruppo di disponibilità**  
  
1.  Passare alla directory (`cd`) all'istanza del server che ospita la replica secondaria di destinazione.  
  
2.  Usare il `Switch-SqlAvailabilityGroup` cmdlet.  
  
    > [!NOTE]  
    >  Per visualizzare la sintassi di un cmdlet, usare il `Get-Help` cmdlet di [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] ambiente PowerShell. Per altre informazioni, vedere [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md).  
  
     Nell'esempio seguente viene eseguito il failover manuale del gruppo di disponibilità *MyAg* alla replica secondaria con il percorso specificato.  
  
    ```  
    Switch-SqlAvailabilityGroup -Path SQLSERVER:\Sql\SecondaryServer\InstanceName\AvailabilityGroups\MyAg  
    ```  
  
 **Per impostare e utilizzare il provider PowerShell per SQL Server**  
  
-   [Provider PowerShell per SQL Server](../../../powershell/sql-server-powershell-provider.md)  
  
-   [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md)  
  
##  <a name="FollowUp"></a> Completamento: Dopo il failover manuale su un gruppo di disponibilità  
 Se è stato eseguito il failover al di fuori del [!INCLUDE[ssFosAuto](../../../includes/ssfosauto-md.md)] del gruppo di disponibilità, modificare i voti del quorum dei nodi WSFC per riflettere la nuova configurazione del gruppo di disponibilità. Per altre informazioni, vedere [WSFC &#40;Windows Server Failover Clustering&#41; con SQL Server](../../../sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Panoramica di gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Failover e modalità di Failover &#40;gruppi di disponibilità AlwaysOn&#41;](failover-and-failover-modes-always-on-availability-groups.md)   
 [Eseguire un failover manuale forzato di un gruppo di disponibilità &#40;SQL Server&#41;](perform-a-forced-manual-failover-of-an-availability-group-sql-server.md)  
  
  
