---
title: Maiuscole/minuscole identificatore | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- identifiers [ODBC], case
- interoperability of SQL statements [ODBC], identifier case
ms.assetid: ee8a31aa-389d-4dd1-bfa9-547f6b50bc70
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6445cffd5faa8b825c81ec729d7b28c90e14a7b3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/01/2018
ms.locfileid: "47678351"
---
# <a name="identifier-case"></a>Maiuscole/minuscole per gli identificatori
In istruzioni SQL e gli argomenti della funzione del catalogo, identificatori e gli identificatori delimitati possono essere uno tra maiuscole e minuscole o non, quale un'applicazione può determinare chiamando **SQLGetInfo** specificando le SQL_IDENTIFIER_CASE SQL_QUOTED_ Opzioni IDENTIFIER_CASE.  
  
 Ognuna di queste opzioni ha quattro valori restituiti possibili: uno che informa che l'identificatore o maiuscole/minuscole identificatore tra virgolette è sensibile e tre che informa che non è sensibile. I tre valori che non fanno distinzione maiuscole/minuscole descrivono ulteriormente il caso in cui gli identificatori sono archiviati nel catalogo di sistema. Come gli identificatori vengono archiviati nel catalogo di sistema sono rilevanti solo per scopi di visualizzazione, ad esempio quando un'applicazione consente di visualizzare i risultati di una funzione di catalogo. non modifica la distinzione maiuscole/minuscole degli identificatori.
