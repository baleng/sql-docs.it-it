---
title: Connettere componenti in un flusso di dati | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- components [Integration Services], connections
- connections [Integration Services], data flow components
ms.assetid: 70616a58-8921-4218-85bf-f3e90c5a9dbf
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: bd6904980e160b027147649751d076085307a3ec
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/02/2018
ms.locfileid: "48204461"
---
# <a name="connect-components-in-a-data-flow"></a>Connessione di componenti in un flusso di dati
  Questa procedura descrive la connessione dell'output dei componenti di un flusso di dati ad altri componenti dello stesso flusso di dati.  
  
### <a name="to-connect-components-in-a-data-flow"></a>Per connettere componenti in un flusso di dati  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]aprire il progetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] che contiene il pacchetto desiderato.  
  
2.  In Esplora soluzioni fare doppio clic sul pacchetto per aprirlo.  
  
3.  Fare clic sulla scheda **Flusso di controllo** , quindi fare doppio clic sull'attività Flusso di dati che contiene il flusso di dati in cui si desidera connettere i componenti.  
  
4.  Nell'area di progettazione della scheda **Flusso di dati** selezionare la trasformazione o l'origine da connettere.  
  
5.  Trascinare la freccia verde dell'output di un'origine o trasformazione a una destinazione o trasformazione. In alcuni componenti flussi di dati sono inclusi output degli errori che è possibile connettere allo stesso modo.  
  
    > [!NOTE]  
    >  Alcuni componenti flussi di dati possono includere più output ed è possibile connettere ogni output a una trasformazione o destinazione diversa.  
  
6.  Per salvare il pacchetto aggiornato, scegliere **Salva elementi selezionati** dal menu **File** .  
  
## <a name="see-also"></a>Vedere anche  
 [Aggiunta o eliminazione di un componente in un flusso di dati](data-flow.md)   
 [Configurare un Output degli errori in un componente del flusso di dati](../configure-an-error-output-in-a-data-flow-component.md)   
 [Flusso di dati](data-flow.md)  
  
  
