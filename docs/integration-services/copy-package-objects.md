---
title: Copiare oggetti di pacchetto | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- control flow [Integration Services], copying objects
- copying package objects [Integration Services]
- data flow [Integration Services], copying objects
- connection managers [Integration Services], copying
ms.assetid: 99b85e5c-d6bd-4e7c-afe4-51f6ce151c2f
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a3f537581dca2880d31efc10e0e3a5ac339f6622
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52526157"
---
# <a name="copy-package-objects"></a>Copia di oggetti di pacchetto
  In questo argomento viene descritta la procedura per copiare elementi di un flusso di controllo, elementi di un flusso di dati e gestioni connessioni all'interno di un pacchetto o tra pacchetti diversi.  
  
### <a name="to-copy-control-and-data-flow-items"></a>Per copiare elementi di un flusso di controllo o di un flusso di dati  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]aprire il progetto di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] contenente i pacchetti da usare.  
  
2.  In Esplora soluzioni fare doppio clic sui pacchetti tra cui si desidera copiare gli elementi.  
  
3.  In Progettazione [!INCLUDE[ssIS](../includes/ssis-md.md)] fare clic sulla scheda corrispondente al pacchetto che contiene gli elementi da copiare e quindi fare clic sulla scheda **Flusso di controllo**, **Flusso di dati**o **Gestori eventi** .  
  
4.  Selezionare gli elementi del flusso di controllo o di dati che si desidera copiare. È possibile selezionare un elemento alla volta, facendo clic sugli elementi desiderati mentre si tiene premuto il tasto MAIUSC, oppure selezionarli come gruppo, trascinando il puntatore del mouse sugli elementi desiderati.  
  
    > [!IMPORTANT]  
    >  Quando si selezionano due elementi connessi, i vincoli di precedenza e i percorsi che li connettono non vengono selezionati automaticamente. Per copiare un flusso di lavoro ordinato, come un segmento di un flusso di controllo o di dati, assicurarsi di copiare anche i percorsi e i vincoli di precedenza.  
  
5.  Fare clic con il pulsante destro del mouse su un elemento selezionato e quindi scegliere **Copia**.  
  
6.  Se si copiano elementi in un pacchetto diverso, fare clic sul pacchetto in cui si desidera copiare gli elementi e quindi fare clic sulla scheda corrispondente al tipo di elemento.  
  
    > [!IMPORTANT]  
    >  È possibile copiare un flusso di dati in un pacchetto solo se il pacchetto contiene almeno un'attività Flusso di dati.  
  
7.  Fare clic con il pulsante destro del mouse e scegliere **Incolla**.  
  
### <a name="to-copy-connection-managers"></a>Per copiare gestioni connessioni  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]aprire il progetto di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] contenente il pacchetto da usare.  
  
2.  In Esplora soluzioni fare doppio clic sul pacchetto.  
  
3.  In Progettazione [!INCLUDE[ssIS](../includes/ssis-md.md)] fare clic sulla scheda **Flusso di controllo**, **Flusso di dati**o **Gestori eventi** .  
  
4.  Nella sezione **Gestioni connessioni** fare clic con il pulsante destro del mouse sulla gestione connessione e quindi scegliere **Copia**. È possibile copiare una sola gestione connessione alla volta.  
  
5.  Se si copiano elementi in un pacchetto diverso, fare clic sul pacchetto in cui si vogliono copiare gli elementi e quindi fare clic sulla scheda **Flusso di controllo**, **Flusso di dati**o **Gestori eventi** .  
  
6.  Fare clic con il pulsante destro del mouse nella sezione **Gestioni connessioni** e scegliere **Incolla**.  
  
## <a name="see-also"></a>Vedere anche  
 [Flusso di controllo](../integration-services/control-flow/control-flow.md)   
 [Flusso di dati](../integration-services/data-flow/data-flow.md)   
 [Connessioni in Integration Services &#40;SSIS&#41;](../integration-services/connection-manager/integration-services-ssis-connections.md)   
 [Copia di elementi di progetto](https://msdn.microsoft.com/library/1606c54d-20f9-49f3-a4ef-caad83a772aa)  
  
  
