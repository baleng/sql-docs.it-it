---
title: MSSQLSERVER_32043 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 32043 (Database Engine error)
ms.assetid: a0c48ae3-4c8c-419c-afb5-579fcefac01d
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b8892eb88a943176a5d99bdada398d004e983658
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/02/2018
ms.locfileid: "48098741"
---
# <a name="mssqlserver32043"></a>MSSQLSERVER_32043
    
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|32043|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|SQLErrorNum32043|  
|Testo del messaggio|Generato avviso relativo a un log non ripristinato. Il valore corrente di '%d' è maggiore della soglia '%d'.|  
  
## <a name="explanation"></a>Spiegazione  
 Questo evento di mirroring del database viene generato nell'istanza del server mirror per indicare che la quantità di log non ripristinato ha raggiunto un valore soglia specificato dall'utente. In genere questo evento viene generato a causa di un cambiamento delle prestazioni del sistema. La larghezza di banda disponibile tra i due sistemi è diminuita o il carico è aumentato.  
  
 Per log non ripristinato si intende un log ricevuto dall'istanza del server mirror e scritto su disco ma in attesa di essere ripristinato nel database mirror. La quantità di log non ripristinato espressa in KB corrisponde a una misurazione delle prestazioni che consente di valutare il tempo di failover corrente. Il tempo necessario per l'applicazione del log non ripristinato rappresenta il fattore principale del tempo di failover, unitamente all'ulteriore tempo necessario per recuperare il database e portarlo online.  
  
> [!NOTE]  
>  Per un failover automatico, il tempo necessario al sistema per rilevare l'errore è indipendente dal tempo di failover.  
  
## <a name="user-action"></a>Azione dell'utente  
 Controllare il carico delle istanze del server principale e del server mirror e la connessione di rete tra i sistemi per determinare la causa del problema.  
  
## <a name="see-also"></a>Vedere anche  
 [Mirroring del database &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)   
 [Usare valori di soglia avvisi e avvisi sulle metriche delle prestazioni di mirroring &#40;SQL Server&#41;](../../database-engine/database-mirroring/use-warning-thresholds-and-alerts-on-mirroring-performance-metrics-sql-server.md)  
  
  
