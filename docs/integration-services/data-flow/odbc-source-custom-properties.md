---
title: Proprietà personalizzate dell'origine ODBC | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 362bbcd8-b7b0-4bab-8afe-1212b2ad1af9
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: b961bb0dff9f832660807211cf59189db036dd23
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/01/2018
ms.locfileid: "47730179"
---
# <a name="odbc-source-custom-properties"></a>Proprietà personalizzate dell'origine ODBC
  Nella tabella seguente vengono descritte le proprietà personalizzate dell'origine ODBC. È possibile impostare tutte le proprietà dalle espressioni di proprietà SSIS.  
  
|Nome proprietà|Tipo di dati|Descrizione|  
|-------------------|---------------|-----------------|  
|Connessione|ODBC Connection|Connessione ODBC per accedere al database di origine.|  
|AccessMode|Integer (enumerazione)|Modalità utilizzata per accedere al database. I valori possibili sono Table Name (0) e SQL Command (1).<br /><br /> Il valore predefinito è Table Name (0).|  
|BatchSize|Valore intero|Dimensioni del batch per l'estrazione bulk. Corrisponde al numero di record estratti come matrice. Se il provider ODBC selezionato non supporta le matrici, le dimensioni del batch sono pari a 1.|  
|BindCharColumnAs|Integer (enumerazione)|Questa proprietà determina il modo in cui l'origine ODBC associa colonne con tipi string a più byte quali SQL_CHAR, SQL_VARCHAR o SQL_LONGVARCHAR.<br /><br /> I valori possibili sono Unicode (0), che specifica l'associazione delle colonne come SQL_C_WCHAR, e ANSI (1), che specifica l'associazione delle colonne come SQL_C_CHAR. Il valore predefinito è Unicode (0).<br /><br /> **Nota**: questa proprietà non è disponibile nell' **Editor origine ODBC**, ma può essere impostata tramite l' **Editor avanzato**.|  
|BindNumericAs|Integer (enumerazione)|Questa proprietà determina il modo in cui l'origine ODBC associa colonne con dati numerici con tipi di dati SQL_TYPE_NUMERIC e SQL_TYPE_DECIMAL.<br /><br /> Le opzioni possibili sono Char (0), che specifica l'associazione delle colonne come SQL_C_WCHAR, e Numeric (1), che specifica l'associazione delle colonne come SQL_C_NUMERIC. Il valore predefinito è Char (0).<br /><br /> **Nota**: questa proprietà non è disponibile nell' **Editor origine ODBC**, ma può essere impostata tramite l' **Editor avanzato**.|  
|DefaultCodePage|Valore intero|Tabella codici da utilizzare per le colonne di output di tipo string.<br /><br /> **Nota**: questa proprietà non è disponibile nell' **Editor origine ODBC**, ma può essere impostata tramite l' **Editor avanzato**.|  
|ExposeCharColumnsAsUnicode|Boolean|Questa proprietà determina il modo in cui le colonne CHAR vengono esposte dal componente. Il valore predefinito è False, che indica che le colonne CHAR vengono esposte come stringhe a più byte (DT_STR). Se il valore è True, le colonne CHAR vengono esposte come stringhe wide (DT_WSTR).<br /><br /> **Nota**: questa proprietà non è disponibile nell' **Editor origine ODBC**, ma può essere impostata tramite l' **Editor avanzato**.|  
|FetchMethod|Integer (enumerazione)|Metodo utilizzato per recuperare i dati. Le possibili opzioni sono Row by row (0) e Batch (1). Il valore predefinito è Batch (1).<br /><br /> Per altre informazioni su queste opzioni, vedere [Origine ODBC](../../integration-services/data-flow/odbc-source.md).<br /><br /> **Nota**: questa proprietà non è disponibile nell' **Editor origine ODBC**, ma può essere impostata tramite l' **Editor avanzato**.|  
|SqlCommand|String|Comando SQL da eseguire quando la proprietà AccessMode è impostata su SQL Command.|  
|StatementTimeout|Valore intero|Numero di secondi di attesa per l'esecuzione di un'istruzione SQL prima di tornare all'applicazione con un errore. Il valore predefinito è 0. Il valore 0 indica che al sistema non viene applicato alcun timeout.|  
|TableName|String|Nome della tabella con i dati in uso quando la proprietà AccessMode è impostata su Table Name.|  
|LobChunckSize|Valore intero|Allocazione delle dimensioni del blocco per colonne LOB.|  
||||  
  
## <a name="see-also"></a>Vedere anche  
 [Origine ODBC](../../integration-services/data-flow/odbc-source.md)   
 [Editor origine ODBC &#40;pagina Gestione connessione&#41;](../../integration-services/data-flow/odbc-source-editor-connection-manager-page.md)  
  
  
