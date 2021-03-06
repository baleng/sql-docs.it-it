---
title: Disconnessione e riconnessione del Recordset | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Recordset object [ADO], disconnecting and reconnecting
ms.assetid: c5134af7-81d6-4de4-9fd1-cfe29973545e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0cefdb81aa9e9a1a5f7ad7ba1f6db86d1ae95e2d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/01/2018
ms.locfileid: "47771999"
---
# <a name="disconnecting-and-reconnecting-the-recordset"></a>Disconnessione e riconnessione del recordset
Una delle funzionalità più potenti disponibili in ADO è la possibilità di aprire un set di record del lato client da un'origine dati e quindi disconnettere il Recordset dall'origine dati. Una volta il Recordset è stato disconnesso, la connessione all'origine dati è chiuso, per rilasciare le risorse del server utilizzato per la manutenzione. È possibile continuare a visualizzare e modificare i dati nel set di record, mentre è disconnessa e riconnettersi in seguito all'origine dati e inviare gli aggiornamenti in modalità batch.  
  
 Per disconnettere un Recordset, aprirlo con una posizione del cursore di adUseClient e quindi impostare la proprietà ActiveConnection uguale a Nothing. (Gli utenti di C++ devono impostare la proprietà ActiveConnection su NULL per disconnettersi.)  
  
 Si userà un Recordset disconnesso più avanti in questa sezione relativa alla persistenza dei Recordset affrontare uno scenario in cui è necessario avere i dati in un set di record disponibili per un'applicazione mentre il computer client non è connesso a una rete.  
  
## <a name="see-also"></a>Vedere anche  
 [Modalità batch](../../../ado/guide/data/batch-mode.md)
