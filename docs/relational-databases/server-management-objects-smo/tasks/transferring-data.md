---
title: Il trasferimento dei dati | Documenti Microsoft
ms.custom: 
ms.date: 08/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: smo
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- data transfers [SMO]
- transferring data
ms.assetid: eea255c3-8251-40f0-973b-fe4ef6cb5261
caps.latest.revision: "50"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7a5be776cd4852c09ae6a3cbc2b344646f8504fc
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/17/2017
---
# <a name="transferring-data"></a>Trasferimento di dati
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]La <xref:Microsoft.SqlServer.Management.Smo.Transfer> classe è una classe di utilità che fornisce gli strumenti per trasferire oggetti e dati.  
  
 Gli oggetti nello schema del database vengono trasferiti eseguendo uno script generato sul server di destinazione. I dati <xref:Microsoft.SqlServer.Management.Smo.Table> vengono trasferiti con un pacchetto DTS creato dinamicamente.  
  
 Il <xref:Microsoft.SqlServer.Management.Smo.Transfer> viene utilizzata da object il [SQLBulkCopy](https://msdn.microsoft.com/library/system.data.sqlclient.sqlbulkcopy.aspx) API per trasferire i dati. Inoltre, i metodi e le proprietà utilizzati per eseguire trasferimenti di dati si trovano nell'oggetto <xref:Microsoft.SqlServer.Management.Smo.Transfer> anziché nell'oggetto <xref:Microsoft.SqlServer.Management.Smo.Database>. Lo spostamento delle funzionalità dalle classi di istanze alle classi di utilità è coerente con un modello a oggetti semplificato poiché il codice per le attività specifiche viene caricato solo quando è richiesto.  
  
 L'oggetto <xref:Microsoft.SqlServer.Management.Smo.Transfer> non supporta trasferimenti di dati in un database di destinazione con una proprietà <xref:Microsoft.SqlServer.Management.Smo.Database.CompatibilityLevel%2A> inferiore alla versione dell'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="example"></a>Esempio  
Per usare qualsiasi esempio di codice fornito, è necessario scegliere l'ambiente di programmazione, il modello di programmazione e il linguaggio di programmazione per la creazione dell'applicazione. Per ulteriori informazioni, vedere [crea un Visual C &#35; Progetto SMO in Visual Studio .NET](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
 
  
## <a name="transferring-schema-and-data-from-one-database-to-another-in-visual-basic"></a>Trasferimento di schemi e dati da un database a un altro in Visual Basic  
 In questo esempio di codice viene illustrato come trasferire schemi e dati da un database all'altro utilizzando l'oggetto <xref:Microsoft.SqlServer.Management.Smo.Transfer>.  
  
```VBNET
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server
'Reference the AdventureWorks2012 2008R2 database
Dim db As Database
db = srv.Databases("AdventureWorks2012")
'Create a new database that is to be destination database.
Dim dbCopy As Database
dbCopy = New Database(srv, "AdventureWorks2012Copy")
dbCopy.Create()
'Define a Transfer object and set the required options and properties.
Dim xfr As Transfer
xfr = New Transfer(db)
xfr.CopyAllTables = True
xfr.Options.WithDependencies = True
xfr.Options.ContinueScriptingOnError = True
xfr.DestinationDatabase = "AdventureWorks2012Copy"
xfr.DestinationServer = srv.Name
xfr.DestinationLoginSecure = True
xfr.CopySchema = True
'Script the transfer. Alternatively perform immediate data transfer with TransferData method.
xfr.ScriptTransfer()
```
  
## <a name="transferring-schema-and-data-from-one-database-to-another-in-visual-c"></a>Trasferimento di schemi e dati da un database all'altro in Visual C#  
 In questo esempio di codice viene illustrato come trasferire schemi e dati da un database all'altro utilizzando l'oggetto <xref:Microsoft.SqlServer.Management.Smo.Transfer>.  
  
```csharp  
{  
            Server srv;  
            srv = new Server();  
            //Reference the AdventureWorks2012 database   
            Database db;  
            db = srv.Databases["AdventureWorks2012"];  
            //Create a new database that is to be destination database.   
            Database dbCopy;  
            dbCopy = new Database(srv, "AdventureWorks2012Copy");  
            dbCopy.Create();  
            //Define a Transfer object and set the required options and properties.   
            Transfer xfr;  
            xfr = new Transfer(db);  
            xfr.CopyAllTables = true;  
            xfr.Options.WithDependencies = true;  
            xfr.Options.ContinueScriptingOnError = true;  
            xfr.DestinationDatabase = "AdventureWorks2012Copy";  
            xfr.DestinationServer = srv.Name;  
            xfr.DestinationLoginSecure = true;  
            xfr.CopySchema = true;  
            //Script the transfer. Alternatively perform immediate data transfer   
            // with TransferData method.   
            xfr.ScriptTransfer();  
        }   
```  
  
## <a name="transferring-schema-and-data-from-one-database-to-another-in-powershell"></a>Trasferimento di schemi e dati da un database all'altro in PowerShell  
 In questo esempio di codice viene illustrato come trasferire schemi e dati da un database all'altro utilizzando l'oggetto <xref:Microsoft.SqlServer.Management.Smo.Transfer>.  
  
```powershell  
#Connect to the local, default instance of SQL Server.  
  
#Get a server object which corresponds to the default instance  
$srv = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Server  
  
#Reference the AdventureWorks2012 database.  
$db = $srv.Databases["AdventureWorks2012"]  
  
#Create a database to hold the copy of AdventureWorks  
$dbCopy = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Database -argumentlist $srv, "AdventureWorksCopy"  
$dbCopy.Create()  
  
#Define a Transfer object and set the required options and properties.  
$xfr = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Transfer -argumentlist $db  
  
#Set this objects properties  
$xfr.CopyAllTables = $true  
$xfr.Options.WithDependencies = $true  
$xfr.Options.ContinueScriptingOnError = $true  
$xfr.DestinationDatabase = "AdventureWorksCopy"  
$xfr.DestinationServer = $srv.Name  
$xfr.DestinationLoginSecure = $true  
$xfr.CopySchema = $true  
"Scripting Data Transfer"  
#Script the transfer. Alternatively perform immediate data transfer with TransferData method.  
$xfr.ScriptTransfer()  
```  
  
  