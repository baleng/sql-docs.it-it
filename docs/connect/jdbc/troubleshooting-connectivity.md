---
title: Risoluzione dei problemi di connettività | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: bfba0b49-2e1f-411d-a625-d25fad9ea12d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7ae5f65538c0303a92fdb86f71d75a556ad3f458
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 10/01/2018
ms.locfileid: "47840889"
---
# <a name="troubleshooting-connectivity"></a>Risoluzione dei problemi di connettività
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Per garantire la comunicazione tra [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] e il database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è necessario che TCP/IP sia installato e in esecuzione. Per verificare quali protocolli della libreria di rete sono installati, è possibile usare Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Sono molti i motivi per cui una connessione di database può avere esito negativo, tra cui i seguenti:  
  
-   TCP/IP non è abilitato per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o il server o il numero di porta specificato non è corretto. Verificare che [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sia in attesa con TCP/IP sul server e sulla porta specificati. Questa condizione potrebbe essere segnalata da un'eccezione simile alla seguente: "Accesso non riuscito. La connessione TCP/IP all'host ha avuto esito negativo." In questo caso è possibile che si sia verificata una delle seguenti condizioni:  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è installato ma TCP/IP non è stato installato come protocollo di rete per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando l'utilità Configurazione di rete di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] o Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versioni successive.  
  
    -   TCP/IP è installato come protocollo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ma non è in attesa sulla porta specificata nell'URL della connessione JDBC. La porta predefinita è la 1433, ma al momento dell'installazione del prodotto, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] può essere configurato per restare in attesa su qualsiasi porta. Verificare che [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sia in attesa sulla porta 1433. In alternativa, se la porta è stata modificata, assicurarsi che la porta specificata nell'URL della connessione JDBC corrisponda al nuovo valore. Per altre informazioni sugli URL delle connessioni JDBC, vedere [Building the Connection URL](../../connect/jdbc/building-the-connection-url.md).  
  
    -   L'indirizzo del computer specificato nell'URL della connessione JDBC non fa riferimento a un server in cui è installato e avviato [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
    -   La comunicazione di rete di TCP/IP tra il client e il server in cui è in esecuzione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non è in funzione. È possibile verificare la connettività TCP/IP a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tramite telnet. Al prompt dei comandi digitare, ad esempio `telnet 192.168.0.0 1433`, in cui 192.168.0.0 è l'indirizzo del computer che esegue [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e 1433 è la porta di attesa. Se viene visualizzato un messaggio per indicare che non è possibile connettersi tramite telnet, TCP/IP non è in attesa delle connessioni [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sulla porta indicata. Usare l'utilità Configurazione di rete di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] o Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versioni successive per assicurarsi che [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sia configurato per usare TCP/IP sulla porta 1433.  
  
    -   La porta utilizzata dal server non è stata aperta nel firewall. In questo modo viene inclusa la porta utilizzata dal server o, facoltativamente, la porta associata a un'istanza denominata del server.  
  
-   Il nome del database specificato non è corretto. Assicurarsi di accedere a un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esistente.  
  
-   Il nome utente o la password non sono corretti. Assicurarsi di disporre dei valori corretti.  
  
-   Quando si usa Autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], il driver JDBC richiede che [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sia installato con Autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], configurazione che non corrisponde all'impostazione predefinita. Quando si installa o configura l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], assicurarsi che questa opzione sia inclusa.  
  
## <a name="see-also"></a>Vedere anche  
 [Diagnosi dei problemi relativi al driver JDBC](../../connect/jdbc/diagnosing-problems-with-the-jdbc-driver.md)   
 [Connessione a SQL Server con il driver JDBC](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)  
  
  
