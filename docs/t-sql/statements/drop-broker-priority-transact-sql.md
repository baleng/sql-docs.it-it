---
title: DROP BROKER PRIORITY (Transact-SQL) | Documenti Microsoft
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP_BROKER_PRIORITY_TSQL
- DROP BROKER PRIORITY
dev_langs:
- TSQL
helpviewer_keywords:
- DROP BROKER PRIORITY statement
ms.assetid: 09ee6c5b-af94-4a4b-a0e2-f9eac50e43aa
caps.latest.revision: 15
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 254914f3b92289faf19a37b4651e7c95804ac791
ms.contentlocale: it-it
ms.lasthandoff: 09/01/2017

---
# <a name="drop-broker-priority-transact-sql"></a>DROP BROKER PRIORITY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Rimuove una priorità di conversazione dal database corrente.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
DROP BROKER PRIORITY ConversationPriorityName  
[;]  
```  
  
## <a name="arguments"></a>Argomenti  
 *ConversationPriorityName*  
 Specifica il nome della priorità di conversazione da rimuovere.  
  
## <a name="remarks"></a>Osservazioni  
 Quando si elimina una priorità di conversazione, qualsiasi conversazione esistente continua a funzionare con i livelli di priorità assegnati dalla priorità di conversazione.  
  
## <a name="permissions"></a>Permissions  
 L'autorizzazione per la creazione di una priorità di conversazione viene assegnata per impostazione predefinita ai membri del ruolo predefinito del database db_ddladmin o db_owner e al ruolo predefinito del server sysadmin. È richiesta l'autorizzazione ALTER per il database.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene eliminata la priorità di conversazione denominata `InitiatorAToTargetPriority`.  
  
```  
DROP BROKER PRIORITY InitiatorAToTargetPriority;  
  
```  
  
## <a name="see-also"></a>Vedere anche  
 [ALTER BROKER PRIORITY &#40; Transact-SQL &#41;](../../t-sql/statements/alter-broker-priority-transact-sql.md)   
 [CREARE priorità di Service BROKER &#40; Transact-SQL &#41;](../../t-sql/statements/create-broker-priority-transact-sql.md)   
 [conversation_priorities &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-conversation-priorities-transact-sql.md)  
  
  