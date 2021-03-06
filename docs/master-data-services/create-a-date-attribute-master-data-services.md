---
title: Creare un attributo di data (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology:
- master-data-services
ms.topic: conceptual
helpviewer_keywords:
- creating date attributes [Master Data Services]
- attributes [Master Data Services], creating date attributes
ms.assetid: 22a8f1a3-b4f2-4cfa-8495-7daad5ce9d12
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: aa31a8e2601eba31d1f7579b5f110945a47f4d79
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/27/2018
ms.locfileid: "52395294"
---
# <a name="create-a-date-attribute-master-data-services"></a>Creare un attributo di data (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  In [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]creare un attributo date quando si desidera che gli utenti inseriscano una data come valore di attributo.  
  
> [!NOTE]  
>  L'attributo viene chiamato DateTime, ma i valori ora non sono supportati.  
  
## <a name="prerequisites"></a>Prerequisites  
 Per eseguire questa procedura:  
  
-   È necessario disporre di autorizzazione per accedere all'area funzionale **Amministrazione sistema** .  
  
-   È necessario essere un amministratore del modello. Per altre informazioni, vedere [Amministratori &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
-   È necessario avere un'entità per la quale creare l'attributo. Per altre informazioni, vedere [Creare un'entità &#40;Master Data Services&#41;](../master-data-services/create-an-entity-master-data-services.md).  
  
### <a name="to-create-a-date-attribute"></a>Per creare un attributo di data  
  
1.  In [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], fare clic su **Amministrazione sistema**.  
  
2.  Nella pagina **Gestisci modelli** selezionare un modello dalla griglia, quindi fare clic su **Entità**.  
  
3.  Nella pagina **Gestisci entità** selezionare la riga dell'entità per la quale si vuole creare un attributo.  
  
4.  Fare clic su **Attributi**.  
  
5.  Nella pagina **Gestisci attributi** eseguire una di queste operazioni, quindi fare clic su **Aggiungi**.  
  
    -   Se l'attributo è per i membri foglia, selezionare **Foglia** nella casella di riepilogo **Tipo di membro** .  
  
    -   Se l'attributo è per i membri consolidati, selezionare **Consolidato** nella casella di riepilogo **Tipo di membro** .  
  
    -   Se l'attributo è per le raccolte, selezionare **Raccolta** nella casella di riepilogo **Tipo di membro** .  
  
6.  Nella casella **Nome** digitare un nome per l'attributo. Per un elenco di parole che non vanno usate come nomi di attributo, vedere [Parole riservate &#40;Master Data Services&#41;](../master-data-services/reserved-words-master-data-services.md).  
  
7.  Facoltativamente, digitare un nome visualizzato e specificare una descrizione per l'attributo nella casella **Descrizione**.  
  
8.  Nella casella **Larghezza in pixel visualizzazione** digitare la larghezza della colonna attributo da visualizzare nella griglia **Esplora** .  
  
9. Nell'elenco **Tipo di attributo** selezionare **Formato libero**.  
  
10. Nell'elenco **Tipo di dati** selezionare **DateTime**.  
  
11. Nell'elenco **Maschera di input** selezionare un formato per le date.  
  
12. Facoltativamente, selezionare **Abilita rilevamento modifiche** per tenere traccia delle modifiche a gruppi di attributi. Per altre informazioni, vedere [Aggiungere attributi ad un gruppo rilevamento modifiche &#40;Master Data Services&#41;](../master-data-services/add-attributes-to-a-change-tracking-group-master-data-services.md).  
  
13. Fare clic su **Salva**.  
  
## <a name="to-display-the-time-portion-of-a-datetime-value"></a>Per visualizzare la porzione dell'ora di un valore datetime  
 Per fare in modo che nell'interfaccia utente venga visualizzata la porzione dell'ora di un valore datetime, è necessario selezionare una maschera di input appropriata per l'attributo. Questa operazione non viene effettuata da nessuna delle maschere predefinite per gli attributi Datetime, tuttavia è possibile aggiungerne una nuova tramite cui sarà possibile visualizzare l'ora. A tale scopo, aggiungere una riga nella tabella mdm.tblList del database MDS in cui sono archiviate le maschere predefinite. Nella riga dovrebbero essere presenti i valori seguenti:  
  
|||  
|-|-|  
|ListCode|lstInputMask|  
|ListName|Maschera di input|  
|Seq|19|  
|List Option|dd/MM/yyyy hh:mm:ss tt|  
|Option ID|19|  
|IsVisible|1|  
|Group_ID|3|  
  
 Dopo aver immesso una riga con i valori riportati in precedenza nella tabella mdm.tblList, la maschera "dd/MM/yyyy hh:mm:ss tt" sarà disponibile nella casella di riepilogo Maschera di input. È quindi possibile selezionare questa maschera per visualizzare la data e l'ora in una colonna di attributo datetime di un'entità in Esplora risorse di MDS.  
  
 La maschera di input è una stringa in formato DateTime .NET personalizzato. Per altre informazioni, vedere [Stringhe di formato di data e ora personalizzato](https://msdn.microsoft.com/library/8kb3ddd4\(v=vs.110\).aspx)  
  
## <a name="see-also"></a>Vedere anche  
 [Attributi &#40;Master Data Services&#41;](../master-data-services/attributes-master-data-services.md)   
 [Modificare il nome e il tipo di dati di un attributo &#40;Master Data Services&#41;](../master-data-services/change-an-attribute-name-and-data-type-master-data-services.md)   
 [Creare un attributo basato su dominio &#40;Master Data Services&#41;](../master-data-services/create-a-domain-based-attribute-master-data-services.md)   
 [Creare un attributo di file &#40;Master Data Services&#41;](../master-data-services/create-a-file-attribute-master-data-services.md)  
  
  
