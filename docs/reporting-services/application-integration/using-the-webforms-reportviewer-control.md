---
title: Utilizzo del controllo ReportViewer WebForms | Documenti Microsoft
ms.custom: 
ms.date: 06/12/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- ReportViewer controls
ms.assetid: 4c200f36-4012-4108-8095-370b426ccf8d
caps.latest.revision: 25
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 98afd0f9a34c1b15fce4905fcc1f16c3b9b024fb
ms.contentlocale: it-it
ms.lasthandoff: 06/13/2017

---
# <a name="using-the-webforms-reportviewer-control"></a>Utilizzo del controllo Web Form ReportViewer
  Per visualizzare i report distribuiti in un server di report o presenti in un file system locale, è possibile utilizzare il controllo Web Form ReportViewer per eseguirne il rendering in un'applicazione Web.  
  
## <a name="to-use-the-reportviewer-control-in-a-web-application"></a>Per utilizzare il controllo ReportViewer in un'applicazione Web  
  
1.  Creare un nuovo [!INCLUDE[msCoName](../../includes/msconame-md.md)] sito Web ASP.NET utilizzando [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[csprcs](../../includes/csprcs-md.md)] o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)].  
  
     \-O -  
  
     Aprire un sito Web ASP.NET esistente e aggiungere un nuovo Web Form.  
  
2.  Individuare il **ScriptManager** controllo il **Estensioni AJAX** gruppo il **della casella degli strumenti** finestra e trascinarlo nell'area di progettazione del Web form.  
  
     Se il **della casella degli strumenti** è non è visibile, è possibile accedervi dal **vista** menu selezionando **della casella degli strumenti**.  
  
3.  Individuare il **ReportViewer** controllo il **della casella degli strumenti** e trascinarlo nell'area di progettazione sotto la **ScriptManager** controllo.  
  
     Il **ReportViewer** controllo denominato reportViewer1 verrà aggiunto al form.  
  
 Dopo il controllo viene aggiunto al form il **attività di ReportViewer** viene visualizzato smart tag che richiede di selezionare un report. Se il report che si desidera visualizzare è stato distribuito a un server di report selezionare il  **\<Report Server >** opzione il **Scegli Report** elenco a discesa. Una volta il  **\<Report Server >** opzione è selezionata due proprietà aggiuntive verranno visualizzate, **Url Server di Report** e **percorso Report**. Il **Url Server di Report** è l'indirizzo del server di report e **percorso Report** è il percorso completo del report che si desidera eseguire il rendering.  
  
 Se si desidera visualizzare un report in modalità locale, è possibile selezionare l'opzione di **Progetta nuovo report** opzione per avviare Progettazione report oppure selezionare un report che fa già parte del progetto esistente. Dopo aver selezionato un report, assicurarsi di immettere il nome del file RDLC del report nel **ReportPath** proprietà del controllo ReportViewer. Questa proprietà viene visualizzata sotto il **LocalReport** nodo il **proprietà** riquadro.  
  
 È possibile nascondere uno o più elementi sulla barra degli strumenti di ReportViewer quando viene eseguito il rendering del report. Ad esempio, è possibile nascondere il pulsante di stampa. Per nascondere gli elementi della barra degli strumenti, impostare le proprietà seguenti di ReportViewer **False** nel **proprietà** riquadro.  
  
-   **ShowBackButton**  
  
-   **ShowExportControls**  
  
-   **ShowFindControls**  
  
-   **ShowPageNavigationControls**  
  
-   **ShowPrintButton**  
  
-   **ShowRefreshButton**  
  
-   **ShowZoomControl**  
  
## <a name="viewing-reports-in-remote-processing-mode"></a>Visualizzazione di report in modalità di elaborazione remota  
 Nell'esempio seguente viene illustrato come eseguire il rendering di un report distribuito in un server di report. In questo esempio viene usato il report Sales Order Detail incluso nel progetto di report di esempio [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
 Nell'esempio viene utilizzata l'autenticazione integrata di Windows, pertanto è innanzitutto necessario abilitare la rappresentazione. Per eseguire questo inserire la riga seguente nel **Web. config** file:  
  
