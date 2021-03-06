---
title: Using the Detail Property to Handle Specific Errors | (Uso della proprietà Detail per la gestione di errori specifici) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.topic: reference
helpviewer_keywords:
- exceptions [Reporting Services], Detail property
- Detail property
- InnerText property
ms.assetid: 4392633d-b46b-41e6-bc12-efb64e166704
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 1966cd4898731b5176541a8dd0707bf0deef25bf
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/02/2018
ms.locfileid: "48222881"
---
# <a name="using-the-detail-property-to-handle-specific-errors"></a>Utilizzo della proprietà Detail per la gestione di errori specifici
  Per classificare ulteriormente le eccezioni, [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] restituisce informazioni aggiuntive sull'errore nella proprietà **InnerText** degli elementi figlio nella proprietà **Detail** dell'eccezione SOAP. Poiché la proprietà **Detail** è un oggetto **XmlNode**, è possibile accedere al testo interno dell'elemento figlio **Message** usando il codice seguente.  
  
 Per un elenco di tutti gli elementi figlio disponibili inclusi nella proprietà **Detail**, vedere [Detail Property](../soapexception-class/detail-property.md). Per altre informazioni, vedere l'argomento relativo alla proprietà Detail nella documentazione di [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] SDK.  
  
```vb  
Try  
' Code for accessing the report server  
Catch ex As SoapException  
   ' The exception is a SOAP exception, so use  
   ' the Detail property's Message element.  
   Console.WriteLine(ex.Detail("Message").InnerXml)  
End Try  
```  
  
```csharp  
try  
{  
   // Code for accessing the report server  
}  
catch (SoapException ex)  
{  
   // The exception is a SOAP exception, so use  
   // the Detail property's Message element.  
   Console.WriteLine(ex.Detail["Message"].InnerXml);  
}  
```  
  
```vb  
Try  
' Code for accessing the report server  
Catch ex As SoapException  
   If ex.Detail("ErrorCode").InnerXml = "rsInvalidItemName" Then  
   End If ' Perform an action based on the specific error code  
End Try  
```  
  
```csharp  
try  
{  
   // Code for accessing the report server  
}  
catch (SoapException ex)  
{  
   if (ex.Detail["ErrorCode"].InnerXml == "rsInvalidItemName")  
   {  
      // Perform an action based on the specific error code  
   }  
}  
```  
  
 Tramite la riga di codice seguente viene scritto il codice di errore specifico restituito nell'eccezione SOAP alla console. È anche possibile valutare il codice di errore ed eseguire azioni specifiche.  
  
```vb  
Console.WriteLine(ex.Detail("ErrorCode").InnerXml)  
```  
  
```csharp  
Console.WriteLine(ex.Detail["ErrorCode"].InnerXml);  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Introduzione alla gestione delle eccezioni in Reporting Services](../introducing-exception-handling-in-reporting-services.md)   
 [Classe SoapException di Reporting Services](../soapexception-class/reporting-services-soapexception-class.md)   
 [Tabella degli errori SoapException](../soapexception-class/soapexception-errors-table.md)  
  
  
