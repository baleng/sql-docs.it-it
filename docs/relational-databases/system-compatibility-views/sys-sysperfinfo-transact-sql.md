---
title: sys.sysperfinfo (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysperfinfo_TSQL
- sys.sysperfinfo_TSQL
- sys.sysperfinfo
- sysperfinfo
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sysperfinfo compatibility view
- sysperfinfo system table
ms.assetid: e22a81cd-27de-4690-9443-6aad6393bd3c
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 954ad81a9bbc2c2a76e825a944a292b00e478218
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/01/2018
ms.locfileid: "47596700"
---
# <a name="syssysperfinfo-transact-sql"></a>sys.sysperfinfo (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene un [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] rappresentazione dei contatori delle prestazioni interni che possono essere visualizzati tramite il monitoraggio di sistema di Windows.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|Nome colonna|Tipo di dati|Description|  
|-----------------|---------------|-----------------|  
|**object_name**|**nchar(128)**|Nome dell'oggetto prestazione, ad esempio **SQLServer:LockManager** oppure **SQLServer:BufferManager**.|  
|**counter_name**|**nchar(128)**|Nome del contatore delle prestazioni all'interno dell'oggetto, ad esempio **richieste di pagine** oppure **richieste di blocco**.|  
|**instance_name**|**nchar(128)**|Istanza denominata del contatore. Ad esempio, sono disponibili contatori mantenuti per ogni tipo di blocco, ad esempio **tabella**, **pagina**, **chiave**e così via. Il nome dell'istanza consente di contraddistinguere contatori simili.|  
|**cntr_value**|**bigint**|Valore effettivo del contatore. Spesso si tratta di un contatore a incremento progressivo costante che conta le occorrenze dell'evento dell'istanza.|  
|**cntr_type**|**int**|Tipo di contatore definito dall'architettura di controllo delle prestazioni di Windows.|  
  
## <a name="see-also"></a>Vedere anche  
 [Mapping di tabelle di sistema a viste di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Viste della compatibilità &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
