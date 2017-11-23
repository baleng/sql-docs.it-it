---
title: sp_execute_remote (Database SQL di Azure) | Documenti Microsoft
ms.custom: 
ms.date: 02/01/2017
ms.prod: 
ms.prod_service: sql-database
ms.reviewer: 
ms.service: sql-database
ms.component: system-stored-procedures
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sp_execute_remote
- sp_execute_remote_TSQL
helpviewer_keywords:
- remote execution
- queries, remote execution
ms.assetid: ca89aa4c-c4c1-4c46-8515-a6754667b3e5
caps.latest.revision: "17"
author: CarlRabeler
ms.author: carlrab
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f3ce5718a35f8411a5333a200d6ea75f2326c79e
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/17/2017
---
# <a name="spexecuteremote-azure-sql-database"></a>sp_execute_remote (Database SQL di Azure)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Esegue un [!INCLUDE[tsql](../../includes/tsql-md.md)] istruzione su un singolo Database SQL di Azure remoto o un set di database che funge da partizioni in uno schema di partizionamento orizzontale.  
  
 La stored procedure è parte della funzionalità di query flessibile.  Vedere [panoramica delle query di Database di SQL Azure database elastico](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-overview/) e [query di database elastico per il partizionamento orizzontale (partizionamento orizzontale)](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-horizontal-partitioning/).  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
sp_execute_remote [ @data_source_name = ] datasourcename  
[ , @stmt = ] statement  
[   
  { , [ @params = ] N'@parameter_name data_type [,...n ]' }   
     { , [ @param1 = ] 'value1' [ ,...n ] }  
]  
```  
  
## <a name="arguments"></a>Argomenti  
 [ @data_source_name =] *datasourcename*  
 Identifica l'origine dati esterna in cui viene eseguita l'istruzione. Vedere [Crea origine dati esterna &#40; Transact-SQL &#41; ](../../t-sql/statements/create-external-data-source-transact-sql.md). L'origine dati esterna può essere di tipo "RDBMS" o "SHARD_MAP_MANAGER".  
  
 [ @stmt=] *istruzione*  
 È una stringa Unicode che contiene un [!INCLUDE[tsql](../../includes/tsql-md.md)] istruzione o il batch. @stmtdeve essere una costante Unicode o una variabile Unicode. Non sono consentite le espressioni Unicode più complesse, ad esempio per la concatenazione di due stringhe tramite l'operatore +. Le costanti di tipo carattere non sono consentite. Se viene specificata una costante Unicode, devono essere preceduto da un **N**. Ad esempio, la costante Unicode **n' sp_who'** è valido, ma la costante carattere **'sp_who'** non. Le dimensioni massime della stringa dipendono dalla memoria disponibile nel server di database. Nel server a 64 bit, le dimensioni della stringa sono limitata a 2 GB, la dimensione massima di **nvarchar (max)**.  
  
> [!NOTE]  
>  @stmtpuò contenere parametri con lo stesso formato di un nome di variabile, ad esempio:`N'SELECT * FROM HumanResources.Employee WHERE EmployeeID = @IDParameter'`  
  
 A ogni parametro incluso in @stmt deve corrispondere una voce nell'elenco delle definizioni dei parametri @params e nell'elenco dei valori dei parametri.  
  
 [ @params=] N'@*parameter_name**data_type* [,... *n* ] '  
 Stringa contenente le definizioni di tutti i parametri che sono stati incorporati in @stmt. La stringa deve essere una costante o una variabile Unicode. Ogni definizione di parametro è costituita da un nome del parametro e da un tipo di dati. *n*è un segnaposto che indica definizioni di parametro aggiuntive. Ogni parametro specificato in @stmtmust essere definito in @params. Se l'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] o il batch in @stmt non contiene parametri, @params non è necessario. Il valore predefinito per questo parametro è NULL.  
  
 [ @param1=] '*value1*'  
 Valore per il primo parametro definito nella stringa di parametri. Il valore può essere una costante o una variabile Unicode. È necessario che sia disponibile un valore di parametro per ogni parametro incluso in @stmt. I valori non sono necessari se l'istruzione o il batch [!INCLUDE[tsql](../../includes/tsql-md.md)] in @stmt è privo di parametri.  
  
 *n*  
 Segnaposto per i valori di parametri aggiuntivi. I valori possono essere solo costanti o variabili. Non sono consentite espressioni più complesse quali funzioni o espressioni compilate tramite operatori.  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o valore diverso da zero (esito negativo)  
  
## <a name="result-sets"></a>Set di risultati  
 Restituisce il set di risultati dalla prima istruzione SQL.  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'autorizzazione `ALTER ANY EXTERNAL DATA SOURCE`.  
  
## <a name="remarks"></a>Osservazioni  
 `sp_execute_remote`i parametri devono essere inseriti nell'ordine specifico, come descritto nella sezione relativa alla sintassi precedente. Se i parametri non vengono immessi in ordine, verrà visualizzato un messaggio di errore.  
  
 `sp_execute_remote`ha lo stesso comportamento come [EXECUTE &#40; Transact-SQL &#41; ](../../t-sql/language-elements/execute-transact-sql.md) per quanto riguarda i batch e l'ambito dei nomi. L'istruzione Transact-SQL o il batch nel sp_execute_remote  *@stmt*  parametro non viene compilato finché non viene eseguita l'istruzione sp_execute_remote.  
  
 `sp_execute_remote`Aggiunge una colonna aggiuntiva al set di risultati denominato '$ShardName' che contiene il nome del database remoto che ha generato la riga.  
  
 `sp_execute_remote`può essere utilizzato come [sp_executesql &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-executesql-transact-sql.md).  
  
## <a name="examples"></a>Esempi  
### <a name="simple-example"></a>Esempio semplice  
 Nell'esempio seguente crea ed esegue un'istruzione SELECT semplice in un database remoto.  
  
```tsql  
EXEC sp_execute_remote  
    N'MyExtSrc',  
    N'SELECT COUNT(w_id) AS Count_id FROM warehouse'   
```  
  
### <a name="example-with-multiple-parameters"></a>Esempio con più parametri  
Creare le credenziali con ambito database in un database utente, specificare le credenziali di amministratore per il database master. Creare un'origine dati esterna che punta al database master e specificando le credenziali con ambito database. Quindi seguente, riportato nel database utente, viene eseguito il `sp_set_firewall_rule` procedure nel database master. Il `sp_set_firewall_rule` procedura richiede 3 parametri e richiede il `@name` parametro Unicode.

```
EXEC sp_execute_remote @data_source_name  = N'PointToMaster', 
@stmt = N'sp_set_firewall_rule @name, @start_ip_address, @end_ip_address', 
@params = N'@name nvarchar(128), @start_ip_address varchar(50), @end_ip_address varchar(50)',
@name = N'TempFWRule', @start_ip_address = '0.0.0.2', @end_ip_address = '0.0.0.2';
```

## <a name="see-also"></a>Vedere anche:

[CREARE CON AMBITO DATABASE DELLE CREDENZIALI](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)  
[CREARE l'origine dati esterna (Transact-SQL)](../../t-sql/statements/create-external-data-source-transact-sql.md)  
    