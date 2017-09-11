---
title: WITH XMLNAMESPACES (Transact-SQL) | Documenti Microsoft
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- WITH_XMLNAMESPACES_TSQL
- WITH XMLNAMESPACES
dev_langs:
- TSQL
helpviewer_keywords:
- adding XML namespaces
- XML namespace declarations [SQL Server]
- clauses [SQL Server], WITH XMLNAMESPACES
- WITH XMLNAMESPACES clause
- declaring XML namespaces
ms.assetid: 3b32662b-566f-454d-b7ca-e247002a9a0b
caps.latest.revision: 17
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c34d67133c083c0dba5325548971997e8b95d6c5
ms.contentlocale: it-it
ms.lasthandoff: 09/01/2017

---
# <a name="with-xmlnamespaces"></a>WITH XMLNAMESPACES
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Dichiara uno o più spazi dei nomi XML.  
  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
WITH XMLNAMESPACES ( <XML namespace declaration item>  
[ { , <XML namespace declaration item> }...] )   
  
<XML namespace declaration item> ::=  
<xml_namespace_uri> AS <xml_namespace_prefix>  
| <XML default namespace declaration item>  
<xml_namespace_uri> ::= <character string literal>  
```  
  
```  
  
<xml_namespace_prefix> ::= <identifier>  
```  
  
```  
  
<XML default namespace declaration item> ::=  
DEFAULT <xml_namespace_uri>  
  
```  
  
## <a name="arguments"></a>Argomenti  
 *xml_namespace_uri*  
 URI (Uniform Resource Identifier) che identifica lo spazio dei nomi XML da dichiarare. *xml_namespace_uri* è una stringa SQL.  
  
 *xml_namespace_prefix*  
 Specifica un prefisso per eseguire il mapping e associato al valore URI dello spazio dei nomi specificato in *xml_namespace_uri*. *xml_namespace_prefix* deve essere un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] identificatore.  
  
## <a name="remarks"></a>Osservazioni  
 Se si utilizza la clausola WITH XMLNAMESPACES in un'istruzione che include inoltre un'espressione di tabella comune, è necessario che la clausola WITH XMLNAMESPACES preceda tale espressione.  
  
 Di seguito sono riportate le regole sintattiche generali in caso di utilizzo della clausola WITH XMLNAMESPACES:  
  
-   Ogni dichiarazione di spazio dei nomi XML deve contenere almeno un elemento di dichiarazione dello spazio dei nomi XML predefinito.  
  
-   Ogni prefisso dello spazio dei nomi XML utilizzato deve essere un nome privo di due punti (NCName) in cui il carattere due punti (:) non fa parte del nome.  
  
-   Non è possibile definire un prefisso di spazio dei nomi due volte.  
  
-   I prefissi degli spazi dei nomi XML e gli URI fanno distinzione tra maiuscole e minuscole.  
  
-   Non è possibile dichiarare il prefisso di spazio dei nomi XML `xmlns`.  
  
-   Il prefisso di spazio dei nomi XML `xml` non può essere sovrascritto da uno spazio dei nomi diverso dall'URI dello spazio dei nomi `'http://www.w3.org/XML/1998/namespace'`. A questo URI non può essere assegnato un prefisso diverso.  
  
-   Il prefisso di spazio dei nomi XML `xsi` non può essere dichiarato nuovamente se la direttiva ELEMENTS XSINIL è utilizzata nella query.  
  
-   I valori stringa dell'URI sono codificati in base alla tabella codici delle regole di confronto del database corrente e vengono convertite internamente in Unicode.  
  
-   Lo spazio dei nomi XML URI può essere spazio compresso segue lo spazio vuoto XSD comprimere le regole utilizzate per **xs: anyURI**. Non viene eseguita alcuna operazione di sostituzione con entità o sostituzione con caratteri nei valori di URI dello spazio dei nomi XML.  
  
-   Nell'URI dello spazio dei nomi XML verrà controllato se sono inclusi caratteri XML 1.0 non validi. Se il controllo ha esito positivo, verrà generato un errore, ad esempio U+0007.  
  
-   In seguito alla compressione di tutti gli spazi vuoti, l'URI dello spazio dei nomi XML non può essere una stringa di lunghezza zero. In caso contrario viene generato un errore per segnalare che un URI dello spazio dei nomi vuoto non è valido.  
  
-   La parola chiave XMLNAMESPACES è riservata nel contesto della clausola WITH.  
  
## <a name="examples"></a>Esempi  
 Per esempi, vedere [aggiungere spazi dei nomi alle query con WITH XMLNAMESPACES](../../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimento al linguaggio XQuery &#40;SQL Server&#41;](../../xquery/xquery-language-reference-sql-server.md)  
  
  
