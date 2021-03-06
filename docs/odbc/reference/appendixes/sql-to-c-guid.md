---
title: 'SQL a c: GUID | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from SQL to C types [ODBC], GUID
- data conversions from SQL to C types [ODBC], guid
- GUID data type [ODBC]
ms.assetid: cf56c684-c261-4b89-994a-db14ab2241d6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 21054bdb3f869a0f06349b32e481144b3582de4e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/01/2018
ms.locfileid: "47848999"
---
# <a name="sql-to-c-guid"></a>Da SQL a C: GUID
L'identificatore per il tipo di dati SQL ODBC GUID è:  
  
 SQL_GUID  
  
 Nella tabella seguente mostra i dati ODBC C i tipi di dati a cui possono essere convertiti i dati di SQL GUID. Per una spiegazione delle colonne e le condizioni nella tabella, vedere [conversione di dati da SQL a tipi di dati C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md).  
  
|Identificatore di tipo C|Test|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|*BufferLength* > lunghezza in byte di caratteri|data|36|n/d|  
||*BufferLength* < 37|Non definito|Non definito|22003|  
|SQL_C_WCHAR|*BufferLength* > lunghezza in caratteri|data|36|n/d|  
||*BufferLength* < 37|Non definito|Non definito|22003|  
|SQL_C_BINARY|Lunghezza in byte dei dati \< =  *BufferLength*|data|Lunghezza in byte dei dati|n/d|  
||Lunghezza in byte di dati > *BufferLength*|Non definito|Non definito|22003|  
|SQL_C_GUID|Nessuno [a]|data|16 [b]|n/d|  
  
 [a] hodnotou *BufferLength* viene ignorata per questa conversione. Il driver presuppone che le dimensioni di **TargetValuePtr* è la dimensione del tipo di dati C.  
  
 [b] questa è la dimensione del tipo di dati C corrispondente.
