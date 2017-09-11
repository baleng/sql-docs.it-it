---
title: OBJECTPROPERTY (Transact-SQL) | Documenti Microsoft
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- OBJECTPROPERTY
- OBJECTPROPERTY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- displaying schema-scoped object information
- viewing schema-scoped object information
- OBJECTPROPERTY function
- schema-scoped objects [SQL Server]
- objects [SQL Server], schema-scoped
ms.assetid: 27569888-f8b5-4cec-a79f-6ea6d692b4ae
caps.latest.revision: 81
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0ee3350b200f0f42203a89d06ddb587b0792ee18
ms.contentlocale: it-it
ms.lasthandoff: 09/01/2017

---
# <a name="objectproperty-transact-sql"></a>OBJECTPROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Restituisce informazioni sugli oggetti con ambito schema nel database corrente. Per un elenco di oggetti con ambito schema, vedere [Sys. Objects &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md). Questa funzione non può essere utilizzata per gli oggetti che non sono definiti a livello di ambito schema, ad esempio i trigger DDL (Data Definition Language) e le notifiche di eventi.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
OBJECTPROPERTY ( id , property )   
```  
  
## <a name="arguments"></a>Argomenti  
 *id*  
 Espressione che rappresenta l'ID dell'oggetto nel database corrente. *ID* è **int** e si presuppone che sia un oggetto con ambito schema nel contesto del database corrente.  
  
 *proprietà*  
 È un'espressione che rappresenta le informazioni da restituire per l'oggetto specificato da *id*. *proprietà* può essere uno dei valori seguenti.  
  
> [!NOTE]  
>  Se non diversamente specificato, viene restituito NULL quando *proprietà* non è un nome di proprietà valido, *id* non è un ID di oggetto valido, *id* è un tipo di oggetto non supportato per l'oggetto specificato *proprietà*, oppure il chiamante non dispone dell'autorizzazione per visualizzare i metadati dell'oggetto.  
  
|Nome proprietà|Tipo oggetto|Descrizione e valori restituiti|  
|-------------------|-----------------|-------------------------------------|  
|CnstIsClustKey|Vincolo|Vincolo PRIMARY KEY con un indice cluster.<br /><br /> 1 = True<br /><br /> 0 = False|  
|CnstIsColumn|Vincolo|Vincolo CHECK, DEFAULT o FOREIGN KEY per una singola colonna.<br /><br /> 1 = True<br /><br /> 0 = False|  
|CnstIsDeleteCascade|Vincolo|Vincolo FOREIGN KEY con l'opzione ON DELETE CASCADE.<br /><br /> 1 = True<br /><br /> 0 = False|  
|CnstIsDisabled|Vincolo|Vincolo disabilitato.<br /><br /> 1 = True<br /><br /> 0 = False|  
|CnstIsNonclustKey|Vincolo|Vincolo PRIMARY KEY o UNIQUE con un indice non cluster.<br /><br /> 1 = True<br /><br /> 0 = False|  
|CnstIsNotRepl|Vincolo|Vincolo definito con le parole chiave NOT FOR REPLICATION.<br /><br /> 1 = True<br /><br /> 0 = False|  
|CnstIsNotTrusted|Vincolo|Vincolo abilitato senza alcuna verifica delle righe esistenti e che pertanto potrebbe non essere mantenuto attivo in tutte le righe.<br /><br /> 1 = True<br /><br /> 0 = False|  
|CnstIsUpdateCascade|Vincolo|Vincolo FOREIGN KEY con l'opzione ON UPDATE CASCADE.<br /><br /> 1 = True<br /><br /> 0 = False|  
|ExecIsAfterTrigger|Trigger|Trigger AFTER.<br /><br /> 1 = True<br /><br /> 0 = False|  
|ExecIsAnsiNullsOn|Funzione [!INCLUDE[tsql](../../includes/tsql-md.md)], procedura [!INCLUDE[tsql](../../includes/tsql-md.md)], trigger [!INCLUDE[tsql](../../includes/tsql-md.md)], vista|Impostazione di ANSI_NULLS in fase di creazione.<br /><br /> 1 = True<br /><br /> 0 = False|  
|ExecIsDeleteTrigger|Trigger|Trigger DELETE.<br /><br /> 1 = True<br /><br /> 0 = False|  
|ExecIsFirstDeleteTrigger|Trigger|Primo trigger attivato quando si esegue un'istruzione DELETE sulla tabella.<br /><br /> 1 = True<br /><br /> 0 = False|  
|ExecIsFirstInsertTrigger|Trigger|Primo trigger attivato quando si esegue un'istruzione INSERT sulla tabella.<br /><br /> 1 = True<br /><br /> 0 = False|  
|ExecIsFirstUpdateTrigger|Trigger|Primo trigger attivato quando si esegue un'istruzione UPDATE sulla tabella.<br /><br /> 1 = True<br /><br /> 0 = False|  
|ExecIsInsertTrigger|Trigger|Trigger INSERT.<br /><br /> 1 = True<br /><br /> 0 = False|  
|ExecIsInsteadOfTrigger|Trigger|Trigger INSTEAD OF.<br /><br /> 1 = True<br /><br /> 0 = False|  
|ExecIsLastDeleteTrigger|Trigger|Ultimo trigger attivato quando viene eseguita un'istruzione DELETE sulla tabella.<br /><br /> 1 = True<br /><br /> 0 = False|  
|ExecIsLastInsertTrigger|Trigger|Ultimo trigger attivato quando viene eseguita un'istruzione INSERT sulla tabella.<br /><br /> 1 = True<br /><br /> 0 = False|  
|ExecIsLastUpdateTrigger|Trigger|Ultimo trigger attivato quando viene eseguita un'istruzione UPDATE sulla tabella.<br /><br /> 1 = True<br /><br /> 0 = False|  
|ExecIsQuotedIdentOn|Funzione [!INCLUDE[tsql](../../includes/tsql-md.md)], procedura [!INCLUDE[tsql](../../includes/tsql-md.md)], trigger [!INCLUDE[tsql](../../includes/tsql-md.md)], vista|Impostazione di QUOTED_IDENTIFIER in fase di creazione.<br /><br /> 1 = True<br /><br /> 0 = False|  
|ExecIsStartup|Procedura|Procedura di avvio.<br /><br /> 1 = True<br /><br /> 0 = False|  
|ExecIsTriggerDisabled|Trigger|Trigger disabilitato.<br /><br /> 1 = True<br /><br /> 0 = False|  
|ExecIsTriggerNotForRepl|Trigger|Trigger definito come NOT FOR REPLICATION.<br /><br /> 1 = True<br /><br /> 0 = False|  
|ExecIsUpdateTrigger|Trigger|Trigger UPDATE.<br /><br /> 1 = True<br /><br /> 0 = False|  
|ExecIsWithNativeCompilation|Stored procedure [!INCLUDE[tsql](../../includes/tsql-md.md)]|**Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> La stored procedure è compilata in modo nativo.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo di dati di base: **int**|  
|HasAfterTrigger|Tabella, vista|Tabella o vista che include un trigger AFTER.<br /><br /> 1 = True<br /><br /> 0 = False|  
|HasDeleteTrigger|Tabella, vista|Tabella o vista che include un trigger DELETE.<br /><br /> 1 = True<br /><br /> 0 = False|  
|HasInsertTrigger|Tabella, vista|Tabella o vista che include un trigger INSERT.<br /><br /> 1 = True<br /><br /> 0 = False|  
|HasInsteadOfTrigger|Tabella, vista|Tabella o vista che include un trigger INSTEAD OF.<br /><br /> 1 = True<br /><br /> 0 = False|  
|HasUpdateTrigger|Tabella, vista|Tabella o vista che include un trigger UPDATE.<br /><br /> 1 = True<br /><br /> 0 = False|  
|IsAnsiNullsOn|Funzione [!INCLUDE[tsql](../../includes/tsql-md.md)], procedura [!INCLUDE[tsql](../../includes/tsql-md.md)], tabella, trigger [!INCLUDE[tsql](../../includes/tsql-md.md)], vista|L'opzione ANSI NULLS per la tabella è impostata su ON, ovvero tutti i confronti di un valore Null restituiscono UNKNOWN. Questa impostazione viene applicata a tutte le espressioni nella definizione di tabella, inclusi i vincoli e le colonne calcolate, per tutto il tempo in cui la tabella è disponibile.<br /><br /> 1 = True<br /><br /> 0 = False|  
|IsCheckCnst|Qualsiasi oggetto con ambito schema|Vincolo CHECK.<br /><br /> 1 = True<br /><br /> 0 = False|  
|IsConstraint|Qualsiasi oggetto con ambito schema|Vincolo CHECK, DEFAULT o FOREIGN KEY a colonna singola su una colonna o tabella.<br /><br /> 1 = True<br /><br /> 0 = False|  
|IsDefault|Qualsiasi oggetto con ambito schema|**Si applica a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Valore predefinito associato.<br /><br /> 1 = True<br /><br /> 0 = False|  
|IsDefaultCnst|Qualsiasi oggetto con ambito schema|Vincolo DEFAULT.<br /><br /> 1 = True<br /><br /> 0 = False|  
|IsDeterministic|Funzione, vista|Proprietà deterministica della funzione o della vista.<br /><br /> 1 = Deterministica<br /><br /> 0 = Non deterministica|  
|IsEncrypted|Funzione [!INCLUDE[tsql](../../includes/tsql-md.md)], procedura [!INCLUDE[tsql](../../includes/tsql-md.md)], tabella, trigger [!INCLUDE[tsql](../../includes/tsql-md.md)], vista|Indica che il testo originale dell'istruzione del modulo è stato convertito in un formato offuscato. L'output dell'offuscamento non è visibile direttamente nelle viste del catalogo in [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Gli utenti che non hanno accesso a tabelle di sistema o file del database non possono recuperare il testo offuscato. Tuttavia, il testo è disponibile agli utenti di accesso a tabelle di sistema tramite il [porta DAC](../../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md) o accesso diretto a file di database. Gli utenti in grado di collegare un debugger al processo del server possono inoltre recuperare la procedura originale dalla memoria in fase di esecuzione.<br /><br /> 1 = Crittografato<br /><br /> 0 = Non crittografato<br /><br /> Tipo di dati di base: **int**|  
|IsExecuted|Qualsiasi oggetto con ambito schema|L'oggetto può essere eseguito (vista, procedura, funzione o trigger).<br /><br /> 1 = True<br /><br /> 0 = False|  
|IsExtendedProc|Qualsiasi oggetto con ambito schema|Procedura estesa.<br /><br /> 1 = True<br /><br /> 0 = False|  
|IsForeignKey|Qualsiasi oggetto con ambito schema|Vincolo FOREIGN KEY.<br /><br /> 1 = True<br /><br /> 0 = False|  
|IsIndexed|Tabella, vista|Tabella o vista contenente un indice.<br /><br /> 1 = True<br /><br /> 0 = False|  
|IsIndexable|Tabella, vista|Tabella o vista in cui è possibile creare un indice.<br /><br /> 1 = True<br /><br /> 0 = False|  
|IsInlineFunction|Funzione|Funzione inline.<br /><br /> 1 = Funzione inline<br /><br /> 0 = Funzione non inline|  
|IsMSShipped|Qualsiasi oggetto con ambito schema|Oggetto creato durante l'installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> 1 = True<br /><br /> 0 = False|  
|IsPrimaryKey|Qualsiasi oggetto con ambito schema|Vincolo PRIMARY KEY.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> NULL = Non è una funzione oppure l'ID di oggetto non è valido.|  
|IsProcedure|Qualsiasi oggetto con ambito schema|Procedura.<br /><br /> 1 = True<br /><br /> 0 = False|  
|IsQuotedIdentOn|Funzione [!INCLUDE[tsql](../../includes/tsql-md.md)], procedura [!INCLUDE[tsql](../../includes/tsql-md.md)], tabella, trigger [!INCLUDE[tsql](../../includes/tsql-md.md)], vista, vincolo CHECK, definizione DEFAULT|L'identificatore tra virgolette per la tabella è impostato su ON, ovvero gli identificatori sono racchiusi tra virgolette doppie in tutte le espressioni alle quali viene fatto riferimento nella definizione dell'oggetto.<br /><br /> 1 = ON<br /><br /> 0 = OFF|  
|IsQueue|Qualsiasi oggetto con ambito schema|Coda di Service Broker.<br /><br /> 1 = True<br /><br /> 0 = False|  
|IsReplProc|Qualsiasi oggetto con ambito schema|Procedura di replica.<br /><br /> 1 = True<br /><br /> 0 = False|  
|IsRule|Qualsiasi oggetto con ambito schema|Regola associata.<br /><br /> 1 = True<br /><br /> 0 = False|  
|IsScalarFunction|Funzione|Funzione con valori scalari.<br /><br /> 1 = Funzione con valori scalari<br /><br /> 0 = Funzione senza valori scalari|  
|IsSchemaBound|Funzione, vista|Funzione o vista associata a schema creata con la clausola SCHEMABINDING.<br /><br /> 1 = Associata a uno schema<br /><br /> 0 = Non associata a uno schema|  
|IsSystemTable|Tabella|Tabella di sistema.<br /><br /> 1 = True<br /><br /> 0 = False|  
|IsTable|Tabella|Tabella.<br /><br /> 1 = True<br /><br /> 0 = False|  
|IsTableFunction|Funzione|Funzione con valori di tabella.<br /><br /> 1 = Funzione con valori di tabella<br /><br /> 0 = Funzione senza valori di tabella|  
|IsTrigger|Qualsiasi oggetto con ambito schema|Trigger.<br /><br /> 1 = True<br /><br /> 0 = False|  
|IsUniqueCnst|Qualsiasi oggetto con ambito schema|Vincolo UNIQUE.<br /><br /> 1 = True<br /><br /> 0 = False|  
|IsUserTable|Tabella|Tabella definita dall'utente.<br /><br /> 1 = True<br /><br /> 0 = False|  
|IsView|Visualizza|Vista.<br /><br /> 1 = True<br /><br /> 0 = False|  
|OwnerId|Qualsiasi oggetto con ambito schema|Proprietario dell'oggetto.<br /><br /> **Nota:** proprietario dello schema non è necessariamente il proprietario dell'oggetto. Ad esempio, gli oggetti figlio (quelli che *parent_object_id* è diverso da null) restituirà sempre lo stesso ID proprietario dell'elemento padre.<br /><br /> Valore non Null = ID utente del database per il proprietario dell'oggetto.|  
|TableDeleteTrigger|Tabella|La tabella include un trigger DELETE.<br /><br /> >1 = ID del primo trigger del tipo specificato.|  
|TableDeleteTriggerCount|Tabella|La tabella include il numero di trigger DELETE specificato.<br /><br /> >0 = Numero di trigger DELETE.|  
|TableFullTextMergeStatus|Tabella|**Si applica a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Indica se una tabella dispone di un indice full-text su cui è attualmente in corso un'operazione di unione.<br /><br /> 0 = La tabella non dispone di un indice full-text o sull'indice full-text non è in corso un'operazione di unione.<br /><br /> 1 = Sull'indice full-text è in corso un'operazione di unione.|  
|TableFullTextBackgroundUpdateIndexOn|Tabella|**Si applica a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Nella tabella è abilitato l'indice full-text ad aggiornamento in background (rilevamento automatico delle modifiche).<br /><br /> 1 = TRUE<br /><br /> 0 = FALSE|  
|TableFulltextCatalogId|Tabella|**Si applica a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> ID del catalogo full-text contenente i dati dell'indice full-text per la tabella.<br /><br /> Valore diverso da zero = ID del catalogo full-text associato all'indice univoco che identifica le righe di una tabella con indicizzazione full-text.<br /><br /> 0 = La tabella non include un indice full-text.|  
|TableFulltextChangeTrackingOn|Tabella|**Si applica a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Nella tabella è abilitato il rilevamento delle modifiche full-text.<br /><br /> 1 = TRUE<br /><br /> 0 = FALSE|  
|TableFulltextDocsProcessed|Tabella|**Si applica a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Numero di righe elaborate dopo l'avvio dell'indicizzazione full-text. In una tabella sottoposta a indicizzazione ai fini della ricerca full-text tutte le colonne di una riga vengono considerate come appartenenti a un unico documento da indicizzare.<br /><br /> 0 = Nessuna ricerca per indicizzazione attiva oppure l'indicizzazione full-text è stata completata.<br /><br /> > 0 = uno dei seguenti (A o B): A) il numero di documenti elaborati da inserire o aggiornare operazioni dopo l'avvio completo, incrementale o manuale popolamento con rilevamento delle. B) il numero di righe elaborate da insert o operazioni di aggiornamento dopo l'attivazione di rilevamento con popolamento dell'indice di aggiornamento in background, modificare lo schema di indice full-text, il ricompilazione del catalogo full-text o l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] riavviate e così via.<br /><br /> NULL = La tabella non include un indice full-text.<br /><br /> Questa proprietà non monitora né conta le righe eliminate.|  
|TableFulltextFailCount|Tabella|**Si applica a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Numero di righe non indicizzate dalla ricerca full-text.<br /><br /> 0 = Popolamento completato.<br /><br /> > 0 = uno dei seguenti (A o B): A) il numero di documenti non indicizzati dopo l'avvio del popolamento di rilevamento delle modifiche completo, incrementale e aggiornamento manuale. B) di rilevamento delle modifiche con sfondo aggiornare l'indice, il numero di righe che non indicizzati dopo l'inizio della popolazione o il riavvio della popolazione. Questa situazione può essere dovuta a una modifica dello schema, alla ricompilazione del catalogo, al riavvio del server e così via.<br /><br /> NULL = La tabella non include un indice full-text.|  
|TableFulltextItemCount|Tabella|**Si applica a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Numero di righe per cui l'indicizzazione full-text ha avuto esito positivo.|  
|TableFulltextKeyColumn|Tabella|**Si applica a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> ID della colonna associata all'indice univoco a colonna singola a cui viene fatto riferimento nella definizione dell'indice full-text.<br /><br /> 0 = La tabella non include un indice full-text.|  
|TableFulltextPendingChanges|Tabella|**Si applica a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Numero di voci in sospeso del rilevamento delle modifiche da elaborare.<br /><br /> 0 = Il rilevamento delle modifiche non è abilitato.<br /><br /> NULL = La tabella non include un indice full-text.|  
|TableFulltextPopulateStatus|Tabella|**Si applica a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> 0 = Inattivo<br /><br /> 1 = Popolamento completo in corso.<br /><br /> 2 = Popolamento incrementale in corso.<br /><br /> 3 = Propagazione delle modifiche rilevate in corso.<br /><br /> 4 = Operazione in corso per l'indice ad aggiornamento in background, ad esempio il rilevamento automatico delle modifiche.<br /><br /> 5 = Indicizzazione full-text rallentata o sospesa.|  
|TableHasActiveFulltextIndex|Tabella|**Si applica a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> La tabella include un indice full-text attivo.<br /><br /> 1 = True<br /><br /> 0 = False|  
|TableHasCheckCnst|Tabella|La tabella include un vincolo CHECK.<br /><br /> 1 = True<br /><br /> 0 = False|  
|TableHasClustIndex|Tabella|La tabella include un indice cluster.<br /><br /> 1 = True<br /><br /> 0 = False|  
|TableHasDefaultCnst|Tabella|La tabella include un vincolo DEFAULT.<br /><br /> 1 = True<br /><br /> 0 = False|  
|TableHasDeleteTrigger|Tabella|La tabella include un trigger DELETE.<br /><br /> 1 = True<br /><br /> 0 = False|  
|TableHasForeignKey|Tabella|La tabella include un vincolo FOREIGN KEY.<br /><br /> 1 = True<br /><br /> 0 = False|  
|TableHasForeignRef|Tabella|Un vincolo FOREIGN KEY fa riferimento alla tabella.<br /><br /> 1 = True<br /><br /> 0 = False|  
|TableHasIdentity|Tabella|La tabella include una colonna Identity.<br /><br /> 1 = True<br /><br /> 0 = False|  
|TableHasIndex|Tabella|La tabella include un indice di qualsiasi tipo.<br /><br /> 1 = True<br /><br /> 0 = False|  
|TableHasInsertTrigger|Tabella|L'oggetto include un trigger INSERT.<br /><br /> 1 = True<br /><br /> 0 = False|  
|TableHasNonclustIndex|Tabella|La tabella include un indice non cluster.<br /><br /> 1 = True<br /><br /> 0 = False|  
|TableHasPrimaryKey|Tabella|La tabella include una chiave primaria.<br /><br /> 1 = True<br /><br /> 0 = False|  
|TableHasRowGuidCol|Tabella|Tabella include un ROWGUIDCOL per una **uniqueidentifier** colonna.<br /><br /> 1 = True<br /><br /> 0 = False|  
|TableHasTextImage|Tabella|Tabella include un **testo**, **ntext**, o **immagine** colonna.<br /><br /> 1 = True<br /><br /> 0 = False|  
|TableHasTimestamp|Tabella|Tabella include un **timestamp** colonna.<br /><br /> 1 = True<br /><br /> 0 = False|  
|TableHasUniqueCnst|Tabella|La tabella include un vincolo UNIQUE.<br /><br /> 1 = True<br /><br /> 0 = False|  
|TableHasUpdateTrigger|Tabella|L'oggetto include un trigger UPDATE.<br /><br /> 1 = True<br /><br /> 0 = False|  
|TableHasVarDecimalStorageFormat|Tabella|Tabella è abilitata per **vardecimal** il formato di archiviazione.<br /><br /> 1 = True<br /><br /> 0 = False|  
|TableInsertTrigger|Tabella|La tabella include un trigger INSERT.<br /><br /> >1 = ID del primo trigger del tipo specificato.|  
|TableInsertTriggerCount|Tabella|La tabella include il numero specificato di trigger INSERT.<br /><br /> >0 = Numero di trigger INSERT.|  
|TableIsFake|Tabella|La tabella non è reale, ma viene creata internamente su richiesta da [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].<br /><br /> 1 = True<br /><br /> 0 = False|  
|TableIsLockedOnBulkLoad|Tabella|Nella tabella è bloccata a causa di un **bcp** o BULK INSERT.<br /><br /> 1 = True<br /><br /> 0 = False|  
|TableIsMemoryOptimized|Tabella|**Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> La tabella prevede l'ottimizzazione per la memoria<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo di dati di base: **int**<br /><br /> Per altre informazioni, vedere [OLTP in memoria &#40;ottimizzazione in memoria&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md).|  
|TableIsPinned|Tabella|La tabella è bloccata per essere mantenuta nella cache dei dati.<br /><br /> 0 = False<br /><br /> Questa funzionalità non è supportata in [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versioni successive.|  
|TableTextInRowLimit|Tabella|Numero massimo di byte consentito per l'opzione text in row.<br /><br /> 0 se l'opzione text in row non è impostata.|  
|TableUpdateTrigger|Tabella|La tabella include un trigger UPDATE.<br /><br /> > 1 = ID del primo trigger del tipo specificato.|  
|TableUpdateTriggerCount|Tabella|La tabella include il numero specificato di trigger UPDATE.<br /><br /> > 0 = Numero di trigger UPDATE.|  
|TableHasColumnSet|Tabella|Indica se la tabella include un set di colonne.<br /><br /> 0 = False<br /><br /> 1 = True<br /><br /> Per altre informazioni, vedere [Usare set di colonne](../../relational-databases/tables/use-column-sets.md).|  
|TableTemporalType|Tabella|**Si applica a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Specifica il tipo di tabella.<br /><br /> 0 = la tabella non temporale<br /><br /> 1 = la tabella di cronologia per la tabella con controllo delle versioni del sistema<br /><br /> 2 = tabella temporale con controllo delle versioni del sistema|  
  
## <a name="return-types"></a>Tipi restituiti  
 **int**  
  
## <a name="exceptions"></a>Eccezioni  
 Restituisce NULL in caso di errore o se un chiamante non dispone dell'autorizzazione necessaria per visualizzare l'oggetto.  
  
 Un utente può visualizzare esclusivamente i metadati delle entità a sicurezza diretta di cui è proprietario o per cui ha ricevuto un'autorizzazione. Di conseguenza, le funzioni predefinite di creazione dei metadati come OBJECTPROPERTY possono restituire NULL se l'utente non dispone di alcuna autorizzazione per l'oggetto. Per altre informazioni, vedere [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="remarks"></a>Osservazioni  
 Il [!INCLUDE[ssDE](../../includes/ssde-md.md)] si presuppone che *object_id* è nel contesto del database corrente. Una query che fa riferimento a un *object_id* in un altro database restituisce NULL oppure risultati errati. Ad esempio, nella query seguente il contesto del database corrente è il database master. Il [!INCLUDE[ssDE](../../includes/ssde-md.md)] tenterà di restituire il valore della proprietà per l'oggetto specificato *object_id* in tale database anziché il database specificato nella query. La query restituisce risultati non corretti perché la vista `vEmployee` non è presente nel database master.  
  
```  
USE master;  
GO  
SELECT OBJECTPROPERTY(OBJECT_ID(N'AdventureWorks2012.HumanResources.vEmployee'), 'IsView');  
GO  
```  
  
 OBJECTPROPERTY (*view_id*, 'IsIndexable') può richiedere risorse significative computer perché la valutazione della proprietà IsIndexable richiede l'analisi della definizione della vista, della normalizzazione e ottimizzazione parziale. Sebbene la proprietà IsIndexable identifichi tabelle o viste che è possibile indicizzare, la creazione effettiva dell'indice può avere esito negativo se non vengono soddisfatti determinati requisiti riguardanti la chiave di indice. Per altre informazioni, vedere [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md).  
  
 OBJECTPROPERTY (*table_id*, 'TableHasActiveFulltextIndex') restituirà il valore 1 (true) quando almeno una colonna di una tabella viene aggiunta per l'indicizzazione. L'indicizzazione full-text risulta attiva per il popolamento non appena viene aggiunta la prima colonna per l'indicizzazione.  
  
 Durante la creazione di una tabella, l'opzione QUOTED IDENTIFIER viene sempre archiviata con l'impostazione ON nei metadati della tabella, anche se l'opzione viene impostata su OFF quando si crea la tabella. Pertanto, OBJECTPROPERTY (*table_id*, 'IsQuotedIdentOn') restituirà sempre un valore pari a 1 (true).  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-verifying-that-an-object-is-a-table"></a>A. Verifica che un oggetto sia una tabella  
 Nell'esempio seguente viene verificato se `UnitMeasure` è una tabella nel database [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
```  
USE AdventureWorks2012;  
GO  
IF OBJECTPROPERTY (OBJECT_ID(N'Production.UnitMeasure'),'ISTABLE') = 1  
   PRINT 'UnitMeasure is a table.'  
