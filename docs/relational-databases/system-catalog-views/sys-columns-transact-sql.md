---
title: Sys. Columns (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/21/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.columns_TSQL
- sys.columns
- columns_TSQL
- columns
dev_langs:
- TSQL
helpviewer_keywords:
- sys.columns catalog view
ms.assetid: 323ac9ea-fc52-4b8c-8a7e-e0e44f8ed86c
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 40209fae182a31a701fe1a8ccad0149cc66dff58
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/15/2018
ms.locfileid: "51681299"
---
# <a name="syscolumns-transact-sql"></a>sys.columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Restituisce una riga per ogni colonna di un oggetto contenente colonne, ad esempio viste o tabelle. Nell'elenco seguente sono inclusi i tipi di oggetti contenenti colonne.  
  
-   Funzioni assembly con valori di tabella (FT)  
  
-   Funzioni SQL inline con valori di tabella (IF)  
  
-   Tabelle interne (IT)  
  
-   Tabelle di sistema (S)  
  
-   Funzioni SQL con valori di tabella (TF)  
  
-   Tabelle utente (U)  
  
-   Viste (V)  
  
|Nome colonna|Tipo di dati|Description|  
|-----------------|---------------|-----------------|  
|object_id|**int**|ID dell'oggetto a cui appartiene la colonna.|  
|NAME|**sysname**|Nome della colonna. Valore univoco all'interno dell'oggetto.|  
|column_id|**int**|ID della colonna. Valore univoco all'interno dell'oggetto.<br /><br /> È possibile che gli ID di colonna non siano sequenziali.|  
|system_type_id|**tinyint**|ID del tipo di sistema della colonna.|  
|user_type_id|**int**|ID del tipo di colonna definito dall'utente.<br /><br /> Per restituire il nome del tipo, aggiungere il [Sys. Types](../../relational-databases/system-catalog-views/sys-types-transact-sql.md) su questa colonna vista del catalogo.|  
|max_length|**smallint**|Lunghezza massima in byte della colonna.<br /><br /> -1 = il tipo di dati della colonna **varchar (max)**, **nvarchar (max)**, **varbinary (max)**, oppure **xml**.<br /><br /> Per la **testo** colonne, il valore max_length sarà 16 o il valore impostato dall'opzione 'text in row' di sp_tableoption.|  
|precisione|**tinyint**|Precisione della colonna se la colonna è di tipo numerico. In caso contrario, 0.|  
|scala|**tinyint**|Scala della colonna se di tipo numerico, altrimenti 0.|  
|collation_name|**sysname**|Nome delle regole di confronto della colonna se la colonna è di tipo carattere. In caso contrario, NULL.|  
|is_nullable|**bit**|1 = La colonna ammette valori Null.|  
|is_ansi_padded|**bit**|1 = La colonna utilizza l'opzione ANSI_PADDING ON se è di tipo carattere, binary o variant.<br /><br /> 0 = La colonna non è di tipo carattere, binary o variant.|  
|is_rowguidcol|**bit**|1 = La colonna è una parola chiave ROWGUIDCOL dichiarata.|  
|is_identity|**bit**|1 = La colonna ha valori Identity|  
|is_computed|**bit**|1 = La colonna è una colonna calcolata.|  
|is_filestream|**bit**|1 = la colonna è una colonna FILESTREAM.|  
|is_replicated|**bit**|1 = La colonna viene replicata.|  
|is_non_sql_subscribed|**bit**|1 = la colonna ha un Sottoscrittore non SQL Server.|  
|is_merge_published|**bit**|1 = La colonna è inclusa in una pubblicazione di tipo merge.|  
|is_dts_replicated|**bit**|1 = La colonna viene replicata tramite [!INCLUDE[ssIS](../../includes/ssis-md.md)].|  
|is_xml_document|**bit**|1 = Il contenuto è un documento XML completo.<br /><br /> 0 = il contenuto è un frammento di documento o il tipo di dati di colonna non è **xml**.|  
|xml_collection_id|**int**|Diverso da zero se il tipo di dati della colonna **xml** e XML è tipizzato. Il valore sarà l'ID della raccolta che include lo spazio dei nomi dell'XML Schema di convalida della colonna.<br /><br /> 0 = Nessuna raccolta di XML Schema.|  
|default_object_id|**int**|ID dell'oggetto predefinito, indipendentemente dal tipo di un oggetto autonomo [Sys. sp_bindefault](../../relational-databases/system-stored-procedures/sp-bindefault-transact-sql.md), o un vincolo DEFAULT a livello di colonna inline. La colonna parent_object_id di un oggetto predefinito inline a livello di colonna è un riferimento alla tabella stessa.<br /><br /> 0 = nessun valore predefinito.|  
|rule_object_id|**int**|ID della regola autonoma associata alla colonna tramite sys.sp_bindrule.<br /><br /> 0 = Nessuna regola autonoma. Per i vincoli CHECK a livello di colonna, vedere [Sys. check_constraints &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-check-constraints-transact-sql.md).|  
|is_sparse|**bit**|1 = La colonna è di tipo sparse. Per altre informazioni, vedere [Usare le colonne di tipo sparse](../../relational-databases/tables/use-sparse-columns.md).|  
|is_column_set|**bit**|1 = La colonna è un set di colonne. Per altre informazioni, vedere [Usare le colonne di tipo sparse](../../relational-databases/tables/use-sparse-columns.md).|  
|generated_always_type|**tinyint**|**Si applica a**: da [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)].<br /><br /> Identifica quando viene generato il valore della colonna (sarà sempre 0 per le colonne nelle tabelle di sistema):<br /><br /> 0 = NOT_APPLICABLE<br /><br /> 1 = AS_ROW_START<br /><br /> 2 = AS_ROW_END<br /><br /> Per altre informazioni, vedere [tabelle temporali &#40;database relazionali&#41;](../../relational-databases/tables/temporal-tables.md).|  
|generated_always_type_desc|**nvarchar(60)**|**Si applica a**: da [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)].<br /><br /> Descrizione testuale del `generated_always_type`del valore (sempre NOT_APPLICABLE per le colonne nelle tabelle di sistema) <br /><br /> NOT_APPLICABLE<br /><br /> AS_ROW_START<br /><br /> AS_ROW_END|  
|encryption_type|**int**|**Si applica a**: da [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)].<br /><br /> Tipo di crittografia:<br /><br /> 1 = la crittografia deterministica<br /><br /> 2 = crittografia casuale|  
|encryption_type_desc|**nvarchar(64)**|**Si applica a**: da [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)].<br /><br /> Descrizione del tipo di crittografia:<br /><br /> CASUALE<br /><br /> DETERMINISTIC|  
|encryption_algorithm_name|**sysname**|**Si applica a**: da [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)].<br /><br /> Nome dell'algoritmo di crittografia.<br /><br /> È supportato solo AEAD_AES_256_CBC_HMAC_SHA_512.|  
|column_encryption_key_id|**int**|**Si applica a**: da [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)].<br /><br /> ID della chiave CEK.|  
|column_encryption_key_database_name|**sysname**|**Si applica a**: da [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDW_md](../../includes/sssds-md.md)].<br /><br /> Il nome del database in cui è presente la chiave di crittografia della colonna se diverso da quello del database della colonna. NULL se la chiave non esiste nello stesso database della colonna.|  
|is_hidden|**bit**|**Si applica a**: da [!INCLUDE[ssCurrentLong](../../includes/sscurrent-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)].<br /><br /> Indica se la colonna è nascosta:<br /><br /> 0 = la colonna regolare, non-nascosto, visibile<br /><br /> 1 = colonna nascosta|  
|is_masked|**bit**|**Si applica a**: da [!INCLUDE[ssCurrentLong](../../includes/sscurrent-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)].<br /><br /> Indica se la colonna è nascosta da una maschera dati dinamica:<br /><br /> 0 = la colonna regolare, non filtrato<br /><br /> 1 = colonna è nascosta|  


 
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Per altre informazioni, vedere [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Viste di sistema &#40;Transact-SQL&#41;](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [Viste del catalogo dell'oggetto &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Viste del catalogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [L'esecuzione di query nel catalogo di sistema SQL Server domande frequenti](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [sys.all_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-all-columns-transact-sql.md)   
 [Sys.system_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-system-columns-transact-sql.md)  
  
  
