---
title: Esempio di diagnostica di Driver basati su file | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- file-based driver diagnostic [ODBC]
- diagnostic information [ODBC], examples
- error messages [ODBC], diagnostic messages
ms.assetid: 0575fccd-4641-478d-a3cc-5a764e35bae2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: decb09098cee4b9ab6473e3c622b9917a89e9b09
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/01/2018
ms.locfileid: "47809319"
---
# <a name="file-based-driver-diagnostic-example"></a>Esempio di diagnostica di driver basato su file
Un driver basati su file agisce sia come un driver ODBC come origine dati. Può pertanto generare errori e avvisi sia come componente in una connessione ODBC e come un'origine dati. Poiché si tratta anche il componente che si interfaccia con gestione Driver, viene formattato e restituisce gli argomenti per **SQLGetDiagRec**.  
  
 Ad esempio, se un driver Microsoft® per dBASE non è riuscito ad allocare memoria sufficiente, potrebbe restituire i valori seguenti dal **SQLGetDiagRec**:  
  
```  
SQLSTATE:         "HY001"  
Native Error:      42052  
Diagnostic Msg:   "[Microsoft][ODBC dBASE Driver]Unable to allocate sufficient memory."  
```  
  
 Poiché questo errore non è correlato all'origine dati, il driver aggiunto solo i prefissi per il messaggio di diagnostica per il fornitore ([Microsoft]) e il driver ([Driver dBASE ODBC]).  
  
 Se il driver non è stato possibile trovare il file Employee. dbf, potrebbe restituire i valori seguenti dal **SQLGetDiagRec**:  
  
```  
SQLSTATE:         "42S02"  
Native Error:      -1305  
Diagnostic Msg:   "[Microsoft][ODBC dBASE Driver][dBASE]No such table or object"  
```  
  
 Poiché questo errore è correlato all'origine dati, il driver aggiunto il formato di file dell'origine dati ([dBASE]) come prefisso per il messaggio di diagnostica. Poiché il driver è stato anche il componente che interfaccia duale con l'origine dati, aggiunto i prefissi per il fornitore ([Microsoft]) e il driver ([Driver dBASE ODBC]).
