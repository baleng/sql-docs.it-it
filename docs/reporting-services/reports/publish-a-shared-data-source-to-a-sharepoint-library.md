---
title: Pubblicare un'origine dati condivisa in una raccolta di SharePoint | Microsoft Docs
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: reports
ms.topic: conceptual
helpviewer_keywords:
- data sources [Reporting Services], publishing to a SharePoint library
- SharePoint integration [Reporting Services], publishing to a library
- publishing reports [Reporting Services], to a SharePoint library
ms.assetid: 966ed425-3ce2-4e76-8237-3c1c977954ae
author: markingmyname
ms.author: maghan
ms.openlocfilehash: a2b2d16b5815a665e718e16fb04f74ff408fefae
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52527587"
---
# <a name="publish-a-shared-data-source-to-a-sharepoint-library"></a>Pubblicare un'origine dati condivisa in una raccolta di SharePoint
  Per pubblicare un'origine dati condivisa in un server di report eseguito in modalità integrata SharePoint, è necessario impostare le proprietà del progetto report in Progettazione report. Nelle proprietà del progetto tutti i riferimenti a server, report e origini dati condivise devono essere URL completi.  
  
 È necessario disporre dell'autorizzazione **Membro** o **Proprietario** il sito di SharePoint. Per altre informazioni, vedere [Esempi di URL per elementi di report pubblicati in un server di report in modalità SharePoint &#40;SSRS&#41;](../../reporting-services/tools/url-examples-for-items-on-a-report-server-sharepoint-mode.md).  
  
### <a name="to-publish-a-shared-data-source-to-a-sharepoint-site"></a>Per pubblicare un'origine dati condivisa in un sito di SharePoint  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]aprire un progetto del server di report esistente o nuovo.  
  
2.  Scegliere **Proprietà** dal menu **Progetto**. Verrà visualizzata la finestra di dialogo _\<Pagine delle proprietà_ **del progetto**.  
  
3.  Nella casella **Configurazione** scegliere quella da utilizzare per la pubblicazione in un sito di SharePoint.  
  
4.  Se si desidera pubblicare le origini dati condivise nel progetto e sovrascrivere origini dati condivise pubblicate in precedenza, impostare **OverwriteDataSources** su **True**.  
  
5.  (Facoltativo) Per **TargetDataSourceFolder**, digitare un URL a una raccolta di SharePoint oppure a una cartella della raccolta, ad esempio `https://TestServer/TestSite/Documents/DataSources`.  
  
     Se non si specifica alcun valore, verrà utilizzato il valore **TargetReportFolder** .  
  
6.  Per **TargetReportFolder**, digitare l'URL di una raccolta o di una cartella della raccolta, ad esempio `https://TestServer/TestSite/Documents/Reports`.  
  
7.  Per **TargetServerURL**, digitare l'URL di un sito principale o secondario di SharePoint. Se non si specifica un sito, verrà utilizzato il sito principale predefinito, Ad esempio `https://servername`, `https://servername/site` o `https://servername/site/subsite`.  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
9. In Esplora soluzioni fare clic con il pulsante destro del mouse sull'origine dati condivisa da pubblicare e quindi scegliere **Distribuisci**. L'origine dei dati verrà pubblicata nel percorso specificato in **TargetDataSourceFolder**. Gli eventuali errori di distribuzioni verranno visualizzati nella finestra di output.  
  
    > [!NOTE]  
    >  Dopo la pubblicazione di un'origine dati condivisa in un sito di SharePoint, l'estensione del file viene cambiata in rsds. È possibile modificare e gestire direttamente un'origine dati condivisa nel sito di SharePoint. Per altre informazioni, vedere [Creare e gestire origini dati condivise &#40;Reporting Services in modalità integrata SharePoint&#41;](https://msdn.microsoft.com/library/2d3428e4-a810-4e66-a287-ff18e57fad76).  
  
## <a name="see-also"></a>Vedere anche  
 [Pubblicare un report in una raccolta di SharePoint](../../reporting-services/reports/publish-a-report-to-a-sharepoint-library.md)   
 [Esempi di URL per elementi di report pubblicati in un server di report in modalità SharePoint &#40;SSRS&#41;](../../reporting-services/tools/url-examples-for-items-on-a-report-server-sharepoint-mode.md)   
 [Finestra di dialogo Pagine delle proprietà del progetto](../../reporting-services/tools/project-property-pages-dialog-box.md)   
 [Impostare le proprietà di distribuzione &#40;Reporting Services&#41;](../../reporting-services/tools/set-deployment-properties-reporting-services.md)   
 [Pubblicazione dei report in un server di report](../../reporting-services/reports/publishing-reports-to-a-report-server.md)   
 [Usare una connessione Office Data Connection &#40;.odc&#41; ai report &#40;Reporting Services in modalità integrata SharePoint&#41;](../../reporting-services/report-data/use-an-office-data-connection-odc-with-reports.md)  
  
  
