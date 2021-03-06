---
title: Lo scorrimento e recupero di righe (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- scrollable cursors [ODBC]
- fetches [ODBC], scrollable cursors
- cursors [ODBC], scrollable
- scrolling rows [ODBC]
ms.assetid: c43764cb-5841-4b89-9dc0-984a7488b3c1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 884c798e14964fbcaaf3ca9ba6656f4d62738fe8
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/01/2018
ms.locfileid: "47642749"
---
# <a name="scrolling-and-fetching-rows-odbc"></a>Scorrimento e recupero di righe (ODBC)
Quando si usa un cursore scorrevole, le applicazioni chiamano **SQLFetchScroll** per posizionare il cursore e recuperare le righe. **SQLFetchScroll** supporta lo scorrimento relativo (successivo e precedente relativo *n* righe), lo scorrimento assoluto (, cognome e di riga *n*) e il posizionamento dal segnalibro. Il *FetchOrientation* e *FetchOffset* argomenti nel **SQLFetchScroll** specificare quale set di righe da recuperare, come illustrato nelle figure seguenti.  
  
 ![Recupero del successivo, precedente, primo e ultimo set di righe](../../../odbc/reference/develop-app/media/pr20_2.gif "pr20_2")  
  
 **Recupero del successivo, precedente, primo e ultimo set di righe**  
  
 ![Recupero set di righe assoluto, relativo e con segnalibro](../../../odbc/reference/develop-app/media/pr20_1.gif "pr20_1")  
  
 **Il recupero dei set di righe assoluto, relativo e con segnalibro**  
  
 **SQLFetchScroll** posiziona il cursore nella riga specificata e restituisce le righe nel set di righe a partire da tale riga. Se il set di righe specificato si sovrappone la fine del set di risultati, viene restituito un set di righe parziale. Se il set di righe specificato si sovrappone all'inizio del risultato è impostato, il primo set di righe nel risultato viene in genere restituito gruppo; Per informazioni dettagliate, vedere la [SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md) descrizione della funzione.  
  
 In alcuni casi, l'applicazione potrebbe essere necessario posizionare il cursore senza recuperare Nessun dato. Ad esempio, è possibile verificare l'esistenza di una riga oppure ottenere semplicemente il segnalibro per la riga senza visualizzare altri dati attraverso la rete. A tale scopo, imposta l'attributo di istruzione SQL_ATTR_RETRIEVE_DATA SQL_RD_OFF. La variabile associata alla colonna segnalibro (se presente) viene sempre aggiornata, indipendentemente dall'impostazione di questo attributo di istruzione.  
  
 Dopo aver recuperato il set di righe, l'applicazione può chiamare **SQLSetPos** per posizionarsi su una particolare riga nelle righe del set di righe o l'aggiornamento del set di righe. Per altre informazioni sull'uso **SQLSetPos**, vedere [aggiornamento dei dati con SQLSetPos](../../../odbc/reference/develop-app/updating-data-with-sqlsetpos.md).  
  
> [!NOTE]  
>  Lo scorrimento è supportato in ODBC 2. *x* i driver **SQLExtendedFetch**. Per altre informazioni, vedere [cursori rettangolari, cursori scorrevoli e compatibilità con le versioni precedenti](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md)nell'appendice g: Driver le linee guida per la compatibilità con le versioni precedenti.
