---
title: MSSQLSERVER_3181 | Microsoft Docs
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
- 3181 (Database Engine error)
ms.assetid: e6d2e716-5263-477c-ad0e-7bcbfef4c1f3
caps.latest.revision: 13
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 745311b0a43b588bc1aead412a0c47c9ba943bb3
ms.lasthandoff: 04/11/2017

---
# <a name="mssqlserver3181"></a>MSSQLSERVER_3181
  
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|ID evento|3181|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|LDDB_STORAGE_VERIFY|  
|Testo del messaggio|Durante il tentativo di ripristinare questo backup potrebbero verificarsi problemi relativi allo spazio di archiviazione. Ulteriori informazioni verranno fornite nei successivi messaggi.|  
  
## <a name="explanation"></a>Spiegazione  
Con l'istruzione RESTORE VERIFYONLY viene controllato lo spazio di archiviazione disponibile sul disco in cui il database deve essere ripristinato.  
  
### <a name="possible-causes"></a>Possibili cause  
È possibile che lo spazio disponibile su disco sia insufficiente per il ripristino del backup verificato.  
  
## <a name="user-action"></a>Azione dell'utente  
Ripristinare il backup in una posizione con spazio su disco sufficiente oppure aumentare lo spazio sul disco.  
  
## <a name="see-also"></a>Vedere anche  
[Ripristinare un database in una nuova posizione &#40;SQL Server&#41;](~/relational-databases/backup-restore/restore-a-database-to-a-new-location-sql-server.md)  
[Ripristinare i file in una nuova posizione &#40;SQL Server&#41;](~/relational-databases/backup-restore/restore-files-to-a-new-location-sql-server.md)  
[RESTORE &#40;Transact-SQL&#41;](~/t-sql/statements/restore-statements-transact-sql.md)  
[RESTORE VERIFYONLY &#40;Transact-SQL&#41;](~/t-sql/statements/restore-statements-verifyonly-transact-sql.md)  
  
