---
title: Trasferire gli account di accesso attività Editor (pagina account di accesso) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.transferloginstask.logins.f1
helpviewer_keywords:
- Transfer Logins Task Editor
ms.assetid: bf244c24-bd45-4ece-b66b-78b488f35c5b
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 877d7d8e4831a785586680ce57d21975443da645
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/02/2018
ms.locfileid: "48070051"
---
# <a name="transfer-logins-task-editor-logins-page"></a>Editor attività Trasferisci account di accesso (pagina Account di accesso)
  Usare la pagina **Account di accesso** della finestra di dialogo **Editor attività Trasferisci account di accesso** per impostare le proprietà per la copia di uno o più account di accesso di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] da un'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] a un altra. Per altre informazioni su questa attività, vedere [Attività Trasferisci account di accesso](control-flow/transfer-logins-task.md).  
  
> [!IMPORTANT]  
>  Durante l'esecuzione di questa attività, sul server di destinazione vengono creati gli account di accesso con password casuali e le password vengono disabilitate. Per usare questi account di accesso, è necessario che un membro del ruolo predefinito del server **sysadmin** cambi le password e quindi le attivi. L'account di accesso **sa** non può essere trasferito.  
  
## <a name="options"></a>Opzioni  
 **SourceConnection**  
 Selezionare una gestione connessione SMO nell'elenco o fare clic su **\<Nuova connessione...>** per creare una nuova connessione al server di origine.  
  
 **DestinationConnection**  
 Selezionare una gestione connessione SMO nell'elenco o fare clic su **Nuova connessione...>\<** per creare una nuova connessione al server di destinazione.  
  
 **LoginsToTransfer**  
 Consente di selezionare gli account di accesso di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] da copiare dal server di origine a quello di destinazione. Per questa proprietà sono disponibili le opzioni elencate nella tabella seguente:  
  
|valore|Description|  
|-----------|-----------------|  
|**AllLogins**|Tutti gli account di accesso di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] nel server di origine verranno copiati in quello di destinazione.|  
|**SelectedLogins**|Solo gli account di accesso specificati in **LoginsList** verranno copiati nel server di destinazione.|  
|**AllLoginsFromSelectedDatabases**|Tutti gli account di accesso nel database specificato in **DatabasesList** verranno copiati nel server di destinazione.|  
  
 **LoginsList**  
 Consente di selezionare gli account di accesso nel server di origine da copiare in quello di destinazione. Questa opzione è disponibile solo se è selezionata **SelectedLogins** per **LoginsToTransfer**.  
  
 **DatabasesList**  
 Consente di selezionare i database nel server di origine contenenti gli account di accesso da copiare sul server di destinazione. Questa opzione è disponibile solo se è selezionata **AllLoginsFromSelectedDatabases** per **LoginsToTransfer**.  
  
 **IfObjectExists**  
 Consente di selezionare la modalità di gestione dei nomi già esistenti nel server di destinazione da parte dell'attività  
  
 Per questa proprietà sono disponibili le opzioni elencate nella tabella seguente:  
  
|valore|Description|  
|-----------|-----------------|  
|**FailTask**|L'attività ha esito negativo se esistono già account di accesso con lo stesso nome nel server di destinazione.|  
|**Overwrite**|L'attività sovrascrive gli account di accesso con lo stesso nome nel server di destinazione.|  
|**Skip**|L'attività ignora gli account di accesso con lo stesso nome nel server di destinazione.|  
  
 **CopySids**  
 Consente di indicare se gli identificatori di sicurezza associati agli account di accesso devono essere copiati sul server di destinazione. L'opzione**CopySids** deve essere impostata su **True** se l'attività Trasferisci account di accesso viene usata contestualmente all'attività Trasferisci database. In caso contrario, gli account di accesso copiati non verranno riconosciuti dal database trasferito.  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimento ai messaggi e agli errori di Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Attività di Integration Services](control-flow/integration-services-tasks.md)   
 [Trasferire gli account di accesso attività Editor &#40;pagina Generale&#41;](general-page-of-integration-services-designers-options.md)   
 [Pagina espressioni](expressions/expressions-page.md)   
 [Gestione connessione SMO](connection-manager/smo-connection-manager.md)   
 [Password complesse](../relational-databases/security/strong-passwords.md)   
 [Considerazioni sulla sicurezza per un'installazione di SQL Server](../../2014/sql-server/install/security-considerations-for-a-sql-server-installation.md)  
  
  
