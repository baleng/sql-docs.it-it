---
title: SQLCancel | Documenti di Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQLCancel function
ms.assetid: d4c965ae-c1ac-4e9d-b4b9-32b561401106
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 816e93c7cf65d622bcd48cbf5a93eb5abba32adb
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/02/2018
ms.locfileid: "48077797"
---
# <a name="sqlcancel"></a>SQLCancel
  Il [SQLCancel](http://go.microsoft.com/fwlink/?LinkId=203516) argomento afferma che in ODBC 2.x, se un'applicazione chiama `SQLCancel` quando non si è fatta alcuna elaborazione nell'istruzione `SQLCancel` ha lo stesso effetto `SQLFreeStmt` con le `SQL_CLOSE` opzione; questo comportamento viene definito solo per motivi di completezza e le applicazioni devono chiamare `SQLFreeStmt` o `SQLCloseCursor` per chiudere i cursori. Tuttavia, anche se l'applicazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client consente di impostare la versione dell'API ODBC 3.5.x o successiva, nella funzione `SQLCancel` verrà utilizzato il comportamento ODBC 2.x.  
  
## <a name="see-also"></a>Vedere anche  
 [SQLCancel](http://go.microsoft.com/fwlink/?LinkId=203516)   
 [Dettagli di implementazione dell'API ODBC](odbc-api-implementation-details.md)  
  
  
