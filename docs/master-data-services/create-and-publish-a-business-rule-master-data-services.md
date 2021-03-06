---
title: Creare e pubblicare una regola business (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology:
- master-data-services
ms.topic: conceptual
helpviewer_keywords:
- business rules [Master Data Services], creating
- creating business rules [Master Data Services]
ms.assetid: 6961d636-4d69-468e-81f7-8d0be6a4a039
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 8ed7c2329742cea3b7fb0fbd43b33233bb846a98
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/01/2018
ms.locfileid: "47628639"
---
# <a name="create-and-publish-a-business-rule-master-data-services"></a>Creare e pubblicare una regola business (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  In [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]creare una regola business per garantire l'accuratezza dei dati master. Dopo avere creato una regola, è necessario pubblicarla prima di poterla applicare ai dati.  
  
## <a name="prerequisites"></a>Prerequisites  
 Per eseguire questa procedura:  
  
-   È necessario disporre di autorizzazione per accedere all'area funzionale **Amministrazione sistema** .  
  
-   È necessario essere un amministratore del modello. Per altre informazioni, vedere [Amministratori &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
### <a name="to-create-and-publish-a-business-rule"></a>Per creare e pubblicare una regola business  
  
1.  In [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], fare clic su **Amministrazione sistema**.  
  
2.  Dalla barra dei menu scegliere **Gestisci** e fare clic su **Regole business**.  
  
3.  Nella pagina **Regola business** selezionare un modello nell'elenco a discesa **Modello** .  
  
4.  Nell'elenco a discesa **Entità** selezionare un'entità.  
  
5.  Nell'elenco a discesa **Tipi di membri** selezionare un tipo di membro a cui applicare la regola business.  
  
6.  Scegliere **Aggiungi**.  
  
7.  Nella casella **Nome** digitare un nome per la regola business.  
  
8.  Nel campo **Descrizione** digitare la descrizione aggiornata della regola di business (facoltativo).  
  
9. Facoltativamente, selezionare l'opzione **Invia notifiche** e, dall'elenco a discesa, selezionare un utente o un gruppo a cui inviare la notifica di posta elettronica.  
  
    > [!NOTE]  
    >  Le notifiche vengono inviate soltanto per le regole che prevedono un'azione di convalida.  
  
10. Nel blocco **If** fare clic su **Aggiungi**. Viene visualizzato un pannello.  
  
11. Nell'elenco a discesa **Attributo** selezionare un attributo.  
  
12. Nell'elenco a discesa **Operatore** selezionare una condizione.  
  
13. Completare tutti i campi obbligatori.  
  
14. Fare clic sul pulsante **Salva** . Viene aggiunta una nuova riga alla griglia **If** .  
  
    > [!TIP]  
    >  È possibile eliminare gli elementi dalla regola di business facendo clic su ognuno di essi con il pulsante destro del mouse e scegliendo **Elimina**.  
  
15. Aggiungere facoltativamente più condizioni alla regola. Per altre informazioni, vedere [Aggiungere più condizioni a una regola business &#40;Master Data Services&#41;](../master-data-services/add-multiple-conditions-to-a-business-rule-master-data-services.md).  
  
16. Nel blocco **Then** fare clic su **Aggiungi** . Viene visualizzato un pannello.  
  
17. Nell'elenco a discesa **Attributo** selezionare un attributo.  
  
18. Nell'elenco a discesa **Operatore** selezionare un'azione.  
  
19. Completare tutti i campi obbligatori.  
  
20. Fare clic su **Salva**. Viene aggiunta una nuova riga alla griglia **Then** .  
  
21. Facoltativamente, per aggiungere l'azione **Else** , attenersi alla procedura seguente.  
  
    1.  Nel blocco **Else** fare clic su **Aggiungi**. Viene visualizzato un pannello.  
  
    2.  Nell'elenco a discesa **Attributo** selezionare un attributo.  
  
    3.  Nell'elenco a discesa **Operatore** selezionare un'azione.  
  
    4.  Completare tutti i campi obbligatori.  
  
    5.  Fare clic su **Salva**. Viene aggiunta una nuova riga alla griglia **Else** .  
  
22. Fare clic su **Salva**. Viene aggiunta una nuova riga alla griglia delle regole business.  
  
23. Fare clic su **Pubblica tutto**.  
  
24. Nella finestra di dialogo di conferma, fare clic su **OK**. Il valore nella colonna **Stato della regola di business** è **Attiva**.  
  
## <a name="grid-columns"></a>Colonne della griglia  
 Per ogni regola business creata viene aggiunta alla griglia una riga con sei colonne. Di seguito sono elencate le colonne.  
  
|nome|Descrizione|  
|----------|-----------------|  
|Stato|Quando si fa clic su **Salva** , viene visualizzata l'immagine seguente che indica che la regola di business è in fase di aggiornamento.<br /><br /> ![mds_BR_refresh](../master-data-services/media/mds-br-refresh.png "mds_BR_refresh")<br /><br /> Se si verificano errori durante la creazione o la modifica di una regola business, viene visualizzata l'immagine seguente.<br /><br /> ![mds_br_error](../master-data-services/media/mds-br-error.png "mds_br_error")<br /><br /> Se lo stato è OK, viene visualizzata l'immagine seguente.<br /><br /> ![mds_BR_success](../master-data-services/media/mds-br-success.png "mds_BR_success")|  
|nome|Nome della regola business.|  
|Descrizione|Descrizione della regola business.|  
|Stato della regola di business|Uno degli stati seguenti della regola business: Regola non definita, Attiva, Esclusa, Modifiche in sospeso, Esclusione in sospeso ed Eliminazione in sospeso.|  
|Esclusione|Specifica se la regola business è esclusa.|  
|Notification|Specifica l'utente o il gruppo selezionato a cui inviare la notifica tramite posta elettronica.|  
  
## <a name="next-steps"></a>Next Steps  
  
-   Applicare regole business ai dati eseguendo una delle procedure riportate di seguito:  
  
    -   [Convalidare membri specifici rispetto a regole business &#40;Master Data Services&#41;](../master-data-services/validate-specific-members-against-business-rules-master-data-services.md)  
  
    -   [Convalidare una versione usando le regole di business &#40;Master Data Services&#41;](../master-data-services/validate-a-version-against-business-rules-master-data-services.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Configurare le regole di business per l'invio di notifiche &#40;Master Data Services&#41;](../master-data-services/configure-business-rules-to-send-notifications-master-data-services.md)   
 [Modificare il nome di una regola business &#40;Master Data Services&#41;](../master-data-services/change-a-business-rule-name-master-data-services.md)   
 [Aggiungere più condizioni a una regola business &#40;Master Data Services&#41;](../master-data-services/add-multiple-conditions-to-a-business-rule-master-data-services.md)  
  
  
