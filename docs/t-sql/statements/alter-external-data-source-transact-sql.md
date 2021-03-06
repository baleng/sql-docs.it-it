---
title: ALTER EXTERNAL DATA SOURCE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/09/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER EXTERNAL DATA SOURCE
- ALTER_EXTERNAL_DATA_SOURCE
dev_langs:
- TSQL
helpviewer_keywords:
- polybase, alter external data source statement
- ALTER EXTERNAL DATA SOURCE statement
ms.assetid: a34b9e90-199d-46d0-817a-a7e69387bf5f
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 3654e06666c4b8d9639cf3d6ce792cdf80e4cdd6
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/27/2018
ms.locfileid: "52396814"
---
# <a name="alter-external-data-source-transact-sql"></a>ALTER EXTERNAL DATA SOURCE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Modifica un'origine dati esterna usata per creare una tabella esterna. L'origine dati esterna può essere un'archiviazione BLOB di Azure o di Hadoop.
  
## <a name="syntax"></a>Sintassi  
  
```  
-- Modify an external data source
-- Applies to: SQL Server (2016 or later)
ALTER EXTERNAL DATA SOURCE data_source_name SET
    {   
        LOCATION = 'server_name_or_IP' [,] |
        RESOURCE_MANAGER_LOCATION = <'IP address;Port'> [,] |
        CREDENTIAL = credential_name
    }  
    [;]  

-- Modify an external data source pointing to Azure Blob storage
-- Applies to: SQL Server (starting with 2017)
ALTER EXTERNAL DATA SOURCE data_source_name
    WITH (
        TYPE = BLOB_STORAGE,
        LOCATION = 'https://storage_account_name.blob.core.windows.net'
        [, CREDENTIAL = credential_name ]
    )  
```  
  
## <a name="arguments"></a>Argomenti  
 data_source_name Specifica il nome definito dall'utente per l'origine dati. Il nome deve essere univoco.
  
 LOCATION = 'server_name_or_IP' Specifica il nome del server o un indirizzo IP.
  
 RESOURCE_MANAGER_LOCATION = '\<IP address;Port>' Specifica la Gestione risorse di Hadoop. Quando specificato, Query Optimizer può scegliere di pre-elaborare i dati di una query PolyBase usando le funzionalità di calcolo di Hadoop. Questa decisione si basa sui costi. La cosiddetta distribuzione del predicato può ridurre notevolmente il volume dei dati trasferiti tra Hadoop e SQL e pertanto migliorare le prestazioni delle query.
  
 CREDENTIAL = Credential_Name Specifica la credenziale denominata. Vedere [CREATE DATABASE SCOPED CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-database-scoped-credential-transact-sql.md).

TYPE = BLOB_STORAGE   
**Si applica a:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)].
Solo per le operazioni bulk, `LOCATION` deve essere l'URL valido dell'archiviazione BLOB di Azure. Non inserire **/**, nome file o parametri di firma per l'accesso condiviso alla fine dell'URL `LOCATION`.
La credenziale usata deve essere creata usando `SHARED ACCESS SIGNATURE` come identità. Per altre informazioni sulle firme di accesso condiviso, vedere [Uso delle firme di accesso condiviso](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1).

  
  
## <a name="remarks"></a>Remarks
 È possibile modificare una sola origine per volta. Le richieste simultanee di modifica della stessa origine mettono in attesa un'istruzione. È invece possibile modificare origini diverse nello stesso momento. Questa istruzione può essere eseguita contemporaneamente ad altre istruzioni.
  
## <a name="permissions"></a>Permissions  
 È necessaria l'autorizzazione ALTER ANY EXTERNAL DATA SOURCE.
 > [!IMPORTANT]  
 >  L'autorizzazione ALTER ANY EXTERNAL DATA SOURCE concede a qualsiasi entità di sicurezza la possibilità di creare e modificare qualsiasi oggetto origine dati esterna e, di conseguenza, la possibilità di accedere a tutte le credenziali con ambito database per il database. Questa autorizzazione deve essere considerata con privilegi elevati e quindi essere concessa solo a entità attendibili nel sistema.

  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene modificato il percorso e il percorso di Gestione risorse di un'origine dati esistente.
  
```  
ALTER EXTERNAL DATA SOURCE hadoop_eds SET
     LOCATION = 'hdfs://10.10.10.10:8020',
     RESOURCE_MANAGER_LOCATION = '10.10.10.10:8032'
    ;
  
```  

 Nell'esempio seguente viene modificata la credenziale per connettersi a un'origine dati esistente.
  
```  
ALTER EXTERNAL DATA SOURCE hadoop_eds SET
   CREDENTIAL = new_hadoop_user
    ;
```
