---
title: SQLSetEnvAttr e la libreria di cursori | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetEnvAttr function [ODBC], Cursor Library
ms.assetid: 59cc8eae-09ae-4796-869a-c5806488ae83
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 74e57f98b7d5e3e1508a960b342521ea5d315a3d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/01/2018
ms.locfileid: "47693489"
---
# <a name="sqlsetenvattr-and-the-cursor-library"></a>SQLSetEnvAttr e la libreria di cursori
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di utilizzarla nelle nuove attività di sviluppo e pianificare la modifica delle applicazioni che utilizzano attualmente questa funzionalità. Microsoft consiglia di usare le funzionalità del driver del cursore.  
  
 In questo argomento viene illustrato l'utilizzo dei **SQLSetEnvAttr** funzione con la libreria di cursori. Per informazioni generali sul **SQLSetEnvAttr**, vedere [SQLSetEnvAttr-funzione](../../../odbc/reference/syntax/sqlsetenvattr-function.md).  
  
 La libreria di cursori non è interessata dall'impostazione dell'attributo environment SQL_ATTR_ODBC_VERSION, indipendentemente dalla versione dell'applicazione o versione del driver.
