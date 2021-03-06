---
title: SELECT FROM &lt;modello&gt;. SAMPLE_CASES (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f4443f05fbee790f5f1d266f451e1105b9c00197
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2018
ms.locfileid: "37992043"
---
# <a name="select-from-ltmodelgtsamplecases-dmx"></a>SELECT FROM &lt;modello&gt;. SAMPLE_CASES (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Restituisce case di esempio rappresentativi dei case utilizzati per il training del modello di data mining.  
  
 Per utilizzare questa istruzione, è necessario attivare il drill-through alla creazione del modello di data mining. Per altre informazioni su come abilitare il drill-through, vedere [CREATE MINING MODEL &#40;DMX&#41;](../dmx/create-mining-model-dmx.md), [SELECT INTO &#40;DMX&#41;](../dmx/select-into-dmx.md), e [ALTER MINING STRUCTURE &#40;DMX&#41;](../dmx/alter-mining-structure-dmx.md).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
SELECT [FLATTENED] [TOP <n>] <expression list> FROM <model>.SAMPLE_CASES  
[WHERE <condition list>] ORDER BY <expression> [DESC|ASC]]  
```  
  
## <a name="arguments"></a>Argomenti  
 *n*  
 Facoltativo. Valore intero mediante il quale viene specificato il numero di righe da restituire.  
  
 *elenco di espressioni*  
 Elenco delimitato da virgole contenente identificatori di colonna correlati.  
  
 *model*  
 Identificatore del modello.  
  
 *Elenco condizioni*  
 Facoltativo. Condizioni per limitare i valori restituiti dall'elenco di colonne.  
  
 *expression*  
 Facoltativo. Espressione che restituisce un valore scalare.  
  
## <a name="remarks"></a>Note  
 I case di esempio potrebbero essere generati e potrebbero non esistere effettivamente nei dati utilizzati per il training. Il case restituito è rappresentativo del nodo di contenuto specificato.  
  
 Anche se il [!INCLUDE[msCoName](../includes/msconame-md.md)] è l'unico algoritmo Sequence Clustering [!INCLUDE[msCoName](../includes/msconame-md.md)] algoritmo che supporta l'utilizzo di SELECT FROM \<modello >. SAMPLE_CASES, gli algoritmi di terze parti possono anche supportarla.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente vengono restituiti i case di esempio utilizzati per il training del modello di data mining Target Mail. Usando il [IsInNode &#40;DMX&#41; ](../dmx/isinnode-dmx.md) funzionare nel **in cui** la clausola restituisce solo i case associati con il nodo '000000003'. La stringa del nodo si trova nella colonna NODE_UNIQUE_NAME del set di righe dello schema.  
  
```  
Select * from [Sequence Clustering].SAMPLE_Cases  
WHERE IsInNode('000000003')  
```  
  
## <a name="see-also"></a>Vedere anche  
 [SELEZIONARE &AMP;#40;DMX&AMP;#41;](../dmx/select-dmx.md)   
 [Le estensioni di Data Mining di dati &#40;DMX&#41; istruzioni di definizione dei dati](../dmx/dmx-statements-data-definition.md)   
 [Le estensioni di Data Mining di dati &#40;DMX&#41; istruzioni di manipolazione dei dati](../dmx/dmx-statements-data-manipulation.md)   
 [Guida di riferimento alle istruzioni DMX &#40;Data Mining Extensions&#41;](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
