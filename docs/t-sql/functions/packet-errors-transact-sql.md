---
title: '@@PACKET_ERRORS (Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 09/18/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- '@@PACKET_ERRORS'
- '@@PACKET_ERRORS_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- '@@PACKET_ERRORS function'
- number of packet errors
- packets [SQL Server], errors
- networking [SQL Server], packet errors
- connections [SQL Server], packets
ms.assetid: f7da1b80-5cbe-42fa-be71-40c6af16383a
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 70ca00e7a75016db53ee5277034fb09f8a8e9ea1
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/01/2018
ms.locfileid: "47804229"
---
# <a name="x40x40packeterrors-transact-sql"></a>&#x40;&#x40;PACKET_ERRORS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce il numero di errori di pacchetto di rete che si sono verificati nelle connessioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dopo l'ultimo avvio di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
@@PACKET_ERRORS  
```  
  
## <a name="return-types"></a>Tipi restituiti  
 **integer**  
  
## <a name="remarks"></a>Remarks  
 Per visualizzare un report contenente dati statistici relativi a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], incluso il numero di errori dei pacchetti, eseguire **sp_monitor**.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene illustrato l'utilizzo di `@@PACKET_ERRORS`.  
  
```  
SELECT @@PACKET_ERRORS AS 'Packet Errors';  
```  
  
 Set di risultati di esempio:  
  
```  
Packet Errors  
-------------  
0  
```  
  
## <a name="see-also"></a>Vedere anche  
 [@@PACK_RECEIVED &#40;Transact-SQL&#41;](../../t-sql/functions/pack-received-transact-sql.md)   
 [@@PACK_SENT &#40;Transact-SQL&#41;](../../t-sql/functions/pack-sent-transact-sql.md)   
 [sp_monitor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-monitor-transact-sql.md)   
 [Funzioni statistiche di sistema &#40;Transact-SQL&#41;](../../t-sql/functions/system-statistical-functions-transact-sql.md)  
  
  
