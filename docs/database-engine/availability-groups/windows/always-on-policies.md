---
title: Criteri dei gruppi di disponibilità Always On (SQL Server) | Microsoft Docs
ms.custom: ag-guide
ms.date: 06/13/2017
ms.prod: sql-server-2016
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 26bf8f71-c2b8-45ef-b3a3-372b96c9e6e3
caps.latest.revision: 7
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: d7cd99126a198826749466e04dfabf332628c7d4
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/16/2018
---
# <a name="always-on-availability-groups-policies"></a>Criteri dei gruppi di disponibilità Always On
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  I criteri di sistema dei gruppi di disponibilità Always On sono utilizzati dal dashboard Always On per comunicare all'utente informazioni sullo stato di integrità dei gruppi di disponibilità. Sono molto utili per le attività iniziali di risoluzione dei problemi operativi con un gruppo di disponibilità. Questi criteri possono essere estesi e utilizzati per personalizzare il dashboard Always On o eseguiti immediatamente per segnalare le informazioni di integrità desiderate.  
  
 Esistono 14 criteri di sistema per i gruppi di disponibilità. Per informazioni dettagliate su ogni criterio, vedere [Criteri Always On per problemi operativi con gruppi di disponibilità Always On (SQL Server)](always-on-policies-for-operational-issues-always-on-availability.md).  
  
## <a name="view-or-evaluate-availability-groups-system-policies"></a>Visualizzare o valutare i criteri di sistema dei gruppi di disponibilità  
 Per visualizzare o eseguire i criteri di sistema dei gruppi di disponibilità in SQL Server Management Studio (SSMS), eseguire le operazioni seguenti:  
  
1.  In **Esplora oggetti** espandere **Gestione**, **Gestione criteri**, **Criteri** e quindi **Criteri di sistema**.  
  
2.  Fare clic con il pulsante destro su uno dei criteri e fare clic su **Valuta**. Se l'intenzione era valutare il criterio selezionato, l'operazione è conclusa. Fare clic su **Visualizza** nella casella **Dettagli destinazione** per visualizzare i dettagli dei risultati della valutazione.  
  
3.  Per visualizzare tutti i criteri di sistema dei gruppi di disponibilità, fare clic su **Selezione** nel riquadro **Seleziona una pagina**.  
  
## <a name="next-steps"></a>Passaggi successivi  
 [The Always On health model, part 2: Extending the health model (Modello di integrità Always On, parte 2: Estensione del modello di integrità)](http://blogs.msdn.com/b/sqlalwayson/archive/2012/02/13/extending-the-alwayson-health-model.aspx).  
  
  