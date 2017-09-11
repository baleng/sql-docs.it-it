---
title: Set di righe DISCOVER_INSTANCES | Documenti Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- DISCOVER_INSTANCES
apitype: NA
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- DISCOVER_INSTANCES rowset
ms.assetid: e0842e63-089d-468d-869f-634da343d9fb
caps.latest.revision: 30
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: fbed6de71f83da959591003039fe5910a1a4c53d
ms.contentlocale: it-it
ms.lasthandoff: 09/01/2017

---
# <a name="discoverinstances-rowset"></a>Set di righe DISCOVER_INSTANCES
  Descrive le istanze nel server.  
  
## <a name="rowset-columns"></a>Colonne del set di righe  
 Il **DISCOVER_INSTANCES** set di righe contiene le colonne seguenti.  
  
|Nome colonna|Indicatore del tipo|Lunghezza|Description|  
|-----------------|--------------------|------------|-----------------|  
|**INSTANCE_NAME**|**DBTYPE_WSTR**||Nome dell’istanza.|  
|**INSTANCE_PORT_NUMBER**|**DBTYPE_I4**||Numero di porta su cui l'istanza resta in attesa.|  
|**INSTANCE_STATE**|**DBTYPE_I4**||Stato dell'istanza del server:<br /><br /> **Avviato**<br /><br /> **Stopped**<br /><br /> **Avvio**<br /><br /> **L'arresto**<br /><br /> **In sospeso**|  
  
 Questo set di righe dello schema non è ordinato.  
  
## <a name="restriction-columns"></a>Colonne di restrizione  
 Il **DISCOVER_INSTANCES** righe può essere limitato sulle colonne elencate nella tabella seguente.  
  
|Nome colonna|Indicatore del tipo|Stato della restrizione|  
|-----------------|--------------------|-----------------------|  
|**INSTANCE_NAME**|**DBTYPE_WSTR**|Facoltativa.|  
  
## <a name="see-also"></a>Vedere anche  
 [OLE DB per OLAP i rowset dello Schema](../../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)  
  
  