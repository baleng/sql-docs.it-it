---
title: 'Lezione 12: Analizzare in Excel | Microsoft Docs'
ms.date: 08/22/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: c42a45ec20edbde61a2f1b7c5b026f3467cd2371
ms.sourcegitcommit: e8e013b4d4fbd3b25f85fd6318d3ca8ddf73f31e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/23/2018
ms.locfileid: "42795650"
---
# <a name="lesson-12-analyze-in-excel"></a>Lezione 12: Analizzare in Excel
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

In questa lezione si utilizzerà l'analizza nella funzionalità di Excel in SSDT per aprire Microsoft Excel, creare automaticamente una connessione all'origine dati all'area di lavoro modello e aggiungere automaticamente una tabella pivot al foglio di lavoro. La funzionalità Analizza in Excel offre un metodo rapido e semplice per testare l'efficacia della progettazione del modello prima di distribuirlo. Non si eseguirà alcuna analisi dei dati in questa lezione. Lo scopo di questa lezione è acquisire familiarità con gli strumenti che è possibile utilizzare per testare la progettazione del modello. A differenza dell'utilizzo di analisi nella funzionalità di Excel, che è destinato agli autori di modelli, gli utenti finali utilizzeranno applicazioni di creazione report come Excel o Power BI per connettersi e sfogliare i dati del modello di distribuzione client.  
  
Per completare questa lezione, è necessario che Excel sia installato nello stesso computer di SSDT. Per i dettagli, vedere [Analizza in Excel](../analysis-services/tabular-models/analyze-in-excel-ssas-tabular.md).  
  
Tempo stimato per il completamento della lezione: **20 minuti**  
  
## <a name="prerequisites"></a>Prerequisiti  
Questo argomento fa parte di un'esercitazione relativa alla modellazione tabulare che deve essere completata nell'ordine specificato. Prima di eseguire le attività in questa lezione, è necessario avere completato la lezione precedente: [lezione 11: creare ruoli](../analysis-services/lesson-11-create-roles.md).  
  
## <a name="browse-using-the-default-and-internet-sales-perspectives"></a>Sfogliare il modello utilizzando la prospettiva predefinita e la prospettiva Internet Sales  
In queste prime attività, si sfoglierà il modello usando la prospettiva predefinita, che include tutti gli oggetti modello, e anche tramite la prospettiva Internet Sales è in precedenza. La prospettiva Internet Sales esclude l'oggetto Customer table.  
  
#### <a name="to-browse-by-using-the-default-perspective"></a>Per sfogliare il modello tramite la prospettiva predefinita  
  
1.  Scegliere il **Model** menu > **analizza in Excel**.  
  
2.  Nella finestra di dialogo **Analizza in Excel** fare clic su **OK**.  
  
    Verrà aperto Excel con una nuova cartella di lavoro. Viene creata una connessione all'origine dati utilizzando l'account utente corrente e la prospettiva predefinita viene utilizzata per definire campi visualizzabili. Una tabella pivot viene aggiunta automaticamente al foglio di lavoro.  
  
3.  In Excel, nel **elenco campi tabella pivot**, si noti il **DimDate** e **FactInternetSales** vengono visualizzati i gruppi di misure, nonché il **DimCustomer**, **DimDate**, **DimGeography**, **DimProduct**, **DimProductCategory**,  **DimProductSubcategory**, e **FactInternetSales** vengono visualizzate le tabelle con tutte le rispettive colonne.  
  
4.  Chiudere Excel senza salvare la cartella di lavoro.  
  
#### <a name="to-browse-by-using-the-internet-sales-perspective"></a>Per sfogliare il modello tramite la prospettiva Internet Sales  
  
1.  Scegliere il **Model** menu e quindi fare clic su **analizza in Excel**.  
  
2.  Nella finestra di dialogo **Analizza in Excel** lasciare selezionata l'opzione **Utente di Windows corrente** , quindi nell'elenco a discesa **Prospettiva** selezionare **Internet Sales**e fare clic su **OK**. 
    
    ![come-tabulare-lesson12-prospettiva](../analysis-services/media/as-tabular-lesson12-perspective.png)
    
3.  In Excel, in **PivotTable Fields**, notare che la tabella DimCustomer è esclusa dall'elenco dei campi.  
    
    ![come in formato tabulare-lesson12-campi](../analysis-services/media/as-tabular-lesson12-fields.png)
    
4.  Chiudere Excel senza salvare la cartella di lavoro.  
  
## <a name="browse-by-using-roles"></a>Sfoglia tramite i ruoli  
I ruoli sono una parte integrante di qualsiasi modello tabulare. Senza almeno un ruolo a cui gli utenti vengono aggiunti come membri, gli utenti non saranno in grado di accedere e analizzare i dati usando il modello. La funzionalità Analizza in Excel consente di testare i ruoli che sono stati definiti dall'utente.  
  
#### <a name="to-browse-by-using-the-sales-manager-user-role"></a>Per esplorare utilizzando il ruolo utente Sales Manager  
  
1.  In SSDT scegliere il **Model** menu e quindi fare clic su **analizza in Excel**.  
  
2.  Nel **analizza in Excel** nella finestra di dialogo **specificare il nome utente o ruolo da utilizzare per connettersi al modello**, selezionare **ruolo**, quindi nella casella di riepilogo discesa, selezionare **Responsabile vendite**, quindi fare clic su **OK**.  
  
    Verrà aperto Excel con una nuova cartella di lavoro. Viene creata automaticamente una tabella pivot. L'elenco di campi tabella pivot include tutti i campi dati disponibili nel nuovo modello.  
      
3.  Chiudere Excel senza salvare la cartella di lavoro.  
  
## <a name="whats-next"></a>Quali sono le operazioni successive?
Passare alla lezione successiva: [lezione 13: distribuire](../analysis-services/lesson-13-deploy.md).

  
  
  
