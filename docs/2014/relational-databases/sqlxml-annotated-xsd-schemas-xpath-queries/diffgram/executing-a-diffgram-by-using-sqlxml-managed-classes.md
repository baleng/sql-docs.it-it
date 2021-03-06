---
title: Esecuzione di un DiffGram con SQLXML classi gestite | Documenti di Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- DiffGrams [SQLXML], Managed Classes
- SQLXML Managed Classes, DiffGrams
- Managed Classes [SQLXML], DiffGrams
- SQLXML, Managed Classes
ms.assetid: 81c687ca-8c9f-4f58-801f-8dabcc508a06
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 238d4871c8c738dbb7038b182800ea7eee645d65
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/02/2018
ms.locfileid: "48057121"
---
# <a name="executing-a-diffgram-by-using-sqlxml-managed-classes"></a>Esecuzione di un DiffGram mediante classi gestite SQLXML
  In questo esempio viene illustrato come eseguire un file DiffGram nel [!INCLUDE[msCoName](../../../includes/msconame-md.md)] ambiente .NET Framework per applicare i dati degli aggiornamenti per [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tabelle usando le classi gestite SQLXML (Microsoft.Data.SqlXml).  
  
 In questo esempio DiffGram viene utilizzato per aggiornare le informazioni per il cliente ALFKI (CompanyName e ContactName).  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql" sql:mapping-schema="DiffGramSchema.xml">  
  <diffgr:diffgram   
           xmlns:msdata="urn:schemas-microsoft-com:xml-msdata"   
           xmlns:diffgr="urn:schemas-microsoft-com:xml-diffgram-v1">  
    <DataInstance>  
      <Customer diffgr:id="Customer1"   
                msdata:rowOrder="0" diffgr:hasChanges="modified"   
                CustomerID="ALFKI">  
          <CompanyName>Bottom Dollar Markets</CompanyName>  
          <ContactName>Antonio Moreno</ContactName>  
      </Customer>  
    </DataInstance>  
    <diffgr:before>  
     <Customer diffgr:id="Customer1"   
               msdata:rowOrder="0"   
               CustomerID="ALFKI">  
        <CompanyName>Alfreds Futterkiste</CompanyName>  
        <ContactName>Maria Anders</ContactName>  
      </Customer>  
    </diffgr:before>  
  </diffgr:diffgram>  
</ROOT>  
```  
  
 Il  **\<prima di >** blocco include un  **\<cliente >** elemento (**diffgr: ID = "Customer1"**). Il  **\<DataInstance >** inclusioni di blocco corrispondente  **\<cliente >** elemento con stesso **id**. Il  **\<cliente >** elemento il  **\<NewDataSet >** specifica inoltre **diffgr: HasChanges = "modified"**. indicando un'operazione di aggiornamento e il record del cliente nella tabella Cust viene aggiornato di conseguenza. Si noti che se il **diffgr: HasChanges** attributo non viene specificato, la logica di elaborazione DiffGram ignora questo elemento e viene eseguito alcun aggiornamento.  
  
 Di seguito è riportato il codice per un'esercitazione applicazione c# che illustra come usare le classi gestite SQLXML per eseguire il DiffGram sopra riportato e aggiornamento di due tabelle (Cust, Ord) verrà creata anche nel **tempdb** database.  
  
```  
using System;  
using System.Data;  
using Microsoft.Data.SqlXml;  
using System.IO;  
class Test  
{  
   static string ConnString = "Provider=SQLOLEDB;Server=MyServer;database=tempdb;Integrated Security=SSPI;";  
   public static int testParams()  
   {  
      SqlXmlAdapter ad;  
      // Need a memory stream to hold diff gram temporarily  
      MemoryStream ms = new MemoryStream();  
      SqlXmlCommand cmd = new SqlXmlCommand(ConnString);  
      cmd.RootTag = "ROOT";  
      cmd.CommandStream = new FileStream("MyDiffgram.xml", FileMode.Open, FileAccess.Read);  
      cmd.CommandType = SqlXmlCommandType.DiffGram;  
      cmd.SchemaPath = "DiffGramSchema.xml";  
      // Load data set  
      DataSet ds = new DataSet();  
      ad = new SqlXmlAdapter(cmd);  
      ad.Fill(ds);  
      ad.Update(ds);  
      return 0;  
   }  
   public static int Main(String[] args)  
   {  
      testParams();  
      return 0;  
   }  
}  
```  
  
### <a name="to-test-the-application"></a>Per testare l'applicazione  
  
1.  Verificare che .NET Framework sia installato nel computer.  
  
2.  Salvare lo schema XSD seguente (DiffGramSchema.xml) in una cartella:  
  
    ```  
    <xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
                xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
     <xsd:annotation>  
      <xsd:documentation>  
        Diffgram Customers/Orders Schema.  
      </xsd:documentation>  
      <xsd:appinfo>  
           <sql:relationship name="CustomersOrders"   
                      parent="Cust"  
                      parent-key="CustomerID"  
                      child-key="CustomerID"  
                      child="Ord"/>  
      </xsd:appinfo>  
     </xsd:annotation>  
     <xsd:element name="Customer" sql:relation="Cust">  
      <xsd:complexType>  
        <xsd:sequence>  
          <xsd:element name="CompanyName"    type="xsd:string"/>  
          <xsd:element name="ContactName"    type="xsd:string"/>  
           <xsd:element name="Order" sql:relation="Ord" sql:relationship="CustomersOrders">  
            <xsd:complexType>  
              <xsd:attribute name="OrderID" type="xsd:int" sql:field="OrderID"/>  
              <xsd:attribute name="CustomerID" type="xsd:string"/>  
            </xsd:complexType>  
          </xsd:element>  
        </xsd:sequence>  
        <xsd:attribute name="CustomerID" type="xsd:string" sql:field="CustomerID"/>  
      </xsd:complexType>  
     </xsd:element>  
    </xsd:schema>  
    ```  
  
3.  Creare le tabelle nel **tempdb** database.  
  
    ```  
    CREATE TABLE Cust(  
            CustomerID  nchar(5) Primary Key,  
            CompanyName nvarchar(40) NOT NULL ,  
            ContactName nvarchar(60) NULL)  
    GO  
  
    CREATE TABLE Ord(  
       OrderID    int Primary Key,  
       CustomerID nchar(5) Foreign Key REFERENCES Cust(CustomerID))  
    GO  
    ```  
  
4.  Aggiungere i dati di esempio seguenti:  
  
    ```  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ALFKI', N'Alfreds Futterkiste', N'Maria Anders')  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ANATR', N'Ana Trujillo Emparedados y helados', N'Ana Trujillo')  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ANTON', N'Antonio Moreno Taquería', N'Antonio Moreno')  
  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(1, N'ALFKI')  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(2, N'ANATR')  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(3, N'ANTON')  
    ```  
  
5.  Copiare il DiffGram sopra riportato e incollarlo in un file di testo. Salvare il file con il nome MyDiffGram.xml nella stessa cartella utilizzata nel passaggio 1.  
  
6.  Salvare il codice C# (DiffgramSample.cs) sopra riportato nella stessa cartella in cui DiffGramSchema.xml e MyDiffGram.xml sono stati archiviati nei passaggi precedenti.  
  
    > [!NOTE]  
    >  Sarà necessario aggiornare il nome dell'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] nella stringa di connessione da '`MyServer`' al nome effettivo dell'istanza installata di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
     Se si archiviano i file in un'altra cartella, sarà necessario modificare il codice e specificare il percorso di directory appropriato per lo schema di mapping.  
  
7.  Compilare il codice. Per compilare il codice al prompt dei comandi, utilizzare:  
  
    ```  
    csc /reference:Microsoft.Data.SqlXML.dll DiffgramSample.cs  
    ```  
  
     Viene creato un file eseguibile (DiffgramSample.exe).  
  
8.  Al prompt dei comandi eseguire DiffgramSample.exe.  
  
## <a name="see-also"></a>Vedere anche  
 [Esempi di DiffGram &#40;SQLXML 4.0&#41;](diffgram-examples-sqlxml-4-0.md)  
  
  
