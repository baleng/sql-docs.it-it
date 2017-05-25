---
title: Concetti di base relativi ai file eseguibili dell&quot;agente di replica | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- programming interfaces [SQL Server replication]
- programming [SQL Server replication], agents
- replication [SQL Server], agents and profiles
- agents [SQL Server replication], executables
- command prompt [SQL Server replication]
ms.assetid: cba476df-d4ea-44c9-bb86-81488971e328
caps.latest.revision: 38
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 096156484b2378713485e1177eb9b0cfd6faa5d8
ms.lasthandoff: 04/11/2017

---
# <a name="replication-agent-executables-concepts"></a>Concetti di base relativi ai file eseguibili dell'agente di replica
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gli agenti di replica possono essere controllati a livello di codice nei modi seguenti:  
  
-   Tramite le interfacce di programmazione gestite dall'agente nello spazio dei nomi <xref:Microsoft.SqlServer.Replication>.  
  
-   Richiamo dei file eseguibili dell'agente dal prompt dei comandi con un set di parametri fornito.  
  
 Il richiamo diretto degli agenti di replica dal prompt dei comandi consente l'accesso a livello di codice agli agenti da script della riga di comando inclusi in file batch. Quando viene richiamato dal prompt dei comandi, l'agente viene eseguito con l'account di sicurezza di [!INCLUDE[msCoName](../../../includes/msconame-md.md)] dell'utente che ha richiamato l'agente o avviato il file batch.  
  
 Le istanze degli agenti di replica seguenti possono essere eseguite utilizzando file eseguibili.  
  
-   [Agente distribuzione repliche](../../../relational-databases/replication/agents/replication-distribution-agent.md)  
  
-   [Agente lettura log repliche](../../../relational-databases/replication/agents/replication-log-reader-agent.md)  
  
-   [Agente merge repliche](../../../relational-databases/replication/agents/replication-merge-agent.md)  
  
-   [Agente di lettura coda repliche](../../../relational-databases/replication/agents/replication-queue-reader-agent.md)  
  
-   [Agente snapshot repliche](../../../relational-databases/replication/agents/replication-snapshot-agent.md)  
  
 Quando si richiamano gli agenti di replica, è possibile utilizzare profili di prestazioni per passare automaticamente un set di parametri definito al file eseguibile dell'agente. Per altre informazioni, vedere [Replication Agent Profiles](../../../relational-databases/replication/agents/replication-agent-profiles.md).  
  
## <a name="examples"></a>Esempi  
 Negli esempi seguenti viene illustrato come richiamare gli agenti di replica dal prompt dei comandi. Gli agenti di replica possono inoltre essere richiamati utilizzando RMO (Replication Management Objects). Per altre informazioni, vedere [Sincronizzare le sottoscrizioni &#40;replica&#41;](../../../relational-databases/replication/synchronize-subscriptions-replication.md).  
  
> [!NOTE]  
>  Le interruzioni di riga presenti negli esempi sono state aggiunte per facilitare la lettura. I comandi in un file batch devono essere inseriti in un'unica riga.  
  
### <a name="running-the-snapshot-agent"></a>Esecuzione dell'agente snapshot  
 Questo file batch di esempio richiama l'agente snapshot dal prompt dei comandi per generare uno snapshot per la pubblicazione **AdvWorksSalesOrdersMerge**. Gli script seguenti usano il percorso dei file di [!INCLUDE[ssSQL15_md](../../../includes/sssql15-md.md)] (versione 130). È necessario adeguare gli script in modo che puntino ai file per la versione in uso di [!INCLUDE[ssNoVersion_md](../../../includes/ssnoversion-md.md)].  
  
```  
REM -- Declare variables  
SET Publisher=%InstanceName%;  
SET PublicationDB=AdventureWorks2012;   
SET Publication=AdvWorksSalesOrdersMerge;   
  
REM --Start the Snapshot Agent to generate the snapshot for AdvWorksSalesOrdersMerge.  
"C:\Program Files\Microsoft SQL Server\130\COM\SNAPSHOT.EXE" -Publication %Publication%   
-Publisher %Publisher% -Distributor %Publisher% -PublisherDB %PublicationDB%   
-ReplicationType 2 -OutputVerboseLevel 1 -DistributorSecurityMode 1 ;  
  
```  
  
### <a name="running-the-distribution-agent"></a>Esecuzione dell'agente di distribuzione  
 Questo file batch di esempio richiama l'agente di distribuzione dal prompt dei comandi per replicare continuamente le modifiche dalla pubblicazione **AdvWorksProductTran** in un server di sottoscrizione push.  
  
```  
REM -- Declare the variables.  
SET Publisher=%instancename%;  
SET Subscriber=%instancename%;  
SET PublicationDB=AdventureWorks2012;  
SET SubscriptionDB=AdventureWorks2012Replica;   
SET Publication=AdvWorksProductsTran;  
  
REM -- Start the Distribution Agent with four subscription streams.  
REM -- The following command must be supplied without line breaks.  
"C:\Program Files\Microsoft SQL Server\130\COM\DISTRIB.EXE" -Subscriber %Subscriber%   
-SubscriberDB %SubscriptionDB% -SubscriberSecurityMode 1 -Publication %Publication%   
-Publisher %Publisher% -PublisherDB %PublicationDB% -Distributor %Publisher%   
-DistributorSecurityMode 1 -Continuous -SubscriptionType 0 -SubscriptionStreams 4 ;  
  
```  
  
### <a name="running-the-merge-agent"></a>Esecuzione dell'agente di merge  
 Questo file batch di esempio richiama l'agente di merge dal prompt dei comandi per sincronizzare una sottoscrizione pull con la pubblicazione **AdvWorksSalesOrdersMerge**.  
  
```  
REM -- Declare the variables.  
SET Publisher=%instancename%;  
SET Subscriber=%instancename%;  
SET PublicationDB=AdventureWorks2012;  
SET SubscriptionDB=AdventureWorks2012Replica;   
SET Publication=AdvWorksSalesOrdersMerge;  
  
REM --Start the Merge Agent with concurrent upload and download processes.  
REM -- The following command must be supplied without line breaks.  
"C:\Program Files\Microsoft SQL Server\130\COM\REPLMERG.EXE" -Publication %Publication%    
-Publisher %Publisher%  -Subscriber  %Subscriber%  -Distributor %Publisher%    
-PublisherDB %PublicationDB%  -SubscriberDB %SubscriptionDB% -PublisherSecurityMode 1    
-OutputVerboseLevel 2  -SubscriberSecurityMode 1  -SubscriptionType 1 -DistributorSecurityMode 1    
-Validate 3  -ParallelUploadDownload 1 ;  
  
```  
  
  