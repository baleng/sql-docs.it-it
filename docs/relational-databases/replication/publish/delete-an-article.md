---
title: Eliminare un articolo | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- articles [SQL Server replication], dropping
- sp_droparticle
- sp_dropmergearticle
- deleting articles
- removing articles
- dropping articles
ms.assetid: 185b58fc-38c0-4abe-822e-6ec20066c863
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 40a543a8b95853cacfb00f284e916ca216cd57b3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/01/2018
ms.locfileid: "47759223"
---
# <a name="delete-an-article"></a>Eliminazione di un articolo
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  In questo argomento viene descritto come eliminare un articolo in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] tramite [!INCLUDE[tsql](../../../includes/tsql-md.md)] o RMO (Replication Management Objects). Per informazioni sulle condizioni per l'eliminazione degli articoli e sulla necessità di creare un nuovo snapshot o reinizializzare le sottoscrizioni in seguito all'eliminazione di un articolo, vedere [Aggiungere ed eliminare articoli in pubblicazioni esistenti](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md).  
  
 **Contenuto dell'argomento**  
  
-   **Per eliminare un articolo tramite:**  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [Oggetti RMO (Replication Management Objects)](#RMOProcedure)  
  
##  <a name="TsqlProcedure"></a> Uso di Transact-SQL  
 È possibile eliminare gli articoli a livello di programmazione tramite le stored procedure di replica. Le stored procedure utilizzate dipenderanno dal tipo di pubblicazione a cui appartiene l'articolo.  
  
#### <a name="to-delete-an-article-from-a-snapshot-or-transactional-publication"></a>Per eliminare un articolo da una pubblicazione snapshot o transazionale  
  
1.  Eseguire [sp_droparticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-droparticle-transact-sql.md) per eliminare un articolo, indicato da **@article**, da una pubblicazione, indicata da **@publication**. Specificare il valore **1** per **@force_invalidate_snapshot**.  
  
2.  (Facoltativo) Per rimuovere completamente l'oggetto pubblicato dal database, eseguire il comando `DROP <objectname>` nel database di pubblicazione del server di pubblicazione.  
  
#### <a name="to-delete-an-article-from-a-merge-publication"></a>Per eliminare un articolo da una pubblicazione di tipo merge  
  
1.  Eseguire [sp_dropmergearticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-dropmergearticle-transact-sql.md) per eliminare un articolo, indicato da **@article**, da una pubblicazione, indicata da **@publication**. Se necessario, specificare un valore **1** per **@force_invalidate_snapshot** e il valore **1** per **@force_reinit_subscription**.  
  
2.  (Facoltativo) Per rimuovere completamente l'oggetto pubblicato dal database, eseguire il comando `DROP <objectname>` nel database di pubblicazione del server di pubblicazione.  
  
###  <a name="TsqlExample"></a> Esempi (Transact-SQL)  
 Nell'esempio seguente un articolo viene eliminato da una pubblicazione transazionale. Perché questa modifica rende non valido lo snapshot esistente, viene specificato il valore **1** per il parametro **@force_invalidate_snapshot** .  
  
```  
DECLARE @publication AS sysname;  
DECLARE @article AS sysname;  
SET @publication = N'AdvWorksProductTran';   
SET @article = N'Product';   
  
-- Drop the transactional article.  
USE [AdventureWorks]  
EXEC sp_droparticle   
  @publication = @publication,   
  @article = @article,  
  @force_invalidate_snapshot = 1;  
GO  
```  
  
 Nell'esempio seguente due articoli vengono eliminati da una pubblicazione di tipo merge. Perché queste modifiche rendono non valido lo snapshot esistente, viene specificato il valore **1** per il parametro **@force_invalidate_snapshot** .  
  
```  
DECLARE @publication AS sysname;  
DECLARE @article1 AS sysname;  
DECLARE @article2 AS sysname;  
SET @publication = N'AdvWorksSalesOrdersMerge';  
SET @article1 = N'SalesOrderDetail';   
SET @article2 = N'SalesOrderHeader';   
  
-- Remove articles from a merge publication.  
USE [AdventureWorks]  
EXEC sp_dropmergearticle   
  @publication = @publication,   
  @article = @article1,  
  @force_invalidate_snapshot = 1;  
EXEC sp_dropmergearticle   
  @publication = @publication,   
  @article = @article2,  
  @force_invalidate_snapshot = 1;  
GO  
```  
  
##  <a name="RMOProcedure"></a> Utilizzo di RMO (Replication Management Objects)  
 È possibile eliminare articoli a livello di programmazione tramite gli oggetti RMO (Replication Management Objects). Le classi RMO utilizzate per l'eliminazione di un articolo dipendono dal tipo di pubblicazione cui appartiene l'articolo.  
  
#### <a name="to-delete-an-article-that-belongs-to-a-snapshot-or-transactional-publication"></a>Per eliminare un articolo che appartiene a una pubblicazione snapshot o transazionale  
  
1.  Creare una connessione al server di pubblicazione tramite la classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Creare un'istanza della classe <xref:Microsoft.SqlServer.Replication.TransArticle> .  
  
3.  Impostare le proprietà <xref:Microsoft.SqlServer.Replication.Article.Name%2A>, <xref:Microsoft.SqlServer.Replication.Article.PublicationName%2A>e <xref:Microsoft.SqlServer.Replication.Article.DatabaseName%2A> .  
  
4.  Impostare la connessione del passaggio 1 per la proprietà <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> .  
  
5.  Controllare la proprietà <xref:Microsoft.SqlServer.Replication.ReplicationObject.IsExistingObject%2A> per verificare che l'articolo esista. Se il valore di questa proprietà è **false**, le proprietà dell'articolo sono state definite in modo non corretto nel passaggio 3 oppure l'articolo non esiste.  
  
6.  Chiamare il metodo <xref:Microsoft.SqlServer.Replication.Article.Remove%2A> .  
  
7.  Chiudere tutte le connessioni.  
  
#### <a name="to-delete-an-article-that-belongs-to-a-merge-publication"></a>Per eliminare un articolo che appartiene a una pubblicazione di tipo merge  
  
1.  Creare una connessione al server di pubblicazione tramite la classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Creare un'istanza della classe <xref:Microsoft.SqlServer.Replication.MergeArticle> .  
  
3.  Impostare le proprietà <xref:Microsoft.SqlServer.Replication.Article.Name%2A>, <xref:Microsoft.SqlServer.Replication.Article.PublicationName%2A>e <xref:Microsoft.SqlServer.Replication.Article.DatabaseName%2A> .  
  
4.  Impostare la connessione del passaggio 1 per la proprietà <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> .  
  
5.  Controllare la proprietà <xref:Microsoft.SqlServer.Replication.ReplicationObject.IsExistingObject%2A> per verificare che l'articolo esista. Se il valore di questa proprietà è **false**, le proprietà dell'articolo sono state definite in modo non corretto nel passaggio 3 oppure l'articolo non esiste.  
  
6.  Chiamare il metodo <xref:Microsoft.SqlServer.Replication.Article.Remove%2A> .  
  
7.  Chiudere tutte le connessioni.  
  
## <a name="see-also"></a>Vedere anche  
 [Aggiungere ed eliminare articoli in pubblicazioni esistenti](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md)   
 [Concetti di base relativi alle stored procedure del sistema di replica](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)  
  
  