ELSE IF OBJECTPROPERTY (OBJECT_ID(N'Production.UnitMeasure'),'ISTABLE') = 0  
   PRINT 'UnitMeasure is not a table.'  
ELSE IF OBJECTPROPERTY (OBJECT_ID(N'Production.UnitMeasure'),'ISTABLE') IS NULL  
   PRINT 'ERROR: UnitMeasure is not a valid object.';  
GO  
  
```  
  
### <a name="b-verifying-that-a-scalar-valued-user-defined-function-is-deterministic"></a>B. Verifica che una funzione a valori scalari definita dall'utente sia deterministica  
 Nell'esempio seguente viene verificato se la funzione a valori scalari definita dall'utente `ufnGetProductDealerPrice`, che restituisce un **money** valore, è deterministica.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT OBJECTPROPERTY(OBJECT_ID('dbo.ufnGetProductDealerPrice'), 'IsDeterministic');  
GO  
```  
  
 Il set di risultati indica che `ufnGetProductDealerPrice` non è una funzione deterministica.  
  
 `-----`  
  
 `0`  
  
### <a name="c-finding-the-objects-that-belong-to-a-specific-schema"></a>C. Ricerca di oggetti appartenenti a uno schema specifico  
 Nell'esempio seguente viene utilizzata la proprietà `SchemaId` per restituire tutti gli oggetti che appartengono allo schema `Production`.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT name, object_id, type_desc  
