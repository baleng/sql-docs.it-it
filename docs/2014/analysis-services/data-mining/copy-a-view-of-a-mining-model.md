---
title: Copiare una vista di un modello di Data Mining | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- clipboards [data mining]
- Mining Model Viewer [Analysis Services], clipboards
- copying mining models to clipboard
ms.assetid: 768372db-e5b4-4990-b459-03d854fd9a6d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 62d699d068832e1b3e264a9346d03553b9a05d80
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/02/2018
ms.locfileid: "48225381"
---
# <a name="copy-a-view-of-a-mining-model"></a>Copiare una vista di un modello di data mining
  Nella scheda **Visualizzatore modello di data mining** di Progettazione modelli di data mining in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] viene usato un visualizzatore separato per ogni tipo di modello di data mining. Alcuni visualizzatori includono componenti da cui è possibile copiare i contenuti negli Appunti e quindi incollarli in un documento o in un software per la modifica di immagini. Questa funzionalità è disponibile nei componenti seguenti:  
  
-   Diagramma dei cluster nel Visualizzatore [!INCLUDE[msCoName](../../includes/msconame-md.md)] Clustering e nel Visualizzatore [!INCLUDE[msCoName](../../includes/msconame-md.md)] Sequence Clustering  
  
-   Albero delle decisioni nel Visualizzatore [!INCLUDE[msCoName](../../includes/msconame-md.md)] Trees e nel Visualizzatore [!INCLUDE[msCoName](../../includes/msconame-md.md)] Time Series  
  
-   Transizioni di stato nel Visualizzatore [!INCLUDE[msCoName](../../includes/msconame-md.md)] Sequence Clustering  
  
-   Rete di dipendenze nel Visualizzatore [!INCLUDE[msCoName](../../includes/msconame-md.md)] Association Rules, nel Visualizzatore [!INCLUDE[msCoName](../../includes/msconame-md.md)] Naive Bayes e nel Visualizzatore [!INCLUDE[msCoName](../../includes/msconame-md.md)] Decision Trees  
  
-   Contenuto del modello di data mining, dal riquadro Dettagli nodo di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Generic Content Tree Viewer  
  
 È possibile copiare l'intera rappresentazione del modello di data mining oppure solo la parte visibile nel visualizzatore.  
  
> [!WARNING]  
>  Quando si copia un modello utilizzando il visualizzatore, non si crea un nuovo oggetto modello. Per creare un nuovo modello, è necessario utilizzare la procedura guidata oppure Progettazione modelli di data mining. Per altre informazioni, vedere [Eseguire una copia di un modello di data mining](make-a-copy-of-a-mining-model.md).  
  
### <a name="to-copy-the-complete-model-to-the-clipboard"></a>Per copiare l'intero modello negli Appunti  
  
1.  Nell'elenco **Modello di data mining** nella scheda **Visualizzatore modello di data mining** selezionare il modello di data mining che si desidera visualizzare.  
  
2.  Selezionare la scheda appropriata, ad esempio la scheda **Rete di dipendenze** , quindi fare clic su **Copia grafico intero** sulla barra degli strumenti della scheda.  
  
### <a name="to-copy-the-visible-piece-of-the-model-to-the-clipboard"></a>Per copiare la parte visibile del modello negli Appunti  
  
1.  Nell'elenco **Modello di data mining** nella scheda **Visualizzatore modello di data mining** selezionare il modello di data mining che si desidera visualizzare.  
  
2.  Selezionare la scheda appropriata, ad esempio la scheda **Rete di dipendenze** , quindi ingrandire o ridurre la visualizzazione del modello in base al livello desiderato.  
  
3.  Fare clic su **Copia parte visibile del grafico** sulla barra degli strumenti della scheda selezionata.  
  
### <a name="to-copy-the-mining-model-content-to-the-clipboard"></a>Per copiare il contenuto di un modello di data mining negli Appunti  
  
1.  Nell'elenco **Modello di data mining** nella scheda **Visualizzatore modello di data mining** selezionare il modello di data mining che si desidera visualizzare.  
  
2.  Dall'elenco a discesa **Visualizzatore** selezionare **Microsoft Generic Content Tree Viewer**.  
  
3.  Nel riquadro **Didascalia nodo (ID univoco)** fare clic su un nodo.  
  
4.  Fare clic con il pulsante destro del mouse sul riquadro **Dettagli nodo** , quindi scegliere **Seleziona tutto**.  
  
5.  Fare nuovamente clic con il pulsante destro del mouse sul riquadro **Dettagli nodo** , quindi scegliere **Copia**.  
  
## <a name="see-also"></a>Vedere anche  
 [Attività e procedure relative al visualizzatore modello di data mining](mining-model-viewer-tasks-and-how-tos.md)  
  
  
