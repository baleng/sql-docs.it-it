---
title: Elemento DiscretizationMethod (ASSL) | Documenti Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- DiscretizationMethod Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- DiscretizationMethod
helpviewer_keywords:
- DiscretizationMethod element
ms.assetid: 4cfe015f-ad6c-47e1-8aff-c9c7677867b1
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e2bbf548ba16ccc81d1536c5c64a22e9c69d96d1
ms.contentlocale: it-it
ms.lasthandoff: 09/01/2017

---
# <a name="discretizationmethod-element-assl"></a>Elemento DiscretizationMethod (ASSL)
  Definisce il metodo da usare per la discretizzazione.  
  
## <a name="syntax"></a>Sintassi  
  
```xml  
  
<DimensionAttribute> <!-- or ScalarMiningStructureColumn -->  
   ...  
   <DiscretizationMethod>...</DiscretizationMethod>  
   ...  
</DimensionAttribute>  
```  
  
## <a name="element-characteristics"></a>Caratteristiche elemento  
  
|Caratteristica|Descrizione|  
|--------------------|-----------------|  
|Tipo di dati e lunghezza|String (enumerazione)|  
|Valore predefinito|*Nessuno*|  
|Cardinalità|0-1: elemento facoltativo che può ricorrere una sola volta.|  
  
## <a name="element-relationships"></a>Relazioni elemento  
  
|Relazione|Elemento|  
|------------------|-------------|  
|Elementi padre|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md), [ScalarMiningStructureColumn](../../../analysis-services/scripting/data-type/scalarminingstructurecolumn-data-type-assl.md)|  
|Elementi figlio|Nessuno|  
  
## <a name="remarks"></a>Osservazioni  
 Il valore della **DiscretizationMethod** elemento determina come i valori per il **DimensionAttribute** o **ScalarMiningStructureColumn** vengono discretizzati o organizzati in un set di gruppi specifico. Per ulteriori informazioni sui metodi di discretizzazione, vedere [metodi di discretizzazione &#40; Data Mining &#41;](../../../analysis-services/data-mining/discretization-methods-data-mining.md).  
  
 Il valore di questo elemento è limitato a una delle stringhe nella tabella seguente.  
  
|Valore|Descrizione|  
|-----------|-----------------|  
|*Automatico*|Equivale al metodo di discretizzazione AUTOMATIC per le colonne della struttura di data mining.|  
|*EqualAreas*|Equivale al metodo di discretizzazione EQUAL_AREAS per le colonne della struttura di data mining.|  
|*Cluster*|Equivale al metodo di discretizzazione CLUSTERS per le colonne della struttura di data mining.|  
|*Thresholds*|Equivale al metodo di discretizzazione THRESHOLDS per le colonne della struttura di data mining.|  
|*EqualRanges*|Equivale al metodo di discretizzazione EQUAL_RANGES per le colonne della struttura di data mining.|  
  
 L'enumerazione che corrisponde ai valori consentiti per **DiscretizationMethod** nell'oggetto oggetti AMO (Analysis Management) è modello <xref:Microsoft.AnalysisServices.DiscretizationMethod>.  
  
## <a name="see-also"></a>Vedere anche  
 [Proprietà &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  