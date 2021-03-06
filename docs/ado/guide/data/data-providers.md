---
title: Provider di dati | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- data providers [ADO]
- OLE DB providers [ADO]
- ADO, OLE DB providers
ms.assetid: 877b9f25-60c4-4ab6-8052-2c28a3849e89
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3c3b8a4ac0da80303a63bd62f7b4d6f51faab1fb
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/01/2018
ms.locfileid: "47692939"
---
# <a name="data-providers"></a>Provider di dati
Provider di dati rappresentano diverse origini dei dati, ad esempio database SQL, file sequenziali-indicizzate, fogli di calcolo, archivi di documenti e i file di posta elettronica. I provider di espongono i dati in modo uniforme tramite un'astrazione comune definita set di righe.  
  
 ADO è potente e flessibile perché può connettersi a una qualsiasi di diversi provider di dati diversi e ancora esporre il modello di programmazione stesso, indipendentemente dalle funzionalità specifiche di qualsiasi altro provider specificato. Tuttavia, poiché ogni provider di dati è univoco, come l'applicazione interagisce con ADO dipendono dal provider di dati.  
  
 Ad esempio, le funzionalità e caratteristiche del Provider OLE DB per SQL Server, che viene usato per accedere ai database Microsoft SQL Server, sono considerevolmente diverse da quelle di Provider Microsoft OLE DB per Internet Publishing, che consente di accedere ai file archivi in un server Web.