```  
<!-- Web.config file. -->  
<identity impersonate="true"/>  
```  
  
> [!NOTE]  
>  Per impostazione predefinita, la rappresentazione è disabilitata.  

**LINGUAGGIO C#**
```
protected void Page_Init(object sender, EventArgs e)  
{  
    if (!Page.IsPostBack)  
    {  
        // Set the processing mode for the ReportViewer to Remote  
        reportViewer.ProcessingMode = ProcessingMode.Remote;  
  
        ServerReport serverReport = reportViewer.ServerReport;  
  
        // Set the report server URL and report path  
        serverReport.ReportServerUrl =  
            new Uri("http://<Server Name>/reportserver");  
        serverReport.ReportPath =  
            "/AdventureWorks Sample Reports/Sales Order Detail";  
  
        // Create the sales order number report parameter  
        ReportParameter salesOrderNumber = new ReportParameter();  
        salesOrderNumber.Name = "SalesOrderNumber";  
        salesOrderNumber.Values.Add("SO43661");  
  
        // Set the report parameters for the report  
        reportViewer.ServerReport.SetParameters(  
            new ReportParameter[] { salesOrderNumber });  
    }  
}  
```  
  
**VISUAL BASIC.NET**
```
Imports Microsoft.Reporting.WebForms  
  
Partial Class _Default  
    Inherits System.Web.UI.Page  
  
    Protected Sub Page_Init(ByVal sender As Object, _  
            ByVal e As System.EventArgs) Handles Me.Init  
  
        If Not Page.IsPostBack Then  
  
            'Set the processing mode for the ReportViewer to Remote  
            reportViewer.ProcessingMode = ProcessingMode.Remote  
  
            Dim serverReport As ServerReport  
            serverReport = reportViewer.ServerReport  
  
            'Set the report server URL and report path  
            serverReport.ReportServerUrl = _  
                New Uri("http://<Server Name>/reportserver")  
            serverReport.ReportPath = _  
                "/AdventureWorks Sample Reports/Sales Order Detail"  
  
            'Create the sales order number report parameter  
            Dim salesOrderNumber As New ReportParameter()  
            salesOrderNumber.Name = "SalesOrderNumber"  
            salesOrderNumber.Values.Add("SO43661")  
  
            'Set the report parameters for the report  
            Dim parameters() As ReportParameter = {salesOrderNumber}  
            serverReport.SetParameters(parameters)  
  
        End If  
  
    End Sub  
  
End Class  
```  
  
## <a name="viewing-reports-in-local-processing-mode"></a>Visualizzazione di report in modalità di elaborazione locale  
 Nell'esempio seguente viene illustrato come eseguire il rendering di un report che fa parte di un'applicazione Windows e non è stato distribuito in un server di report.  
  
###### <a name="to-add-the-sales-order-detail-report-to-a-web-site"></a>Per aggiungere il report Sales Order Detail a un sito Web  
  
1.  Aprire il sito Web a cui verrà aggiunto il report.  
  
2.  Dal **sito Web** dal menu **Aggiungi elemento esistente**.  
  
3.  Passare al percorso di installazione del progetto di report di esempio AdventureWorks.  
  
     Il percorso predefinito è C:\Programmi\Microsoft SQL Server\100\Samples\Reporting Services\Report Samples\AdventureWorks Sample Reports.  
  
4.  Selezionare il file Sales Order Detail.rdl e fare clic su di **Aggiungi** pulsante.  
  
     Il file Sales Order Detail.rdl dovrebbe ora far parte del progetto.  
  
5.  Il file Sales Order Detail.rdl in Esplora soluzioni e selezionare **rinominare**. Rinominare il report in **Sales Order rdlc** e premere INVIO.  
  
     Se Esplora soluzioni non è visibile, è possibile aprirlo dal **vista** menu scegliendo Esplora soluzioni.  
  
 Nell'esempio di codice seguente viene creato un set di dati per i dati dell'ordine di vendita, quindi viene eseguito il rendering del report Sales Order Detail in modalità locale.  

