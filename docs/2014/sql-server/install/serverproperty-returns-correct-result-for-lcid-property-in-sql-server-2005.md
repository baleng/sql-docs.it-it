---
title: SERVERPROPERTY restituisce il risultato corretto della proprietà LCID in SQL Server 2005 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- SERVERPROPERTY function
ms.assetid: 833a2fc9-b480-4697-aa7b-9677e78ee0b4
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a05202e19e95e719c8518f785be7ee1a1fbd8fff
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/02/2018
ms.locfileid: "48163101"
---
# <a name="serverproperty-returns-correct-result-for-lcid-property-in-sql-server-2005"></a>In SQL Server 2005 SERVERPROPERTY restituisce il valore corretto della proprietà LCID
  Se si esegue SERVERPROPERTY ('LCID') su server che utilizzano regole di confronto binarie, la funzione restituisce l'identificatore delle impostazioni locali (LCID) di Windows corrispondente alle regole di confronto del server.  
  
> [!NOTE]  
>  Per i file batch e di traccia che contengono riferimenti a SERVERPROPERTY ('LCID') e vengono eseguiti in altre istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], questa modifica di comportamento verrà rilevata solo se le regole di confronto delle altre istanze sono identiche a quelle dell'istanza corrente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="corrective-action"></a>Azione correttiva  
 Modificare le applicazioni per prevedere che SERVERPROPERTY ('LCID') restituisca l'identificatore LCID di Windows che corrisponde alle regole di confronto del server.  
  
## <a name="see-also"></a>Vedere anche  
 [Problemi di aggiornamento del motore di database](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Preparazione aggiornamento a SQL Server 2014 &#91;new&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
