---
title: Elemento AssociationSet (CSDLBI) | Documenti Microsoft
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: 93e5ac4d-d7e8-490e-b775-28263a48cfcc
caps.latest.revision: 8
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f8635a526095a7182c8415f571e26e6818f209a8
ms.contentlocale: it-it
ms.lasthandoff: 09/01/2017

---
# <a name="associationset-element-csdlbi"></a>Elemento AssociationSet (CSDLBI)
  L'elemento **AssociationSet** è un tipo complesso che definisce un'associazione. Nei modelli di dati CSDLBI, un'associazione è una relazione tra due tabelle.  
  
 Per ogni relazione univoca in un modello, è necessario specificare un elemento **AssociationSet**. Per definire gli endpoint, **AssociationSet** usa l'elemento **Association**. L'elemento **AssociationSet** definisce inoltre i metadati sulla relazione e sul relativo utilizzo nel modello di dati.  
  
## <a name="applicable-attributes"></a>Attributi applicabili  
 Nella tabella seguente vengono elencati gli attributi e gli elementi che definiscono l'elemento **AssociationSet**.  
  
|Nome|Obbligatorio|Description|  
|----------|-----------------|-----------------|  
|State|Sì|Stringa che indica se l'associazione è attiva o meno. Il valore è definito dall'elemento State.|  
|Hidden|No|Valore booleano che indica se la relazione è visibile. Per impostazione predefinita, il valore di Hidden è **false**, ovvero tutte le relazioni sono visibili nel modello.|  
  
## <a name="state-element"></a>Elemento State  
 L'elemento **State** è un tipo semplice che descrive se un'associazione è attiva e deve essere utilizzata nei calcoli o se invece è inattiva e vi si deve far riferimento in modo esplicito nei calcoli.  
  
 Se sono presenti più set di associazioni che connettono due entità, solo un set di associazioni può essere contrassegnato come Active. In altre parole, se esistono due relazioni tra due medesime tabelle, solo una relazione può essere attiva.  
  
 Nella tabella seguente vengono elencati i valori dell'elemento **State**.  
  
|Valore|Description|  
|-----------|-----------------|  
|Attiva|L'associazione è attiva.|  
|Inactive|L'associazione è attiva.|  
  
## <a name="example"></a>Esempio  
 **Tabella**  
  
 Nell'esempio seguente viene illustrata una relazione del modello tabulare AdventureWorks, in CSDLBI versione 1.1. L'associazione viene contrassegnata come Inactive in quanto esiste una relazione tra OrderKey e Date.  
  
```  
<AssociationSet   
    Name="InternetSales_Date_Date_Date"  
    Association="Sandbox.InternetSales_Date_Date_Date">  
    <End EntitySet="InternetSales" />  
    <End EntitySet="DimDate" />  
<bi:AssociationSet State="Inactive" />  
</AssociationSet>  
  
```  
  
## <a name="example"></a>Esempio  
 **Multidimensionale**  
  
 Nell'esempio seguente viene illustrata la relazione definita tra le tabelle Sales e Currency nel cubo Operations di Contoso.  
  
```  
<AssociationSet   
    Name ="Sales_Currency_Currency_Currency_Name2"  
    Association ="Sandbox.Sales_Currency_Currency_Currency_Name2">  
    <End EntitySet ="Sales" />  
    <End EntitySet ="Currency" />  
<bi:AssociationSet />  
</AssociationSet>  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimento tecnico per le annotazioni di Business Intelligence per CSDL](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/technical-reference-for-bi-annotations-to-csdl.md)  
  
  