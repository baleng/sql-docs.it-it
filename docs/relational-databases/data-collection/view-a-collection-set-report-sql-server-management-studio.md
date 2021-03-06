---
title: Visualizzare un report sui set di raccolta (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- sql13.swb.dc.reporthistory.calendar.f1
helpviewer_keywords:
- collection sets [SQL Server], viewing reports
- reports [SQL Server], viewing collection set
ms.assetid: c3b1e791-9aa1-4bba-9622-4954568e1820
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9c6dd8a715e9f6f009335fe54bc591262c6479fd
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/01/2018
ms.locfileid: "47606529"
---
# <a name="view-a-collection-set-report-sql-server-management-studio"></a>Visualizzare un report sui set di raccolta (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Dopo avere configurato il data warehouse di gestione, è possibile visualizzare un report del set di raccolta in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. I report vengono forniti per i set di raccolta dati di sistema installati durante l'installazione Sono disponibili i report seguenti:  
  
-   Riepilogo utilizzo disco  
  
-   Cronologia statistiche query  
  
-   Cronologia attività server  
  
 Tramite questa procedura viene visualizzato il report per il set di raccolta **Utilizzo disco** . È possibile seguire la stessa procedura generale per visualizzare i report per gli altri set di raccolta dati di sistema.  
  
### <a name="to-view-a-collection-set-report"></a>Per visualizzare un report di un set di raccolta  
  
1.  Le tabelle necessarie per un report vengono create solo la prima volta che i dati raccolti vengono caricati. Se si tenta di visualizzare un report prima che venga effettuato il primo caricamento, si verifica un errore e non viene visualizzato alcun report. Per caricare dati per il set di raccolta Utilizzo disco, in Esplora oggetti espandere la cartella **Gestione** , espandere **Raccolta dati**e **Set di raccolta dati di sistema**, fare clic con il pulsante destro del mouse sul set di raccolta **Utilizzo disco** e quindi scegliere **Raccogli e carica**.  
  
2.  Per visualizzare il report, in Esplora oggetti espandere la cartella **Gestione** , fare clic con il pulsante destro del mouse su **Raccolta dati**, scegliere **Report**, **Data warehouse di gestione**e quindi fare clic su **Riepilogo utilizzo disco**.  
  
    > [!NOTE]  
    >  Alcuni report potrebbero mostrare un pulsante calendario sotto la cronologia della raccolta dati. Fare clic su questo pulsante per accedere al **Calendario report di raccolta dati**.  
  
#### <a name="data-collection-report-calendar"></a>Calendario report di raccolta dati  
 Utilizzare questa finestra di dialogo per specificare la data e l'ora di inizio e la durata relative ai dati per cui si desidera creare il report. Potrebbe essere necessario ad esempio creare un report relativo all'utilizzo del disco di un server per un periodo specifico di 12 ore mercoledì scorso.  
  
 **Data inizio**  
 Immettere una data iniziale per i dati del report o selezionarne una dal calendario.  
  
 **Ora inizio**  
 Immettere un'ora iniziale per i dati del report o fare clic sulle frecce per specificarne una.  
  
 **Durata**  
 Specificare l'intervallo di tempo da includere nel report. Il valore predefinito è 240 minuti. I valori che è possibile selezionare sono 15 minuti, 60 minuti, 240 minuti (4 ore), 720 minuti (12 ore) e 1440 minuti (24 ore).  
  
## <a name="see-also"></a>Vedere anche  
 [Raccolta dati](../../relational-databases/data-collection/data-collection.md)   
 [Report personalizzati in Management Studio](../../ssms/object/custom-reports-in-management-studio.md)   
 [Configurare il data warehouse di gestione &#40;SQL Server Management Studio&#41;](../../relational-databases/data-collection/configure-the-management-data-warehouse-sql-server-management-studio.md)  
  
  
