---
title: Creazione, modifica e rimozione di valori predefiniti | Documenti di Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- defaults [SMO]
ms.assetid: c30ac3b9-8150-4264-ba4c-c549f44261ab
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 69a9a892aa091d6efcd093285ab60b683e2b7920
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/02/2018
ms.locfileid: "48219711"
---
# <a name="creating-altering-and-removing-defaults"></a>Creazione, modifica e rimozione di valori predefiniti
  In SMO ([!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Management Objects), il vincolo predefinito è rappresentato dall'oggetto <xref:Microsoft.SqlServer.Management.Smo.Default>.  
  
 La proprietà <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.TextBody%2A> dell'oggetto <xref:Microsoft.SqlServer.Management.Smo.Default> viene utilizzata per impostare il valore da inserire. Tale valore può essere una costante o un'istruzione [!INCLUDE[tsql](../../../includes/tsql-md.md)] che restituisce un valore costante, ad esempio GETDATE(). La proprietà <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.TextBody%2A> non può essere modificata tramite il metodo <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.Alter%2A>. È invece necessario eliminare l'oggetto <xref:Microsoft.SqlServer.Management.Smo.Default> e quindi ricrearlo.  
  
## <a name="example"></a>Esempio  
 Per usare qualsiasi esempio di codice fornito, è necessario scegliere l'ambiente di programmazione, il modello di programmazione e il linguaggio di programmazione per la creazione dell'applicazione. Per altre informazioni, vedere [creare un progetto Visual Basic SMO in Visual Studio .NET](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md) oppure [creare un Visual C#&#35; progetto SMO in Visual Studio .NET](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
  
## <a name="creating-altering-and-removing-a-default-in-visual-basic"></a>Creazione, modifica e rimozione di un valore predefinito in Visual Basic  
 In questo esempio di codice viene illustrato come creare un valore predefinito rappresentato da testo semplice e un altro valore predefinito rappresentato da un'istruzione [!INCLUDE[tsql](../../../includes/tsql-md.md)]. Il valore predefinito deve essere collegato alla colonna tramite il metodo <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.BindToColumn%2A> e scollegato tramite il metodo <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.UnbindFromColumn%2A>.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBDefaults1](SMO How to#SMO_VBDefaults1)]  -->  
  
## <a name="creating-altering-and-removing-a-default-in-visual-c"></a>Creazione, modifica e rimozione di un valore predefinito in Visual C#  
 In questo esempio di codice viene illustrato come creare un valore predefinito rappresentato da testo semplice e un altro valore predefinito rappresentato da un'istruzione [!INCLUDE[tsql](../../../includes/tsql-md.md)]. Il valore predefinito deve essere collegato alla colonna tramite il metodo <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.BindToColumn%2A> e scollegato tramite il metodo <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.UnbindFromColumn%2A>.  
  
```  
{  
  
          Server srv = new Server();  
  
            //Reference the AdventureWorks2012 database.   
            Database  db = srv.Databases["AdventureWorks2012"];  
  
            //Define a Default object variable by supplying the parent database and the default name   
            //in the constructor.   
            Default def = new Default(db, "Test_Default2");  
  
            //Set the TextHeader and TextBody properties that define the default.   
            def.TextHeader = "CREATE DEFAULT [Test_Default2] AS";  
            def.TextBody = "GetDate()";  
  
            //Create the default on the instance of SQL Server.   
            def.Create();  
  
            //Bind the default to a column in a table in AdventureWorks2012  
            def.BindToColumn("SpecialOffer", "StartDate", "Sales");  
  
            //Unbind the default from the column and remove it from the database.   
            def.UnbindFromColumn("SpecialOffer", "StartDate", "Sales");  
            def.Drop();  
        }  
```  
  
## <a name="creating-altering-and-removing-a-default-in-powershell"></a>Creazione, modifica e rimozione di un valore predefinito in PowerShell  
 In questo esempio di codice viene illustrato come creare un valore predefinito rappresentato da testo semplice e un altro valore predefinito rappresentato da un'istruzione [!INCLUDE[tsql](../../../includes/tsql-md.md)]. Il valore predefinito deve essere collegato alla colonna tramite il metodo <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.BindToColumn%2A> e scollegato tramite il metodo <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.UnbindFromColumn%2A>.  
  
```  
# Set the path context to the local, default instance of SQL Server and get a reference to AdventureWorks2012  
CD \sql\localhost\default\databases  
$db = get-item Adventureworks2012  
  
#Define a Default object variable by supplying the parent database and the default name in the constructor.  
$def = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Default `  
-argumentlist $db, "Test_Default2"  
  
#Set the TextHeader and TextBody properties that define the default.   
$def.TextHeader = "CREATE DEFAULT [Test_Default2] AS"  
$def.TextBody = "GetDate()"  
  
#Create the default on the instance of SQL Server.   
$def.Create()  
  
#Bind the default to the column.   
$def.BindToColumn("SpecialOffer", "StartDate", "Sales")  
  
#Unbind the default from the column and remove it from the database.   
$def.UnbindFromColumn("SpecialOffer", "StartDate", "Sales")  
$def.Drop()  
```  
  
## <a name="see-also"></a>Vedere anche  
 <xref:Microsoft.SqlServer.Management.Smo.Default>  
  
  
