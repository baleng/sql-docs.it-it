---
title: Allocare un Handle di ambiente | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, environment handles
- ODBC applications, connections
- handles [SQL Server Native Client]
- environment handles [SQLNCLI]
ms.assetid: 15c1b428-ea6d-4672-894c-f0e289e2da3f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 66afa14ccb1953265f526f8c8861237638f569fd
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/02/2018
ms.locfileid: "48151271"
---
# <a name="allocating-an-environment-handle"></a>Allocazione di un handle di ambiente
  Prima di poter chiamare una funzione ODBC, un'applicazione deve inizializzare l'ambiente ODBC e allocare un handle di ambiente. Si tratta dell'handle dell'ambito globale che funge da segnaposto per gli altri handle in ODBC. Eseguire questa operazione chiamando **SQLAllocHandle** con il *HandleType* parametro impostato su SQL_HANDLE_ENV e *InputHandle* impostato su SQL_NULL_HANDLE.  
  
 Dopo avere allocato l'handle di ambiente, l'applicazione deve impostare gli attributi di ambiente per indicare la versione delle chiamate alle funzioni ODBC che verrà utilizzata. Per usare ODBC 3. *x* funzioni, chiamate [SQLSetEnvAttr](../native-client-odbc-api/sqlsetenvattr.md) con il *attributo* parametro impostato su SQL_ATTR_ODBC_VERSION e *ValuePtr* impostato su SQL_OV_ ODBC3.  
  
## <a name="see-also"></a>Vedere anche  
 [Comunicazione con SQL Server &#40;ODBC&#41;](communicating-with-sql-server-odbc.md)  
  
  
