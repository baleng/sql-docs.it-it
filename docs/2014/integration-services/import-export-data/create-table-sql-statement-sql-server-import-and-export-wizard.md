---
title: Istruzione SQL CREATE TABLE (Importazione/Esportazione guidata SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.impexpwizard.createtablesql.f1
ms.assetid: 0d6f6b3b-d023-4770-a8a9-65b2977c8d05
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 50b98c3038d8ec1af9272eb9da0ad6d8ec0e3139
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/02/2018
ms.locfileid: "48215695"
---
# <a name="create-table-sql-statement-sql-server-import-and-export-wizard"></a>Istruzione SQL CREATE TABLE (Importazione/Esportazione guidata SQL Server)
  Usare la **istruzione SQL Create Table** finestra di dialogo per visualizzare l'istruzione generata automaticamente, oppure a modificarla in base alle proprie esigenze. Se si modifica l'istruzione, potrebbe essere necessario apportare le modifiche adeguate al mapping delle colonne, nonché, in seguito, gestire manualmente l'istruzione SQL modificata.  
  
> [!NOTE]  
>  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] genera un'istruzione CREATE TABLE predefinita basata sull'origine dati connessa. Questa istruzione CREATE TABLE predefinita non includerà l'attributo FILESTREAM anche se la tabella di origine include una colonna con l'attributo FILESTREAM dichiarato. Per eseguire un componente [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] con l'attributo FILESTREAM, implementare innanzitutto l'archiviazione di FILESTREAM nel database di destinazione. Aggiungere quindi l'attributo FILESTREAM all'istruzione CREATE TABLE nella finestra di dialogo **Crea tabella**. Per altre informazioni, vedere [Dati BLOB &#40;Binary Large Object&#41; &#40;SQL Server&#41;](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md).  
  
 Per altre informazioni su questa procedura guidata, vedere [SQL Server importazione / esportazione guidata](import-and-export-data-with-the-sql-server-import-and-export-wizard.md). Per altre informazioni sulle opzioni per avviare la procedura guidata, nonché le autorizzazioni necessarie per eseguire correttamente la procedura guidata, vedere [esecuzione di SQL Server importazione / esportazione guidata](start-the-sql-server-import-and-export-wizard.md).  
  
 Lo scopo di Importazione/Esportazione guidata SQL Server è la copia di dati da un'origine a una destinazione. La procedura guidata può inoltre creare automaticamente un database di destinazione e le tabelle di destinazione. Se tuttavia è necessario copiare più database o tabelle, o altri tipi di oggetti di database, è preferibile utilizzare Copia guidata database. Per altre informazioni, vedere [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md).  
  
## <a name="options"></a>Opzioni  
 **Istruzione SQL**  
 Consente di visualizzare l'istruzione SQL generata automaticamente ed eventualmente di modificarla.  
  
> [!NOTE]  
>  Se si desidera includere un ritorno a capo nell'istruzione SQL, premere CTRL+INVIO. Premere solo INVIO per chiudere la finestra di dialogo.  
  
 **Genera automaticamente**  
 Il pulsante **Genera automaticamente** consente di ripristinare l'istruzione SQL predefinita, qualora fosse stata modificata.  
  
  
