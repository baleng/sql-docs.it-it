---
title: Impostare il periodo di scadenza per le sottoscrizioni | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- replication
ms.topic: conceptual
helpviewer_keywords:
- subscriptions [SQL Server replication], expiration
- expiration [SQL Server replication]
- retention periods [SQL Server replication]
- deactivating subscriptions
ms.assetid: 542f0613-5817-42d0-b841-fb2c94010665
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: bc35e6e4f0fe4befe6db2ba93f990b9a7b8c6434
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/02/2018
ms.locfileid: "48220842"
---
# <a name="set-the-expiration-period-for-subscriptions"></a>Impostazione del periodo di scadenza per le sottoscrizioni
  In questo argomento si illustra come impostare il periodo di scadenza per le sottoscrizioni in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] tramite [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../../includes/tsql-md.md)]. Il periodo di scadenza per le sottoscrizioni determina il periodo tempo che deve trascorrere prima che una sottoscrizione scada e venga rimossa. Per altre informazioni, vedere [Subscription Expiration and Deactivation](../subscription-expiration-and-deactivation.md).  
  
 **Contenuto dell'argomento**  
  
-   **Prima di iniziare:**  
  
     [Indicazioni](#Recommendations)  
  
-   **Per impostare il periodo di scadenza per le sottoscrizioni, utilizzando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Recommendations"></a> Indicazioni  
  
-   Il periodo di scadenza della sottoscrizione viene inoltre denominato *periodo di memorizzazione della pubblicazione*. La pulizia dei metadati di replica di tipo merge dipende da questa impostazione:  
  
    -   La replica non è in grado di eliminare i metadati dei database di pubblicazione e sottoscrizione prima della scadenza del periodo di memorizzazione. Quando si imposta un valore elevato per il periodo di memorizzazione, verificare che non sia tale da avere effetti negativi sulle prestazioni della replica. Se si prevede che la sincronizzazione di tutti i Sottoscrittori verrà eseguita regolarmente entro tale periodo di tempo, è consigliabile specificare un valore inferiore.  
  
         Il periodo di memorizzazione per le pubblicazioni di tipo merge ha un periodo di prova di 24 ore per adattarsi ai Sottoscrittori dei diversi fusi orari. Se, ad esempio, si imposta un periodo di memorizzazione di un giorno, il periodo di memorizzazione effettivo sarà di 48 ore.  
  
    -   È possibile specificare che le sottoscrizioni non devono scadere, ma è consigliabile non utilizzare questo valore, perché impedisce l'eliminazione dei metadati.  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
 Impostare il periodo di scadenza per le sottoscrizioni nella pagina **Generale** della finestra di dialogo **Proprietà pubblicazione - \<Pubblicazione>**. Per ulteriori informazioni sull'accesso a questa finestra di dialogo, vedere [View and Modify Publication Properties](view-and-modify-publication-properties.md).  
  
#### <a name="to-set-the-expiration-period-for-subscriptions"></a>Per impostare il periodo di scadenza per le sottoscrizioni  
  
1.  Specificare se le sottoscrizioni avranno una scadenza nella sezione **Scadenza sottoscrizione** della pagina **Generale** della finestra di dialogo **Proprietà pubblicazione - \<Pubblicazione>**.  
  
2.  Se le sottoscrizioni avranno una scadenza, specificarne il periodo di tempo.  
  
##  <a name="TsqlProcedure"></a> Uso di Transact-SQL  
 Per impostare questo valore quando viene creata una pubblicazione o per modificarlo in un secondo momento, è possibile utilizzare le stored procedure di replica.  
  
#### <a name="to-set-the-expiration-period-for-a-subscription-to-a-snapshot-or-transactional-publication"></a>Per impostare il periodo di scadenza per una sottoscrizione di una pubblicazione snapshot o transazionale  
  
1.  Nel server di pubblicazione eseguire [sp_addpublication](/sql/relational-databases/system-stored-procedures/sp-addpublication-transact-sql). Specificare il periodo di scadenza desiderato per la sottoscrizione, in ore, per **@retention**. Il periodo di scadenza predefinito è 336 ore. Per altre informazioni, vedere [Create a Publication](create-a-publication.md).  
  
#### <a name="to-set-the-expiration-period-for-a-subscription-to-a-merge-publication"></a>Per impostare il periodo di scadenza per una sottoscrizione di una pubblicazione di tipo merge  
  
1.  Nel server di pubblicazione eseguire [sp_addmergepublication](/sql/relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql). Specificare il valore desiderato per il periodo di scadenza della sottoscrizione per **@retention**. Specificare per **@retention_period_unit**le unità in cui esprimere il periodo di scadenza, che possono essere una delle seguenti:  
  
    -   **1** = Settimana  
  
    -   **2** = Mese  
  
    -   **3** = Anno  
  
     Il periodo di scadenza predefinito è 14 giorni. Per altre informazioni, vedere [Create a Publication](create-a-publication.md).  
  
#### <a name="to-change-the-expiration-period-for-a-subscription-to-a-snapshot-or-transactional-publication"></a>Per modificare il periodo di scadenza per una sottoscrizione di una pubblicazione snapshot o transazionale  
  
1.  Nel server di pubblicazione eseguire [sp_changepublication](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql). Specificare **retention** per **@property** e il nuovo periodo di scadenza della sottoscrizione, in ore, per **@value**.  
  
#### <a name="to-change-the-expiration-period-for-a-subscription-to-a-merge-publication"></a>Per modificare il periodo di scadenza per una sottoscrizione di una pubblicazione di tipo merge  
  
1.  Nel server di pubblicazione eseguire [sp_helpmergepublication](/sql/relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql), specificando **@publication** e **@publisher**. Si noti il valore di **retention_period_unit** nel set di risultati, che può essere uno dei seguenti:  
  
    -   **0** = giorno  
  
    -   **1** = Settimana  
  
    -   **2** = Mese  
  
    -   **3** = Anno  
  
2.  Nel server di pubblicazione eseguire [sp_changemergepublication](/sql/relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql). Specificare **retention** per **@property** e il nuovo periodo di scadenza della sottoscrizione, come testo basato sull'unità del periodo di memorizzazione indicata nel passaggio 1, per **@value**.  
  
3.  (Facoltativo) Nel server di pubblicazione eseguire [sp_changemergepublication](/sql/relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql). Specificare **retention_period_unit** per **@property** e una nuova unità per il periodo di scadenza della sottoscrizione per **@value**.  
  
## <a name="see-also"></a>Vedere anche  
 [Replication System Stored Procedures Concepts](../concepts/replication-system-stored-procedures-concepts.md)   
 [Subscription Expiration and Deactivation](../subscription-expiration-and-deactivation.md)  
  
  
