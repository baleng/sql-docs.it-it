---
title: Posizionare dati e file di log in unità distinte | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 6cbedc27-4d77-44ad-bed2-c23b628475a7
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: b7f44018f5a027e429029b86a2532d60b27d6540
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/02/2018
ms.locfileid: "48085281"
---
# <a name="place-data-and-log-files-on-separate-drives"></a>Posizionamento di dati e file di log in unità distinte
  Questa regola consente di controllare se i dati e i file di log si trovano in unità logiche distinte. Il posizionamento dei dati e dei file di log nello stesso dispositivo può provocare contesa nel dispositivo stesso e comportare prestazioni insufficienti. Il posizionamento dei file in unità distinte fa sì che l'attività di I/O si verifichi contemporaneamente sia per i dati sia per i file di log.  
  
## <a name="best-practices-recommendations"></a>Procedure consigliate  
 Quando si crea un nuovo database, specificare unità distinte per i dati e per il log. Per spostare i file una volta creato il database, è necessario che il database sia offline. Per spostare i file, utilizzare uno dei metodi seguenti:  
  
> [!NOTE]  
>  Questi criteri non sono in grado di rilevare dispositivi fisici separati mediante punti di montaggio  
  
-   Ripristinare il database dal backup utilizzando l'istruzione RESTORE DATABASE con l'opzione WITH MOVE.  
  
-   Scollegare e quindi ricollegare il database specificando posizioni distinte per i dispositivi dei dati e dei log.  
  
-   Specificare una nuova posizione eseguendo l'istruzione ALTER DATABASE con l'opzione MODIFY FILE, riavviando quindi l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="for-more-information"></a>Ulteriori informazioni  
 [Spostare file del database](../databases/move-database-files.md)  
  
 [Spostare database utente](../databases/move-user-databases.md)  
  
 [Collegamento e scollegamento di un database &#40;SQL Server&#41;](../databases/database-detach-and-attach-sql-server.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Monitorare e applicare le procedure consigliate tramite la gestione basata su criteri](monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
