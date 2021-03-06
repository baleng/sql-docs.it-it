---
title: ObjectProxy (ADO - WFC sintassi) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- ObjectProxy collection [ADO]
ms.assetid: f68f58bc-ad28-46cc-9fb3-099e1a678397
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: af28755fee20c478237edec22936fc694995d554
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/01/2018
ms.locfileid: "47678509"
---
# <a name="objectproxy-ado---wfc-syntax"></a>ObjectProxy (sintassi ADO/WFC)
Un **ObjectProxy** oggetto rappresenta un server e viene restituito dal **createObject** metodo per il [DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md) oggetto. La classe ObjectProxy dispone del metodo **chiamare**, che può richiamare un metodo nel server e restituire un oggetto risultante dalla chiamata.  
  
 **package com.ms.wfc.data**  
  
## <a name="methods"></a>Metodi  
  
### <a name="call-method-adowfc-syntax"></a>Chiama il metodo (sintassi ADO/WFC)  
 Richiama un metodo nel server rappresentato dall'oggetto ObjectProxy. Facoltativamente, gli argomenti del metodo possono essere passati come matrice di oggetti.  
  
#### <a name="syntax"></a>Sintassi  
  
```  
public Object ObjectProxy.( String method )  
public Object ObjectProxy.( String method, Object[] args)  
```  
  
#### <a name="returns"></a>Valori di codice restituiti  
 Object  
 Oggetto risultante dalla chiamata del metodo.  
  
#### <a name="parameters"></a>Parametri  
 *ObjectProxy*  
 Un' **ObjectProxy** oggetto che rappresenta il server.  
  
 *(Metodo)*  
 Stringa contenente il nome del metodo da richiamare sul server.  
  
 *args*  
 Facoltativo. Matrice di oggetti che rappresentano argomenti del metodo nel server. Tipi di dati Java vengono automaticamente convertiti in tipi di dati adatti per l'uso nel server.
