---
title: Attività Backup database | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.backupdatabasetask.f1
helpviewer_keywords:
- database backups [Integration Services]
- Back Up Database task [Integration Services]
- backing up databases [Integration Services]
- transaction log backups [Integration Services]
- backing up transaction logs [Integration Services]
ms.assetid: b8839d71-13b7-41f2-a434-cb95020e79d7
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: fff65b87c5497a28945c5133d543346c657c6953
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/02/2018
ms.locfileid: "48063571"
---
# <a name="back-up-database-task"></a>Attività Backup database
  L'attività Backup database consente di eseguire diversi tipi di backup dei database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Per altre informazioni, vedere [Back Up and Restore of SQL Server Databases](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md).  
  
 Tramite l'attività Backup database un pacchetto può eseguire il backup di uno o più database. Se si utilizza l'attività per eseguire il backup di un singolo database, sarà possibile scegliere il componente di cui eseguire il backup, ovvero il database o i relativi file e filegroup.  
  
## <a name="supported-recover-models-and-backup-types"></a>Modelli di recupero e tipi di backup supportati  
 Nella tabella seguente sono elencati i modelli di recupero e i tipi di backup supportati dall'attività Backup database.  
  
|modello di recupero|Database|Differenziale del database|Log delle transazioni|File o differenziale del file|  
|--------------------|--------------|---------------------------|---------------------|-------------------------------|  
|Simple|Obbligatorio|Facoltativo|Non supportato|Non supportato|  
|Full|Obbligatorio|Facoltativo|Obbligatorio|Facoltativo|  
|Registrazione minima delle operazioni bulk|Obbligatorio|Facoltativo|Obbligatorio|Facoltativo|  
  
 L'attività Backup database incapsula l'istruzione Transact-SQL BACKUP. Per altre informazioni, vedere [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql).  
  
## <a name="configuration-of-the-back-up-database-task"></a>Configurazione dell'attività Backup database  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../../includes/ssis-md.md)] . Questa attività è disponibile nella sezione **Attività di manutenzione** della **casella degli strumenti** di Progettazione [!INCLUDE[ssIS](../../../includes/ssis-md.md)] .  
  
 Per ulteriori informazioni sulle proprietà che è possibile impostare in Progettazione [!INCLUDE[ssIS](../../../includes/ssis-md.md)] , fare clic sull'argomento seguente:  
  
-   [Attività Backup database &#40;Piano di manutenzione&#41;](../../relational-databases/maintenance-plans/options-in-the-back-up-database-task-for-maintenance-plan.md)  
  
 Per altre informazioni sull'impostazione di queste proprietà in Progettazione [!INCLUDE[ssIS](../../../includes/ssis-md.md)] , fare clic sull'argomento seguente:  
  
-   [Impostare le proprietà di un'attività o di un contenitore](../set-the-properties-of-a-task-or-container.md)  
  
  
