---
title: KEY_GUID (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- Key_GUID_TSQL
- Key_GUID
dev_langs:
- TSQL
helpviewer_keywords:
- symmetric keys [SQL Server], GUIDs
- KEY_GUID function
- GUIDs [SQL Server]
ms.assetid: 9246c7b2-7098-42c4-a222-cbf30267c46a
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 06ffb5927414cc169863dbe2435fe4221618e5cb
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/01/2018
ms.locfileid: "47799959"
---
# <a name="keyguid-transact-sql"></a>KEY_GUID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Restituisce il GUID di una chiave simmetrica nel database.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Key_GUID( 'Key_Name' )  
```  
  
## <a name="arguments"></a>Argomenti  
 **'** *Key_Name* **'**  
 Nome di una chiave simmetrica nel database.  
  
## <a name="return-types"></a>Tipi restituiti  
 **uniqueidentifier**  
  
## <a name="remarks"></a>Remarks  
 Se è stato specificato un valore Identity al momento della creazione della chiave, il relativo GUID sarà un hash MD5 di tale valore Identity. Se non è stato specificato alcun valore Identity, il GUID viene generato dal server.  
  
 Se la chiave è temporanea, il nome della chiave deve iniziare con il simbolo di cancelletto (#).  
  
## <a name="permissions"></a>Permissions  
 Dal momento che le chiavi temporanee sono disponibili solo nella sessione in cui vengono create, per accedervi non sono necessarie autorizzazioni. Per accedere a una chiave non temporanea, è necessario che il chiamante disponga di un'autorizzazione per la chiave e che non gli sia stata negata l'autorizzazione VIEW per la chiave.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene restituito il GUID di una chiave simmetrica denominata `ABerglundKey1`.  
  
```  
SELECT Key_GUID('ABerglundKey1');  
```  
  
## <a name="see-also"></a>Vedere anche  
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [sys.symmetric_keys &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-symmetric-keys-transact-sql.md)   
 [sys.key_encryptions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-key-encryptions-transact-sql.md)  
  
  
