---
title: ALTER VIEW (Transact-SQL) | Documenti Microsoft
ms.custom: 
ms.date: 05/10/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER_VIEW_TSQL
- ALTER VIEW
dev_langs:
- TSQL
helpviewer_keywords:
- indexed views [SQL Server], modifying
- views [SQL Server], modifying
- modifying views
- ALTER VIEW statement
ms.assetid: 03eba220-13e2-49e3-bd9d-ea9df84dc28c
caps.latest.revision: 32
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 006b9fce1e13833c977d26d4bc0f13a602f2c96c
ms.contentlocale: it-it
ms.lasthandoff: 09/01/2017

---
# <a name="alter-view-transact-sql"></a>ALTER VIEW (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Modifica una vista creata in precedenza. È possibile utilizzare questa istruzione anche per le viste indicizzate. ALTER VIEW non influisce sulle stored procedure o i trigger dipendenti e non comporta modifiche delle autorizzazioni.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
ALTER VIEW [ schema_name . ] view_name [ ( column [ ,...n ] ) ]   
[ WITH <view_attribute> [ ,...n ] ]   
AS select_statement   
[ WITH CHECK OPTION ] [ ; ]  
  
<view_attribute> ::=   
{   
    [ ENCRYPTION ]  
    [ SCHEMABINDING ]  
    [ VIEW_METADATA ]       
}   
```  
  
## <a name="arguments"></a>Argomenti  
 *schema_name*  
 Nome dello schema a cui appartiene la vista.  
  
 *view_name*  
 Vista da modificare.  
  
 *colonna*  
 Nome o elenco di nomi delimitato da virgole delle colonne che si desidera includere nella vista specificata.  
  
> [!IMPORTANT]  
>  Le autorizzazioni di colonna vengono mantenute solo se il nome delle colonne rimane uguale prima e dopo l'esecuzione dell'istruzione ALTER VIEW.  
  
> [!NOTE]  
>  Nelle colonne di una vista, le autorizzazioni assegnate per un nome di colonna rimangono valide tra istruzioni CREATE VIEW e ALTER VIEW, indipendentemente dall'origine dei dati sottostanti. Ad esempio, se vengono concesse autorizzazioni per il **SalesOrderID** colonna in un'istruzione CREATE VIEW, un'istruzione ALTER VIEW è possibile rinominare il **SalesOrderID** colonna, ad esempio in **OrderRef**e mantenere comunque le autorizzazioni associate alla vista che utilizza **SalesOrderID**.  
  
 ENCRYPTION  
 **Si applica a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Crittografa le voci nella [Sys. syscomments](../../relational-databases/system-compatibility-views/sys-syscomments-transact-sql.md) che contengono il testo dell'istruzione ALTER VIEW. Se si utilizza WITH ENCRYPTION, la vista non viene pubblicata nell'ambito della replica di SQL Server.  
  
 SCHEMABINDING  
 Associa la vista allo schema della tabella o delle tabelle sottostanti. Se si specifica SCHEMABINDING non è possibile apportare modifiche alle tabelle di base, che influiscono sulla definizione della vista. In questi casi, è necessario modificare o eliminare la definizione della vista per rimuovere le dipendenze dalla tabella da modificare. Quando si utilizza SCHEMABINDING, il *select_statement* deve includere i nomi di due parti (*schema***.** *oggetto*) di tabelle, viste o funzioni definite dall'utente a cui fa riferimento. Tutti gli oggetti a cui viene fatto riferimento devono essere presenti nello stesso database.  
  
 Le viste o tabelle che fanno parte di una vista creata con la clausola SCHEMABINDING non possono essere eliminate, a meno che tale vista non venga eliminata o modificata in modo che non sia più associata a uno schema. In caso contrario, nel [!INCLUDE[ssDE](../../includes/ssde-md.md)] viene generato un errore. Inoltre, le istruzioni ALTER TABLE eseguite su tabelle che fanno parte di viste associate a schema hanno esito negativo se modificano la definizione della vista.  
  
 VIEW_METADATA  
 Specifica che l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dovrà restituire alle API DB-Library, ODBC e OLE DB le informazioni sui metadati relativi alla vista anziché alla tabella o alle tabelle di base quando vengono richiesti metadati in modalità browse per una query che fa riferimento alla vista. I metadati in modalità browse sono metadati aggiuntivi restituiti dall'istanza di [!INCLUDE[ssDE](../../includes/ssde-md.md)] alle API DB-Library, ODBC e OLE DB sul lato client. Questi metadati consentono alle API sul lato client di implementare cursori sul lato client aggiornabili. I metadati in modalità browse includono informazioni sulla tabella di base a cui appartengono le colonne del set di risultati.  
  
 Per le viste create con VIEW_METADATA, i metadati in modalità browse restituiscono il nome della vista anziché i nomi delle tabelle di base nella descrizione delle colonne della vista nel set di risultati.  
  
 Quando viene creata una vista con WITH VIEW_METADATA, tutte le relative colonne, tranne una **timestamp** , sono aggiornabili se la vista dispone di INSERT o UPDATE INSTEAD OF attiva. Per ulteriori informazioni, vedere la sezione Osservazioni in [CREATE VIEW &#40; Transact-SQL &#41; ](../../t-sql/statements/create-view-transact-sql.md).  
  
 AS  
 Azioni che la vista deve eseguire.  
  
 *select_statement*  
 Istruzione SELECT che definisce la vista.  
  
 WITH CHECK OPTION  
 Impone a tutte le istruzioni di modifica dei dati eseguite sulla vista di soddisfare i criteri impostati nel *select_statement*.  
  
## <a name="remarks"></a>Osservazioni  
 Per ulteriori informazioni sull'istruzione ALTER VIEW, vedere la sezione Osservazioni in [CREATE VIEW &#40; Transact-SQL &#41; ](../../t-sql/statements/create-view-transact-sql.md).  
  
> [!NOTE]  
>  Se la definizione precedente della vista è stata creata con WITH ENCRYPTION o CHECK OPTION, queste opzioni vengono abilitate solo se sono incluse nell'istruzione ALTER VIEW.  
  
 Se si modifica una vista in uso con ALTER VIEW, nel [!INCLUDE[ssDE](../../includes/ssde-md.md)] viene accettato un blocco di schema esclusivo sulla vista. Quando viene concesso il blocco e non esistono utenti attivi della vista, [!INCLUDE[ssDE](../../includes/ssde-md.md)] elimina tutte le copie della vista dalla cache delle procedure. I piani esistenti che fanno riferimento alla vista rimangono nella cache, ma vengono ricompilati per chiamate successive.  
  
 È possibile utilizzare ALTER VIEW per viste indicizzate. Tuttavia, in questo caso vengono eliminati tutti gli indici nella vista, senza eccezioni.  
  
## <a name="permissions"></a>Permissions  
 Per eseguire ALTER VIEW, è richiesta come minimo l'autorizzazione ALTER per OBJECT.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene creata una vista contenente tutti i dipendenti e le relative date di assunzione, denominata `EmployeeHireDate`. Vengono concesse autorizzazioni alla vista, ma è richiesta una modifica dei requisiti per selezionare i dipendenti con date di assunzione precedenti alla data specificata. La vista viene quindi sostituita tramite l'istruzione `ALTER VIEW`.  
  
```  
USE AdventureWorks2012 ;  
GO  
CREATE VIEW HumanResources.EmployeeHireDate  
AS  
SELECT p.FirstName, p.LastName, e.HireDate  
FROM HumanResources.Employee AS e JOIN Person.Person AS  p  
ON e.BusinessEntityID = p.BusinessEntityID ;  
GO  
  
```  
  
 È necessario modificare la vista per includere solo i dipendenti assunti prima del `2002`. Se non si utilizza ALTER VIEW, ma si elimina e ricrea la vista, sarà necessario specificare nuovamente l'istruzione GRANT utilizzata in precedenza e qualsiasi altra istruzione correlata alle autorizzazioni per questa vista.  
  
```  
ALTER VIEW HumanResources.EmployeeHireDate  
AS  
SELECT p.FirstName, p.LastName, e.HireDate  
FROM HumanResources.Employee AS e JOIN Person.Person AS  p  
ON e.BusinessEntityID = p.BusinessEntityID  
WHERE HireDate < CONVERT(DATETIME,'20020101',101) ;  
GO  
  
```  
  
## <a name="see-also"></a>Vedere anche  
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [CREATE VIEW &#40;Transact-SQL&#41;](../../t-sql/statements/create-view-transact-sql.md)   
 [DROP VIEW &#40; Transact-SQL &#41;](../../t-sql/statements/drop-view-transact-sql.md)   
 [Creazione di una stored procedure](../../relational-databases/stored-procedures/create-a-stored-procedure.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [Apportare modifiche allo schema nei database di pubblicazione](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)  
  
  
