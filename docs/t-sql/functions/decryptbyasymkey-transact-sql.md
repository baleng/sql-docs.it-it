---
title: DECRYPTBYASYMKEY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DECRYPTBYASYMKEY
- DECRYPTBYASYMKEY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- asymmetric keys [SQL Server], DECRYPTBYASYMKEY function
- DECRYPTBYASYMKEY function
- decryption [SQL Server], asymmetric keys
ms.assetid: d9ebcd30-f01c-4cfe-b95e-ffe6ea13788b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: cd2e34d7ceca82bf0fa9c0509092e276b1538414
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/01/2018
ms.locfileid: "47740759"
---
# <a name="decryptbyasymkey-transact-sql"></a>DECRYPTBYASYMKEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Questa funzione usa una chiave asimmetrica per decrittografare i dati crittografati.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
DecryptByAsymKey (Asym_Key_ID , { 'ciphertext' | @ciphertext }   
    [ , 'Asym_Key_Password' ] )  
```  
  
## <a name="arguments"></a>Argomenti  
 *Asym_Key_ID*  
ID di una chiave asimmetrica nel database. *Asym_Key_ID* ha un tipo di dati **int**.  
  
 *ciphertext*  
Stringa di dati crittografata con la chiave asimmetrica.  
  
 @ciphertext  
Variabile di tipo **varbinary** contenente dati crittografati con la chiave asimmetrica.  
  
 *Asym_Key_Password*  
Password usata per crittografare la chiave asimmetrica nel database.  
  
## <a name="return-types"></a>Tipi restituiti  
**varbinary** con un valore massimo di 8.000 byte.  
  
## <a name="remarks"></a>Remarks  
Rispetto alla crittografia simmetrica / decrittografia, la crittografia con chiave asimmetrica / decrittografia ha un costo elevato. Quando si lavora con set di dati di grandi dimensioni, ad esempio nel caso di dati dell'utente archiviati in tabelle, è consigliabile che gli sviluppatori evitino la crittografia con chiave asimmetrica / decrittografia.  
  
## <a name="permissions"></a>Permissions  
`DECRYPTBYASYMKEY` richiede l'autorizzazione CONTROL per la chiave asimmetrica.  
  
## <a name="examples"></a>Esempi  
In questo esempio viene decrittografato il testo originariamente crittografato con la chiave asimmetrica `JanainaAsymKey02`. `AdventureWorks2012.ProtectedData04` ha archiviato tale chiave asimmetrica. Nell'esempio sono stati decrittografati i dati restituiti con la chiave asimmetrica `JanainaAsymKey02`. Nell'esempio è stata usata la password `pGFD4bb925DGvbd2439587y` per decrittografare la chiave asimmetrica. Nell'esempio il testo non crittografato restituito è stato convertito al tipo **nvarchar**.  
  
```  
SELECT CONVERT(nvarchar(max),  
    DecryptByAsymKey( AsymKey_Id('JanainaAsymKey02'),   
    ProtectedData, N'pGFD4bb925DGvbd2439587y' ))   
AS DecryptedData   
FROM [AdventureWorks2012].[Sales].[ProtectedData04]   
WHERE Description = N'encrypted by asym key''JanainaAsymKey02''';  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [ENCRYPTBYASYMKEY &#40;Transact-SQL&#41;](../../t-sql/functions/encryptbyasymkey-transact-sql.md)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [ALTER ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-asymmetric-key-transact-sql.md)   
 [DROP ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-asymmetric-key-transact-sql.md)   
 [Scelta di un algoritmo di crittografia](../../relational-databases/security/encryption/choose-an-encryption-algorithm.md)   
 [Gerarchia di crittografia](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
