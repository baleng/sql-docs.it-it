---
title: Valori restituiti da SQLGetInfo per Paradox | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC desktop database drivers [ODBC], Paradox driver
- SQLGetInfo function [ODBC], returned values for Paradox
- desktop database drivers [ODBC], Paradox driver
- Paradox driver [ODBC], SQLGetInfo
- Jet-based ODBC drivers [ODBC], Paradox driver
ms.assetid: 543526fb-7c54-42f7-9371-926730ca5483
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a06cfce6ca1afb23f0257c64c5acdd8695cac68b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/01/2018
ms.locfileid: "47813169"
---
# <a name="sqlgetinfo-returned-values-for-paradox"></a>Valori restituiti da SQLGetInfo per Paradox
La tabella seguente elenca il linguaggio C# defines per il *fInfoType* argomento e i corrispondenti valori restituiti dal **SQLGetInfo**. Queste informazioni possono essere recuperate passando il linguaggio C elencato #defines **SQLGetInfo** nel *fInfoType* argomento. Per altre informazioni sui valori restituiti da **SQLGetInfo**, vedere la *riferimento per programmatori ODBC*.  
  
> [!NOTE]  
>  In cui **SQLGetInfo** restituisce una maschera di bit a 32 bit, una barra verticale (&#124;) rappresenta un'operazione OR.  
  
|InfoType|Valore restituito|  
|--------------|--------------------|  
|SQL_ACCESSIBLE_PROCEDURES|"N"|  
|SQL_ACCESSIBLE_TABLES|"Y"|  
|SQL_ACTIVE_ENVIRONMENTS|0|  
|SQL_AGGREGATE_FUNCTIONS|Tutti i set|  
|SQL_ALTER_DOMAIN|0|  
|SQL_ALTER_TABLE|Più valori|  
|SQL_ASYNC_MODE|0|  
|SQL_BATCH_ROW_COUNT|0|  
|SQL_BATCH_SUPPORT|0|  
|SQL_BOOKMARK_PERSISTENCE|Più valori|  
|SQL_CATALOG_LOCATION|SQL_QL_START|  
|SQL_CATALOG_NAME|"Y"|  
|SQL_CATALOG_NAME_SEPARATOR|"\\"|  
|SQL_CATALOG_TERM|"Directory"|  
|SQL_CATALOG_USAGE|Più valori|  
|SQL_COLLATION_SEQ|""|  
|SQL_COLUMN_ALIAS|"Y"|  
|SQL_CONCAT_NULL_BEHAVIOR|SQL_CB_NON_NULL|  
|SQL_CONVERT_BIGINT|0|  
|SQL_CONVERT_BINARY|Più valori|  
|SQL_CONVERT_BIT|0|  
|SQL_CONVERT_CHAR|Più valori|  
|SQL_CONVERT_DATE|Più valori|  
|SQL_CONVERT_DECIMAL|0|  
|SQL_CONVERT_DOUBLE|Più valori|  
|SQL_CONVERT_FLOAT|Più valori|  
|SQL_CONVERT_FUNCTIONS|SQL_FN_CVT_CONVERT|  
|SQL_CONVERT_INTEGER|Più valori|  
|SQL_CONVERT_LONGVARBINARY|Più valori|  
|SQL_CONVERT_LONGVARCHAR|Più valori|  
|SQL_CONVERT_NUMERIC|Più valori|  
|SQL_CONVERT_REAL|Più valori|  
|SQL_CONVERT_SMALLINT|Più valori|  
|SQL_CONVERT_TIME|Più valori|  
|SQL_CONVERT_TIMESTAMP|Più valori|  
|SQL_CONVERT_TINYINT|Più valori|  
|SQL_CONVERT_VARBINARY|Più valori|  
|SQL_CONVERT_VARCHAR|Più valori|  
|SQL_CORRELATION_NAME|SQL_CN_ANY|  
|SQL_CREATE_ASSERTION|0|  
|SQL_CREATE_CHARACTER_SET|0|  
|SQL_CREATE_COLLATION|0|  
|SQL_CREATE_DOMAIN|0|  
|SQL_CREATE_SCHEMA|0|  
|SQL_CREATE_TABLE|SQL_CT_CREATE_TABLE|  
|SQL_CREATE_TRANSLATION|0|  
|SQL_CREATE_VIEW|0|  
|SQL_CURSOR_COMMIT_BEHAVIOR|SQL_CB_CLOSE|  
|SQL_CURSOR_ROLLBACK_BEHAVIOR|SQL_CB_CLOSE|  
|SQL_CURSOR_SENSITIVITY|SQL_UNSPECIFIED|  
|SQL_DATA_SOURCE_NAME|Il DSN di ODBC. ini, o "" se parola chiave DRIVER viene usato in ODBC. ini|  
|SQL_DATA_SOURCE_READ_ONLY|"N" (seconda sull'origine dati).|  
|SQL_DATABASE_NAME|Directory database corrente|  
|SQL_DATETIME_LITERALS|0|  
|SQL_DBMS_NAME|"PARADOX"|  
|SQL_DBMS_VER|Più valori|  
|SQL_DDL_INDEX|Più valori|  
|SQL_DEFAULT_TXN_ISOLATION|0|  
|SQL_DESCRIBE_PARAMETER|0|  
|SQL_DRIVER_HDBC|Gestito da Gestione Driver.|  
|SQL_DRIVER_HENV|Gestito da Gestione Driver.|  
|SQL_DRIVER_HLIB|Gestito da Gestione Driver.|  
|SQL_DRIVER_HSTMT|Gestito da Gestione Driver.|  
|SQL_DRIVER_NAME|"OdbcJt32.dll"|  
|SQL_DRIVER_ODBC_VER|"3.51.0000"|  
|SQL_DRIVER_VER|"4.00.*nnnn*" (*nnnn* specifica la data di compilazione)|  
|SQL_DROP_ASSERTION|0|  
|SQL_DROP_CHARACTER_SET|0|  
|SQL_DROP_COLLATION|0|  
|SQL_DROP_DOMAIN|0|  
|SQL_DROP_SCHEMA|0|  
|SQL_DROP_TABLE|SQL_DT_DROP_TABLE|  
|SQL_DROP_TRANSLATION|0|  
|SQL_DROP_VIEW|SQL_DV_DROP_VIEW|  
|SQL_EXPRESSIONS_IN_ORDERBY|"Y"|  
|SQL_FILE_USAGE|SQL_FILE_TABLE|  
|SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1|SQL_CA1_NEXT|  
|SQL_GETDATA_EXTENSIONS|Più valori|  
|SQL_GROUP_BY|SQL_GB_GROUP_BY_CONTAINS_SELECT|  
|SQL_IDENTIFIER_CASE|SQL_IC_MIXED|  
|SQL_IDENTIFIER_QUOTE_CHAR|"'" (virgolette inverse)|  
|SQL_KEYWORDS|Più valori|  
|SQL_LIKE_ESCAPE_CLAUSE|"N"|  
|SQL_MAX_BINARY_LITERAL_LEN|255|  
|SQL_MAX_CATALOG_NAME_LEN|66|  
|SQL_MAX_CHAR_LITERAL_LEN|255|  
|SQL_MAX_COLUMN_NAME_LEN|25|  
|SQL_MAX_COLUMNS_IN_GROUP_BY|10|  
|SQL_MAX_COLUMNS_IN_INDEX|0 (limitare sconosciuto o non applicabile)|  
|SQL_MAX_COLUMNS_IN_ORDER_BY|10|  
|SQL_MAX_COLUMNS_IN_SELECT|255|  
|SQL_MAX_COLUMNS_IN_TABLE|255|  
|SQL_MAX_CONCURRENT_ACTIVITIES|0|  
|SQL_MAX_CURSOR_NAME_LEN|64|  
|SQL_MAX_DRIVER_CONNECTIONS|64|  
|SQL_MAX_INDEX_SIZE|1350|  
|SQL_MAX_PROCEDURE_NAME_LEN|0|  
|SQL_MAX_ROW_SIZE|1350|  
|SQL_MAX_ROW_SIZE_INCLUDES_LONG|"N"|  
|SQL_MAX_SCHEMA_NAME_LEN|0|  
|SQL_MAX_STATEMENT_LEN|65000|  
|SQL_MAX_TABLE_NAME_LEN|12|  
|SQL_MAX_TABLES_IN_SELECT|16|  
|SQL_MAX_USER_NAME_LEN|0|  
|SQL_MULT_RESULT_SETS|"N"|  
|SQL_MULTIPLE_ACTIVE_TXN|"Y"|  
|SQL_NEED_LONG_DATA_LEN|"N"|  
|SQL_NON_NULLABLE_COLUMNS|SQL_NNC_NON_NULL|  
|SQL_NULL_COLLATION|SQL_NC_LOW|  
|SQL_NUMERIC_FUNCTIONS|Più valori|  
|SQL_ODBC_SAG_CLI_ CONFORMANCE|SQL_OSCC_COMPLIANT|  
|SQL_ODBC_SQL_INTEGRITY|"N"|  
|SQL_ODBC_VER|Da Gestione Driver|  
|SQL_OJ_CAPABILITIES|Più valori|  
|SQL_ORDER_BY_COLUMNS_IN_SELECT|"N"|  
|SQL_OUTER_JOINS|"Y"|  
|SQL_PROCEDURE_TERM|""|  
|SQL_PROCEDURES|"N"|  
|SQL_QUOTED_IDENTIFIER_CASE|SQL_IC_MIXED|  
|SQL_ROW_UPDATES|"N"|  
|SQL_SCHEMA_TERM|""|  
|SQL_SCHEMA_USAGE|0|  
|SQL_SCROLL_OPTIONS|Più valori|  
|SQL_SEARCH_PATTERN_ESCAPE|"\\"|  
|SQL_SERVER_NAME|"PARADOX"|  
|SQL_SPECIAL_CHARACTERS|"~`@#$%^&*_-+=\\}{"';:?/><,.!'[]&#124;"|  
|SQL_STRING_FUNCTIONS|Più valori|  
|SQL_SUBQUERIES|Più valori|  
|SQL_SYSTEM_FUNCTIONS|0|  
|SQL_TABLE_TERM|"TABLE"|  
|SQL_TIMEDATE_ADD_INTERVALS|0|  
|SQL_TIMEDATE_DIFF_INTERVALS|0|  
|SQL_TIMEDATE_FUNCTIONS|Più valori|  
|SQL_TXN_CAPABLE|SQL_TC_NONE|  
|SQL_TXN_ISOLATION_OPTION|0|  
|SQL_UNION|Più valori|  
|SQL_USER_NAME|""|
