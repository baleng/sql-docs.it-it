---
title: SQRT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SQRT
- SQRT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- SQRT function
- square root values
ms.assetid: 26e244e8-e82d-4664-a445-1226230ee1c5
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a32b4247a138c3cf6d87dcb166c30083280dfccb
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/01/2018
ms.locfileid: "47596747"
---
# <a name="sqrt-transact-sql"></a>SQRT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Restituisce la radice quadrata del valore float specificato.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
SQRT ( float_expression )  
```  
  
## <a name="arguments"></a>Argomenti  
 *float_expression*  
 [Espressione](../../t-sql/language-elements/expressions-transact-sql.md) di tipo **float** oppure di un tipo che può essere convertito in modo implicito in float.  
  
## <a name="return-types"></a>Tipi restituiti  
 **float**  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene restituita la radice quadrata dei numeri compresi tra `1.00` e `10.00`.  
  
```  
DECLARE @myvalue float;  
SET @myvalue = 1.00;  
WHILE @myvalue < 10.00  
   BEGIN  
      SELECT SQRT(@myvalue);  
      SET @myvalue = @myvalue + 1  
   END;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
------------------------   
1.0                        
------------------------   
1.4142135623731            
------------------------   
1.73205080756888           
------------------------   
2.0                        
------------------------   
2.23606797749979           
------------------------   
2.44948974278318           
------------------------   
2.64575131106459           
------------------------   
2.82842712474619           
------------------------   
3.0  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Esempi: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 Nell'esempio seguente viene restituita la radice quadrata dei numeri `1.00` e `10.00`.  
  
```  
SELECT SQRT(1.00), SQRT(10.00);  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
----------  ------------  
1.00        3.16
```  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni matematiche &#40;Transact-SQL&#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)  
  
  

