---
title: Oggetto Backup Device di SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
s.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- SQLServer:Backup Device
- Backup Device object
ms.assetid: 52e7febf-d5e0-4674-945b-aacc40a9ad6e
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 30371a600f59801710ce27db084f887eeb1727e0
ms.sourcegitcommit: ca038f1ef180e4e1b27910bbc5d87822cd1ed176
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/20/2018
ms.locfileid: "52158979"
---
# <a name="sql-server-backup-device-object"></a>Oggetto Backup Device di SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  L'oggetto **Backup Device** include contatori per il monitoraggio dei dispositivi di backup di Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usati per le operazioni di backup e ripristino. Monitorare i dispositivi di backup se si desidera determinare la velocità effettiva oppure lo stato di avanzamento e le prestazioni delle operazioni di backup e ripristino per ogni dispositivo. Per monitorare la velocità effettiva di un'operazione di backup o ripristino dell'intero database, usare il contatore **Velocità effettiva backup o ripristino/sec** dell'oggetto [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Databases** object. Per altre informazioni, vedere [SQL Server, Databases Object](../../relational-databases/performance-monitor/sql-server-databases-object.md).  
  
 In questa tabella viene descritto il contatore dell'oggetto [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Backup Device** counter.  
  
|Contatore dell'oggetto Backup Device di SQL Server|Descrizione|  
|---------------------------------------|-----------------|  
|**Byte/sec velocità effettiva dispositivo**|Velocità effettiva delle operazioni di lettura e scrittura (in byte al secondo) di un dispositivo di backup utilizzato durante il backup o il ripristino dei database. Il contatore è disponibile solo durante l'esecuzione dell'operazione di backup o ripristino.|  
  
## <a name="see-also"></a>Vedere anche  
 [Dispositivi di backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)   
 [Monitorare l'utilizzo delle risorse &#40;Monitor di sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
