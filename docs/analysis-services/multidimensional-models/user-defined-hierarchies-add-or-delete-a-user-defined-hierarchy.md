---
title: Aggiungere o eliminare una gerarchia definita dall'utente | Documenti Microsoft
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- hierarchies [Analysis Services], adding
- removing hierarchies
- adding hierarchies
- deleting hierarchies
- hierarchies [Analysis Services], removing
ms.assetid: 953818b4-9543-4c01-bb20-1d45ec6dfb91
caps.latest.revision: 51
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b64b9cd9512b07a308574cd4cf398f8ae72a2460
ms.contentlocale: it-it
ms.lasthandoff: 09/01/2017

---
# <a name="user-defined-hierarchies---add-or-delete-a-user-defined-hierarchy"></a>Gerarchie definite dall'utente, aggiungere o eliminare una gerarchia definita dall'utente
  È possibile aggiungere o rimuovere una gerarchia definita dall'utente in una dimensione nella scheda **Struttura dimensione** di Progettazione dimensioni in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
 Quando si aggiunge una gerarchia definita dall'utente, questa non risulta disponibile per gli utenti finché non ne viene creata un'istanza in un'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e non viene elaborata la dimensione. Per altre informazioni, vedere [Database modelli multidimensionali &#40;SSAS&#41;](../../analysis-services/multidimensional-models/multidimensional-model-databases-ssas.md) e [Elaborazione di un modello multidimensionale &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md).  
  
### <a name="to-add-a-user-defined-hierarchy-to-a-dimension"></a>Per aggiungere una gerarchia definita dall'utente a una dimensione  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]aprire il progetto appropriato di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , quindi aprire la dimensione che si desidera utilizzare.  
  
     La dimensione viene aperta nella scheda **Struttura dimensione** di Progettazione dimensioni.  
  
2.  Trascinare l'attributo che si vuole usare nella gerarchia definita dall'utente dal riquadro **Attributi** al riquadro **Gerarchie** .  
  
3.  Trascinare ulteriori attributi per formare i livelli della gerarchia definita dall'utente.  
  
     L'ordine nel quale sono elencati gli attributi è determinante. Ad esempio, in una gerarchia temporale, gli anni devono essere visualizzati più in alto dei giorni nell'elenco della gerarchia.  
  
4.  Facoltativamente, riorganizzare i livelli della gerarchia definita dall'utente trascinandoli nelle posizioni corrette.  
  
5.  Facoltativamente, modificare le proprietà della gerarchia definita dall'utente o dei relativi livelli.  
  
     Può essere ad esempio utile specificare un nome per la gerarchia definita dall'utente, rinominarne uno o più livelli e definire un nome personalizzato per il livello Totale. Per altre informazioni, vedere [Proprietà delle gerarchie definite dall'utente](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/user-hierarchies-properties.md)e [Proprietà livello - Gerarchie utente](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/user-hierarchies-level-properties.md).  
  
    > [!NOTE]  
    >  Per impostazione predefinita, una gerarchia definita dall'utente è solo un percorso che consente agli utenti di eseguire il drill-down delle informazioni. Se esistono relazioni tra i livelli, tuttavia, è possibile incrementare le prestazioni di esecuzione delle query configurando relazioni tra attributi per i livelli. Per altre informazioni, vedere [Relazioni tra attributi](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attribute-relationships.md) e [Definire relazioni tra attributi](../../analysis-services/multidimensional-models/attribute-relationships-define.md).  
  
### <a name="to-remove-a-user-defined-hierarchy-from-a-dimension"></a>Per rimuovere una gerarchia definita dall'utente da una dimensione  
  
-   Nella scheda **Struttura dimensione** fare clic sulla gerarchia definita dall'utente che si vuole rimuovere nel riquadro **Gerarchie** . Fare clic su **Elimina**sulla barra degli strumenti.  
  
     - o -  
  
-   Fare clic con il pulsante destro del mouse sulla gerarchia definita dall'utente che si vuole rimuovere nel riquadro **Gerarchie** e quindi scegliere **Elimina**.  
  
     - o -  
  
-   Trascinare la gerarchia definita dall'utente al di fuori dell'area di progettazione.  
  
## <a name="see-also"></a>Vedere anche  
 [Gerarchie definite dall'utente](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/user-hierarchies.md)   
 [Creare gerarchie definite dall'utente](../../analysis-services/multidimensional-models/user-defined-hierarchies-create.md)  
  
  