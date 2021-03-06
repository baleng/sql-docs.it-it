---
title: Risoluzione dei problemi di connettività dei pacchetti degli strumenti | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Integration Services packages, troubleshooting
- SSIS packages, troubleshooting
- Integration Services, troubleshooting
- connectivity [Integration Services], troubleshooting
- errors [Integration Services], troubleshooting
- packages [Integration Services], troubleshooting
ms.assetid: 08a019f5-8ba7-4527-97c1-e9846d4022ff
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 4e8059fcb984b4b2d6450cefaa20e5e01e06fb0b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/02/2018
ms.locfileid: "48051201"
---
# <a name="troubleshooting-tools-package-connectivity"></a>Risoluzione dei problemi relativi alla connettività dei pacchetti degli strumenti
  In [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] sono disponibili gli strumenti e le caratteristiche per la risoluzione dei problemi relativi alla connettività tra pacchetti e alle origini dati da cui i pacchetti estraggono e caricano i dati.  
  
## <a name="troubleshooting-issues-with-external-data-providers"></a>Risoluzione dei problemi relativi a provider di dati esterni  
 In molti pacchetti si verificano degli errori durante le interazioni con provider di dati esterni. Tuttavia, i messaggi restituiti a [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] dai provider spesso non contengono informazioni sufficienti per risolvere i problemi dell'interazione. A questo scopo, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] include nuovi messaggi che è possibile utilizzare per risolvere i problemi relativi all'interazione di un pacchetto con origini dati esterne.  
  
-   **Abilitare la registrazione e selezionare l'evento Diagnostic del pacchetto per visualizzare i messaggi per la risoluzione dei problemi**. Tramite i componenti di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] seguenti può venire scritto un messaggio nel log prima e dopo ogni chiamata a un provider di dati esterno:  
  
    -   Gestione connessione OLE DB, origine OLE DB e destinazione OLE DB  
  
    -   Gestione connessione [!INCLUDE[vstecado](../../includes/vstecado-md.md)] e origine ADO NET  
  
    -   Attività Esegui SQL  
  
    -   Trasformazione Ricerca, trasformazione Comando OLE DB e trasformazione Dimensione a modifica lenta  
  
     I messaggi del log includono il nome del metodo chiamato. Questi messaggi del log, ad esempio, potrebbero includere il metodo `Open` di un oggetto `Connection` OLE DB o il metodo `ExecuteNonQuery` di un oggetto `Command`. I messaggi presentano il formato seguente, dove '%1!s!' è un segnaposto per le informazioni sul metodo:  
  
    ```  
    ExternalRequest_pre: The object is ready to make the following external request: '%1!s!'.  
    ExternalRequest_post: '%1!s!'. The external request has completed.  
    ```  
  
     Per risolvere i problemi relativi all'interazione con il provider di dati esterno, controllare nel log che per ogni messaggio che precede la richiesta (`ExternalRequest_pre`) sia presente un messaggio che la segue (`ExternalRequest_post`). Se tale messaggio successivo non è presente, il provider di dati esterno non ha risposto come previsto.  
  
     Di seguito sono riportate alcune righe di esempio di un log contenente questi messaggi di registrazione:  
  
    ```  
    ExternalRequest_pre: The object is ready to make the following external request: 'ITransactionJoin::JoinTransaction'.  
    ExternalRequest_post: 'ITransactionJoin::JoinTransaction succeeded'. The external request has completed.  
    ExternalRequest_pre: The object is ready to make the following external request: 'IDbConnection.Open'.  
    ExternalRequest_post: 'IDbConnection.Open succeeded'. The external request has completed.  
    ExternalRequest_pre: The object is ready to make the following external request: 'IDbConnection.CreateCommand'.  
    ExternalRequest_post: 'IDbConnection.CreateCommand finished'. The external request has completed."  
    ExternalRequest_pre: The object is ready to make the following external request: 'IDbCommand.ExecuteReader'.  
    ExternalRequest_post: 'IDbCommand.ExecuteReader finished'. The external request has completed."  
    ExternalRequest_pre: The object is ready to make the following external request: 'IDataReader.GetSchemaTable'.  
    ExternalRequest_post: 'IDataReader.GetSchemaTable finished'. The external request has completed."  
    ExternalRequest_pre: The object is ready to make the following external request: 'IDataReader.Close'.  
    ExternalRequest_post: 'IDataReader.Close finished'. The external request has completed."  
    ExternalRequest_pre: The object is ready to make the following external request: 'IDbConnection.Close'.  
    ExternalRequest_post: 'IDbConnection.Close finished'. The external request has completed."  
    ```  
  
## <a name="see-also"></a>Vedere anche  
 [Risoluzione dei problemi degli strumenti per lo sviluppo di pacchetti](troubleshooting-tools-for-package-development.md)   
 [Strumenti per la risoluzione dei problemi relativi all'esecuzione dei pacchetti](troubleshooting-tools-for-package-execution.md)  
  
  
