---
title: Non è possibile aggiornare i database di sola lettura | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- database cannot be upgraded
ms.assetid: 27964211-ea30-4390-b791-dcf225fb9ae7
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 3757183f61a3f70097d5abb7a0d01d6381a1d10e
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/02/2018
ms.locfileid: "48134091"
---
# <a name="read-only-databases-cannot-be-upgraded"></a>Non è possibile aggiornare database di sola lettura
  Alcuni database di questa istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non possono essere aggiornati.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Description  
 È stato rilevato un database di sola lettura. Per aggiornare il database, è necessario che sia accessibile in scrittura dal programma di installazione.  
  
## <a name="corrective-action"></a>Azione correttiva  
 Quando non venga utilizzato il database, usare il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise Manager [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], oppure l'istruzione ALTER DATABASE per modificare il database in lettura / scrittura. Per impostare il database in lettura/scrittura, utilizzare l'istruzione seguente.  
  
```  
USE master;  
GO  
ALTER DATABASE <database name>  
SET READ_WRITE;  
GO  
```  
  
 Per ulteriori informazioni sull'istruzione ALTER DATABASE, vedere l'argomento "ALTER DATABASE ([!INCLUDE[tsql](../../includes/tsql-md.md)])" argomento nella documentazione online di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Vedere anche  
 [Problemi di aggiornamento del motore di database](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Preparazione aggiornamento a SQL Server 2014 &#91;new&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
