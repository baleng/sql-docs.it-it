---
title: Identificatori SRID (Spatial Reference Identifier) | Microsoft Docs
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- Spatial Reference Identifiers (SRIDs)
- geodetic spatial data [SQL Server], identifiers
- SRID
ms.assetid: 0612658a-7d1b-4178-bdc2-42b914ea31a7
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 0cba308c746bd3cec33742cbdf8231371d18aab3
ms.sourcegitcommit: 87f29b23d5ab174248dab5d558830eeca2a6a0a4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/05/2018
ms.locfileid: "51018996"
---
# <a name="spatial-reference-identifiers-srids"></a>identificatori SRID (Spatial Reference Identifier)
  Ogni istanza spaziale ha un identificatore SRID. L'identificatore SRID corrisponde a un sistema di riferimento spaziale basato sullo specifico ellissoide utilizzato per il mapping terra piatta o terra rotonda.  
  
> [!IMPORTANT]  
>  Per una descrizione dettagliata e alcuni esempi delle funzionalità spaziali introdotte in [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], tra cui un nuovo SRID, scaricare il white paper [New Spatial Features in SQL Server 2012](http://go.microsoft.com/fwlink/?LinkId=226407)(Nuove funzionalità spaziali in SQL Server 2012).  
  
 Una colonna spaziale può contenere oggetti con identificatori SRID. Tuttavia, solo le istanze spaziali con lo stesso identificatore SRID possono essere utilizzate se si eseguono operazioni con i metodi dei dati spaziali [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sui dati. Il risultato di qualsiasi metodo spaziale derivato da due istanze dei dati spaziali è valido solo se quelle istanze hanno lo stesso identificatore SRID, basato sulla stessa unità di misura, data e proiezione utilizzata per determinare le coordinate delle istanze. Le unità di misura più comuni di un identificatore SRID sono metri o metri quadrati.  
  
 Se due istanze spaziali non hanno lo stesso SRID, i risultati di un metodo tipo dati `geometry` o `geography` utilizzati nelle istanze restituiranno NULL. Ad esempio, affinché il seguente termine di predicato restituisca un risultato non NULL, le due istanze `geometry`, `geometry1` e `geometry2` devono avere stesso identificatore SRID:  
  
 `geometry1.STIntersects(geometry2) = 1`  
  
> [!NOTE]  
>  Il sistema SRID è definito dallo standard [European Petroleum Survey Group (EPSG)](http://go.microsoft.com/fwlink/?LinkId=99349) , un set di standard sviluppato per cartografia, rilevamenti e archiviazione dei dati geodetici. Questo standard è di proprietà di Oil and Gas Producers (OGP) Surveying and Positioning Committee.  
  
## <a name="see-also"></a>Vedere anche  
 [Panoramica dei tipi di dati spaziali](spatial-data-types-overview.md)  
  
  
