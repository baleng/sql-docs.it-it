---
title: Utilizzo dei cursori (ODBC) | Documenti Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-cursors
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, cursors
- ODBC cursors, about ODBC cursors
- ODBC applications, cursors
- cursors [ODBC]
- ODBC cursors
ms.assetid: 51322f92-0d76-44c9-9c33-9223676cf1d3
caps.latest.revision: "36"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7770a2fa27cc99d7f164db9ed3129c470bc43064
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/17/2017
---
# <a name="using-cursors-odbc"></a>Uso dei cursori (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  ODBC supporta un modello di cursore che consente:  
  
-   Diversi tipi di cursori.  
  
-   Scorrimento e posizionamento all'interno di un cursore.  
  
-   Diverse opzioni di concorrenza.  
  
-   Aggiornamenti posizionati.  
  
 Le applicazioni ODBC raramente dichiarano e aprono cursori o utilizzano istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] correlate ai cursori. ODBC apre automaticamente un cursore per ogni set di risultati restituito da un'istruzione SQL. Caratteristiche dei cursori sono controllate da attributi di istruzione impostati con [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) prima l'istruzione SQL viene eseguita l'istruzione. Le funzioni delle API ODBC per l'elaborazione di set di risultati supportano l'intervallo completo delle funzionalità del cursore, inclusi il recupero, lo scorrimento e gli aggiornamenti posizionati.  
  
 Di seguito viene presentato un confronto tra il funzionamento dei cursori nelle applicazioni ODBC e negli script [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
|Azione|[!INCLUDE[tsql](../../includes/tsql-md.md)]|ODBC|  
|------------|------------------------|----------|  
|Definire il comportamento del cursore|Specificare tramite parametri DECLARE CURSOR|Impostare gli attributi del cursore utilizzando [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)|  
|Aprire un cursore|DECLARE CURSOR OPEN *cursor_name*|**SQLExecDirect** o **SQLExecute**|  
|Recuperare righe|FETCH|**SQLFetch** o [SQLFetchScroll](../../relational-databases/native-client-odbc-api/sqlfetchscroll.md)|  
|Aggiornamento posizionato|Clausola WHERE CURRENT OF su UPDATE o DELETE|**SQLSetPos**|  
|Chiudere un cursore|Chiudi *cursor_name* DEALLOCATE|[SQLCloseCursor](../../relational-databases/native-client-odbc-api/sqlclosecursor.md)|  
  
 I cursori server implementati in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] supportano la funzionalità del modello del cursore ODBC. Il driver ODBC di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client utilizza cursori server per supportare la funzionalità del cursore dell'API ODBC.  
  
## <a name="in-this-section"></a>Argomenti della sezione  
  
-   [Modalità di implementazione dei cursori](../../relational-databases/native-client-odbc-cursors/implementation/how-cursors-are-implemented.md)  
  
-   [Tipi di cursore](../../relational-databases/native-client-odbc-cursors/cursor-types.md)  
  
-   [Comportamenti del cursore](../../relational-databases/native-client-odbc-cursors/cursor-behaviors.md)  
  
-   [Proprietà del cursore](../../relational-databases/native-client-odbc-cursors/properties/cursor-properties.md)  
  
-   [Informazioni sulla programmazione dei cursori &#40; ODBC &#41;](../../relational-databases/native-client-odbc-cursors/programming/cursor-programming-details-odbc.md)  
  
-   [Scorrimento e recupero di righe](../../relational-databases/native-client-odbc-cursors/scrolling-and-fetching-rows.md)  
  
-   [Posizionato aggiornamenti &#40; ODBC &#41;](../../relational-databases/native-client-odbc-cursors/positioned-updates-odbc.md)  
  
## <a name="see-also"></a>Vedere anche  
 [SQL Server Native Client &#40; ODBC &#41;](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)   
 [Chiudi &#40; Transact-SQL &#41;](../../t-sql/language-elements/close-transact-sql.md)   
 [Cursori](../../relational-databases/cursors.md)   
 [DEALLOCARE &#40; Transact-SQL &#41;](../../t-sql/language-elements/deallocate-transact-sql.md)   
 [DECLARE CURSOR &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-cursor-transact-sql.md)   
 [Operazione di recupero &#40; Transact-SQL &#41;](../../t-sql/language-elements/fetch-transact-sql.md)   
 [Apri &#40; Transact-SQL &#41;](../../t-sql/language-elements/open-transact-sql.md)  
  
  