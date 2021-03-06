---
title: Istanza server mirror (Configurazione guidata sicurezza mirroring del database) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.configdbmsecurwiz.mirrorsrvr.f1
ms.assetid: 53223432-615e-440f-904d-925d33ec2144
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 83a92633a4c466e72c8cc2de0cc1c220e88e01bb
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/02/2018
ms.locfileid: "48079691"
---
# <a name="mirror-server-instance-configure-database-mirroring-security-wizard"></a>Istanza server mirror (Configurazione guidata sicurezza mirroring del database)
  Utilizzare questa pagina per specificare le informazioni relative all'istanza del server del database mirror.  
  
> [!IMPORTANT]  
>  L'istanza del server mirror deve essere in esecuzione nella stessa edizione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], Standard o Enterprise, come l'istanza del server principale. È inoltre consigliabile che vengano eseguite in sistemi simili in grado di gestire carichi di lavoro identici.  
  
 **Per configurare il mirroring del database tramite SQL Server Management Studio**  
  
-   [Stabilire una sessione di mirroring del database tramite autenticazione di Windows &#40;SQL Server Management Studio&#41;](establish-database-mirroring-session-windows-authentication.md)  
  
-   [Avvio della Configurazione guidata sicurezza mirroring del database &#40;SQL Server Management Studio&#41;](start-the-configuring-database-mirroring-security-wizard.md)  
  
## <a name="options"></a>Opzioni  
 **Istanza server mirror**  
 Se nella pagina **Mirroring** della finestra di dialogo **Proprietà database** è già stata specificata un'istanza del server mirror, tale istanza viene visualizzata. Per altre informazioni, vedere [Proprietà del database &#40;Pagina Mirroring&#41;](../../relational-databases/databases/database-properties-mirroring-page.md).  
  
 In caso contrario, immettere il nome dell'istanza del server mirror. Si noti che l'istanza del server mirror non può essere la stessa istanza del server principale.  
  
 **Connect**  
 Se non è stata specificata un'istanza del server mirror, fare clic su **Connetti**. Verrà visualizzata la finestra di dialogo **Connetti al server** nella quale è possibile specificare l'istanza del server e stabilire una connessione.  
  
 Se è stata specificata l'istanza, ma non è disponibile una connessione con autorizzazioni sufficienti per il controllo dell'esistenza dell'endpoint, fare clic su **Connetti**. Verrà visualizzata la finestra di dialogo **Connetti al server** in cui l'istanza del server risulterà selezionata automaticamente e non sarà possibile modificarla. Specificare un account di dominio dotato di autorizzazioni sufficienti e connettersi all'istanza del server.  
  
> [!NOTE]  
>  Quando viene stabilita la connessione all'istanza del server, la Configurazione guidata sicurezza mirroring del database usa le credenziali della finestra di dialogo **Connetti al server** . Queste credenziali sono diverse da quelle di una sessione di mirroring, che utilizza le credenziali dell'account di avvio con il quale l'istanza del server è in esecuzione come servizio.  
  
 **Porta di attesa**  
 Il funzionamento di questa opzione dipende dalla presenza dell'endpoint di mirroring per l'istanza del server corrente, come illustrato di seguito:  
  
-   Se non esiste una porta di attesa per l'istanza del server, nella casella di testo **Porta** verrà visualizzato il numero di porta 5022. È possibile utilizzare qualsiasi numero di porta disponibile, ad esempio 7022.  
  
-   Se esiste già l'endpoint del mirroring, verrà visualizzato il numero di porta dell'endpoint. Se è necessario modificare la porta, utilizzare un comando ALTER ENDPOINT. Per altre informazioni, vedere [ALTER ENDPOINT &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-endpoint-transact-sql).  
  
    > [!NOTE]  
    >  È necessario un numero di porta.  
  
 **Nome endpoint**  
 Se l'endpoint di mirroring esiste per l'istanza del server, viene visualizzato il nome dell'endpoint. Se l'endpoint non esiste, è possibile specificare il nome dell'endpoint.  
  
 **Crittografa i dati inviati tramite questo endpoint**  
 La crittografia è abilitata per impostazione predefinita. Quando è abilitata, la crittografia non solo è supportata, ma è anche necessaria e utilizza i valori predefiniti per tutte le opzioni di crittografia. Per altre informazioni, vedere [CREATE ENDPOINT &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-endpoint-transact-sql).  
  
 Per disabilitare la crittografia, deselezionare la casella di controllo. Per abilitare di nuovo la crittografia, selezionare la casella di controllo.  
  
## <a name="see-also"></a>Vedere anche  
 [Endpoint del mirroring del database &#40;SQL Server&#41;](the-database-mirroring-endpoint-sql-server.md)   
 [Proprietà del database &#40;Pagina Mirroring&#41;](../../relational-databases/databases/database-properties-mirroring-page.md)   
 [Creare un endpoint del mirroring del database per l'autenticazione Windows &#40;Transact-SQL&#41;](create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)   
 [Avviare il monitoraggio mirroring del database &#40;SQL Server Management Studio&#41;](../database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)   
 [Mirroring del database &#40;SQL Server&#41;](database-mirroring-sql-server.md)  
  
  
