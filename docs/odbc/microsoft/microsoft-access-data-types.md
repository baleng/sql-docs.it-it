---
title: I tipi di dati Microsoft Access | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC desktop database drivers [ODBC], Access driver
- Jet-based ODBC drivers [ODBC], Access driver
- desktop database drivers [ODBC], Access driver
- Access driver [ODBC], data types
- access data types [ODBC]
- data types [ODBC], Access driver
ms.assetid: b537348a-bea0-4bd6-84a4-52a75292957f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 11f45698a5ad8b7fd05052cbb2d23520790c425a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/01/2018
ms.locfileid: "47692979"
---
# <a name="microsoft-access-data-types"></a>Tipi di dati Microsoft Access
Nella tabella seguente illustra i tipi di dati Microsoft Access, tipi di dati utilizzati per creare tabelle e tipi di dati SQL ODBC.  
  
|Tipo di dati Microsoft Access|Tipo di dati (CREATETABLE)|Tipo di dati SQL ODBC|  
|--------------------------------|-------------------------------|------------------------|  
|BIGBINARY [1]|LONGBINARY|SQL_LONGVARBINARY|  
|BINARY|BINARY|SQL_BINARY|  
|BIT|BIT|SQL_BIT|  
|CONTATORE|CONTATORE|SQL_INTEGER|  
|CURRENCY|CURRENCY|SQL_NUMERIC|  
|DATA/ORA|DATETIME|SQL_TIMESTAMP|  
|GUID|GUID|SQL_GUID|  
|BINARIO LONG|LONGBINARY|SQL_LONGVARBINARY|  
|TESTO LUNGO|LONGTEXT|SQL_WLONGVARCHAR SQL_LONGVARCHAR [2] [3]|  
|MEMO|LONGTEXT|SQL_WLONGVARCHAR SQL_LONGVARCHAR [2] [3]|  
|NUMERO (Dimensione campo = CELIBE / nubile)|SINGOLO|SQL_REAL|  
|NUMERO (Dimensione campo = valore DOUBLE)|DOUBLE|SQL_DOUBLE|  
|NUMERO (Dimensione campo = BYTE)|BYTE SENZA SEGNO|SQL_TINYINT|  
|NUMERO (Dimensione campo = INTEGER)|BREVE|SQL_SMALLINT|  
|NUMERO (Dimensione campo = valore LONG INTEGER)|LONG|SQL_INTEGER|  
|NUMERIC|NUMERIC|SQL_NUMERIC|  
|OLE|LONGBINARY|SQL_LONGVARBINARY|  
|TEXT|VARCHAR|SQL_WVARCHAR SQL_VARCHAR [1] [2]|  
ARBINARY|VARBINARY|SQL_VARBINARY|  
  
 [1] solo le applicazioni di accesso 4.0. Lunghezza massima di 4000 byte. Comportamento simile a LONGBINARY.  
  
 [2] solo applicazioni ANSI.  
  
 [3] Unicode e 4.0 di accesso solo applicazioni.  
  
> [!NOTE]  
>  **SQLGetTypeInfo** restituisce tipi di dati ODBC. Non restituirà tutti i tipi di dati di Microsoft Access se più di un tipo di accesso di Microsoft è mappato al tipo di dati SQL ODBC stesso. Tutte le conversioni nell'appendice D i *riferimento per programmatori ODBC* sono supportati per i tipi di dati SQL elencati nella tabella precedente.  
  
 La tabella seguente illustra le limitazioni sui tipi di dati Microsoft Access.  
  
|Tipo di dati|Description|  
|---------------|-----------------|  
|BINARY, VARBINARY e VARCHAR|Creazione di una colonna BINARY, VARBINARY o VARCHAR pari a zero o di lunghezza non specificata restituisce effettivamente una colonna di 510 byte.|  
|BYTE|Anche se un campo del numero di accesso ai Microsoft con una dimensione pari a BYTE senza segno, un numero negativo può essere inserito nel campo quando si usa il driver Microsoft Access.|  
|VARCHAR, LONGVARCHAR e CHAR|Un valore letterale stringa di caratteri può contenere qualsiasi carattere ANSI (1-255 decimale). Usare due virgolette singole consecutive (") per rappresentare una virgoletta singola (').<br /><br /> Usare le procedure per passare dati di tipo carattere quando si usa qualsiasi carattere speciale in una colonna di tipo di dati character.|  
|DATE|I valori delle date devono essere delimitato da secondo il formato di date canoniche ODBC o delimitati dal delimitatore di data/ora ("#"). In caso contrario, Microsoft Access considererà il valore come un'espressione aritmetica e non genera un avviso o errore.<br /><br /> Ad esempio, la data "5 marzo 1996" deve essere rappresentato come {1!d ' 1996-03-05'} & 03/05 # / 1996; o in caso contrario, se solo l'invio di 03/05/1993, Microsoft Access valuterà questo come 3 diviso 5 diviso 1996. Questo valore Arrotonda per eccesso all'intero 0, e poiché il zero-day è mappato a 1899-12-31, questa è la data utilizzata.<br /><br /> Un carattere barra verticale (&#124;) non possono essere usati in un valore di data, anche se indietro racchiuso tra virgolette.|  
|GUID|Tipo di dati limitato alla versione 4.0 di Microsoft Access.|  
|NUMERIC|Tipo di dati limitato alla versione 4.0 di Microsoft Access.|  
  
 Altre limitazioni sui tipi di dati sono disponibili nel [limitazioni del tipo di dati](../../odbc/microsoft/data-type-limitations.md).
