---
title: Barra di divisione CDC | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.designer.cdcsplitter.f1
ms.assetid: 167bc5c6-fa36-439d-987c-b20acd1a77e2
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 03f677f8214fb086f3feb6077608fed83d7089d4
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/02/2018
ms.locfileid: "48086256"
---
# <a name="cdc-splitter"></a>CDC Splitter
  La barra di divisione CDC suddivide un singolo flusso di righe delle modifiche da un flusso di dati dell'origine CDC in diversi flussi di dati per operazioni di inserimento, aggiornamento ed eliminazione. Il flusso di dati viene suddiviso in base alla colonna obbligatoria `__$operation` e ai relativi valori standard nelle tabelle delle modifiche di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] .  
  
|Valore dell'operazione|Output|Description|  
|------------------------|------------|-----------------|  
|1|DELETE|Riga eliminata|  
|2|Insert|Riga inserita (non disponibile quando si usa la modalità CDC **Net with Merge** (Rete con unione))|  
|3|Update|Riga prima dell'aggiornamento (disponibile solo quando si usa la modalità CDC **All with Old Values** (Tutto con valori precedenti))|  
|4|Update|Riga dopo l'aggiornamento (segue l'operazione prima dell'aggiornamento)|  
|5|Update|Unione della riga (disponibile solo quando si usa la modalità CDC **Net with Merge** (Rete con unione))|  
|Altro|Errore||  
  
 È possibile utilizzare la barra di divisione per connettersi ad output INSERT, DELETE e UPDATE predefiniti per l'ulteriore elaborazione.  
  
 La trasformazione CDC Splitter include un input normale e un output degli errori.  
  
## <a name="error-handling"></a>Gestione degli errori  
 La trasformazione CDC Splitter include un output degli errori. Le righe di input con un valore non valido della colonna $operation vengono considerate errate e vengono gestite in base alla proprietà **ErrorRowDisposition** dell'input.  
  
 L'output degli errori del componente include le colonne di output seguenti:  
  
-   **Error Code**: impostare su 1.  
  
-   **Error Column**(Colonna errore): colonna di origine che provoca l'errore (per gli errori di conversione).  
  
-   **Error Row Columns**: colonne di input della riga che ha provocato l'errore.  
  
## <a name="configuring-the-cdc-splitter"></a>Configurazione della barra di divisione CDC  
 Non sono disponibili proprietà configurabili per la barra di divisione CDC.  
  
 Per ulteriori informazioni sull'utilizzo della barra di divisione CDC, vedere Componenti CDC per Microsoft SQL Server Integration Services.  
  
 La finestra di dialogo **Editor avanzato** contiene le proprietà che è possibile impostare a livello di codice.  
  
 Per aprire la finestra di dialogo **Editor avanzato** :  
  
-   Nella schermata **Flusso di dati** del progetto di [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] fare clic con il pulsante destro del mouse sulla barra di divisione CDC e scegliere **Visualizza editor avanzato**.  
  
## <a name="see-also"></a>Vedere anche  
 [Indirizzare il flusso CDC in base al tipo di modifica](direct-the-cdc-stream-according-to-the-type-of-change.md)  
  
  
