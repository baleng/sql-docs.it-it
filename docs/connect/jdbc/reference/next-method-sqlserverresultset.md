---
title: Metodo Next (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.next
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 60248447-6908-4036-a779-a501453cd553
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c2b5611c9f925c95a49982f8f9c936a6d84952f4
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 10/01/2018
ms.locfileid: "47702841"
---
# <a name="next-method-sqlserverresultset"></a>Metodo next (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Sposta il cursore di una riga verso il basso dalla posizione corrente.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public boolean next()  
```  
  
## <a name="return-value"></a>Valore restituito  
 **true** se la nuova riga corrente è valida. **false** se sono presenti altre righe da elaborare.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Questo metodo next viene specificato dal metodo next nell'interfaccia java.sql.ResultSet.  
  
 Un cursore del set di risultati viene posizionato inizialmente prima della prima riga. La prima chiamata al metodo next rende la prima riga quella corrente, la seconda chiamata rende la seconda riga quella corrente e così via.  
  
 Se un flusso di input è aperto per la riga corrente, una chiamata al metodo next lo chiuderà in modo implicito. Una catena di avvisi per l'oggetto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) viene cancellata quando viene letta una nuova riga.  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
