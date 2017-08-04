---
title: IsGeneration (MDX) | Documenti Microsoft
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ISGENERATION
dev_langs:
- kbMDX
helpviewer_keywords:
- IsGeneration function
ms.assetid: fd11d2e0-d81d-45af-ac45-c98634d05550
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: bdb02d424cb58aab2e8af8695b9751e495ba7175
ms.contentlocale: it-it
ms.lasthandoff: 08/02/2017

---
# <a name="isgeneration-mdx"></a>IsGeneration (MDX)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../includes/tsql-appliesto-ss2008-all-md.md)]

  Indica se il membro specificato è incluso in una generazione specifica.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
IsGeneration(Member_Expression, Generation_Number)   
```  
  
## <a name="arguments"></a>Argomenti  
 *Member_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un membro.  
  
 *Generation_Number*  
 Espressione numerica valida che specifica la generazione rispetto alla quale il membro specificato viene valutato.  
  
## <a name="remarks"></a>Osservazioni  
 Il **IsGeneration** risultato della funzione **true** se il membro specificato è il numero di generazione specificata. In caso contrario, la funzione restituisce **false**. Inoltre, se il membro specificato restituisce un membro vuoto, il **IsGeneration** risultato della funzione **false**.  
  
 I membri foglia hanno indice di generazione 0. L'indice di generazione dei membri non foglia viene determinato aggiungendo 1 all'indice di generazione più alto ottenuto dall'unione di tutti i membri figlio del membro specificato. Dato il modo in cui viene determinato l'indice di generazione dei membri non foglia, è possibile che un determinato membro non foglia appartenga a più generazioni.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene restituito TRUE se [Date].[Fiscal].CurrentMember è parte della seconda generazione:  
  
 `WITH MEMBER MEASURES.ISGENERATIONDEMO AS`  
  
 `IsGeneration([Date].[Fiscal].CURRENTMEMBER, 2)`  
  
 `SELECT {MEASURES.ISGENERATIONDEMO} ON 0,`  
  
 `[Date].[Fiscal].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimento alla funzione MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
