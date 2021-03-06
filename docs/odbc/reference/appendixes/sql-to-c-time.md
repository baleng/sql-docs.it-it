---
title: 'SQL a c: ora | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from SQL to C types [ODBC], time
- time data type [ODBC]
- data conversions from SQL to C types [ODBC], time
ms.assetid: 6dc59973-7bb5-40f1-87c8-5bf68b3bf2ee
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e028502bd7bc6ac1a81006d340b6ce606a0ae337
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/01/2018
ms.locfileid: "47757693"
---
# <a name="sql-to-c-time"></a>Da SQL a C: ora
L'identificatore per il periodo di tempo è il tipo di dati SQL ODBC:  
  
 SQL_TYPE_TIME  
  
 Nella tabella seguente mostra i dati ODBC C i tipi di dati a cui possono essere convertiti i dati SQL ora. Per una spiegazione delle colonne e le condizioni nella tabella, vedere [conversione di dati da SQL a tipi di dati C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md).  
  
|Identificatore di tipo C|Test|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|*BufferLength* > lunghezza in byte di caratteri<br /><br /> *9* <= *BufferLength* < = lunghezza in byte di caratteri<br /><br /> *BufferLength* < 9|data<br /><br /> Dati troncati [a]<br /><br /> Non definito|Lunghezza in byte dei dati<br /><br /> Lunghezza in byte dei dati<br /><br /> Non definito|n/d<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|*BufferLength* > lunghezza in caratteri<br /><br /> *9* <= *BufferLength* < = lunghezza in caratteri<br /><br /> *BufferLength* < 9|data<br /><br /> Dati troncati [a]<br /><br /> Non definito|Lunghezza dei dati in caratteri<br /><br /> Lunghezza dei dati in caratteri<br /><br /> Non definito|n/d<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_BINARY|Lunghezza in byte dei dati < = *BufferLength*<br /><br /> Lunghezza in byte di dati > *BufferLength*|data<br /><br /> Non definito|Lunghezza in byte dei dati<br /><br /> Non definito|n/d<br /><br /> 22003|  
|SQL_C_TYPE_TIME|Nessuno [b]|data|6 [d]|n/d|  
|SQL_C_TYPE_TIMESTAMP|Nessuno [b]|Dati [c]|16 [d]|n/d|  
  
 [a] vengono troncati i secondi frazionari del tempo.  
  
 [b] il valore di *BufferLength* viene ignorata per questa conversione. Il driver presuppone che le dimensioni di **TargetValuePtr* è la dimensione del tipo di dati C.  
  
 [c] i campi data della struttura di timestamp sono impostati sulla data corrente e il campo secondi frazionari della struttura di timestamp è impostato su zero.  
  
 [d] è la dimensione del tipo di dati C corrispondente.  
  
 Quando i dati SQL ora viene convertiti in dati di tipo carattere C, la stringa risultante è nel "*hh*:*mm*:*ss*" formato. Questo formato non è interessato dall'impostazione paese Windows®.
