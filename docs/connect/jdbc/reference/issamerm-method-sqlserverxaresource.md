---
title: Metodo isSameRM (SQLServerXAResource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerXAResource.isSameRM
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: bfa24c46-b7cf-470a-afa1-52301847a448
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0cbe71d1ff4d19da3baba87210a1444e83d4f98e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 10/01/2018
ms.locfileid: "47633775"
---
# <a name="issamerm-method-sqlserverxaresource"></a>Metodo isSameRM (SQLServerXAResource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Determina se l'istanza dello strumento di gestione delle risorse rappresentata dall'oggetto di destinazione è uguale a quella rappresentata dall'oggetto XAResource specificato.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public boolean isSameRM(javax.transaction.xa.XAResource xares)  
```  
  
#### <a name="parameters"></a>Parametri  
 *xares*  
  
 Oggetto XAResource.  
  
## <a name="return-value"></a>Valore restituito  
 **true** se le istanze sono uguali. In caso contrario, **false**.  
  
## <a name="exceptions"></a>Eccezioni  
 javax.transaction.xa.XAException  
  
## <a name="remarks"></a>Remarks  
 Questo metodo commit viene specificato dal metodo commit nell'interfaccia javax.transaction.xa.XAResource.  
  
## <a name="see-also"></a>Vedere anche  
 [Metodi di SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-methods.md)   
 [Membri di SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-members.md)   
 [Classe SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md)  
  
  
