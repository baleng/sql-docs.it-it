---
title: Forzare un server di destinazione a eseguire il polling del server master | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- forcing master server polling
- polling master servers [SQL Server]
- master servers [SQL Server], polling
- target servers [SQL Server], polling the master server
ms.assetid: f1189a47-5ac3-45e2-9c5f-847810672279
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: c0f3c9d209055bc05ff53c64f354b282e32be8c3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/01/2018
ms.locfileid: "47740499"
---
# <a name="force-a-target-server-to-poll-the-master-server"></a>Forzare un server di destinazione a eseguire il polling del server master
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> In [Istanza gestita di database SQL di Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) sono attualmente supportate la maggior parte delle funzionalità di SQL Server Agent, ma non tutte. Per informazioni dettagliate, vedere [Differenze T-SQL tra Istanza gestita del database SQL di Azure e SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

In questo argomento viene descritta la procedura per il polling forzato del server di destinazione al server master. Il server di destinazione deve essere registrato nel server master.  
  
Un processo è una serie specificata di azioni eseguite da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Un processo multiserver è un processo eseguito da un server master in uno o più server di destinazione. Ogni server di destinazione può eseguire contemporaneamente una sola istanza dello stesso processo. Ogni server di destinazione esegue periodicamente il polling del server master, scarica una copia dei nuovi processi assegnati al server di destinazione, quindi si disconnette. Il server di destinazione esegue il processo in locale, quindi si riconnette al server master per caricare lo stato del risultato del processo una volta terminato.  
  
> [!NOTE]  
> Se il server master non è accessibile quando il server di destinazione tenta di caricare lo stato del processo, per tale stato viene eseguito lo spooling fino a quando non è possibile accedere al server master.  
  
-   **Prima di iniziare:**  [Limitazioni e restrizioni](#Restrictions), [Sicurezza](#Security)  
  
-   **Per forzare un server di destinazione a eseguire il polling del server master con:** [SQL Server Management Studio](#SSMS)  
  
## <a name="BeforeYouBegin"></a>Prima di iniziare  
  
### <a name="Restrictions"></a>Limitazioni e restrizioni  
Il server di destinazione deve essere registrato nel server master. È necessario eseguire le istruzioni fornite in questo argomento dal server master.  
  
### <a name="Security"></a>Sicurezza  
Per informazioni dettagliate, vedere [Implement SQL Server Agent Security](../../ssms/agent/implement-sql-server-agent-security.md) e [Choose the Right SQL Server Agent Service Account for Multiserver Environments](../../ssms/agent/choose-the-right-sql-server-agent-service-account-for-multiserver-environments.md).  
  
## <a name="SSMS"></a>Utilizzo di SQL Server Management Studio  
**Per forzare un server di destinazione a eseguire il polling del server master**  
  
1.  In **Esplora oggetti**espandere il server master.  
  
2.  Fare clic con il pulsante destro del mouse su **SQL Server Agent**, scegliere **Amministrazione multiserver**e fare clic su **Gestione server di destinazione**.  
  
3.  Selezionare un server di destinazione e fare clic su **Forza polling**.  
  
