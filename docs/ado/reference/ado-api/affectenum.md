---
title: AffectEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- AffectEnum
helpviewer_keywords:
- AffectEnum enumeration [ADO]
ms.assetid: 1ab921a0-6c57-43b4-9291-701b2599f3e8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3a26d1f9b1e8ff7cf9ed127dc78a02827952d411
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/01/2018
ms.locfileid: "47772199"
---
# <a name="affectenum"></a>AffectEnum
Consente di specificare quali record sono interessati da un'operazione.  
  
|Costante|valore|Description|  
|--------------|-----------|-----------------|  
|**adAffectAll**|3|Se non è presente una [filtro](../../../ado/reference/ado-api/filter-property.md) applicato per il **Recordset**, influisce su tutti i record.<br /><br /> Se il **filtro** è impostata su un criterio di tipo stringa (ad esempio "autore ="Smith""), quindi l'operazione interessa record visibili nel capitolo corrente.<br /><br /> Se il **filtro** è impostata su un membro del [FilterGroupEnum](../../../ado/reference/ado-api/filtergroupenum.md) o una matrice di segnalibri, quindi l'operazione verrà applicate a tutte le righe del **Recordset**. **Nota:****adAffectAll** è nascosto nel Visualizzatore oggetti Visual Basic.  |  
|**adAffectAllChapters**|4|Influisce su tutti i record in tutti i capitoli di pari livello dei **Recordset**, inclusi quelli non visibili tramite qualsiasi **filtro** attualmente applicato.|  
|**adAffectCurrent**|1|Interessa solo il record corrente.|  
|**adAffectGroup**|2|Interessa solo i record che soddisfano l'oggetto corrente [filtro](../../../ado/reference/ado-api/filter-property.md) l'impostazione della proprietà. È necessario impostare il **filtro** proprietà di un **FilterGroupEnum** valore o una matrice di **segnalibri** per usare questa opzione.|  
  
## <a name="adowfc-equivalent"></a>Equivalente di ADO o WFC  
 Package: **com.ms.wfc.data**  
  
|Costante|  
|--------------|  
|AdoEnums.Affect.ALL|  
|AdoEnums.Affect.ALLCHAPTERS|  
|AdoEnums.Affect.CURRENT|  
|AdoEnums.Affect.GROUP|  
  
## <a name="applies-to"></a>Si applica a  
  
|||  
|-|-|  
|[Metodo CancelBatch (ADO)](../../../ado/reference/ado-api/cancelbatch-method-ado.md)|[Metodo Delete (recordset ADO)](../../../ado/reference/ado-api/delete-method-ado-recordset.md)|  
|[Metodo Resync](../../../ado/reference/ado-api/resync-method.md)|[Metodo UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)|
