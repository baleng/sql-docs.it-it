---
title: xml_schema_components (Transact-SQL) | Documenti Microsoft
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- xml_schema_components
- sys.xml_schema_components_TSQL
- sys.xml_schema_components
- xml_schema_components_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.xml_schema_components catalog view
ms.assetid: 70142d3a-f8b5-4ee2-8287-3935f0f67aa2
caps.latest.revision: "35"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3d2aaecd2ac13ca87619c1ed923d4577ee6fd034
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/17/2017
---
# <a name="sysxmlschemacomponents-transact-sql"></a>sys.xml_schema_components (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce una riga per componente di un XML Schema. La coppia (**collection_id**, **namespace_id**) è una chiave esterna composta allo spazio dei nomi che lo contiene. Per i componenti, i valori per denominati **symbol_space**, **nome**, **scoping_xml_component_id**, **is_qualified**,  **xml_namespace_id**, **xml_collection_id** siano univoci.  
  
||  
|-|  
|**Si applica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (da[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a [versione corrente](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
|Nome colonna|Tipo di dati|Description|  
|-----------------|---------------|-----------------|  
|**xml_component_id**|**int**|ID univoco del componente di XML Schema nel database.|  
|**xml_collection_id**|**int**|ID della raccolta di XML Schema contenente lo spazio dei nomi del componente.|  
|**xml_namespace_id**|**int**|ID dello spazio dei nomi XML all'interno della raccolta.|  
|**is_qualified**|**bit**|1 = Il componente dispone di un qualificatore esplicito degli spazi dei nomi.<br /><br /> 0 = Si tratta di un componente con ambito locale. In questo caso, la coppia di **namespace_id**, **collection_id**, il "Nessuno spazio dei nomi" si intende **targetNamespace**.<br /><br /> Per i componenti con caratteri jolly questo valore sarà uguale a 1.|  
|**name**|**nvarchar**<br /><br /> **(4000)**|Nome univoco del componente di XML Schema. È NULL se il componente è senza nome.|  
|**symbol_space**|**Char (1)**|Spazio in cui il nome del simbolo è univoco in base alle **tipo**:<br /><br /> N = Nessuno<br /><br /> T = Tipo<br /><br /> E = Elemento<br /><br /> M = Gruppo di modelli<br /><br /> A = Attributo<br /><br /> G = Gruppo di attributi|  
|**symbol_space_desc**|**nvarchar**<br /><br /> **(60)**|Descrizione dello spazio in cui il nome del simbolo è univoco, in base a **tipo**:<br /><br /> Nessuno<br /><br /> TYPE<br /><br /> ELEMENT<br /><br /> MODEL_GROUP<br /><br /> ATTRIBUTE<br /><br /> ATTRIBUTE_GROUP|  
|**tipo**|**Char (1)**|Tipo di componente di XML Schema.<br /><br /> N = Qualsiasi tipo (componente intrinseco speciale)<br /><br /> Z = Qualsiasi tipo semplice (componente intrinseco speciale)<br /><br /> P = Tipo primitivo (tipi intrinseci)<br /><br /> S = Tipo semplice<br /><br /> L = Tipo elenco<br /><br /> U = Tipo unione<br /><br /> C = Tipo semplice complesso (derivato da semplice)<br /><br /> K = Tipo complesso<br /><br /> E = Elemento<br /><br /> M = Gruppo di modelli<br /><br /> W = Carattere jolly dell'elemento<br /><br /> A = Attributo<br /><br /> G = Gruppo di attributi<br /><br /> V = Carattere jolly dell'attributo|  
|**kind_desc**|**nvarchar**<br /><br /> **(60)**|Descrizione del tipo di componente di XML Schema:<br /><br /> ANY_TYPE<br /><br /> ANY_SIMPLE_TYPE<br /><br /> PRIMITIVE_TYPE<br /><br /> SIMPLE_TYPE<br /><br /> LIST_TYPE<br /><br /> UNION_TYPE<br /><br /> COMPLEX_SIMPLE_TYPE<br /><br /> COMPLEX_TYPE<br /><br /> ELEMENT<br /><br /> MODEL_GROUP<br /><br /> ELEMENT_WILDCARD<br /><br /> ATTRIBUTE<br /><br /> ATTRIBUTE_GROUP<br /><br /> ATTRIBUTE_WILDCARD|  
|**derivazione**|**Char (1)**|Metodo di derivazione per i tipi derivati:<br /><br /> N = Nessuno (non derivato)<br /><br /> X = Estensione<br /><br /> R = Restrizione<br /><br /> S = Sostituzione|  
|**derivation_desc**|**nvarchar**<br /><br /> **(60)**|Descrizione del metodo di derivazione per i tipi derivati:<br /><br /> Nessuno<br /><br /> EXTENSION<br /><br /> RESTRICTION<br /><br /> SUBSTITUTION|  
|**base_xml_component_id**|**int**|ID del componente da cui viene derivato il componente. È NULL se non è presente alcun ID.|  
|**scoping_xml_component_id**|**int**|ID univoco del componente di definizione dell'ambito. È NULL se non è presente alcun ID (ambito globale).|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Per altre informazioni, vedere [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Viste del catalogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [XML Schema &#40; Sistema di tipi XML &#41; Viste del catalogo &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/xml-schemas-xml-type-system-catalog-views-transact-sql.md)  
  
  