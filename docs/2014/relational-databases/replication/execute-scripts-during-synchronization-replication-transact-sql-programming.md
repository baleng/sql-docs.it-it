---
title: Eseguire script durante la sincronizzazione (programmazione Transact-SQL della replica) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- synchronization [SQL Server replication], scripts
- scripts [SQL Server replication], synchronization and
- sp_addscriptexec
ms.assetid: b58a0877-4e43-4fab-a281-24e6022d3fb1
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c60c75366d13fc73963c916d588010cc738858a9
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/02/2018
ms.locfileid: "48172041"
---
# <a name="execute-scripts-during-synchronization-replication-transact-sql-programming"></a>Esecuzione di script durante la sincronizzazione (programmazione Transact-SQL della replica)
  La replica supporta l'esecuzione di script su richiesta per i Sottoscrittori di pubblicazioni transazionali e di tipo merge. Con questa funzionalità lo script viene copiato nella directory di lavoro della replica e quindi viene applicato al Sottoscrittore tramite **sqlcmd** . Per impostazione predefinita, se si verifica un errore durante l'applicazione dello script per una sottoscrizione di una pubblicazione transazionale, l'agente di distribuzione verrà arrestato. È possibile specificare uno script [!INCLUDE[tsql](../../includes/tsql-md.md)] da eseguire a livello di programmazione tramite le stored procedure di replica.  
  
### <a name="to-specify-a-script-to-run-for-all-subscribers-to-a-snapshot-transactional-or-merge-publication"></a>Per specificare uno script da eseguire per tutti i Sottoscrittori di una pubblicazione snapshot, transazionale o di tipo merge  
  
1.  Comporre e testare lo script [!INCLUDE[tsql](../../includes/tsql-md.md)] che verrà eseguito su richiesta.  
  
2.  Salvare il file script in un percorso in cui sia accessibile all'agente snapshot per la pubblicazione.  
  
3.  Nel database di pubblicazione del server di pubblicazione eseguire [sp_addscriptexec &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addscriptexec-transact-sql). Specificare **@publication**, il nome del file script con il percorso UNC completo creato nel passaggio 2 per **@scriptfile**e uno dei valori seguenti per **@skiperror**:  
  
    -   **0** : l'agente arresterà l'esecuzione dello script se viene rilevato un errore.  
  
    -   **1** : l'agente registrerà gli errori e continuerà l'esecuzione dello script quando vengono rilevati errori.  
  
4.  Lo script specificato verrà eseguito in ogni Sottoscrittore la volta successiva che l'agente verrà eseguito per sincronizzare la sottoscrizione.  
  
## <a name="see-also"></a>Vedere anche  
 [Sincronizzare i dati](synchronize-data.md)  
  
  
