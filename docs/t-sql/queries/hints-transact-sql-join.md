---
title: Hint di join (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- Join Hint
- Join_Hint_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- HASH join hint
- REMOTE join hint
- LOOP join hint
- join hints
- MERGE join hint
- hints [SQL Server], join
ms.assetid: 09069f4a-f2e3-4717-80e1-c0110058efc4
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 270aaf41f6cb081f3c57156c10e3b448540a6731
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/01/2018
ms.locfileid: "47621349"
---
# <a name="hints-transact-sql---join"></a>Hint (Transact-SQL) - Join
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gli hint di join specificano che Query Optimizer deve imporre una strategia di join tra due tabelle in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Per informazioni generali sui join e sulla relativa sintassi, vedere [FROM &#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md).  
  
> [!IMPORTANT]  
>  Poiché Query Optimizer di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sceglie in genere il piano di esecuzione migliore per una query, è consigliabile che gli hint come \<join_hint> vengano usati solo se strettamente necessario da sviluppatori e amministratori esperti di database.
  
 **Si applica a:**  
  
 [DELETE](../../t-sql/statements/delete-transact-sql.md)  
  
 [SELECT](../../t-sql/queries/select-transact-sql.md)  
  
 [UPDATE](../../t-sql/queries/update-transact-sql.md)  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
<join_hint> ::=   
     { LOOP | HASH | MERGE | REMOTE }  
```  
  
## <a name="arguments"></a>Argomenti  
 LOOP | HASH | MERGE  
 Specifica che il join della query deve essere un join ciclico, hash o di merge. L'utilizzo delle opzioni LOOP | HASH | MERGE consente di applicare un join specifico tra due tabelle. Non è possibile specificare LOOP come tipo di join insieme a RIGHT o FULL.  
  
 REMOTE  
 Specifica che l'operazione di join viene eseguita nella posizione della tabella di destra. Ciò risulta utile quando la tabella di sinistra è una tabella locale e la tabella di destra è una tabella remota. Utilizzare l'opzione REMOTE solo quando il numero di righe della tabella di sinistra è inferiore a quello della tabella di destra.  
  
 Se la tabella di destra è locale, il join viene eseguito localmente. Se entrambe le tabelle sono remote ma l'origine dei dati è diversa, con l'opzione REMOTE il join viene eseguito nella posizione della tabella di destra. Se entrambe le tabelle sono tabelle remote dalla stessa origine dei dati, l'opzione REMOTE non è necessaria.  
  
 Non è possibile utilizzare l'opzione REMOTE quando per uno dei valori confrontati nel predicato di join viene eseguito il casting su regole di confronto diverse tramite la clausola COLLATE.  
  
 L'opzione REMOTE può essere utilizzata solo per operazioni INNER JOIN.  
  
## <a name="remarks"></a>Remarks  
 Gli hint di join vengono specificati nella clausola FROM di una query e consentono di imporre una strategia di join tra due tabelle. Se tra due tabelle viene specificato un hint di join, Query Optimizer impone in modo automatico l'ordine di join per tutte le tabelle unite in join della query, in base alla posizione delle parole chiave ON. Se si utilizza un CROSS JOIN senza la clausola ON, è possibile utilizzare le parentesi per indicare l'ordine di join.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-using-hash"></a>A. Utilizzo di HASH  
 Nell'esempio seguente viene specificato che l'operazione `JOIN` nella query viene eseguita da un join `HASH`. Nell'esempio viene utilizzato il database [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
```  
SELECT p.Name, pr.ProductReviewID  
FROM Production.Product AS p  
LEFT OUTER HASH JOIN Production.ProductReview AS pr  
ON p.ProductID = pr.ProductID  
ORDER BY ProductReviewID DESC;  
```  
  
### <a name="b-using-loop"></a>B. Utilizzo di LOOP  
 Nell'esempio seguente viene specificato che l'operazione `JOIN` nella query viene eseguita da un join `LOOP`. Nell'esempio viene utilizzato il database [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
```  
DELETE FROM Sales.SalesPersonQuotaHistory   
FROM Sales.SalesPersonQuotaHistory AS spqh  
    INNER LOOP JOIN Sales.SalesPerson AS sp  
    ON spqh.SalesPersonID = sp.SalesPersonID  
WHERE sp.SalesYTD > 2500000.00;  
GO  
```  
  
### <a name="c-using-merge"></a>C. Utilizzo di MERGE  
 Nell'esempio seguente viene specificato che l'operazione `JOIN` nella query viene eseguita da un join `MERGE`. Nell'esempio viene utilizzato il database [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
```  
SELECT poh.PurchaseOrderID, poh.OrderDate, pod.ProductID, pod.DueDate, poh.VendorID   
FROM Purchasing.PurchaseOrderHeader AS poh  
INNER MERGE JOIN Purchasing.PurchaseOrderDetail AS pod   
    ON poh.PurchaseOrderID = pod.PurchaseOrderID;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Hint &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql.md)  
  
  
