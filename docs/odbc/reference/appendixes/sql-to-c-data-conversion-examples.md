---
title: SQL a C esempi di conversione dati | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data conversions from SQL to C types [ODBC], examples
- converting data from SQL to C types [ODBC], examples
ms.assetid: 0190c76c-7f9b-42f4-be9d-cef7284840fd
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c528a4a7bf60aae399924d651443e574ba9ae4fb
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/01/2018
ms.locfileid: "47778729"
---
# <a name="sql-to-c-data-conversion-examples"></a>Esempi di conversione di dati da SQL a C
Gli esempi mostrati nella tabella seguente viene illustrato come il driver converte i dati SQL ai dati C:  
  
|Tipo SQL<br /><br /> identificatore|SQL data<br /><br /> Valore|Tipo C<br /><br /> identificatore|Buffer<br /><br /> length|**TargetValuePtr*|SQLSTATE|  
|-----------------------------|------------------------|---------------------------|-----------------------|------------------------|--------------|  
|SQL_CHAR|abcdef|SQL_C_CHAR|7|abcdef\0 [a]|n/d|  
|SQL_CHAR|abcdef|SQL_C_CHAR|6|abcde\0 [a]|01004|  
|SQL_DECIMAL|1234.56|SQL_C_CHAR|8|1234.56\0 [a]|n/d|  
|SQL_DECIMAL|1234.56|SQL_C_CHAR|5|1234\0 [a]|01004|  
|SQL_DECIMAL|1234.56|SQL_C_CHAR|4|----|22003|  
|SQL_DECIMAL|1234.56|SQL_C_FLOAT|Ignorato|1234.56|n/d|  
|SQL_DECIMAL|1234.56|SQL_C_SSHORT|Ignorato|1234|01S07|  
|SQL_DECIMAL|1234.56|SQL_C_STINYINT|Ignorato|----|22003|  
SQL_DOUBLE|1.2345678|SQL_C_DOUBLE|Ignorato|1.2345678|n/d|  
|SQL_DOUBLE|1.2345678|SQL_C_FLOAT|Ignorato|1.234567|n/d|  
|SQL_DOUBLE|1.2345678|SQL_C_STINYINT|Ignorato|1|n/d|  
|SQL_TYPE_DATE|1992-12-31|SQL_C_CHAR|11|1992-12-31\0 [a]|n/d|  
|SQL_TYPE_DATE|1992-12-31|SQL_C_CHAR|10|-----|22003|  
|SQL_TYPE_DATE|1992-12-31|SQL_C_TIMESTAMP|Ignorato|1992,12,31, 0,0,0,0 [b]|n/d|  
|SQL_TYPE_TIMESTAMP|1992-12-31 23:45:55.12|SQL_C_CHAR|23|[a] 23:45:55.12\0 1992-12-31|n/d|  
SQL_TYPE_TIMESTAMP|1992-12-31 23:45:55.12|SQL_C_CHAR|22|[a] 23:45:55.1\0 1992-12-31|01004|  
|SQL_TYPE_TIMESTAMP|1992-12-31 23:45:55.12|SQL_C_CHAR|18|----|22003|  
  
 [a] "\0" rappresenta un byte di terminazione null. Il driver sempre null fa terminare con i dati SQL_C_CHAR.  
  
 [b] i numeri in questo elenco sono i numeri memorizzati nei campi della struttura TIMESTAMP_STRUCT.
