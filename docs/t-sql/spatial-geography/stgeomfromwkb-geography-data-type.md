---
title: STGeomFromWKB (tipo di dati geography) | Microsoft Docs
ms.custom: ''
ms.date: 07/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STGeomFromWKB_TSQL
- STGeomFromWKB (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STGeomFromWKB method
ms.assetid: 79d39d88-5440-49a7-9247-190eafce3f4f
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 71ad47204df46702f63de27d0f30ad6978023073
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/01/2018
ms.locfileid: "47676409"
---
# <a name="stgeomfromwkb-geography-data-type"></a>STGeomFromWKB (tipo di dati geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Restituisce un'istanza **geography** di una rappresentazione WKB (Well-Known Binary) OGC (Open Geospatial Consortium).
  
Questo metodo con tipo di dati **geography** supporta le istanze **FullGlobe** o le istanze spaziali con dimensioni maggiori di un emisfero.
  
## <a name="syntax"></a>Sintassi  
  
```  
  
STGeomFromWKB ( 'WKB_geography' , SRID )  
```  
  
## <a name="arguments"></a>Argomenti  
 *WKB_geography*  
 Rappresentazione WKB dell'istanza **geography** da restituire. *WKB_geography* è un'espressione **varbinary(max)**.  
  
 *SRID*  
 Espressione **int** che rappresenta l'identificatore SRID dell'istanza **geography** da restituire.  
  
## <a name="return-types"></a>Tipi restituiti  
 Tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] restituito: **geography**  
  
 Tipo CLR restituito: **SqlGeography**  
  
## <a name="remarks"></a>Remarks  
 Il tipo OGC dell'istanza **geography** restituita da `STGeomFromText()` è impostato sull'input WKB corrispondente.  
  
 Questo metodo genera un'eccezione **FormatException** se l'input non è formattato in modo corretto.  
  
 Questo metodo genererà un'eccezione **ArgumentException** se l'input contiene un bordo opposto.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene utilizzato il metodo `STGeomFromWKB()` per creare un'istanza `geography`.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromWKB(0x010200000002000000D7A3703D0A975EC08716D9CEF7D34740CBA145B6F3955EC08716D9CEF7D34740, 4326);  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Metodi geography statici OGC](../../t-sql/spatial-geography/ogc-static-geography-methods.md)  
  
  