FROM sys.objects   
WHERE OBJECTPROPERTY(object_id, N'SchemaId') = SCHEMA_ID(N'Production')  
ORDER BY type_desc, name;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Esempi: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="d-verifying-that-an-object-is-a-table"></a>Unità d: verifica che un oggetto è una tabella  
 Nell'esempio seguente viene verificato se `dbo.DimReseller` è una tabella nel database [!INCLUDE[ssawPDW](../../includes/ssawpdw-md.md)].  
  
```  
-- Uses AdventureWorks  
  
IF OBJECTPROPERTY (OBJECT_ID(N'dbo.DimReseller'),'ISTABLE') = 1  
   SELECT 'DimReseller is a table.'  
ELSE   
   SELECT 'DimReseller is not a table.';  
GO  
```  
  
### <a name="e-finding-the-tables-that-belong-to-a-specific-schema"></a>E: le tabelle che appartengono a uno schema specifico di ricerca  
 L'esempio seguente restituisce tutte le tabelle nello schema dbo.  
  
```  
-- Uses AdventureWorks  
  
SELECT name, object_id, type_desc  
FROM sys.objects   
WHERE OBJECTPROPERTY(object_id, N'SchemaId') = SCHEMA_ID(N'dbo')  
ORDER BY type_desc, name;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [COLUMNPROPERTY &#40; Transact-SQL &#41;](../../t-sql/functions/columnproperty-transact-sql.md)   
 [Funzioni per i metadati &#40; Transact-SQL &#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [OBJECTPROPERTYEX &#40; Transact-SQL &#41;](../../t-sql/functions/objectpropertyex-transact-sql.md)   
 [AUTORIZZAZIONE ALTER &#40; Transact-SQL &#41;](../../t-sql/statements/alter-authorization-transact-sql.md)   
 [TYPEPROPERTY &#40; Transact-SQL &#41;](../../t-sql/functions/typeproperty-transact-sql.md)   
 [Sys. Objects &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)  
  
  

