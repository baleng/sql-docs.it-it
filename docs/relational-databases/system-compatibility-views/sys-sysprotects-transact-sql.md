---
title: sys.sysprotects (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysprotects
- sys.sysprotects_TSQL
- sys.sysprotects
- sysprotects_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sysprotects compatibility view
- sysprotects system table
ms.assetid: 49c9658d-fb51-4c77-94a0-fba699b0102d
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 7ce68f5f576754c8f84a5b4ac81aeef162f53c0c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/01/2018
ms.locfileid: "47763055"
---
# <a name="syssysprotects-transact-sql"></a>sys.sysprotects (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Include informazioni sulle autorizzazioni associate agli account di sicurezza nel database tramite le istruzioni GRANT e DENY.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|Nome colonna|Tipo di dati|Description|  
|-----------------|---------------|-----------------|  
|**id**|**int**|ID dell'oggetto a cui sono applicate le autorizzazioni.|  
|**uid**|**smallint**|ID dell'utente o gruppo a cui sono applicate le autorizzazioni. Causa un errore di overflow o restituisce NULL se il numero di utenti e ruoli è maggiore di 32.767.|  
|**action**|**tinyint**|Le possibili autorizzazioni sono le seguenti:<br /><br /> 26 = REFERENCES<br /><br /> 178 = CREATE FUNCTION<br /><br /> 193 = SELECT<br /><br /> 195 = INSERIMENTO<br /><br /> 196 = DELETE<br /><br /> 197 = AGGIORNAMENTO<br /><br /> 198 = CREATE TABLE<br /><br /> 203 = CREATE DATABASE<br /><br /> 207 = CREATE VIEW<br /><br /> 222 = CREATE PROCEDURE<br /><br /> 224 = EXECUTE<br /><br /> 228 = BACKUP DATABASE<br /><br /> 233 = CREATE DEFAULT<br /><br /> 235 = BACKUP LOG<br /><br /> 236 = CREATE RULE|  
|**protecttype**|**tinyint**|I possibili valori sono i seguenti:<br /><br /> 204 = GRANT_W_GRANT<br /><br /> 205 = GRANT<br /><br /> 206 = DENY|  
|**columns**|**varbinary(8000)**|Mappa di bit delle colonne a cui sono applicate le istruzioni SELECT e UPDATE.<br /><br /> Bit 0 = tutte le colonne.<br /><br /> Bit 1 = le autorizzazioni vengono applicate alla colonna specifica.<br /><br /> NULL = nessuna informazione.|  
|**Utente che concede**|**smallint**|ID dell'utente che ha eseguito le autorizzazioni GRANT o DENY. Causa un errore di overflow o restituisce NULL se il numero di utenti e ruoli è maggiore di 32.767.|  
  
## <a name="see-also"></a>Vedere anche  
 [Mapping di tabelle di sistema a viste di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Viste della compatibilità &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
