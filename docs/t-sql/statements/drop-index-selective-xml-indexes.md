---
title: DROP INDEX (indici XML selettivi) | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP XML INDEX statement
dev_langs:
- TSQL
ms.assetid: 4779ae84-e5f4-4d04-8fc1-e24a6631b428
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: db937bd1a5ce723e071acb5077059235a9261193
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/01/2018
ms.locfileid: "47739453"
---
# <a name="drop-index-selective-xml-indexes"></a>DROP INDEX (indici XML selettivi)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Elimina un indice XML selettivo esistente o secondario in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per altre informazioni vedere [Indici XML selettivi &#40;SXI&#41;](../../relational-databases/xml/selective-xml-indexes-sxi.md).  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
DROP INDEX index_name ON <object>  
    [ WITH ( <drop_index_option> [ ,...n ] ) ]  
  
<object> ::=  
{  
    [ database_name. [ schema_name ] . | schema_name. ]   
        table_or_view_name  
}  
  
<drop_index_option> ::=  
{  
    MAXDOP = max_degree_of_parallelism  
    | ONLINE = { ON | OFF }  
}  
```  
  
##  <a name="Arguments"></a> Argomenti  
 *index_name*  
 Nome dell'indice esistente che si desidera eliminare.  
  
 *\< object>* Tabella contenente la colonna XML indicizzata. Utilizzare uno dei seguenti formati:  
  
-   `database_name.schema_name.table_name`  
  
-   `database_name..table_name`  
  
-   `schema_name.table_name`  
  
-   `table_name`  
  
 *\<drop_index_option>* Per informazioni sulle opzioni di eliminazione dell'indice, vedere [DROP INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/drop-index-transact-sql.md).  
  
## <a name="security"></a>Security  
  
### <a name="permissions"></a>Permissions  
 Per eseguire DROP INDEX, è necessario disporre dell'autorizzazione ALTER per la tabella o la vista. Questa autorizzazione viene concessa per impostazione predefinita al ruolo predefinito del server sysadmin e ai ruoli predefiniti del database db_ddladmin e db_owner.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene illustrata un'istruzione DROP INDEX.  
  
```  
DROP INDEX sxi_index ON tbl;  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Indici XML selettivi &#40;SXI&#41;](../../relational-databases/xml/selective-xml-indexes-sxi.md)   
 [Creare, modificare o eliminare indici XML selettivi](../../relational-databases/xml/create-alter-and-drop-selective-xml-indexes.md)  
  
  

