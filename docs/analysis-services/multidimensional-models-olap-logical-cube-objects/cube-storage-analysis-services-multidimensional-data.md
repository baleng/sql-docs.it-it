---
title: Archiviazione (Analysis Services - dati multidimensionali) del cubo | Documenti Microsoft
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: olap
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 05ff45fa98b578fce295ab2113abf301bc3b78ed
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/10/2018
ms.locfileid: "34027501"
---
# <a name="cube-storage-analysis-services---multidimensional-data"></a>Archiviazione di cubi (Analysis Services - Dati multidimensionali)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  L'archiviazione può coinvolgere solo i metadati del cubo oppure tutti i dati di origine della tabella dei fatti nonché le aggregazioni definite dalle dimensioni correlate al gruppo di misure. La quantità di dati archiviata dipende dalla modalità di archiviazione selezionata e dal numero di aggregazioni. La quantità di dati archiviata direttamente influisce sulle prestazioni di esecuzione delle query. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] vengono utilizzate diverse tecniche per ridurre al minimo lo spazio necessario per l'archiviazione dei dati del cubo e le aggregazioni:  
  
-   Le opzioni di archiviazione consentono di selezionare le modalità e le posizioni di archiviazione appropriate per i dati del cubo.  
  
-   Un algoritmo sofisticato configura aggregazioni di riepilogo efficaci per ridurre al minimo lo spazio di archiviazione senza compromettere la velocità.  
  
-   Per le celle vuote non viene allocato alcuno spazio di archiviazione.  
  
 Le impostazioni di archiviazione vengono definite per ogni singola partizione e per ogni gruppo di misure in un cubo esiste almeno una partizione. Per altre informazioni, vedere [partizioni &#40;Analysis Services - dati multidimensionali&#41;](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md), [l'elaborazione e modalità di archiviazione delle partizioni](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-partition-storage-modes-and-processing.md), [gruppidimisureemisure](../../analysis-services/multidimensional-models/measures-and-measure-groups.md), e [creare misure e gruppi di misure nei modelli multidimensionali](../../analysis-services/multidimensional-models/create-measures-and-measure-groups-in-multidimensional-models.md).  
  
## <a name="partition-storage"></a>Partition Storage  
 L'archiviazione di un gruppo di misure può prevedere la suddivisione in più partizioni. Le partizioni consentono di distribuire un gruppo di misure mediante la suddivisione in segmenti discreti in un solo server o in più server e di ottimizzare le prestazioni del processo di archiviazione e delle query. Ogni partizione di un gruppo di misure può essere basata su un'origine dei dati diversa e può prevedere impostazioni di archiviazione diverse.  
  
 L'origine dei dati di una partizione viene specificata quando si crea la partizione. È inoltre possibile modificare l'origine dei dati di una partizione esistente. Un gruppo di misure può essere suddiviso in partizioni verticali o orizzontali. In un gruppo di misure suddiviso in partizioni verticali ogni partizione si basa su una vista filtrata di una singola tabella di origine. Se ad esempio un gruppo di misure si basa su una singola tabella che contiene i dati relativi a più anni, è possibile creare una partizione separata per i dati di ogni anno. Al contrario, in un gruppo di misure suddiviso in partizioni orizzontali ogni partizione si basa su una tabella distinta. Utilizzare le partizioni orizzontali se nell'origine dei dati i dati di ogni anno vengono archiviati in una tabella separata.  
  
 Le partizioni inizialmente vengono create con le stesse impostazioni di archiviazione del gruppo di misure in cui vengono definite. Le impostazioni di archiviazione determinano se i dati dettaglio e relativi alle aggregazioni vengono archiviati in un formato multidimensionale nell'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], in un formato relazionale nel server di origine oppure in una combinazione di entrambi questi formati. Le impostazioni di archiviazione determinano inoltre se viene utilizzata la memorizzazione nella cache attiva per elaborare automaticamente le modifiche dei dati di origine nei dati multidimensionali archiviati in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
 Le partizioni di un cubo non sono visibili all'utente. La scelta di impostazioni di archiviazione per partizioni diverse può tuttavia influire sull'immediatezza dei dati, sulla quantità di spazio su disco utilizzato e sulle prestazioni delle query. È possibile archiviare le partizioni in più istanze di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. In questo modo all'archiviazione dei cubi viene applicata la tecnica dei cluster e il carico di lavoro viene distribuito tra server [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Per altre informazioni, vedere [modalità di archiviazione delle partizioni e l'elaborazione](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-partition-storage-modes-and-processing.md), [partizioni Remote](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-remote-partitions.md), e [partizioni &#40;Analysis Services - dati multidimensionali&#41; ](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md).  
  
## <a name="linked-measure-groups"></a>Gruppi di misure collegati  
 Sebbene l'archiviazione di più copie di un cubo in più istanze di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] possa richiedere uno spazio su disco notevole, tale operazione consente di ridurre considerevolmente lo spazio necessario sostituendo le copie del gruppo di misure con i gruppi di misure collegati. Un gruppo di misure collegato si basa su un gruppo di misure di un cubo in un altro database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], nella stessa istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] oppure in un'istanza diversa. I gruppi di misure collegati possono essere utilizzati anche con le dimensioni collegate dello stesso cubo di origine. Le dimensioni e i gruppi di misure collegati utilizzano le aggregazioni del cubo di origine e non prevedono quindi requisiti di archiviazione dei dati propri. Pertanto, se si archiviano i gruppi di misure e le dimensioni di un'origine in un database e si creano cubi e dimensioni collegati in cubi di altri database, lo spazio su disco necessario per l'archiviazione sarà decisamente inferiore. Per ulteriori informazioni, vedere [Linked Measure Groups](../../analysis-services/multidimensional-models/linked-measure-groups.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Le aggregazioni e progettazione di aggregazioni](../../analysis-services/multidimensional-models-olap-logical-cube-objects/aggregations-and-aggregation-designs.md)  
  
  
