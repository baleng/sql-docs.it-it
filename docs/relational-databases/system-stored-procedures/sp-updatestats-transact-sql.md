---
title: sp_updatestats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/25/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_updatestats_TSQL
- sp_updatestats
dev_langs:
- TSQL
helpviewer_keywords:
- sp_updatestats
ms.assetid: 01184651-6e61-45d9-a502-366fecca0ee4
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 129c7bd5c1932d509b9afc5a28a2548c9fa8c3f9
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/01/2018
ms.locfileid: "47818791"
---
# <a name="spupdatestats-transact-sql"></a>sp_updatestats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Esegue l'istruzione UPDATE STATISTICS su tutte le tabelle definite dall'utente e interne al database corrente.  
  
 Per ulteriori informazioni sull'aggiornamento delle statistiche, vedere [UPDATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md). Per altre informazioni sulle statistiche, vedere [Statistiche](../../relational-databases/statistics/statistics.md).  
    
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_updatestats [ [ @resample = ] 'resample']  
```  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o 1 (esito negativo)  
  
## <a name="arguments"></a>Argomenti  
 [ **@resample** =] **'resample'**  
 Specifica che **sp_updatestats** utilizzerà l'opzione RESAMPLE dell'istruzione [UPDATE STATISTICS](../../t-sql/statements/update-statistics-transact-sql.md). Se **'resample'** non viene specificato, **sp_updatestats** aggiorna le statistiche in base al campionamento predefinito. **@resample** è **varchar (8)** con valore predefinito 'NO'.  
  
## <a name="remarks"></a>Note  
 **sp_updatestats** esegue l'istruzione UPDATE STATISTICS con la parola chiave ALL, in tutte le tabelle definite dall'utente e interne al database. La procedura sp_updatestats mostra i messaggi che indicano lo stato di avanzamento dell'esecuzione. Al termine dell'aggiornamento, viene mostrato un messaggio che indica l'effettivo aggiornamento delle statistiche di tutte le tabelle.  
  
 sp_updatestats aggiorna le statistiche negli indici non cluster disabilitati, mentre non le aggiorna negli indici cluster disabilitati.  
  
 Per le tabelle su disco, **sp_updatestats** aggiorna le statistiche in base al **modification_counter** contenuto nella vista del catalogo **sys.dm_db_stats_properties**, aggiornandole solo nel caso in cui sia stata modificata almeno una riga. Le statistiche sulle tabelle ottimizzate per la memoria vengono sempre aggiornate quando si esegue **sp_updatestats**. Pertanto, non eseguire **sp_updatestats** più del necessario.  
  
 **sp_updatestats** può attivare una ricompilazione di stored procedure o altro codice compilato. Tuttavia, nel caso in cui esista un solo piano di query per le tabelle e gli indici collegati, **sp_updatestats** potrebbe non causare alcuna ricompilazione. Una ricompilazione non è necessaria in tali casi, ma le statistiche vengono comunque aggiornate.  
  
 Per i database con un livello di compatibilità inferiore a 90, l'esecuzione **sp_updatestats** non mantiene l'impostazione più recente di NORECOMPUTE per statistiche specifiche. Per i database con livello di compatibilità pari a 90 o superiore, sp_updatestats mantiene il più recente di NORECOMPUTE per statistiche specifiche. Per altre informazioni sulla disabilitazione e sulla riabilitazione degli aggiornamenti delle statistiche, vedere [Statistiche](../../relational-databases/statistics/statistics.md).  
  
## <a name="permissions"></a>Permissions  
 È necessario appartenere al ruolo server **sysadmin** o essere proprietari del database (**dbo**).  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente vengono aggiornate le statistiche per le tabelle del database [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_updatestats;   
```  
  
## <a name="see-also"></a>Vedere anche  
 [Opzioni di ALTER DATABASE SET &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [CREATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md)   
 [DBCC SHOW_STATISTICS &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)   
 [DROP STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/drop-statistics-transact-sql.md)   
 [sp_autostats &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-autostats-transact-sql.md)   
 [sp_createstats &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-createstats-transact-sql.md)   
 [UPDATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md)   
 [Stored procedure di sistema](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
