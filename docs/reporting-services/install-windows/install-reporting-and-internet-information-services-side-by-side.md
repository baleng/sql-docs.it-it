---
title: Installazione di Reporting e Internet Information Services Side-by-Side | Documenti Microsoft
ms.custom: 
ms.date: 05/30/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- deploying [Reporting Services], IIS
ms.assetid: 9b651fa5-f582-4f18-a77d-0dde95d9d211
caps.latest.revision: 40
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 1818a4b076dd6e1c81c0a9b39b781516bdf718e0
ms.contentlocale: it-it
ms.lasthandoff: 06/13/2017

---

# <a name="install-reporting-and-internet-information-services-side-by-side"></a>Installazione di Reporting e Internet Information Services Side-by-Side

[!INCLUDE[ssrs-appliesto-sql2016-preview](../../includes/ssrs-appliesto-sql2016-preview.md)]

  È possibile installare ed eseguire SQL Server Reporting Services (SSRS) e Internet Information Services (IIS) nello stesso computer. La versione di IIS utilizzata determina i problemi di interoperabilità che è necessario risolvere.  
  
|Versione di IIS|Problemi|Descrizione|  
|-----------------|------------|-----------------|  
|8.0, 8.5|Richieste destinate a un'applicazione vengono accettate da un'applicazione diversa.<br /><br /> HTTP.SYS applica regole di precedenza per le prenotazioni URL. Le richieste inviate ad applicazioni con lo stesso nome di directory virtuale e che eseguono congiuntamente il monitoraggio della porta 80 potrebbero non raggiungere la destinazione desiderata se la prenotazione URL è debole rispetto alla prenotazione URL di un'altra applicazione.|In determinate condizioni, un endpoint registrato che prevale su un altro endpoint URL nello schema di prenotazione degli URL potrebbe ricevere richieste HTTP destinate all'altra applicazione.<br /><br /> L'uso di nomi univoci per le directory virtuali per il servizio Web ReportServer e [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)] consente di evitare questo conflitto.<br /><br /> Informazioni dettagliate su questo scenario vengono fornite nel presente argomento.|  
  
## <a name="precedence-rules-for-url-reservations"></a>Regole di precedenza per le prenotazioni URL  
 Prima di poter passare alla risoluzione dei problemi di interoperabilità tra IIS e [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], è necessario comprendere le regole di precedenza relative alle prenotazioni di URL. Le regole di precedenza possono essere generalizzate nell'affermazione in base alla quale una prenotazione URL che ha valori definiti in modo più esplicito ha la precedenza nella ricezione di richieste che corrispondono all'URL.  
  
-   Una prenotazione URL che specifica una directory virtuale è più esplicita di una prenotazione che la omette.  
  
-   Una prenotazione URL che specifica un solo indirizzo (come indirizzo IP, nome di dominio completo, nome di un computer di rete o nome host) è più esplicita rispetto a un carattere jolly.  
  
-   Una prenotazione URL che specifica un carattere jolly complesso è più esplicita rispetto a una prenotazione che utilizza un carattere jolly vulnerabile.  
  
 Negli esempi seguenti è mostrato un intervallo di prenotazioni URL, ordinate dalle più esplicite a quelle meno esplicite:  
  
|Esempio|Richiesta|  
|-------------|-------------|  
|`http://123.234.345.456:80/reports`|Riceve tutte le richieste inviate al `http://123.234.345.456/reports` o `http://\<computername>/reports` se il servizio DNS può risolvere l'indirizzo IP in tale nome host.|  
|`http://+:80/reports`|Riceve tutte le richieste inviate a qualsiasi indirizzo IP o nome host valido per tale computer finché l'URL contiene il nome della directory virtuale "reports".|  
|`http://123.234.345.456:80`|Riceve qualsiasi richiesta che specifica `http://123.234.345.456` o `http://\<computername>` se il servizio DNS può risolvere l'indirizzo IP in tale nome host.|  
|`http://+:80`|Riceve le richieste che non sono già state ricevute da altre applicazioni, per qualsiasi endpoint dell'applicazione di cui è stato eseguito il mapping all'opzione **Tutti assegnati**.|  
|`http://*:80`|Riceve le richieste che non sono già state ricevute da altre applicazioni, per gli endpoint dell'applicazione di cui è stato eseguito il mapping all'opzione **Non assegnati**.|  
  
 Un'indicazione di un conflitto di porte è la visualizzazione del messaggio di errore seguente: "System.IO.FileLoadException: Il processo non può accedere al file perché è in uso da un altro processo. (Eccezione da HRESULT: 0x80070020)".  
  
