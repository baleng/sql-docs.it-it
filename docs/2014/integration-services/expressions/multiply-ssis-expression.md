---
title: '* * (moltiplicazione) (espressione SSIS)* (moltiplicazione) (espressione SSIS) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- '* (multiply operator)'
- multiply operator (*)
ms.assetid: d457f052-ffbb-4485-833f-f4bed4349b69
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 8a357e02af88c1e3a0c9806b1f1a228881137397
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/02/2018
ms.locfileid: "48069851"
---
# <a name="-multiply-ssis-expression"></a>* (moltiplicazione) (espressione SSIS)
  Vengono moltiplicate due espressioni numeriche.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
numeric_expression1 * numeric_expression2  
  
```  
  
## <a name="arguments"></a>Argomenti  
 *numeric_expression1, numeric_expression2*  
 Espressione valida con tipo di dati numeric. Per altre informazioni, vedere [Tipi di dati di Integration Services](../data-flow/integration-services-data-types.md).  
  
## <a name="result-types"></a>Tipi restituiti  
 Dipendenti dai tipi di dati dei due argomenti. Per altre informazioni, vedere [Tipi di dati nelle espressioni di Integration Services](integration-services-data-types-in-expressions.md).  
  
## <a name="remarks"></a>Note  
 Se uno degli operandi è Null, il risultato sarà Null.  
  
## <a name="expression-examples"></a>Esempi di espressione  
 In questo esempio vengono moltiplicati due valori letterali numerici.  
  
```  
5 * 6.09  
```  
  
 Questo esempio moltiplica i valori nella colonna **ListPrice** per il 10%.  
  
```  
ListPrice * .10  
```  
  
 Questo esempio sottrae il risultato di un'espressione dalla colonna **ListPrice** . Poiché il nome include il carattere %, la variabile **Discount%** deve essere racchiusa tra parentesi. Per altre informazioni, vedere [Identificatori &#40;SSIS&#41;](identifiers-ssis.md).  
  
```  
ListPrice - (ListPrice * @[Discount%])  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Precedenza e associatività degli operatori](operator-precedence-and-associativity.md)   
 [Gli operatori &#40;espressione di SSIS&#41;](operators-ssis-expression.md)  
  
  
