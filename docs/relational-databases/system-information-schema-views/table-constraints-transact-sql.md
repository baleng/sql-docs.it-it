---
title: TABLE_CONSTRAINTS (Transact-SQL) | Documenti Microsoft
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-information-schema-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- TABLE_CONSTRAINTS
- TABLE_CONSTRAINTS_TSQL
dev_langs: TSQL
helpviewer_keywords:
- INFORMATION_SCHEMA.TABLE_CONSTRAINTS view
- TABLE_CONSTRAINTS view
ms.assetid: 687f3284-2849-4853-8a5c-fc936deceae0
caps.latest.revision: "25"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 4b5b62068ab1afb9d697686d259b7fa6d1222a56
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/21/2017
---
# <a name="tableconstraints-transact-sql"></a>TABLE_CONSTRAINTS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Restituisce una riga per ogni vincolo di tabella del database corrente. Questa vista degli schemi delle informazioni restituisce informazioni sugli oggetti per i quali l'utente dispone di autorizzazioni.  
  
 Per recuperare informazioni da queste viste, specificare il nome completo di **INFORMATION_SCHEMA.** *view_name*.  
  
|Nome colonna|Tipo di dati|Description|  
|-----------------|---------------|-----------------|  
|**CONSTRAINT_CATALOG**|**nvarchar (**128**)**|Qualificatore del vincolo.|  
|**CONSTRAINT_SCHEMA**|**nvarchar (**128**)**|Nome dello schema che contiene il vincolo.<br /><br /> **\*\*Importante \* \***  non utilizzare viste INFORMATION_SCHEMA per determinare lo schema di un oggetto. L'unica modalità affidabile per cercare lo schema di un oggetto consiste nell'eseguire una query sulla vista del catalogo sys.objects.|  
|**CONSTRAINT_NAME**|**sysname**|Nome del vincolo.|  
|**TABLE_CATALOG**|**nvarchar (**128**)**|Qualificatore della tabella.|  
|**TABLE_SCHEMA**|**nvarchar (**128**)**|Nome dello schema che contiene la tabella.<br /><br /> **\*\*Importante \* \***  non utilizzare viste INFORMATION_SCHEMA per determinare lo schema di un oggetto. L'unica modalità affidabile per cercare lo schema di un oggetto consiste nell'eseguire una query sulla vista del catalogo sys.objects.|  
|**TABLE_NAME**|**sysname**|Nome della tabella.|  
|**CONSTRAINT_TYPE**|**varchar (**11**)**|Tipo di vincolo:<br /><br /> CHECK<br /><br /> UNIQUE<br /><br /> PRIMARY KEY<br /><br /> FOREIGN KEY|  
|**IS_DEFERRABLE**|**varchar (**2**)**|Specifica se è possibile posticipare la verifica dei vincoli. Restituisce sempre NO.|  
|**INITIALLY_DEFERRED**|**varchar (**2**)**|Specifica se la verifica dei vincoli viene inizialmente posticipata. Restituisce sempre NO.|  
  
## <a name="see-also"></a>Vedere anche  
 [Viste di sistema &#40; Transact-SQL &#41;](http://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [Viste degli schemi delle informazioni &#40; Transact-SQL &#41;](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [Sys. Objects &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [Sys. key_constraints &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-key-constraints-transact-sql.md)   
 [Sys. CHECK_CONSTRAINTS &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-check-constraints-transact-sql.md)   
 [sys.tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md)  
  
  