---
title: Creare relazioni tra tabelle in un diagramma (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- diagrams [SQL Server], designing
ms.assetid: 28e9630c-dff4-46cc-bb0e-fe77998b6ac2
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1cb069a1e28a10036ebea2738f5eea81a9f8932c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/02/2018
ms.locfileid: "48128639"
---
# <a name="create-relationships-between-tables-on-a-diagram-visual-database-tools"></a>Creazione di relazioni tra tabelle in un diagramma (Visual Database Tools)
  È possibile creare relazioni tra le colonne in diverse tabelle in Progettazione diagrammi di database trascinando le colonne all'interno delle tabelle.  
  
### <a name="to-create-a-relationship-graphically"></a>Per creare una relazione graficamente  
  
1.  In Progettazione database fare clic sul selettore delle righe per una o più colonne di database che si desidera correlare a una colonna in un'altra tabella.  
  
2.  Trascinare la colonna o le colonne selezionate nella tabella correlata.  
  
3.  Verranno visualizzate due finestre di dialogo: **Relazione chiavi esterne** e **Tabelle e colonne**, quest'ultima visualizzata in primo piano.  
  
4.  Il**Nome relazione** è assegnato dal sistema nel formato FK_*localtable*_*foreigntable*. È possibile modificare questo valore.  
  
5.  Verificare che in **Tabella di chiave primaria** sia specificata la tabella corretta.  
  
6.  Nella griglia sono indicate le colonne locali e le colonne esterne corrispondenti. È possibile aggiungere o rimuovere le colonne di tabella o modificare i mapping.  
  
7.  Scegliere **OK**.  
  
     Verrà visualizzata la finestra di dialogo **Relazione chiavi esterne** . **Relazione selezionata** visualizza la relazione creata.  
  
8.  Modificare le proprietà della relazione nella griglia.  
  
9. Scegliere **OK** per creare la relazione.  
  
     Progettazione database mostra una relazione tra le colonne selezionate.  
  
## <a name="see-also"></a>Vedere anche  
 [Le tabelle e colonne, finestra di dialogo &#40;Visual Database Tools&#41;](visual-database-tools.md)   
 [I vincoli UNIQUE e Check](../../relational-databases/tables/unique-constraints-and-check-constraints.md)   
 [Utilizzo di tabelle in diagrammi di database &#40;Visual Database Tools&#41;](work-with-tables-in-database-diagram-visual-database-tools.md)  
  
  