**LINGUAGGIO C#**
```csharp  
protected void Page_Init(object sender, EventArgs e)  
{  
    if (!Page.IsPostBack)  
    {  
        // Set the processing mode for the ReportViewer to Local  
        reportViewer.ProcessingMode = ProcessingMode.Local;  
  
        LocalReport localReport = reportViewer.LocalReport;  
  
        localReport.ReportPath = "Sales Order Detail.rdlc";  
  
        DataSet dataset = new DataSet("Sales Order Detail");  
  
        string salesOrderNumber = "SO43661";  
  
        GetSalesOrderData(salesOrderNumber, ref dataset);  
  
        ReportDataSource dsSalesOrder = new ReportDataSource();  
        dsSalesOrder.Name = "SalesOrder";  
        dsSalesOrder.Value = dataset.Tables["SalesOrder"];  
  
        localReport.DataSources.Add(dsSalesOrder);  
  
        GetSalesOrderDetailData(salesOrderNumber, ref dataset);  
  
        ReportDataSource dsSalesOrderDetail = new ReportDataSource();  
        dsSalesOrderDetail.Name = "SalesOrderDetail";  
        dsSalesOrderDetail.Value = dataset.Tables["SalesOrderDetail"];  
  
        localReport.DataSources.Add(dsSalesOrderDetail);  
  
        // Create the sales order number report parameter  
        ReportParameter rpSalesOrderNumber = new ReportParameter();  
        rpSalesOrderNumber.Name = "SalesOrderNumber";  
        rpSalesOrderNumber.Values.Add("SO43661");  
  
        // Set the report parameters for the report  
        localReport.SetParameters(  
            new ReportParameter[] { rpSalesOrderNumber });  
    }  
}  

private void GetSalesOrderData(string salesOrderNumber,  
                           ref DataSet dsSalesOrder)  
{  
    string sqlSalesOrder =  
        "SELECT SOH.SalesOrderNumber, S.Name AS Store, " +  
        "       SOH.OrderDate, C.FirstName AS SalesFirstName, " +  
        "       C.LastName AS SalesLastName, E.Title AS " +  
        "       SalesTitle, SOH.PurchaseOrderNumber, " +  
        "       SM.Name AS ShipMethod, BA.AddressLine1 " +  
        "       AS BillAddress1, BA.AddressLine2 AS " +  
        "       BillAddress2, BA.City AS BillCity, " +  
        "       BA.PostalCode AS BillPostalCode, BSP.Name " +  
        "       AS BillStateProvince, BCR.Name AS " +  
        "       BillCountryRegion, SA.AddressLine1 AS " +  
        "       ShipAddress1, SA.AddressLine2 AS " +  
        "       ShipAddress2, SA.City AS ShipCity, " +  
        "       SA.PostalCode AS ShipPostalCode, SSP.Name " +  
        "       AS ShipStateProvince, SCR.Name AS " +  
        "       ShipCountryRegion, CC.Phone AS CustPhone, " +  
        "       CC.FirstName AS CustFirstName, CC.LastName " +  
        "       AS CustLastName " +  
        "FROM   Person.Address SA INNER JOIN " +  
        "       Person.StateProvince SSP ON " +  
        "       SA.StateProvinceID = SSP.StateProvinceID " +  
        "       INNER JOIN Person.CountryRegion SCR ON " +  
        "       SSP.CountryRegionCode = SCR.CountryRegionCode " +  
        "       RIGHT OUTER JOIN Sales.SalesOrderHeader SOH " +  
        "       LEFT OUTER JOIN  Person.Contact CC ON " +  
        "       SOH.ContactID = CC.ContactID LEFT OUTER JOIN" +  
        "       Person.Address BA INNER JOIN " +  
        "       Person.StateProvince BSP ON " +  
        "       BA.StateProvinceID = BSP.StateProvinceID " +  
        "       INNER JOIN Person.CountryRegion BCR ON " +  
        "       BSP.CountryRegionCode = " +  
        "       BCR.CountryRegionCode ON SOH.BillToAddressID " +  
        "       = BA.AddressID ON  SA.AddressID = " +  
        "       SOH.ShipToAddressID LEFT OUTER JOIN " +  
        "       Person.Contact C RIGHT OUTER JOIN " +  
        "       HumanResources.Employee E ON C.ContactID = " +  
        "       E.ContactID ON SOH.SalesPersonID = " +  
        "       E.EmployeeID LEFT OUTER JOIN " +  
        "       Purchasing.ShipMethod SM ON SOH.ShipMethodID " +  
        "       = SM.ShipMethodID LEFT OUTER JOIN Sales.Store" +  
        "        S ON SOH.CustomerID = S.CustomerID " +  
        "WHERE  (SOH.SalesOrderNumber = @SalesOrderNumber)";  
  
    SqlConnection connection = new  
        SqlConnection("Data Source=(local); " +  
                      "Initial Catalog=AdventureWorks; " +  
                      "Integrated Security=SSPI");  
  
    SqlCommand command =  
        new SqlCommand(sqlSalesOrder, connection);  
  
    command.Parameters.Add(  
        new SqlParameter("SalesOrderNumber",  
        salesOrderNumber));  
  
    SqlDataAdapter salesOrderAdapter = new  
        SqlDataAdapter(command);  
  
    salesOrderAdapter.Fill(dsSalesOrder, "SalesOrder");  
}  
  
private void GetSalesOrderDetailData(string salesOrderNumber,  
                       ref DataSet dsSalesOrder)  
{  
    string sqlSalesOrderDetail =  
        "SELECT  SOD.SalesOrderDetailID, SOD.OrderQty, " +  
        "        SOD.UnitPrice, CASE WHEN " +  
        "        SOD.UnitPriceDiscount IS NULL THEN 0 " +  
        "        ELSE SOD.UnitPriceDiscount END AS " +  
        "        UnitPriceDiscount, SOD.LineTotal, " +  
        "        SOD.CarrierTrackingNumber, " +  
        "        SOD.SalesOrderID, P.Name, P.ProductNumber " +  
        "FROM    Sales.SalesOrderDetail SOD INNER JOIN " +  
        "        Production.Product P ON SOD.ProductID = " +  
        "        P.ProductID INNER JOIN " +  
        "        Sales.SalesOrderHeader SOH ON " +  
        "        SOD.SalesOrderID = SOH.SalesOrderID " +  
        "WHERE   (SOH.SalesOrderNumber = @SalesOrderNumber) " +  
        "ORDER BY SOD.SalesOrderDetailID";  
  
    using (SqlConnection connection = new  
        SqlConnection("Data Source=(local); " +  
                      "Initial Catalog=AdventureWorks; " +  
                      "Integrated Security=SSPI"))  
    {  
  
        SqlCommand command =  
            new SqlCommand(sqlSalesOrderDetail, connection);  
  
        command.Parameters.Add(  
            new SqlParameter("SalesOrderNumber",  
            salesOrderNumber));  
  
        SqlDataAdapter salesOrderDetailAdapter = new  
            SqlDataAdapter(command);  
  
        salesOrderDetailAdapter.Fill(dsSalesOrder,  
            "SalesOrderDetail");  
    }  
}  
```  
**VISUAL BASIC.NET**
```vb  
Imports System.Data  
Imports System.Data.SqlClient  
Imports Microsoft.Reporting.WebForms  
  
Partial Class _Default  
    Inherits System.Web.UI.Page  
  
    Protected Sub Page_Init(ByVal sender As Object, _  
                ByVal e As System.EventArgs) Handles Me.Init  
  
        If Not Page.IsPostBack Then  
  
            'Set the processing mode for the ReportViewer to Local  
            reportViewer.ProcessingMode = ProcessingMode.Local  
  
            Dim localReport As LocalReport  
            localReport = reportViewer.LocalReport  
  
            localReport.ReportPath = "Sales Order Detail.rdlc"  
  
            Dim dataset As New DataSet("Sales Order Detail")  
  
            Dim salesOrderNumber As String = "SO43661"  
  
            'Get the sales order data  
            GetSalesOrderData(salesOrderNumber, dataset)  
  
            'Create a report data source for the sales order data  
            Dim dsSalesOrder As New ReportDataSource()  
            dsSalesOrder.Name = "SalesOrder"  
            dsSalesOrder.Value = dataset.Tables("SalesOrder")  
  
            localReport.DataSources.Add(dsSalesOrder)  
  
            'Get the sales order detail data  
            GetSalesOrderDetailData(salesOrderNumber, dataset)  
  
            'Create a report data source for the sales   
            'order detail data  
            Dim dsSalesOrderDetail As New ReportDataSource()  
            dsSalesOrderDetail.Name = "SalesOrderDetail"  
            dsSalesOrderDetail.Value = _  
                dataset.Tables("SalesOrderDetail")  
  
            localReport.DataSources.Add(dsSalesOrderDetail)  
  
            'Create a report parameter for the sales order number   
            Dim rpSalesOrderNumber As New ReportParameter()  
            rpSalesOrderNumber.Name = "SalesOrderNumber"  
            rpSalesOrderNumber.Values.Add("SO43661")  
  
            'Set the report parameters for the report  
            Dim parameters() As ReportParameter = {rpSalesOrderNumber}  
            localReport.SetParameters(parameters)  
  
        End If  
  
    End Sub  
  
    Private Sub GetSalesOrderData(ByVal salesOrderNumber As String, _  
                               ByRef dsSalesOrder As DataSet)  
  
        Dim sqlSalesOrder As String = _  
            "SELECT SOH.SalesOrderNumber, S.Name AS Store, " & _  
            "       SOH.OrderDate, C.FirstName AS SalesFirstName, " & _  
            "       C.LastName AS SalesLastName, E.Title AS " & _  
            "       SalesTitle, SOH.PurchaseOrderNumber, " & _  
            "       SM.Name AS ShipMethod, BA.AddressLine1 " & _  
            "       AS BillAddress1, BA.AddressLine2 AS " & _  
            "       BillAddress2, BA.City AS BillCity, " & _  
            "       BA.PostalCode AS BillPostalCode, BSP.Name " & _  
            "       AS BillStateProvince, BCR.Name AS " & _  
            "       BillCountryRegion, SA.AddressLine1 AS " & _  
            "       ShipAddress1, SA.AddressLine2 AS " & _  
            "       ShipAddress2, SA.City AS ShipCity, " & _  
            "       SA.PostalCode AS ShipPostalCode, SSP.Name " & _  
            "       AS ShipStateProvince, SCR.Name AS " & _  
            "       ShipCountryRegion, CC.Phone AS CustPhone, " & _  
            "       CC.FirstName AS CustFirstName, CC.LastName " & _  
            "       AS CustLastName " & _  
            "FROM   Person.Address SA INNER JOIN " & _  
            "       Person.StateProvince SSP ON " & _  
            "       SA.StateProvinceID = SSP.StateProvinceID " & _  
            "       INNER JOIN Person.CountryRegion SCR ON " & _  
            "       SSP.CountryRegionCode = SCR.CountryRegionCode " & _  
            "       RIGHT OUTER JOIN Sales.SalesOrderHeader SOH " & _  
            "       LEFT OUTER JOIN  Person.Contact CC ON " & _  
            "       SOH.ContactID = CC.ContactID LEFT OUTER JOIN" & _  
            "       Person.Address BA INNER JOIN " & _  
            "       Person.StateProvince BSP ON " & _  
            "       BA.StateProvinceID = BSP.StateProvinceID " & _  
            "       INNER JOIN Person.CountryRegion BCR ON " & _  
            "       BSP.CountryRegionCode = " & _  
            "       BCR.CountryRegionCode ON SOH.BillToAddressID " & _  
            "       = BA.AddressID ON  SA.AddressID = " & _  
            "       SOH.ShipToAddressID LEFT OUTER JOIN " & _  
            "       Person.Contact C RIGHT OUTER JOIN " & _  
            "       HumanResources.Employee E ON C.ContactID = " & _  
            "       E.ContactID ON SOH.SalesPersonID = " & _  
            "       E.EmployeeID LEFT OUTER JOIN " & _  
            "       Purchasing.ShipMethod SM ON SOH.ShipMethodID " & _  
            "       = SM.ShipMethodID LEFT OUTER JOIN Sales.Store" & _  
            "        S ON SOH.CustomerID = S.CustomerID " & _  
            "WHERE  (SOH.SalesOrderNumber = @SalesOrderNumber)"  
  
        Using connection As New SqlConnection( _  
                      "Data Source=(local); " & _  
                      "Initial Catalog=AdventureWorks; " & _  
                      "Integrated Security=SSPI")  
  
            Dim command As New SqlCommand(sqlSalesOrder, connection)  
  
            Dim parameter As New SqlParameter("SalesOrderNumber", _  
                salesOrderNumber)  
            command.Parameters.Add(parameter)  
  
            Dim salesOrderAdapter As New SqlDataAdapter(command)  
  
            salesOrderAdapter.Fill(dsSalesOrder, "SalesOrder")  
  
        End Using  
  
    End Sub  
  
    Private Sub GetSalesOrderDetailData( _  
                           ByVal salesOrderNumber As String, _  
                           ByRef dsSalesOrder As DataSet)  
  
        Dim sqlSalesOrderDetail As String = _  
            "SELECT  SOD.SalesOrderDetailID, SOD.OrderQty, " & _  
            "        SOD.UnitPrice, CASE WHEN " & _  
            "        SOD.UnitPriceDiscount IS NULL THEN 0 " & _  
            "        ELSE SOD.UnitPriceDiscount END AS " & _  
            "        UnitPriceDiscount, SOD.LineTotal, " & _  
            "        SOD.CarrierTrackingNumber, " & _  
            "        SOD.SalesOrderID, P.Name, P.ProductNumber " & _  
            "FROM    Sales.SalesOrderDetail SOD INNER JOIN " & _  
            "        Production.Product P ON SOD.ProductID = " & _  
            "        P.ProductID INNER JOIN " & _  
            "        Sales.SalesOrderHeader SOH ON " & _  
            "        SOD.SalesOrderID = SOH.SalesOrderID " & _  
            "WHERE   (SOH.SalesOrderNumber = @SalesOrderNumber) " & _  
            "ORDER BY SOD.SalesOrderDetailID"  
  
        Using connection As New SqlConnection( _  
                      "Data Source=(local); " & _  
                      "Initial Catalog=AdventureWorks; " & _  
                      "Integrated Security=SSPI")  
  
            Dim command As New SqlCommand(sqlSalesOrderDetail, _  
                                          connection)  
  
            Dim parameter As New SqlParameter("SalesOrderNumber", _  
                salesOrderNumber)  
            command.Parameters.Add(parameter)  
  
            Dim salesOrderDetailAdapter As New SqlDataAdapter(command)  
  
            salesOrderDetailAdapter.Fill(dsSalesOrder, _  
                "SalesOrderDetail")  
  
        End Using  
  
    End Sub  
  
End Class  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Integrazione di Reporting Services utilizzando i controlli ReportViewer](../../reporting-services/application-integration/integrating-reporting-services-using-reportviewer-controls.md)  
 [Raccolta dei dati 2016 controllo ReportViewer](../../reporting-services/application-integration/integrating-reporting-services-using-reportviewer-controls-data-collection.md)
  
  
