---
title: MSSQLSERVER_825 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 825 (Database Engine error)
ms.assetid: f69f8214-5af1-4769-878b-117ad6eaff52
caps.latest.revision: 16
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 6cf3cceebd5555e91d3753e385d28164680241f5
ms.lasthandoff: 04/11/2017

---
# <a name="mssqlserver825"></a>MSSQLSERVER_825
  
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|825|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|B_RETRYWORKED|  
|Testo del messaggio|Operazione di lettura del file '%ls', offset %#016I64x, riuscita dopo %d tentativo/i con errore: %ls. Per informazioni più dettagliate, vedere i messaggi aggiuntivi nel log degli errori di SQL Server e nel registro eventi di sistema. Questa condizione di errore può costituire un rischio per l'integrità del database e deve essere risolta. Eseguire un controllo di consistenza completo del database (DBCC CHECKDB). L'errore può essere causato da molti fattori. Per ulteriori informazioni, vedere la documentazione online di SQL Server.|  
  
## <a name="explanation"></a>Spiegazione  
Questo messaggio segnala che è stato necessario eseguire nuovamente l'operazione di lettura almeno una volta e indica un problema grave relativo ai componenti hardware del disco. Non indica attualmente un problema relativo a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], tuttavia, se irrisolto, il problema relativo al disco potrebbe causare perdite di dati o il danneggiamento del database. Il log degli eventi di sistema potrebbe includere eventi correlati che consentono di diagnosticare il problema. Per altre informazioni sugli errori di I/O, vedere il capitolo 2 della pagina relativa alle [nozioni fondamentali sull'I/O in Microsoft SQL Server](http://go.microsoft.com/fwlink/?LinkId=69370).  
  
## <a name="user-action"></a>Azione dell'utente  
Le azioni seguenti possono contribuire a identificare e risolvere il problema sottostante:  
  
-   Esaminare il log degli errori e il testo delle variabili di questo messaggio per individuare eventuali indizi che consentano di spiegare il problema.  
  
-   Controllare il sistema di dischi. Il problema potrebbe essere correlato ai dischi, ai controller dei dischi, alle schede di array o ai driver dei dischi.  
  
-   Contattare il produttore dei dischi e richiedere le utilità più recenti per verificare lo stato del sistema di dischi.  
  
-   Contattare il produttore dei dischi e richiedere gli ultimi aggiornamenti dei driver.  
  