## <a name="url-reservations-for-iis-80-85-with-sql-server-reporting-services"></a>Prenotazioni URL per IIS 8.0, 8.5 con SQL Server Reporting Services  
 Stabilite le regole di precedenza descritte nella sezione precedente, è possibile iniziare a comprendere in che modo le prenotazioni URL definite per Reporting Services e IIS agevolino l'interoperabilità. Reporting Services riceve le richieste che specificano in modo esplicito i nomi delle directory virtuali per le proprie applicazioni, mentre IIS riceve tutte le richieste rimanenti che possono pertanto essere dirette ad applicazioni eseguite all'interno del modello di processo di IIS.  
  
|Applicazione|Prenotazione URL|Descrizione|Ricezione richiesta|  
|-----------------|---------------------|-----------------|---------------------|  
|Server di report|`http://+:80/ReportServer`|Carattere jolly complesso sulla porta 80, con directory virtuale del server di report.|Riceve sulla porta 80 tutte le richieste che specificano la directory virtuale del server di report. Il servizio Web ReportServer riceve tutte le richieste a http://\<computername > / reportserver.|  
|Portale Web|`http://+:80/Reports`|Carattere jolly complesso sulla porta 80, con directory virtuale Reports.|Riceve sulla porta 80 tutte le richieste che specificano la directory virtuale reports. Il [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)] riceve tutte le richieste a http://\<computername > / reports.|  
|IIS|`http://*:80/`|Carattere jolly vulnerabile sulla porta 80.|Riceve sulla porta 80 tutte le richieste rimanenti che non vengono ricevute da un'altra applicazione.|  

## <a name="side-by-side-deployments-of-sql-server-reporting-services-on-iis-80-85"></a>Distribuzioni side-by-Side di SQL Server Reporting Services in IIS 8.0, 8.5

 I problemi di interoperabilità tra IIS e Reporting Services si verificano quando i nomi delle directory virtuali dei siti Web di IIS sono identici a quelli utilizzati da Reporting Services. Si supponga ad esempio di disporre della configurazione seguente:  
  
-   Un sito Web in IIS assegnato alla porta 80 e una directory virtuale denominata "Reports".  
  
-   Un'istanza del server di report installata nella configurazione predefinita, in cui anche la prenotazione URL specifica la porta 80 e [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)] applicazione usa "Reports" come nome della directory virtuale.  
  
 Questa configurazione, di una richiesta inviata a http://\<nomecomputer >: 80/reports viene ricevuta dal [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)]. L'applicazione cui si accede tramite la directory virtuale Reports in IIS non riceverà più richieste dopo aver installato l'istanza del server di report.  
  
 Se si eseguono distribuzioni side-by-side di versioni meno recenti e più recenti di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], è possibile che si verifichi il problema di routing descritto in precedenza, perché tutte le versioni di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] usano "ReportServer" e "Reports" come nomi delle directory virtuali per il server di report e le applicazioni di [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)] , aumentando la probabilità di rilevare directory virtuali denominate "reports" e "reportserver" in IIS.  
  
 Per garantire che tutte le applicazioni ricevano richieste, adottare le linee guida seguenti:  
  
-   Per le installazioni di Reporting Services, utilizzare nomi delle directory virtuali che non siano già utilizzati da un sito Web di IIS sulla stessa porta di Reporting Services. Se si verifica un conflitto, installare Reporting Services in modalità "solo file", utilizzando l'opzione Installa senza configurare l'opzione server dell'Installazione guidata, in modo che sia possibile configurare le directory virtuali al termine dell'installazione. Un'indicazione della configurazione come conflitto è la visualizzazione del messaggio di errore seguente: System.IO.FileLoadException: Il processo non può accedere al file perché è in uso da un altro processo. (Eccezione da HRESULT: 0x80070020).  
  
-   Per installazioni da configurare manualmente, adottare le convenzioni di denominazione predefinite negli URL configurati. Se si installa [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] come istanza denominata, includere il nome dell'istanza al momento della creazione di una directory virtuale.  

## <a name="next-steps"></a>Passaggi successivi

[Configurare gli URL di Server di Report](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)   
[Configurare un URL](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)   
[Installare Server di Report di Reporting Services in modalità nativa](../../reporting-services/install-windows/install-reporting-services-native-mode-report-server.md)  

Ulteriori domande? [Provare a porre il forum di Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231)