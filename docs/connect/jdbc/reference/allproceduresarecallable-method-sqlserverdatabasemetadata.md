---
title: Metodo allProceduresAreCallable (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.allProceduresAreCallable
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 8886137d-455e-497c-afea-4b326eda52f1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 43ae9cc9bc9634131c197f634c713125f23ddd86
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 10/01/2018
ms.locfileid: "47790329"
---
# <a name="allproceduresarecallable-method-sqlserverdatabasemetadata"></a>Metodo allProceduresAreCallable (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera un valore che indica se l'utente corrente ha le autorizzazioni necessarie per chiamare tutte le procedure restituite dal metodo [getProcedures](../../../connect/jdbc/reference/getprocedures-method-sqlserverdatabasemetadata.md).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public boolean allProceduresAreCallable()  
```  
  
## <a name="return-value"></a>Valore restituito  
 **true** se l'utente disponga delle autorizzazioni per chiamare tutte le procedure. In caso contrario, **false**.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Questo metodo allProceduresAreCallable viene specificato dal metodo allProceduresAreCallable nell'interfaccia DatabaseMetaData.  
  
## <a name="see-also"></a>Vedere anche  
 [Metodi di SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membri di SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
