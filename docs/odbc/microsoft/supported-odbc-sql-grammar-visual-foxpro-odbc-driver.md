---
title: È supportata la grammatica SQL ODBC (Driver ODBC Visual FoxPro) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- native Visual FoxPro language syntax [ODBC]
- FoxPro ODBC driver [ODBC], SQL grammar
- SQL grammar [ODBC], Visual FoxPro ODBC driver
- Visual FoxPro ODBC driver [ODBC], SQL grammar
- grammar support in Visual FoxPro ODBC driver [ODBC]
- Visual FoxPro ODBC driver [ODBC], native Visual FoxPro language syntax
- FoxPro ODBC driver [ODBC], native Visual FoxPro language syntax
ms.assetid: f41a38c2-e22e-4c65-a32e-9a6777435160
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 10df35f4f29de4ac3899efa0e86e48af861f1e65
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/01/2018
ms.locfileid: "47751019"
---
# <a name="supported-odbc-sql-grammar-visual-foxpro-odbc-driver"></a>Grammatica SQL ODBC supportata (driver ODBC Visual FoxPro)
Il Driver ODBC Microsoft Visual FoxPro supporta quanto segue:  
  
-   Tutte le istruzioni SQL e le clausole nella grammatica SQL minima ODBC  
  
-   Un'ulteriore istruzione SQL da ODBC core grammatica SQL  
  
 Nella tabella seguente vengono elencati gli elementi supportati dal driver, dal livello di grammatica SQL ODBC.  
  
|Level|Elementi|Elemento|  
|-----------|--------------|----------|  
|Minimo|Data Definition Language (DDL)|CREATE TABLE e DROP TABLE|  
||Data Manipulation Language (DML)|Selezionare, inserire, aggiornare ed eliminare|  
||Espressioni|Semplice (ad esempio un > B + C)|  
||Tipi di dati|CHAR, VARCHAR o LONG VARCHAR|  
  
 Oltre la grammatica SQL ODBC supportata, il Driver ODBC Visual FoxPro supporta la sintassi del linguaggio Visual FoxPro nativa completata per i seguenti comandi di Visual FoxPro:  
  
 [ISTRUZIONE ALTER TABLE](../../odbc/microsoft/alter-table-sql-command.md)  
  
 [CREATE TABLE](../../odbc/microsoft/create-table-sql-command.md)  
  
 [DELETE](../../odbc/microsoft/delete-sql-command.md)  
  
 [ELIMINA TAG](../../odbc/microsoft/delete-tag-command.md)  
  
 [DROP TABLE](../../odbc/microsoft/drop-table-command.md)  
  
 [INDEX](../../odbc/microsoft/index-command.md)  
  
 [INSERT](../../odbc/microsoft/insert-sql-command.md)  
  
 [SELECT](../../odbc/microsoft/select-sql-command.md)  
  
 [UPDATE](../../odbc/microsoft/update-sql-command.md)
