---
title: Dimensione di archiviazione | Documenti Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- dimensions [Analysis Services], storage
- storing data [Analysis Services]
- storage [Analysis Services], dimensions
- relational OLAP
- multidimensional OLAP
- MOLAP
- storing data [Analysis Services], dimensions
- ROLAP
ms.assetid: 8d74b932-2174-4e1f-8414-636455880b6a
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b45ab57b151c2cdab5ae7aa133befd06893037bd
ms.contentlocale: it-it
ms.lasthandoff: 09/01/2017

---
# <a name="dimensions---storage"></a>Dimensioni di archiviazione:
  Dimensioni [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] supportano due modalità di archiviazione:  
  
-   OLAP relazionale (ROLAP)  
  
-   OLAP multidimensionale (MOLAP)  
  
 La modalità di archiviazione determina la posizione e la forma dei dati di una dimensione. MOLAP è la modalità di archiviazione predefinita per le dimensioni. **Argomenti correlati:**[l'elaborazione e modalità di archiviazione delle partizioni](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-partition-storage-modes-and-processing.md)  
  
## <a name="molap"></a>MOLAP  
 I dati per una dimensione che utilizza la modalità MOLAP vengono archiviati in una struttura multidimensionale nell'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Tale struttura multidimensionale viene creata e popolata durante l'elaborazione della dimensione. Le dimensioni MOLAP garantiscono prestazioni di esecuzione delle query migliori rispetto alle dimensioni ROLAP.  
  
## <a name="rolap"></a>ROLAP  
 I dati per una dimensione che utilizza la modalità ROLAP vengono effettivamente archiviati nelle tabelle utilizzate per definire la dimensione. La modalità ROLAP può essere utilizzata per supportare dimensioni grandi senza duplicare quantità di dati elevate, a spese, però, delle prestazioni di esecuzione delle query. Poiché la dimensione si basa direttamente sulle tabelle della vista origine dati utilizzata per definire la dimensione, la modalità di archiviazione ROLAP supporta inoltre l'elaborazione OLAP in tempo reale.  
  
> [!IMPORTANT]  
>  Se una dimensione utilizza la modalità di archiviazione ROLAP ed è inclusa in un cubo che utilizza l'archiviazione MOLAP, qualsiasi modifica dello schema nella tabella di origine deve essere seguita dall'immediata elaborazione della dimensione. In caso contrario, i risultati delle query eseguite sui cubi potrebbero essere inconsistenti. **Argomento correlato:**[automatizzare Analysis Services attività amministrative con SSIS](../../analysis-services/instances/automate-analysis-services-administrative-tasks-with-ssis.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Elaborazione e modalità di archiviazione di partizioni](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-partition-storage-modes-and-processing.md)  
  
  