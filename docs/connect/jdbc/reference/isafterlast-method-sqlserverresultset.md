---
title: Metodo isAfterLast (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.isAfterLast
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 19f9d124-3184-4985-8b97-503a8ab8b4f9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 874677b8e82ef9129615daed2170757e908f9455
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 10/01/2018
ms.locfileid: "47809869"
---
# <a name="isafterlast-method-sqlserverresultset"></a>Metodo isAfterLast (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera informazioni sull'eventuale presenza del cursore nella posizione successiva all'ultima riga in questo oggetto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public boolean isAfterLast()  
```  
  
## <a name="return-value"></a>Valore restituito  
 **true** se il cursore si trova dopo l'ultima riga. **false** se il cursore si trova in qualsiasi altra posizione oppure se il set di risultati non contiene righe.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Questo metodo isAfterLast viene specificato dal metodo isAfterLast nell'interfaccia ResultSet.  
  
 Se questo metodo viene utilizzato con cursori dinamici, inclusi i cursori di sola lettura forward-only, e la proprietà di connessione selectMethod viene impostata su "cursor", si verificherà un'eccezione.  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
