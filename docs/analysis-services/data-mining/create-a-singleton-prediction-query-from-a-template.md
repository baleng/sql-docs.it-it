---
title: Creare una Query di stima Singleton da un modello | Documenti Microsoft
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: baa6153adde1a5cc5aaeaad5f8b04366dcb2dad8
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/10/2018
ms.locfileid: "34019768"
---
# <a name="create-a-singleton-prediction-query-from-a-template"></a>Creare una query di stima singleton da un modello
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Una query singleton è utile quando si dispone di un modello che si desidera utilizzare per la stima, ma non si desidera eseguire il mapping a un set di dati di input esterno oppure eseguire stime bulk. Con una query singleton, è possibile fornire uno o più valori al modello e ottenere all'istante il valore stimato.  
  
 Ad esempio, la query DMX seguente rappresenta una query singleton sul modello di mailing diretto, TM_Decision_Tree.  
  
```  
SELECT * FROM [TM_Decision_tree] ;  
NATURAL PREDICTION JOIN  
(SELECT '2' AS [Number Children At Home], '45' as [Age])  
AS [t]  
```  
  
 La procedura che segue descrive come usare Esplora modelli in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] per creare rapidamente questa query.  
  
### <a name="to-open-the-analysis-services-templates-in-sql-server-management-studio"></a>Per aprire i modelli di Analysis Services in SQL Server Management Studio  
  
1.  In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]scegliere **Esplora modelli** dal menu **Visualizza**.  
  
2.  Fare clic sull'icona del cubo per aprire i modelli di **Analysis Server**.  
  
### <a name="to-open-a-prediction-query-template"></a>Per aprire un modello di query di stima  
  
1.  Nell'elenco di modelli di Analysis Server in **Esplora modelli**espandere **DMX**, quindi espandere **Query di stima**.  
  
2.  Fare doppio clic su **Query di stima singleton**.  
  
3.  Nella finestra di dialogo **Connetti ad Analysis Services** digitare il nome del server con l'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] che contiene il modello di data mining su cui eseguire la query.  
  
4.  Fare clic su **Connetti**.  
  
5.  Il modello si apre nel database specificato, insieme con un Visualizzatore oggetti del modello di data mining che contiene le funzioni del data mining e un elenco di strutture di data mining e i modelli correlati.  
  
### <a name="to-customize-the-singleton-query-template"></a>Per personalizzare il modello della query singleton  
  
1.  Nel modello fare clic sull'elenco a discesa **Database disponibili** e quindi selezionare un'istanza di Analysis Services dall'elenco.  
  
2.  Nell'elenco **Modello di data mining** selezionare il modello di data mining su cui si desidera eseguire una query.  
  
     L'elenco di colonne nel modello di data mining viene visualizzato nel riquadro **Metadati** del Visualizzatore oggetti.  
  
3.  Scegliere **Imposta valori per parametri modello** dal menu **Query**.  
  
4.  Nella riga dell' **elenco di selezione** digitare * per ottenere tutte le colonne oppure digitare un elenco delimitato da virgole di colonne ed espressioni per ottenere colonne specifiche.  
  
     Se si digita *, viene restituita la colonna stimabile, insieme con le colonne per le quali vengono forniti nuovi valori nel passaggio 6.  
  
     Per il codice di esempio mostrato all'inizio di questo argomento, la riga dell' **elenco di selezione** è stata impostata su *.  
  
5.  Nella riga del **modello di data mining** digitare il nome del modello di data mining tra quelli presenti nell'elenco dei modelli di data mining visualizzati in **Esplora oggetti**.  
  
     Per il codice di esempio mostrato all'inizio di questo argomento, la riga del **modello di data mining** è stata impostata sul nome, **TM_Decision_Tree**.  
  
6.  Nella riga del **valore** digitare il nuovo valore dei dati per il quale si desidera effettuare una stima.  
  
     Per il codice di esempio mostrato all'inizio di questo argomento, la riga del **valore** è stata impostata su **2** per stimare il comportamento relativo all'acquisto di biciclette sulla base del numero di figli a carico.  
  
7.  Nella riga della **colonna** digitare il nome della colonna nel modello di data mining su cui deve essere eseguito il mapping dei nuovi dati.  
  
     Per il codice di esempio mostrato all'inizio di questo argomento, la riga della **colonna** è stata impostata su **Number Children at Home**.  
  
    > [!NOTE]  
    >  Quando si usa la finestra di dialogo **Specifica valori per parametri modello** , non è necessario racchiudere il nome della colonna tra parentesi quadre. Le parentesi verranno aggiunte automaticamente.  
  
8.  Lasciare l' **alias di input** su **t**.  
  
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
10. Nel riquadro del testo della query cercare la sottolineatura rossa sotto la virgola e i puntini di sospensione che indicano un errore di sintassi. Eliminare i puntini di sospensione e aggiungere le condizioni di query aggiuntive desiderate. Se non si aggiungono altre condizioni, eliminare la virgola.  
  
     Per il codice di esempio mostrato all'inizio di questo argomento, la condizione di query aggiuntive è stata impostata su **'45' as [Age]**.  
  
11. Fare clic su **Esegui**.  
  
## <a name="see-also"></a>Vedere anche  
 [Creazione di stime & #40; Esercitazione di base di Data Mining & #41;](http://msdn.microsoft.com/library/a8410ed2-bb98-4d51-a9eb-b239be1201c2)  
  
  
