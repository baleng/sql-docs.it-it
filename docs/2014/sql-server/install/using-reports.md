---
title: Uso dei report | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- displaying reports
- overriding reports
- Upgrade Advisor Report Viewer
- reports [Upgrade Advisor], about reports
- formatting reports
- resolved issues [Upgrade Advisor]
- distributing reports [Reporting Services]
- filtering reports [Reporting Services]
- removing report items
- viewing reports
- rerunning analysis
- information issues [Upgrade Advisor]
- deleting report items
- icons [Upgrade Advisor]
- Upgrade Advisor [SQL Server], reports
- sending reports
- blocking issues [Upgrade Advisor]
- sharing reports
- reports [Upgrade Advisor]
- SQL Server Upgrade Advisor, reports
- modifying reports
- distributing reports [Reporting Services], about report distribution
- warnings [Upgrade Advisor]
- analyzing system [Upgrade Advisor], reports
ms.assetid: 4a3cb94a-a7ac-4cec-94c7-db26fcf6d161
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0d8ec04baf292807120ed5a26360878ac7e20442
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/02/2018
ms.locfileid: "48070901"
---
# <a name="using-reports"></a>Utilizzo dei report
  Per ogni componente e, se necessario, per ogni istanza analizzata tramite l'Analisi guidata di Preparazione aggiornamento su un server viene generato un report distinto, in cui sono forniti dettagli su problemi noti che influiscono su un aggiornamento. Il report contiene inoltre collegamenti a informazioni e ad azioni consigliate per la risoluzione dei problemi identificati.  
  
> [!NOTE]  
>  Se il Visualizzatore di Report di preparazione aggiornamento non trova alcun report nella directory dei report predefiniti, è possibile caricare un report da una directory diversa utilizzando il **Apri Report** collegamento.  
  
## <a name="viewing-reports"></a>Visualizzazione dei report  
 Utilizzare il Visualizzatore report di Preparazione aggiornamento per visualizzare i report di Preparazione aggiornamento. Per visualizzare i report, nella pagina iniziale di preparazione aggiornamento, fare clic su **avviare Visualizzatore Report Preparazione aggiornamento**.  
  
 Dopo avere caricato un report per un server, è possibile selezionare un componente per cui visualizzare i problemi di aggiornamento. È possibile applicare un filtro dal **Filtra per** casella per visualizzare quanto segue:  
  
-   Tutti i problemi  
  
-   Tutti i problemi di aggiornamento  
  
-   Problemi di pre-aggiornamento  
  
-   Tutti i problemi di migrazione  
  
-   Problemi risolti  
  
-   Problemi irrisolti  
  
 Se il report contiene più di 20 problemi, è possibile spostare al gruppo successivo o precedente di problemi facendo **prossimi 20** oppure **precedenti 20** nella parte superiore o inferiore dell'elenco di problemi.  
  
 È possibile visualizzare fino a cinque report salvati, selezionare il report dal **Report** casella di riepilogo a discesa. I report vengono elencati in base al valore timestamp che indica la data e l'ora in cui sono stati generati.  
  
## <a name="report-format"></a>Formato dei report  
 Il visualizzatore di report suddivide i problemi in tre colonne. Ogni problema è comprimibile, in modo che sia possibile nascondere la descrizione e visualizzare solo le informazioni essenziali.  
  
 La prima colonna è il **importanza** colonna. Le icone indicano l'importanza di ogni problema: viene visualizzato un cerchio rosso con una X per problemi importanti o che bloccano l'aggiornamento oppure un triangolo giallo con un punto esclamativo per problemi paragonabili a messaggi di avviso o informativi. La seconda colonna, **quando correggere**, indica quando è necessario risolvere il problema. È possibile ordinare il report nel **importanza** oppure **quando correggere** colonna. La terza colonna, **descrizione**, sono elencati i titoli del problema.  
  
 È possibile espandere un problema per visualizzare informazioni aggiuntive, un collegamento a informazioni dettagliate sulla risoluzione e un collegamento per visualizzare i dettagli del problema. Quando si fa clic sul collegamento per ottenere informazioni dettagliate per il problema, verrà visualizzato un argomento della Guida con informazioni e istruzioni per risolverlo. Dopo aver risolto un problema o per gestire gli elementi delle azioni, è possibile contrassegnare i problemi come completati selezionando la **questo problema è stato risolto** casella di controllo. Se si desidera rimuovere i problemi risolti dall'elenco dei problemi di aggiornamento, fare clic su **Aggiorna**. Il problema non viene visualizzato nuovamente fino a quando non si esegue l'analisi guidata Preparazione aggiornamento sullo stesso componente o si applicano i **problemi risolti** filtrare dal **Filter By** opzione.  
  
## <a name="report-files"></a>File di report  
 L'analisi guidata Preparazione aggiornamento Crea report nella cartella documenti\\ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] directory eseguire l'aggiornamento Advisor\110\Reports e crea una sottodirectory per ogni server analizzato. I file di report sono in formato XML e seguono una convenzione di denominazione specifica. Quando si avvia il Visualizzatore report di Preparazione aggiornamento, vengono visualizzati i file di report della directory predefinita. Se vengono copiati file di report in questa cartella, è necessario che rispettino la convenzione di denominazione, altrimenti non verranno visualizzati automaticamente.  
  
 Se si desidera condividere le informazioni con altri utenti, è possibile inviare il report XML. In alternativa, se si desidera utilizzare un'altra applicazione, è possibile esportare il report in un file con valori delimitati da virgole da utilizzare per creare un foglio di calcolo, un file di testo o un messaggio di posta elettronica.  
  
## <a name="see-also"></a>Vedere anche  
 [Procedura: visualizzare un Report di preparazione aggiornamento](../../../2014/sql-server/install/how-to-view-an-upgrade-advisor-report.md)   
 [Procedura: esportare i report](../../../2014/sql-server/install/how-to-export-reports.md)   
 [Procedura: filtrare i report](../../../2014/sql-server/install/how-to-filter-reports.md)   
 [Risoluzione dei problemi di aggiornamento](../../../2014/sql-server/install/resolving-upgrade-issues.md)   
 [Preparazione aggiornamento a SQL Server 2014 &#91;new&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
