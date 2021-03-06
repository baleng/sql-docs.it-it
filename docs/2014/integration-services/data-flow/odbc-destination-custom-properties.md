---
title: Proprietà personalizzate della destinazione ODBC | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
ms.assetid: 07508c40-6c08-4359-96cd-8ff17671244d
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: b38679e02b53266bf7bed5488befdc53bb45a1de
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/02/2018
ms.locfileid: "48204211"
---
# <a name="odbc-destination-custom-properties"></a>Proprietà personalizzate della destinazione ODBC
  Nella tabella seguente vengono descritte le proprietà personalizzate della destinazione ODBC. È possibile impostare tutte le proprietà dalle espressioni di proprietà SSIS.  
  
|Nome proprietà|Tipo di dati|Description|  
|-------------------|---------------|-----------------|  
|Connessione|ODBC Connection|Connessione ODBC per accedere al database di destinazione.|  
|BatchSize|Valore intero|Dimensioni del batch per il caricamento bulk. Si tratta del numero di righe caricate come batch. È valido solo se è supportata l'associazione di parametri a livello di riga. Se l'associazione di parametri a livello di riga non è supportata, le dimensioni del batch sono pari a 1.|  
|BindCharColumnAs|Integer (enumerazione)|Questa proprietà determina il modo in cui la destinazione ODBC associa colonne con tipi string a più byte quali SQL_CHAR, SQL_VARCHAR o SQL_LONGVARCHAR.<br /><br /> I valori possibili sono Unicode (0), che specifica l'associazione delle colonne come SQL_C_WCHAR, e ANSI (1), che specifica l'associazione delle colonne come SQL_C_CHAR. Il valore predefinito è Unicode (0).<br /><br /> Unicode è l'opzione migliore per la maggior parte dei provider ODBC 3.x e ODBC 2.x che supportano l'associazione di parametri CHAR come stringhe wide. Quando si seleziona Unicode e ExposeCharColumnsAsUnicode è True, l'utente non deve specificare la tabella codici utilizzata dal database di origine.<br /><br /> **Nota** : questa proprietà non è disponibile nell' **Editor destinazione ODBC**, ma può essere impostata tramite l' **Editor avanzato**.|  
|BindNumericAs|Integer (enumerazione)|Questa proprietà determina il modo in cui la destinazione ODBC associa colonne con dati numerici con tipi di dati SQL_TYPE_NUMERIC e SQL_TYPE_DECIMAL.<br /><br /> I valori possibili sono Char (0), che specifica l'associazione delle colonne come SQL_C_WCHAR, e Numeric (1), che specifica l'associazione delle colonne come SQL_C_NUMERIC. Il valore predefinito è Char (0).<br /><br /> **Nota**: questa proprietà non è disponibile nell' **Editor destinazione ODBC**, ma può essere impostata tramite l' **Editor avanzato**.|  
|DefaultCodePage|Valore intero|Tabella codici da utilizzare per le colonne di tipo string.<br /><br /> **Nota**: questa proprietà non è disponibile nell' **Editor destinazione ODBC**, ma può essere impostata tramite l' **Editor avanzato**.|  
|InsertMethod|Integer (enumerazione)|Metodo utilizzato per l'inserimento dei dati. I valori possibili sono Row by row (0) e Batch (1). Il valore predefinito è Batch (1).<br /><br /> Per altre informazioni su queste opzioni, vedere "Opzioni di caricamento" in [Destinazione ODBC](odbc-destination.md).|  
|StatementTimeout|Valore intero|Numero di secondi di attesa per l'esecuzione di un'istruzione SQL prima di tornare all'applicazione con un errore. Il valore predefinito è 120.|  
|TableName|String|Nome della tabella di destinazione in cui vengono inseriti i dati.|  
|TransactionSize|Valore intero|Numero di inserimenti in una singola transazione. Il valore predefinito è 0, che indica che la destinazione utilizza la modalità di commit automatico.<br /><br /> Poiché la gestione connessione ODBC non supporta transazioni distribuite, è possibile impostare questa proprietà con un valore diverso da 0. Se, tuttavia, la proprietà **RetainSameConnection** della gestione connessione è impostata su **true** , è necessario impostare questa proprietà su 0.<br /><br /> **Nota**: questa proprietà non è disponibile nell' **Editor destinazione ODBC**, ma può essere impostata tramite l' **Editor avanzato**.|  
|LobChunkSize|Valore intero|Allocazione delle dimensioni del blocco per colonne LOB.|  
  
  
