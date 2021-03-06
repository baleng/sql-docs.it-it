---
title: 'Attività 5: Impostazione basate su termini relazioni | Microsoft Docs'
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.topic: conceptual
ms.assetid: 6569d512-637d-4f7b-82e1-1e8582278b37
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 122bd2276705e2485afb296adb66accdaf1ccaaf
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/02/2018
ms.locfileid: "48150081"
---
# <a name="task-5-setting-term-based-relationships"></a>Attività 5: Impostazione delle relazioni basate su termini
  In questa attività, è definito alcune relazioni basate su termini per i valori per il **Supplier Name** dominio. Una relazione basata su termini consente di effettuare una correzione a un termine che fa parte di un valore in un dominio, consentendo in questo modo a più valori identici ad eccezione dell'ortografia di una parte in comune tra essi di essere considerati sinonimi identici. Ad esempio, **Inc** possono essere corretti per **Incorporated**. Queste relazioni vengono utilizzate da DQS nei processi di individuazione delle informazioni, di pulizia o di corrispondenza. Visualizzare [basate su termini creare relazioni](http://msdn.microsoft.com/library/hh510404.aspx) per altri dettagli.  
  
1.  Selezionare **Supplier Name** nel **elenco di domini**.  
  
2.  Passare al **relazioni basate su termini** scheda nel riquadro di destra.  
  
3.  Fare clic su **Aggiungi nuova relazione** pulsante sulla barra degli strumenti per aggiungere una relazione alla tabella.  
  
4.  Tipo **co** per il **valore** campo e **società** per il **Correggi in** campo.  
  
5.  Ripetere i due passaggi precedenti per i valori seguenti:  
  
    |valore|Correggi in|  
    |-----------|----------------|  
    |Corp.|Corporation|  
    |Inc.|Incorporated|  
  
     ![Relazioni basate su termini](../../2014/tutorials/media/et-settingtermbasedrelations.jpg "relazioni basate su termini")  
  
## <a name="next-step"></a>Passaggio successivo  
 [Attività 6: Impostazione di sinonimi](../../2014/tutorials/task-6-setting-synonyms.md)  
  
  
