---
title: Server di pubblicazione | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.configuredistributionwizard.enablepublishers.f1
ms.assetid: 116cd6a5-32ac-4273-81a2-d184408e0f07
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e8370c989cb442de305c57e239beaff827bef37f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/01/2018
ms.locfileid: "47701169"
---
# <a name="publishers"></a>Server di pubblicazione
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  È possibile concedere ad altri server di pubblicazione l'autorizzazione per l'utilizzo del server di distribuzione. Tenere presente che, se si abilita un server di pubblicazione per l'utilizzo di questo server come server di distribuzione remoto, il server non diventerà un server di pubblicazione. È infatti necessario connettersi al server di pubblicazione, configurarlo per la pubblicazione e selezionare questo server come server di distribuzione. Utilizzando la Creazione guidata nuova pubblicazione è possibile configurare il server di pubblicazione e selezionare un server di distribuzione.  
  
 I server selezionati come server di pubblicazione utilizzeranno il database di distribuzione specificato nella pagina **Database di distribuzione** della creazione guidata. Se si desidera utilizzare un database di distribuzione diverso, non abilitare il server di pubblicazione in questa fase. Utilizzare invece la finestra di dialogo **Proprietà server di distribuzione** per aggiungere i server di pubblicazione dopo aver completato la Configurazione guidata distribuzione.  
  
## <a name="options"></a>Opzioni  
 **Server di pubblicazione**  
 Consente di selezionare i server autorizzati all'utilizzo del server di distribuzione corrente. Fare clic sul pulsante delle proprietà (**...**) accanto al server di pubblicazione per visualizzare e impostare proprietà aggiuntive.  
  
 **Aggiungi**  
 Se il server desiderato non è incluso nell'elenco, fare clic su **Aggiungi** per aggiungere un server di pubblicazione [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Oracle all'elenco dei server di pubblicazione disponibili.  
  
## <a name="see-also"></a>Vedere anche  
 [Configura distribuzione](../../relational-databases/replication/configure-distribution.md)   
 [Configurare la pubblicazione e la distribuzione](../../relational-databases/replication/configure-publishing-and-distribution.md)   
 [Visualizzare e modificare le proprietà del server di pubblicazione e del database di distribuzione](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [Creare una pubblicazione](../../relational-databases/replication/publish/create-a-publication.md)  
  
  
