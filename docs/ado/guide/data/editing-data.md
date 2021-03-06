---
title: Modifica dei dati | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO, editing data
- AdUseClient [ADO]
- editing data [ADO]
ms.assetid: ef514f85-c446-4f05-824e-c9313b2ffae1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0c12692a6ebd1467148b52f993a77043ff495d43
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/01/2018
ms.locfileid: "47823386"
---
# <a name="editing-data"></a>Modifica dei dati
Abbiamo illustrato come utilizzare ADO per connettersi a un'origine dati, eseguire un comando, ottenere i risultati un **Recordset** dell'oggetto e spostarsi all'interno di **Recordset**. Questa sezione è incentrata sull'operazione di ADO fondamentale: modifica dei dati.  
  
 In questa sezione continua a usare il codice di esempio **Recordset** introdotte in [analisi dei dati](../../../ado/guide/data/examining-data.md), con una modifica significativa. Il codice seguente viene utilizzato per aprire la **Recordset**:  
  
```  
'BeginEditIntro  
    Dim strSQL As String  
    Dim objRs1 As ADODB.Recordset  
  
    strSQL = "SELECT * FROM Shippers"  
  
    Set objRs1 = New ADODB.Recordset  
  
    objRs1.Open strSQL, GetNewConnection, adOpenStatic, _  
                adLockBatchOptimistic, adCmdText  
  
    ' Disconnect the Recordset from the Connection object.  
    Set objRs1.ActiveConnection = Nothing  
'EndEditIntro  
```  
  
 La modifica significativa al codice comporta l'impostazione di **CursorLocation** proprietà delle **connessione** uguale all'oggetto **adUseClient** nel  *GetNewConnection* funzione (illustrato nell'esempio successivo), che indica l'utilizzo di un cursore client. Per altre informazioni sulle differenze tra i cursori sul lato client e lato server, vedere [informazioni su cursori e blocchi](../../../ado/guide/data/understanding-cursors-and-locks.md).  
  
 Il **CursorLocation** della proprietà **adUseClient** impostazione consente di spostare la posizione del cursore dall'origine dati (il Server SQL, in questo caso) per il percorso del codice client (workstation desktop). Questa impostazione forza ADO per richiamare il motore del cursore Client per OLE DB sul client per creare e gestire il cursore.  
  
 Si può notare inoltre che il **LockType** parametro delle **Open** metodo modificato in **adLockBatchOptimistic**. Verrà aperto il cursore in modalità batch. (Provider memorizza nella cache più modifiche e li scrive all'origine dati sottostante solo quando si chiama il **UpdateBatch** (metodo).) Che sono stati modificati per la **Recordset** non verrà aggiornato nel database fino al **UpdateBatch** viene chiamato il metodo.  
  
 Infine, il codice in questa sezione Usa una versione modificata della funzione GetNewConnection. Questa versione della funzione ora restituisce un cursore lato client. La funzione è simile alla seguente:  
  
```  
'BeginNewConnection  
Public Function GetNewConnection() As ADODB.Connection  
    On Error GoTo ErrHandler:  
  
    Dim objConn As New ADODB.Connection  
    Dim strConnStr As String  
  
    strConnStr = "Provider='SQLOLEDB';Initial Catalog='Northwind';" & _  
                 "Data Source='MySqlServer';Integrated Security='SSPI';"  
  
    objConn.ConnectionString = strConnStr  
    objConn.CursorLocation = adUseClient  
    objConn.Open  
  
    Set GetNewConnection = objConn  
  
    Exit Function  
  
ErrHandler:  
    Set objConn = Nothing  
    Set GetNewConnection = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Function  
'EndNewConnection  
```  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Modifica di record esistenti](../../../ado/guide/data/editing-existing-records.md)  
  
-   [Aggiunta di record](../../../ado/guide/data/adding-records.md)  
  
-   [Determinazione delle funzionalità supportate](../../../ado/guide/data/determining-what-is-supported.md)  
  
-   [Eliminazione di record mediante il metodo Delete](../../../ado/guide/data/deleting-records-using-the-delete-method.md)  
  
-   [Alternative: uso di istruzioni SQL](../../../ado/guide/data/alternatives-using-sql-statements.md)
