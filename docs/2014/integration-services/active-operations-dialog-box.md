---
title: Finestra di dialogo operazioni attive | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.ssms.isoperations.executions.f1
- sql12.ssis.ssms.isoperations.general.f1
ms.assetid: 5bb0fcd6-0ce9-488a-85b8-25dddaa03cda
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: d20e7102df982f961aed770aedc19812c5aca949
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/02/2018
ms.locfileid: "48185881"
---
# <a name="active-operations-dialog-box"></a>Finestra di dialogo Operazioni attive
  Utilizzare la finestra di dialogo **Operazioni attive** per visualizzare lo stato delle operazioni di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] attualmente in esecuzione nel server di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , ad esempio distribuzione, convalida ed esecuzione dei pacchetti. Questi dati vengono archiviati nel catalogo SSISDB.  
  
 Per altre informazioni sulle viste [!INCLUDE[tsql](../includes/tsql-md.md)] correlate, vedere[catalog.operations &#40;SSISDB Database&#41;](/sql/integration-services/system-views/catalog-operations-ssisdb-database), [catalog.validations &#40;SSISDB Database&#41;](/sql/integration-services/system-views/catalog-validations-ssisdb-database) e [catalog.executions &#40;SSISDB Database&#41;](/sql/integration-services/system-views/catalog-executions-ssisdb-database)  
  
 **Per saperne di più**  
  
1.  [Aprire la finestra di dialogo operazioni attive](#open_dialog)  
  
2.  [Configurare le opzioni](#options)  
  
##  <a name="open_dialog"></a> Apertura della finestra di dialogo Operazioni attive  
  
1.  Aprire [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)].  
  
2.  Connettersi al motore di database di Microsoft SQL Server.  
  
3.  In Esplora oggetti espandere il nodo **Integration Services** , fare clic con il pulsante destro del mouse su **SSISDB**, quindi fare clic su **Operazioni attive**.  
  
##  <a name="options"></a> Configurare le opzioni  
  
### <a name="options"></a>Opzioni  
 **Tipo**  
 Consente di specificare il tipo di operazione. Di seguito sono riportati i valori possibili per il **tipo** campo e i valori corrispondenti nella colonna operations_type della finestra di Transact-SQL `catalog.operations` visualizzazione.  
  
|||  
|-|-|  
|Inizializzazione di Integration Services|1|  
|Pulizia di operazioni (processo di SQL Agent)|2|  
|Pulizia delle versioni del progetto (processo di SQL Agent)|3|  
|Distribuzione del progetto|101|  
|Ripristino del progetto|106|  
|Creazione e avvio dell'esecuzione del pacchetto|200|  
|Arresto dell'operazione (arresto di una convalida o di un'esecuzione)|202|  
|Convalida del progetto|300|  
|Convalida del pacchetto|301|  
|Configurazione del catalogo|1000|  
  
 **Arresta**  
 Fare clic per arrestare un'operazione in esecuzione.  
  
  
