---
title: Restituzione di SQL_NO_DATA | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL_NO_DATA [ODBC]
- backward compatibility [ODBC], SQL_NO_DATA
- compatibility [ODBC], SQL_NO_DATA
ms.assetid: deed0163-9d1a-4e9b-9342-3f82e64477d2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 74c122819980abaa328db5ad46f240cae24b92d3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/01/2018
ms.locfileid: "47686379"
---
# <a name="returning-sqlnodata"></a>Restituzione di SQL_NO_DATA
Quando un'applicazione ODBC 2. *x* dell'applicazione con un'applicazione ODBC 3 *. x* driver chiama **SQLExecDirect**, **SQLExecute**, o **SQLParamData**, e un'istruzione delete o aggiornamento con ricerca è stato eseguito ma non ha sulle eventuali righe nell'origine dati, ODBC 3*x* driver deve restituire SQL_SUCCESS. Quando un'applicazione ODBC 3 *. x* funziona con un'applicazione ODBC 3 *. x* driver chiama **SQLExecDirect**, **SQLExecute**, o  **SQLParamData** con lo stesso risultato, ODBC 3*x* driver restituisca SQL_NO_DATA.  
  
 Se una ricerca istruzione update o delete in un batch di istruzioni non influenza tutte le righe nell'origine dati, **SQLMoreResults** restituisce SQL_SUCCESS. Non può restituire SQL_NO_DATA, perché ciò significa che non sono presenti altri risultati, non che vi sia un risultato da una update/delete con ricerca che nessun righe interessate.
