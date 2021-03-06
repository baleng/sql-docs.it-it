---
title: ADCPROP_UPDATECRITERIA_ENUM | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADCPROP_UPDATECRITERIA_ENUM
helpviewer_keywords:
- ADCPROP_UPDATECRITERIA_ENUM [ADO]
ms.assetid: 33fd7b65-2ec8-4f62-91a7-630b5dab1aa2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 91b4d64095c02fbf3f969248fc78d375a191fe72
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/01/2018
ms.locfileid: "47762737"
---
# <a name="adcpropupdatecriteriaenum"></a>ADCPROP_UPDATECRITERIA_ENUM
Specifica quali campi possono essere usati per rilevare i conflitti durante un aggiornamento ottimistica di una riga dell'origine dati con un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) oggetto.  
  
 Utilizzare queste costanti con il **Recordset** "**criteri di aggiornamento**" proprietà dinamiche, che fa riferimento il [indice proprietà dinamica ADO](../../../ado/reference/ado-api/ado-dynamic-property-index.md) e documentate nel [ Microsoft Cursor Service per OLE DB](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md) documentazione.  
  
|Costante|valore|Description|  
|--------------|-----------|-----------------|  
|**adCriteriaAllCols**|1|Rileva i conflitti se qualsiasi colonna della riga di origine dati è stato modificato.|  
|**adCriteriaKey**|0|Rileva i conflitti se la colonna chiave dei dati di riga dell'origine è stato modificato, il che significa che la riga è stata eliminata.|  
|**adCriteriaTimeStamp**|3|Rileva se il timestamp dei dati di origine riga è in conflitto è stato modificato, vale a dire la riga è stato eseguito l'accesso dopo il **Recordset** è stato ottenuto.|  
|**adCriteriaUpdCols**|2|Rileva i conflitti se le colonne dell'origine dati della riga che corrispondono ai campi aggiornati del **Recordset** sono state modificate.|  
  
## <a name="adowfc-equivalent"></a>Equivalente di ADO o WFC  
 Package: **com.ms.wfc.data**  
  
|Costante|  
|--------------|  
|AdoEnums.AdcPropUpdateCriteria.ALLCOLS|  
|AdoEnums.AdcPropUpdateCriteria.KEY|  
|AdoEnums.AdcPropUpdateCriteria.TIMESTAMP|  
|AdoEnums.AdcPropUpdateCriteria.UPDCOLS|
