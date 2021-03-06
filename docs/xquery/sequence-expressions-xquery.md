---
title: Sequenza di espressioni (XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- sequence [XQuery]
- expressions [XQuery], sequence
- filtering sequences [XQuery]
ms.assetid: 41e18b20-526b-45d2-9bd9-e3b7d7fbce4e
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 6c73d2be8550bd6ce3dad9e6c9e07e2403785f7b
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/15/2018
ms.locfileid: "51661825"
---
# <a name="sequence-expressions-xquery"></a>Espressioni di sequenze (XQuery)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] supporta gli operatori XQuery utilizzati per la costruzione, l'applicazione di filtri e la combinazione di una sequenza di elementi. Un elemento può essere un valore atomico o un nodo.  
  
## <a name="constructing-sequences"></a>Costruzione delle sequenze  
 Per costruire una sequenza in cui vengono concatenati elementi è possibile utilizzare l'operatore virgola.  
  
 Una sequenza può contenere valori duplicati. Le sequenze nidificate, ovvero le sequenze che includono un'altra sequenza, vengono compresse. Ad esempio, la sequenza (1, 2, (3, 4, (5))) diventa (1, 2, 3, 4, 5). Di seguito vengono riportati esempi di costruzione delle sequenze.  
  
### <a name="example-a"></a>Esempio A  
 La query seguente restituisce una sequenza di cinque valori atomici:  
  
```  
declare @x xml  
set @x=''  
select @x.query('(1,2,3,4,5)')  
go  
-- result 1 2 3 4 5  
```  
  
 La query seguente restituisce una sequenza di due nodi:  
  
```  
-- sequence of 2 nodes  
declare @x xml  
set @x=''  
select @x.query('(<a/>, <b/>)')  
go  
-- result  
<a />  
<b />  
```  
  
 La query seguente restituisce un errore, perché si sta costruendo una sequenza di valori atomici e di nodi, ovvero una sequenza eterogenea, che non è supportata.  
  
```  
declare @x xml  
set @x=''  
select @x.query('(1, 2, <a/>, <b/>)')  
go  
```  
  
### <a name="example-b"></a>Esempio B  
 La query seguente costruisce una sequenza di valori atomici tramite la combinazione di quattro sequenze di lunghezza diversa in un'unica sequenza.  
  
```  
declare @x xml  
set @x=''  
select @x.query('(1,2),10,(),(4, 5, 6)')  
go  
-- result = 1 2 10 4 5 6  
```  
  
 È possibile ordinare la sequenza utilizzando FLOWR e ORDER BY:  
  
```  
declare @x xml  
set @x=''  
select @x.query('for $i in ((1,2),10,(),(4, 5, 6))  
                  order by $i  
                  return $i')  
go  
```  
  
 È possibile contare gli elementi nella sequenza utilizzando il **fn:count()** (funzione).  
  
```  
declare @x xml  
set @x=''  
select @x.query('count( (1,2,3,(),4) )')  
go  
-- result = 4  
```  
  
### <a name="example-c"></a>Esempio C  
 La query seguente viene specificata sulla colonna AdditionalContactInfo del **xml** tipo della tabella Contact. In questa colonna sono archiviate le informazioni aggiuntive sul contatto, ad esempio numeri di telefono aggiuntivi, numeri di cercapersone e indirizzi. Il \<telephoneNumber >, \<pager >, e altri nodi possono essere visualizzati in qualsiasi punto del documento. La query costruisce una sequenza che contiene tutti i \<telephoneNumber > gli elementi figlio del nodo di contesto, seguita dal \<cercapersone > gli elementi figlio. Si noti che nell'espressione restituita, `($a//act:telephoneNumber, $a//act:pager)`, viene utilizzato l'operatore di sequenza virgola.  
  
```  
WITH XMLNAMESPACES ('https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes' AS act,  
 'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo' AS aci)  
  
SELECT AdditionalContactInfo.query('  
   for $a in /aci:AdditionalContactInfo   
   return ($a//act:telephoneNumber, $a//act:pager)  
') As Result  
FROM Person.Contact  
WHERE ContactID=3  
```  
  
 Risultato:  
  
```  
<act:telephoneNumber xmlns:act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">  
  <act:number>333-333-3333</act:number>  
</act:telephoneNumber>  
<act:telephoneNumber xmlns:act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">  
  <act:number>333-333-3334</act:number>  
</act:telephoneNumber>  
<act:pager xmlns:act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">  
  <act:number>999-555-1244</act:number>  
  <act:SpecialInstructions>  
Page only in case of emergencies.  
</act:SpecialInstructions>  
</act:pager>  
```  
  
## <a name="filtering-sequences"></a>Applicazione di filtri alle sequenze  
 È possibile applicare filtri alla sequenza restituita da un'espressione, aggiungendo un predicato all'espressione. Per altre informazioni, vedere [espressioni di percorso &#40;XQuery&#41;](../xquery/path-expressions-xquery.md). Ad esempio, la query seguente restituisce una sequenza di tre nodi elemento <`a`>:  
  
```  
declare @x xml  
set @x = '<root>  
<a attrA="1">111</a>  
<a></a>  
<a></a>  
</root>'  
SELECT @x.query('/root/a')  
```  
  
 Risultato:  
  
```  
<a attrA="1">111</a>  
<a />  
<a />  
```  
  
 Per recuperare solo gli elementi <`a`> con l'attributo attrA, è possibile specificare un filtro nel predicato. Nella sequenza risultante sarà presente un solo elemento <`a`>.  
  
```  
declare @x xml  
set @x = '<root>  
<a attrA="1">111</a>  
<a></a>  
<a></a>  
</root>'  
SELECT @x.query('/root/a[@attrA]')  
```  
  
 Risultato:  
  
```  
<a attrA="1">111</a>  
```  
  
 Per altre informazioni su come specificare predicati in un'espressione di percorso, vedere [specifica di predicati in un passo dell'espressione di percorso](../xquery/path-expressions-specifying-predicates.md).  
  
 Nell'esempio seguente viene compilata un'espressione di sequenza dei sottoalberi e quindi viene applicato un filtro alla sequenza.  
  
```  
declare @x xml  
set @x = '  
<a>  
  <c>C under a</c>  
</a>  
<b>    
   <c>C under b</c>  
</b>  
<c>top level c</c>  
<d></d>  
'  
```  
  
 L'espressione in `(/a, /b)` costruisce una sequenza con i sottoalberi `/a` e `/b` e quindi l'espressione filtra l'elemento `<c>` dalla sequenza risultante.  
  
```  
SELECT @x.query('  
  (/a, /b)/c  
')  
```  
  
 Risultato:  
  
```  
<c>C under a</c>  
<c>C under b</c>  
```  
  
 Nell'esempio seguente viene applicato un filtro del predicato. L'espressione trova gli elementi <`a`> e <`b`> che contengono elemento <`c`>.  
  
```  
declare @x xml  
set @x = '  
<a>  
  <c>C under a</c>  
</a>  
<b>    
   <c>C under b</c>  
</b>  
  
<c>top level c</c>  
<d></d>  
'  
SELECT @x.query('  
  (/a, /b)[c]  
')  
```  
  
 Risultato:  
  
```  
<a>  
  <c>C under a</c>  
</a>  
<b>  
  <c>C under b</c>  
</b>  
```  
  
### <a name="implementation-limitations"></a>Limitazioni di implementazione  
 Limitazioni:  
  
-   Le espressioni intervallo di XQuery non sono supportate.  
  
-   Le sequenze devono essere omogenee. In particolare, tutti gli elementi di una sequenza devono essere nodi o valori atomici. Per verificarlo, viene eseguito il controllo statico.  
  
-   Non è supportata la combinazione di sequenze di nodi tramite gli operatori UNION, INTERSECT o EXCEPT.  
  
## <a name="see-also"></a>Vedere anche  
 [Espressioni XQuery](../xquery/xquery-expressions.md)  
  
  
