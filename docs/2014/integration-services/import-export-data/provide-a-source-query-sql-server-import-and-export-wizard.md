---
title: Impostazione query di origine (Importazione/Esportazione guidata SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.impexpwizard.providesourcequery.f1
ms.assetid: c8cbd07e-b9c3-422f-94b8-d6fc8cf31cf5
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 3abb49fa9e2e73ae5c610b5e940a6deba5079d62
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/02/2018
ms.locfileid: "48069861"
---
# <a name="provide-a-source-query-sql-server-import-and-export-wizard"></a>Impostazione query di origine (Importazione/Esportazione guidata SQL Server)
  Usare la **impostazione Query di origine** pagina digitare l'istruzione SQL che genera i dati da copiare dall'origine dati nella destinazione.  
  
 Per altre informazioni su questa procedura guidata, vedere [SQL Server importazione / esportazione guidata](import-and-export-data-with-the-sql-server-import-and-export-wizard.md). Per altre informazioni sulle opzioni per avviare la procedura guidata, nonché le autorizzazioni necessarie per eseguire correttamente la procedura guidata, vedere [esecuzione di SQL Server importazione / esportazione guidata](start-the-sql-server-import-and-export-wizard.md).  
  
 Lo scopo di Importazione/Esportazione guidata SQL Server è la copia di dati da un'origine a una destinazione. La procedura guidata può inoltre creare automaticamente un database di destinazione e le tabelle di destinazione. Se tuttavia è necessario copiare più database o tabelle, o altri tipi di oggetti di database, è preferibile utilizzare Copia guidata database. Per altre informazioni, vedere [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md).  
  
## <a name="options"></a>Opzioni  
 **Istruzione SQL**  
 Consente di immettere un'istruzione di query per il recupero delle righe di dati selezionate dal database di origine. Ad esempio, la query seguente istruzione recupera le **SalesPersonID**, **SalesQuota**, e **SalesYTD** di AdventureWorks database per i venditori la cui proprietà percentuale di Commissione è superiore all'1,5%.  
  
```  
SELECT SalesPersonID, SalesQuota, SalesYTD  
FROM Sales.SalesPerson  
WHERE CommissionPct > 0.015  
```  
  
 **Analizza**  
 Controlla la sintassi dell'istruzione SQL nella casella di testo **Istruzione SQL**.  
  
> [!NOTE]  
>  Se il tempo necessario per il controllo della sintassi dell'istruzione supera il valore di timeout di 30 secondi, l'analisi si arresta e viene generato un errore. Non sarà possibile andare oltre questa pagina della procedura guidata fino a quando l'analisi non avrà esito positivo. Una soluzione possibile consiste nel creare una vista di database basata sulla query ed eseguire la query sulla vista dalla procedura guidata, anziché immettere direttamente il testo della query.  
  
 **Sfoglia**  
 Selezionare un file contenente un'istruzione SQL usando il **aperto** nella finestra di dialogo. Selezione di un file copia il testo dal file nei **istruzione di Query** casella di testo.  
  
  
