---
title: Proprietà personalizzate dell'origine XML | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: eb29b28c-3159-41ec-b3d7-fce5b2f2be55
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 60748312c4169eafa50bdf7685c9b5111b3bc66a
ms.sourcegitcommit: 0638b228980998de9056b177c83ed14494b9ad74
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/14/2018
ms.locfileid: "51639158"
---
# <a name="xml-source-custom-properties"></a>Proprietà personalizzate dell'origine XML
  L'origine XML include sia proprietà personalizzate che le proprietà comuni a tutti i componenti del flusso di dati.  
  
 Nella tabella seguente vengono descritte le proprietà personalizzate dell'origine XML. Tutte le proprietà sono di lettura/scrittura.  
  
|Nome proprietà|Tipo di dati|Descrizione|  
|-------------------|---------------|-----------------|  
|AccessMode|Valore intero|Modalità utilizzata per accedere ai dati XML.|  
|UseInlineSchema|Boolean|Valore che indica se utilizzare una definizione dello schema inline all'interno dell'origine XML. Il valore predefinito di questa proprietà è **False**.|  
|XMLData|String|File o variabili da cui recuperare i dati XML.<br /><br /> È possibile specificare il valore di questa proprietà tramite un'espressione di proprietà.|  
|XMLSchemaDefinition|String|Percorso e nome del file di definizione dello schema (estensione xsd).<br /><br /> È possibile specificare il valore di questa proprietà tramite un'espressione di proprietà.|  
  
 Nella tabella seguente vengono descritte le proprietà personalizzate dell'output dell'origine XML. Tutte le proprietà sono di lettura/scrittura.  
  
|Nome proprietà|Tipo di dati|Descrizione|  
|-------------------|---------------|-----------------|  
|RowsetID|String|Valore che identifica il set di righe associato all'output.|  
  
 Le colonne di output dell'origine XML non includono proprietà personalizzate.  
  
 Per altre informazioni, vedere [Origine XML](../../integration-services/data-flow/xml-source.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Proprietà comuni](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
  
