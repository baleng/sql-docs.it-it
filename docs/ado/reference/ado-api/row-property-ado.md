---
title: "Riga di proprietà (ADO) | Documenti Microsoft"
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
- ADORecordConstruction::PutRow
- ADORecordConstruction::GetRow
- ADORecordConstruction::get_Row
- ADORecordConstruction::Row
- ADORecordConstruction::put_Row
helpviewer_keywords:
- Row property [ADO]
ms.assetid: 21019d89-2dd1-4a26-ac6f-384b81d66949
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 19b935d43739d1a1ce19f414cae12b00c311b261
ms.contentlocale: it-it
ms.lasthandoff: 09/09/2017

---
# <a name="row-property-ado"></a>Proprietà di riga (ADO)
Ottiene o imposta OLE DB **riga** oggetto o da un [interfaccia ADORecordConstruction](../../../ado/reference/ado-api/adorecordconstruction-interface.md) oggetto. Quando si utilizza **put_Row** per impostare un **riga** dell'oggetto, una riga viene trasformata in un oggetto ADO **Record** oggetto.  
  
## <a name="readwritesyntax"></a>Lettura/scrittura. Sintassi  
  
```  
HRESULT get_Row([out, retval] IUnknown** ppRow);  
HRESULT put_Row([in] IUnknown* pRow);  
```  
  
## <a name="parameters"></a>Parametri  
 *ppRow*  
 Puntatore a OLE DB **riga** oggetto.  
  
 *PRow*  
 OLE DB **riga** oggetto.  
  
## <a name="return-values"></a>Valori restituiti  
 Metodo di questa proprietà restituisce i valori HRESULT standard, inclusi S_OK ed E_FAIL.  
  
## <a name="applies-to"></a>Si applica a  
 [Interfaccia ADORecordConstruction](../../../ado/reference/ado-api/adorecordconstruction-interface.md)