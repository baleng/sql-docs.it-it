---
title: Eseguire il mapping delle colonne ai domini compositi | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: d9422412-8a3d-45ae-af7f-072c902a09ba
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 2318f93e1bd8b5a11e14c17cb8b662db27b12fdf
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/01/2018
ms.locfileid: "47728782"
---
# <a name="map-columns-to-composite-domains"></a>Eseguire il mapping delle colonne ai domini compositi
  Un dominio composito è costituito da due o più singoli domini. È possibile eseguire il mapping di più colonne oppure di una singola colonna con valori delimitati al dominio.  
  
 Se sono disponibili più colonne, è necessario eseguire il mapping di una colonna a ogni singolo dominio nel dominio composito per applicare le regole di quest'ultimo alla pulizia dati. Selezionare i singoli domini inclusi nel dominio composito nel client Data Quality. Per altre informazioni, vedere [Creare un dominio composito](../../../data-quality-services/create-a-composite-domain.md).  
  
 Se è disponibile una singola colonna con valori delimitati, è necessario eseguire il mapping della singola colonna al dominio composito. I valori devono essere visualizzati nello stesso ordine dei singoli domini nel dominio composito. Il delimitatore nell'origine dati deve corrispondere al delimitatore utilizzato per analizzare i valori del dominio composito. È possibile selezionare il delimitatore per il dominio composito, nonché impostare altre proprietà nel client Data Quality. Per altre informazioni, vedere [Creazione di un dominio composito](../../../data-quality-services/create-a-composite-domain.md).  
  
### <a name="to-map-multiple-columns-to-a-composite-domain"></a>Per eseguire il mapping di più colonne a un dominio composito  
  
1.  Fare clic con il pulsante destro del mouse sulla trasformazione DQS Cleansing e quindi scegliere **Modifica**.  
  
2.  Nella scheda **Gestione connessione** verificare che il dominio composito sia visualizzato nell'elenco dei domini disponibili.  
  
3.  Nella scheda **Mapping** selezionare le colonne nell'area **Colonne di input disponibili** .  
  
4.  Per ogni colonna elencata nel campo **Colonna di input** selezionare un singolo dominio nel campo **Dominio** . Selezionare solo singoli domini disponibili nel dominio composito.  
  
5.  In base alle esigenze, modificare i nomi visualizzati nei campi **Alias di origine**, **Alias di output**e **Alias di stato** .  
  
6.  In base alle esigenze, impostare le proprietà nella scheda **Avanzate** . Per altre informazioni sulle proprietà, vedere [Finestra di dialogo Editor trasformazione DQS Cleansing](../../../integration-services/data-flow/transformations/dqs-cleansing-transformation-editor-dialog-box.md).  
  
### <a name="to-map-a-column-with-delimited-values-to-a-composite-domain"></a>Per eseguire il mapping di una colonna con valori delimitati a un dominio composito  
  
1.  Fare clic con il pulsante destro del mouse sulla trasformazione DQS Cleansing e quindi scegliere **Modifica**.  
  
2.  Nella scheda **Gestione connessione** verificare che il dominio composito sia visualizzato nell'elenco dei domini disponibili.  
  
3.  Nella scheda **Mapping** selezionare la colonna nell'area **Colonne di input disponibili** .  
  
4.  Per la colonna elencata nel campo **Colonna di input** selezionare il dominio composito nel campo **Dominio** .  
  
5.  In base alle esigenze, modificare i nomi visualizzati nei campi **Alias di origine**, **Alias di output**e **Alias di stato** .  
  
6.  In base alle esigenze, impostare le proprietà nella scheda **Avanzate** . Per altre informazioni sulle proprietà, vedere [Finestra di dialogo Editor trasformazione DQS Cleansing](../../../integration-services/data-flow/transformations/dqs-cleansing-transformation-editor-dialog-box.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Trasformazione DQS Cleansing](../../../integration-services/data-flow/transformations/dqs-cleansing-transformation.md)  
  
  
