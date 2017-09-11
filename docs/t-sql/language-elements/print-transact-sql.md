---
title: PRINT (Transact-SQL) | Documenti Microsoft
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- PRINT_TSQL
- PRINT
dev_langs:
- TSQL
helpviewer_keywords:
- PRINT statement
- user-defined messages [SQL Server]
- messages [SQL Server], PRINT statement
- displaying user-defined messages
- viewing user-defined messages
- conditionally returning messages [SQL Server]
ms.assetid: 32ba0729-c4b5-4cfb-a5aa-e8b9402be028
caps.latest.revision: 33
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 51377ebe291fe4c76d8761aaba74eab8f5201108
ms.contentlocale: it-it
ms.lasthandoff: 09/01/2017

---
# <a name="print-transact-sql"></a>STAMPA-Transact-SQL
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Restituisce al client un messaggio definito dall'utente.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  

PRINT msg_str | @local_variable | string_expr  
```  
  
## <a name="arguments"></a>Argomenti  
 *argomento msg_str*  
 Costante di stringa Unicode o stringa di caratteri. Per ulteriori informazioni, vedere [costanti &#40; Transact-SQL &#41; ](../../t-sql/data-types/constants-transact-sql.md).  
  
 **@***local_variable*  
 Variabile costituita da un qualunque tipo di dati character valido. **@***local_variable* deve essere **char**, **nchar**, **varchar**, o **nvarchar**, o deve essere in grado di essere Questo campo viene convertito in modo implicito per i tipi di dati.  
  
 *string_expr*  
 Espressione che restituisce una stringa. Può includere variabili, funzioni e valori letterali concatenati. Per altre informazioni, vedere [Espressioni &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md).  
  
## <a name="remarks"></a>Osservazioni  
 Una stringa di messaggio può contenere al massimo 8.000 caratteri se è una stringa non Unicode e 4.000 caratteri se è una stringa Unicode. Le stringhe più lunghe vengono troncate. Il **varchar (max)** e **nvarchar (max)** tipi di dati vengono troncati in tipi di dati che non superano **varchar(8000)** e **nvarchar(4000)**.  
  
 È possibile utilizzare anche RAISERROR per restituire messaggi. RAISERROR offre questi vantaggi rispetto a PRINT:  
  
-   RAISERROR supporta la sostituzione di argomenti in una stringa di messaggio di errore utilizzando un meccanismo basato sulla funzione printf della libreria standard del linguaggio C.  
  
-   RAISERROR consente di specificare un numero di errore univoco, un livello di gravità e un codice di stato, oltre al messaggio di testo.  
  
-   È possibile utilizzare RAISERROR per restituire messaggi definiti dall'utente creati tramite la stored procedure di sistema sp_addmessage.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-conditionally-executing-print-if-exists"></a>A. Stampa eseguita in modo condizionale (IF EXISTS)  
 Nell'esempio seguente viene utilizzata l'istruzione `PRINT` per restituire un messaggio in modo condizionale.  
  
```  
IF @@OPTIONS & 512 <> 0  
    PRINT N'This user has SET NOCOUNT turned ON.';  
ELSE  
    PRINT N'This user has SET NOCOUNT turned OFF.';  
GO  
```  
  
### <a name="b-building-and-displaying-a-string"></a>B. Compilazione e visualizzazione di una stringa  
 Nell'esempio seguente i risultati della funzione `GETDATE` vengono convertiti nel tipo di dati `nvarchar` e concatenati con il testo letterale restituito dall'istruzione `PRINT`.  
  
```  
-- Build the message text by concatenating  
-- strings and expressions.  
PRINT N'This message was printed on '  
    + RTRIM(CAST(GETDATE() AS nvarchar(30)))  
    + N'.';  
GO  
-- This example shows building the message text  
-- in a variable and then passing it to PRINT.  
-- This was required in SQL Server 7.0 or earlier.  
DECLARE @PrintMessage nvarchar(50);  
SET @PrintMessage = N'This message was printed on '  
    + RTRIM(CAST(GETDATE() AS nvarchar(30)))  
    + N'.';  
PRINT @PrintMessage;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Esempi: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-conditionally-executing-print"></a>C. Stampa eseguita in modo condizionale  
 Nell'esempio seguente viene utilizzata l'istruzione `PRINT` per restituire un messaggio in modo condizionale.  
  
```  
IF DB_ID() = 1  
    PRINT N'The current database is master.';  
ELSE  
    PRINT N'The current database is not master.';  
GO  
```  
  
### <a name="d-building-and-displaying-a-string"></a>D. Compilazione e visualizzazione di una stringa  
 Nell'esempio seguente i risultati della funzione `GETDATE` vengono convertiti nel tipo di dati `nvarchar` e concatenati con il testo letterale restituito dall'istruzione `PRINT`.  
  
```  
-- Build the message text by concatenating  
-- strings and expressions.  
PRINT N'This message was printed on '  
    + RTRIM(CAST(GETDATE() AS nvarchar(30)))  
    + N'.';  
GO  
-- This example shows building the message text  
-- in a variable and then passing it to PRINT.  
DECLARE @PrintMessage nvarchar(50);  
SET @PrintMessage = N'This message was printed on '  
    + RTRIM(CAST(GETDATE() AS nvarchar(30)))  
    + N'.';  
PRINT @PrintMessage;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Tipi di dati &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
 [RAISERROR &#40; Transact-SQL &#41;](../../t-sql/language-elements/raiserror-transact-sql.md)  
  
  

