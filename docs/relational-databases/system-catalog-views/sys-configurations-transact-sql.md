---
title: Sys. Configurations (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.configurations_TSQL
- configurations
- sys.configurations
- configurations_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.configurations catalog view
ms.assetid: c4709ed1-bf88-4458-9e98-8e9b78150441
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5f1a2ae2d0d8f8c5eea00ed5d31ad8aadb88e5ef
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/01/2018
ms.locfileid: "47596109"
---
# <a name="sysconfigurations-transact-sql"></a>sys.configurations (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene una riga per ciascun valore di un'opzione di configurazione valida per l'intero server impostata nel sistema.  
|Nome colonna|Tipo di dati|Description|  
|-----------------|---------------|-----------------|  
|**configuration_id**|**int**|ID univoco del valore di configurazione.|  
|**name**|**nvarchar(35)**|Nome dell'opzione di configurazione.|  
|**Valore**|**sql_variant**|Valore configurato per l'opzione.|  
|**minimum**|**sql_variant**|Valore minimo dell'opzione di configurazione.|  
|**maximum**|**sql_variant**|Valore massimo dell'opzione di configurazione.|  
|**value_in_use**|**sql_variant**|Valore corrente dell'opzione.|  
|**description**|**nvarchar(255)**|Descrizione dell'opzione di configurazione.|  
|**is_dynamic**|**bit**|1 = La variabile viene applicata quando viene eseguita l'istruzione RECONFIGURE.|  
|**is_advanced**|**bit**|1 = la variabile viene visualizzata solo quando la **mostrare advancedoption** è impostata.|  
  
 Per un elenco di tutte le opzioni di configurazione di server, vedere [opzioni di configurazione Server &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md).  
  
> [!NOTE]  
>  Per le opzioni di configurazione a livello di database, vedere [ALTER DATABASE ambito di configurazione &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md). Per configurare Soft-NUMA, vedere [Soft-NUMA &#40;di SQL Server&#41;](../../database-engine/configure-windows/soft-numa-sql-server.md).  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'appartenenza al ruolo **public** . Per altre informazioni, vedere [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Viste del catalogo a livello di server di configurazione &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/server-wide-configuration-catalog-views-transact-sql.md)   
 [Viste del catalogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
