---
title: "Proprietà direzione | Documenti Microsoft"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- _Parameter::Direction
helpviewer_keywords:
- Direction property
ms.assetid: d5732578-3434-4dcd-a9f7-db1abd1b3b94
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 1a81c60a4505e1c5e420583c474109d0d08f4fb6
ms.contentlocale: it-it
ms.lasthandoff: 09/09/2017

---
# <a name="direction-property"></a>Proprietà di direzione
Indica se il [parametro](../../../ado/reference/ado-api/parameter-object.md) rappresenta un parametro di input, un parametro di output, un parametro di input e output, o se il parametro è il valore restituito da una stored procedure.  
  
## <a name="settings-and-return-values"></a>Le impostazioni e valori restituiti  
 Restituisce o imposta un [ParameterDirectionEnum](../../../ado/reference/ado-api/parameterdirectionenum.md) valore.  
  
## <a name="remarks"></a>Osservazioni  
 Utilizzare il **direzione** proprietà per specificare come un parametro viene passato a o da una stored procedure. Il **direzione** proprietà è di lettura/scrittura; in questo modo è possibile lavorare con i provider che non restituiscono le informazioni o per impostare queste informazioni quando non si desidera effettuare una chiamata aggiuntiva al provider per recuperare informazioni sui parametri in ADO.  
  
 Non tutti i provider possono determinare la direzione dei parametri nella stored procedure. In questi casi, è necessario impostare il **direzione** proprietà prima di eseguire la query.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Parameter](../../../ado/reference/ado-api/parameter-object.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di proprietà direzione (VB), CommandText, CommandTimeout, CommandType, dimensioni e ActiveConnection](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vb.md)   
 [Esempio di proprietà direzione (VC + +), CommandText, CommandTimeout, CommandType, dimensioni e ActiveConnection](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vc.md)   
 [ActiveConnection, CommandText, CommandTimeout, CommandType, dimensioni e direzione proprietà esempio (JScript)](../../../ado/reference/ado-api/activeconnection-commandtext-timeout-type-size-example-jscript.md)
