---
title: MSSQL_ENG014010 | Microsoft Docs
ms.custom: ''
ms.date: 08/26/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG014010 error
ms.assetid: 6ea84f2f-e7a2-4028-9ea9-af0d2eba660e
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0d9c46d6ba0abeae6f0b761888da12fbb55edaa3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/01/2018
ms.locfileid: "47781079"
---
# <a name="mssqleng014010"></a>MSSQL_ENG014010
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="message-details"></a>Dettagli messaggio  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|14010|  
|Origine evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nome simbolico||  
|Testo del messaggio|Il server '%s' non è definito come server di sottoscrizione.|  
  
## <a name="explanation"></a>Spiegazione  
 La replica prevede che tutti i server di una topologia vengano registrati utilizzando il nome del computer con il nome di un'istanza opzionale (nel caso di un'istanza cluster il nome del server virtuale [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con il nome dell'istanza opzionale). Per un corretto funzionamento della replica il valore restituito da `SELECT @@SERVERNAME` per ogni server nella topologia deve far corrispondere al nome dell'istanza opzionale il nome del computer o il nome del server virtuale.  
  
 Non sarà possibile eseguire la replica, se una qualsiasi delle istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene registrata utilizzando l'indirizzo IP o il nome di dominio completo (FQDN, Fully Qualified Domain Name). Se al momento della configurazione della replica tali istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sono state registrate per indirizzo IP o per nome completo dominio in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , è possibile che l'errore venga generato.  
  
## <a name="user-action"></a>Azione dell'utente  
 Verificare che tutte le istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nella topologia siano state registrate correttamente. Se il nome di rete del computer e il nome dell'istanza di SQL Server sono diversi, procedere in uno dei modi seguenti:  
  
-   Aggiungere il nome dell'istanza di SQL Server come nome di rete valido. Uno dei metodi disponibili per impostare un nome di rete alternativo consiste nell'aggiungerlo al file hosts locale. Il file hosts locale è disponibile per impostazione predefinita nella cartella WINDOWS\system32\drivers\etc o WINNT\system32\drivers\etc. Per ulteriori informazioni, vedere la documentazione di Windows.  
  
     Ad esempio, se il nome del computer è comp1, l'indirizzo IP del computer è 10.193.17.129 e il nome dell'istanza è inst1/instname, aggiungere la voce seguente al file hosts:  
  
     10.193.17.129 inst1  
  
-   Rimuovere la replica, registrare ogni istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , quindi ristabilire la replica. Se il valore di @@SERVERNAME non è corretto per un'istanza non cluster, eseguire la procedura seguente:  
  
    ```  
    sp_dropserver '<old_name>', 'droplogins'  
    go  
    sp_addserver '<new_name>', 'local'  
    go  
    ```  
  
     Dopo l'esecuzione della stored procedure [sp_addserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md), è necessario riavviare il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per rendere effettiva la modifica apportata a @@SERVERNAME.  
  
     Se il valore di @@SERVERNAME non è corretto per un'istanza cluster, è necessario modificare il nome tramite Amministrazione cluster. Per altre informazioni, vedere [Istanze del cluster di failover Always On &#40;SQL Server&#41;](../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md).  
  
## <a name="see-also"></a>Vedere anche  
 [@@SERVERNAME &#40;Transact-SQL&#41;](../../t-sql/functions/servername-transact-sql.md)   
 [Guida di riferimento a errori ed eventi &#40;replica&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  
