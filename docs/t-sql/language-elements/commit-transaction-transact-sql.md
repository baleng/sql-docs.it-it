---
title: COMMIT TRANSACTION (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/09/2016
ms.prod: sql
ms.prod_service: sql-data-warehouse, database-engine, pdw, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- COMMIT
- COMMIT TRANSACTION
- COMMIT_TSQL
- COMMIT_TRANSACTION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ending transactions [SQL Server]
- user-defined transactions [SQL Server]
- committed transactions
- transactions [SQL Server], ending
- marking end of transactions [SQL Server]
- implicit transactions
- distributed transactions [SQL Server], committed
- transactions [SQL Server], committed
- COMMIT TRANSACTION statement
- rolling back transactions, COMMIT TRANSACTION
ms.assetid: f8fe26a9-7911-497e-b348-4e69c7435dc1
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 3b4a2ef2ec0367bdae858578f07cc062fd5cf50d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/01/2018
ms.locfileid: "47799409"
---
# <a name="commit-transaction-transact-sql"></a>COMMIT TRANSACTION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Contrassegna la fine di una transazione esplicita o implicita completata correttamente. Se il valore di @@TRANCOUNT è 1, COMMIT TRANSACTION rende permanenti nel database tutte le modifiche dei dati apportate dall'inizio della transazione, libera le risorse usate dalla transazione e decrementa il valore di @@TRANCOUNT a 0. Se il valore di @@TRANCOUNT è maggiore di 1, COMMIT TRANSACTION decrementa il valore di @@TRANCOUNT di una sola unità e la transazione rimane attiva.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
-- Applies to SQL Server (starting with 2008) and Azure SQL Database
  
COMMIT [ { TRAN | TRANSACTION }  [ transaction_name | @tran_name_variable ] ] [ WITH ( DELAYED_DURABILITY = { OFF | ON } ) ]  
[ ; ]  
```  
 
```  
-- Applies to Azure SQL Data Warehouse and Parallel Data Warehouse Database
  
COMMIT [ TRAN | TRANSACTION ] 
[ ; ]  
``` 
 
  
## <a name="arguments"></a>Argomenti  
 *transaction_name*  
 **SI APPLICA A:** SQL Server e database SQL di Azure
 
 Ignorato dal [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. *transaction_name* consente di specificare il nome di una transazione assegnato da un'istruzione BEGIN TRANSACTION precedente. *transaction_name* deve essere conforme alle regole relative agli identificatori ma non può superare i 32 caratteri. *transaction_name* può essere usato per facilitare la lettura del codice da parte dei programmatori, indicando quale istruzione BEGIN TRANSACTION annidata è associata a COMMIT TRANSACTION.  
  
 *@tran_name_variable*  
 **SI APPLICA A:** SQL Server e database SQL di Azure  
 
Nome di una variabile definita dall'utente contenente un nome di transazione valido. La variabile deve essere dichiarata con un tipo di dati char, varchar, nchar o nvarchar. Se vengono passati più di 32 caratteri alla variabile vengono utilizzati solo i primi 32 caratteri. Quelli rimanenti vengono troncati.  
  
 DELAYED_DURABILITY  
 **SI APPLICA A:** SQL Server e database SQL di Azure   

 Opzione che richiede il commit della transazione con durabilità posticipata. La richiesta viene ignorata se il database è stato modificato con `DELAYED_DURABILITY = DISABLED` o `DELAYED_DURABILITY = FORCED`. Per altre informazioni, vedere l'argomento [Controllare la durabilità delle transazioni](../../relational-databases/logs/control-transaction-durability.md).  
  
## <a name="remarks"></a>Remarks  
 È compito del programmatore di [!INCLUDE[tsql](../../includes/tsql-md.md)] eseguire l'istruzione COMMIT TRANSACTION solo quando tutti i dati a cui la transazione fa riferimento sono logicamente corretti.  
  
 Se la transazione di cui è stato eseguito il commit è una transazione distribuita di [!INCLUDE[tsql](../../includes/tsql-md.md)], l'istruzione COMMIT TRANSACTION attiva l'utilizzo di un protocollo di commit in due fasi in MS DTC per il commit di tutti i server coinvolti nella transazione. Se una transazione locale si estende su due o più database nella stessa istanza di [!INCLUDE[ssDE](../../includes/ssde-md.md)], per eseguire il commit di tutti i database coinvolti nella transazione viene utilizzato un commit a due fasi interno.  
  
 Quando viene eseguito in transazioni nidificate, il commit delle transazioni interne non libera risorse o non rende permanenti le modifiche. Queste operazioni vengono eseguite solo durante il commit delle transazioni esterne. Ogni COMMIT TRANSACTION eseguita quando il valore di @@TRANCOUNT è maggiore di 1 decrementa il valore di @@TRANCOUNT di una unità. Quando il valore di @@TRANCOUNT risulta uguale a 0, viene eseguito il commit dell'intera transazione esterna. Poiché *transaction_name* viene ignorato dal [!INCLUDE[ssDE](../../includes/ssde-md.md)], l'esecuzione di COMMIT TRANSACTION con riferimento al nome di una transazione esterna quando esistono transazioni interne in attesa comporta la riduzione del valore di @@TRANCOUNT di una unità.  
  
 L'esecuzione di COMMIT TRANSACTION quando @@TRANCOUNT è uguale a 0 genera un errore. Non esiste infatti alcuna istruzione BEGIN TRANSACTION corrispondente.  
  
 Non è possibile eseguire il rollback di una transazione dopo l'esecuzione di un'istruzione COMMIT TRANSACTION. Le modifiche dei dati del database sono diventate permanenti.  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] incrementa il conteggio delle transazioni all'interno di un'istruzione solo quando il numero di transazioni all'inizio dell'istruzione è uguale a 0.  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'appartenenza al ruolo **public** .  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-committing-a-transaction"></a>A. Esecuzione del commit di una transazione  
**SI APPLICA A:** SQL Server, database SQL di Azure, Azure SQL Data Warehouse e Parallel Data Warehouse   

Nell'esempio seguente viene eliminato un candidato di processo. Viene usato AdventureWorks. 
  
```   
BEGIN TRANSACTION;   
DELETE FROM HumanResources.JobCandidate  
    WHERE JobCandidateID = 13;   
COMMIT TRANSACTION;   
```  
  
### <a name="b-committing-a-nested-transaction"></a>B. Esecuzione del commit di una transazione nidificata  
**SI APPLICA A:** SQL Server e database SQL di Azure    

Nell'esempio seguente viene creata una tabella, viene generata una transazione nidificata su tre livelli e viene quindi eseguito il commit della transazione nidificata. Sebbene ogni istruzione `COMMIT TRANSACTION` includa un parametro *transaction_name*, non esiste alcuna relazione tra le istruzioni `COMMIT TRANSACTION` e `BEGIN TRANSACTION`. I parametri *transaction_name* migliorano semplicemente il grado di leggibilità del codice per consentire al programmatore di verificare che venga codificato il numero adeguato di commit per il decremento del valore di `@@TRANCOUNT` a 0 e che venga quindi eseguito il commit della transazione esterna. 
  
```   
IF OBJECT_ID(N'TestTran',N'U') IS NOT NULL  
    DROP TABLE TestTran;  
GO  
CREATE TABLE TestTran (Cola int PRIMARY KEY, Colb char(3));  
GO  
-- This statement sets @@TRANCOUNT to 1.  
BEGIN TRANSACTION OuterTran;  
  
PRINT N'Transaction count after BEGIN OuterTran = '  
    + CAST(@@TRANCOUNT AS nvarchar(10));  
 
INSERT INTO TestTran VALUES (1, 'aaa');  
 
-- This statement sets @@TRANCOUNT to 2.  
BEGIN TRANSACTION Inner1;  
 
PRINT N'Transaction count after BEGIN Inner1 = '  
    + CAST(@@TRANCOUNT AS nvarchar(10));  
  
INSERT INTO TestTran VALUES (2, 'bbb');  
  
-- This statement sets @@TRANCOUNT to 3.  
BEGIN TRANSACTION Inner2;  
  
PRINT N'Transaction count after BEGIN Inner2 = '  
    + CAST(@@TRANCOUNT AS nvarchar(10));  
  
INSERT INTO TestTran VALUES (3, 'ccc');  
  
-- This statement decrements @@TRANCOUNT to 2.  
-- Nothing is committed.  
COMMIT TRANSACTION Inner2;  
 
PRINT N'Transaction count after COMMIT Inner2 = '  
    + CAST(@@TRANCOUNT AS nvarchar(10));  
 
-- This statement decrements @@TRANCOUNT to 1.  
-- Nothing is committed.  
COMMIT TRANSACTION Inner1;  
 
PRINT N'Transaction count after COMMIT Inner1 = '  
    + CAST(@@TRANCOUNT AS nvarchar(10));  
  
-- This statement decrements @@TRANCOUNT to 0 and  
-- commits outer transaction OuterTran.  
COMMIT TRANSACTION OuterTran;  
  
PRINT N'Transaction count after COMMIT OuterTran = '  
    + CAST(@@TRANCOUNT AS nvarchar(10));  
```  
  
## <a name="see-also"></a>Vedere anche  
 [BEGIN DISTRIBUTED TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-distributed-transaction-transact-sql.md)   
 [BEGIN TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-transaction-transact-sql.md)   
 [COMMIT WORK &#40;Transact-SQL&#41;](../../t-sql/language-elements/commit-work-transact-sql.md)   
 [ROLLBACK TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/rollback-transaction-transact-sql.md)   
 [ROLLBACK WORK &#40;Transact-SQL&#41;](../../t-sql/language-elements/rollback-work-transact-sql.md)   
 [SAVE TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/save-transaction-transact-sql.md)   
 [@@TRANCOUNT &#40;Transact-SQL&#41;](../../t-sql/functions/trancount-transact-sql.md)  
  
  
