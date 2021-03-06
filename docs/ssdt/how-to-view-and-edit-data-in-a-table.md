---
title: 'Procedura: Visualizzare e modificare dati in una tabella | Microsoft Docs'
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- SQL.DATA.TOOLS.QUERYRESULTS.F1
- sql.data.tools.queryresults.executequerydeletingrow
ms.assetid: bb67ce83-a87a-4e14-84cd-9a5930fe74c8
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 543611c2e5c327d50ea7155969a670ac4a0e836e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/01/2018
ms.locfileid: "47685431"
---
# <a name="how-to-view-and-edit-data-in-a-table"></a>Procedura: Visualizzazione e modifica di dati in una tabella
È possibile visualizzare, modificare ed eliminare dati di una tabella esistente utilizzando un editor dei dati visivo.  
  
> [!WARNING]  
> Nelle procedure seguenti vengono usate entità create nelle procedure precedenti nella sezione [Sviluppo del database connesso](../ssdt/connected-database-development.md).  
  
### <a name="to-edit-data-in-a-table-visually-using-the-data-editor"></a>Per modificare i dati in una tabella utilizzando visivamente l'Editor dati  
  
1.  Fare clic con il pulsante destro del mouse sulla tabella **Products** in **Esplora oggetti di SQL Server** e selezionare **Visualizza dati**.  
  
2.  Verrà avviato l'Editor dati. Si notino le righe aggiunte alla tabella nelle procedure precedenti.  
  
3.  Fare clic con il pulsante destro del mouse sulla tabella **Fruits** in Esplora oggetti di SQL Server e selezionare **Visualizza dati**.  
  
4.  Nell'Editor dati digitare **1** per **Id** e **True** per **Perishable**, quindi premere INVIO o il tasto TAB per spostare lo stato attivo dalla nuova riga affinché sia possibile eseguirne il commit nel database.  
  
5.  Ripetere il passaggio sopra indicato per immettere **2**, **False** e **3**, **False** nella tabella.  
  
    Si noti che quando si modifica una riga, è sempre possibile ripristinare le modifiche apportate a una cella premendo ESC.  
  
6.  È possibile visualizzare le modifiche come script facendo clic sul pulsante **Script** nella barra degli strumenti. In alternativa, è possibile usare il pulsante **Genera script nel file** per salvarle in un file di script con estensione sql da eseguire in un secondo momento.  
  
7.  Fare clic con il pulsante destro del mouse sul database **Trade** in **Esplora oggetti di SQL Server** e selezionare **Nuova query**. Nell'editor digitare `select * from dbo.PerishableFruits` e premere il pulsante **Esegui query** per restituire i dati rappresentati dalla vista `PerishableFruits`.  
  
