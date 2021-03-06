---
title: Riferimenti ad altri assembly nelle soluzioni di scripting | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- docset-sql-devref
- integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- SSIS Script task, .NET Framework
- Script task [Integration Services], adding references
- referencing custom assemblies
- SSIS Script task, VisualBasic namespace
- assemblies [Integration Services]
- VisualBasic namespace
- Script task [Integration Services], VisualBasic namespace
- Microsoft.VisualBasic namespace
- Script task [Integration Services], .NET Framework
- .NET Framework [Integration Services]
- referencing Web services
ms.assetid: 9b655bcd-19f6-43d8-9f89-1b4d299c6380
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a3b8f04d0df0a56a597c13bc4559c520b820d8de
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/02/2018
ms.locfileid: "48050085"
---
# <a name="referencing-other-assemblies-in-scripting-solutions"></a>Riferimenti ad altri assembly nelle soluzioni di scripting
  La libreria di classi [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] fornisce allo sviluppatore di script un potente set di strumenti per l'implementazione di funzionalità personalizzate nei pacchetti di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. L'attività Script e il componente script possono anche utilizzare assembly gestiti personalizzati.  
  
> [!NOTE]  
>  Per consentire ai pacchetti di usare gli oggetti e i metodi di un servizio Web, usare il comando **Aggiungi riferimento Web** disponibile in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA). Nelle versioni precedenti di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] è necessario generare una classe proxy per utilizzare un servizio Web.  
  
## <a name="using-a-managed-assembly"></a>Utilizzo di un assembly gestito  
 Affinché [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] trovi un assembly gestito in fase di progettazione, è necessario effettuare i passaggi seguenti:  
  
1.  Archiviare l'assembly gestito in qualsiasi cartella del computer.  
  
    > [!NOTE]  
    >  Nelle versioni precedenti di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] è possibile aggiungere solo un riferimento a un assembly gestito archiviato nella cartella %windir%\Microsoft.NET\Framework\vx.x.xxxxx o nella cartella %Programmi%\Microsoft SQL Server\100\SDK\Assemblies.  
  
2.  Aggiungere un riferimento all'assembly gestito.  
  
     Per aggiungere il riferimento, nella scheda **Sfoglia** della finestra di dialogo **Aggiungi riferimento** in VSTA individuare e aggiungere l'assembly gestito.  
  
 Affinché [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] trovi l'assembly gestito in fase di esecuzione, è necessario effettuare i passaggi seguenti:  
  
1.  Firmare l'assembly gestito con un nome sicuro.  
  
2.  Installare l'assembly nella Global Assembly Cache nel computer in cui viene eseguito il pacchetto.  
  
     Per altre informazioni, vedere [Compilazione, distribuzione e debug di oggetti personalizzati](../extending-packages-custom-objects/building-deploying-and-debugging-custom-objects.md).  
  
## <a name="using-the-microsoft-net-framework-class-library"></a>Utilizzo della libreria di classi Microsoft .NET Framework  
 L'attività Script e il componente script possono trarre vantaggio da tutti gli altri oggetti e funzionalità esposti dalla libreria di classi [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]. Ad esempio, tramite [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] è possibile recuperare informazioni sull'ambiente e interagire con il computer in cui viene eseguito il pacchetto.  
  
 In questo elenco vengono descritte alcune delle classi [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] utilizzate più di frequente:  
  
-   `System.Data` Contiene l'architettura ADO.NET.  
  
-   `System.IO` Fornisce un'interfaccia per il file system e i flussi.  
  
-   `System.Windows.Forms` Fornisce la creazione di form.  
  
-   `System.Text.RegularExpressions` Fornisce classi per l'utilizzo di espressioni regolari.  
  
-   `System.Environment` Restituisce informazioni sul computer locale, l'utente corrente e le impostazioni utente e computer.  
  
-   `System.Net` Fornisce comunicazioni di rete.  
  
-   `System.DirectoryServices` Espone Active Directory.  
  
-   `System.Drawing` Fornisce librerie complete immagini manipolazione.  
  
-   `System.Threading` Consente la programmazione multithreading.  
  
 Per ulteriori informazioni su [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], consultare MSDN Library.  
  
![Icona di Integration Services (piccola)](../media/dts-16.gif "icona di Integration Services (piccola)")**rimangono fino a Date con Integration Services** <br /> Per i download, gli articoli, gli esempi e i video Microsoft più recenti, oltre alle soluzioni selezionate dalla community, visitare la pagina [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] sul sito MSDN:<br /><br /> [Visita la pagina di Integration Services su MSDN](http://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Per ricevere una notifica automatica su questi aggiornamenti, sottoscrivere i feed RSS disponibili nella pagina.  
  
## <a name="see-also"></a>Vedere anche  
 [Estensione di pacchetti tramite scripting](extending-packages-with-scripting.md)  
  
  
