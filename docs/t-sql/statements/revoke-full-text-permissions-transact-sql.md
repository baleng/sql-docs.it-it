---
title: REVOCARE le autorizzazioni Full-Text (Transact-SQL) | Documenti Microsoft
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- REVOKE statement, full-text permissions
- full-text catalogs [SQL Server], permissions
- full-text stoplist [SQL Server], permissions
ms.assetid: ef617436-1e86-4573-900a-702e27a202b9
caps.latest.revision: 27
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 33348a7ee48835021143507175165b27fde4b74a
ms.contentlocale: it-it
ms.lasthandoff: 09/01/2017

---
# <a name="revoke-full-text-permissions-transact-sql"></a>REVOKE - autorizzazioni per il catalogo full-text (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Revoca le autorizzazioni per un catalogo full-text o un elenco di parole non significative full-text.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
REVOKE [ GRANT OPTION FOR ] permission [ ,...n ] ON  
    FULLTEXT   
        {  
           CATALOG :: full-text_catalog_name  
           |  
           STOPLIST :: full-text_stoplist_name  
        }  
    { TO | FROM } database_principal [ ,...n ]  
    [ CASCADE ]  
    [ AS revoking_principal ]  
```  
  
## <a name="arguments"></a>Argomenti  
 GRANT OPTION FOR  
 Indica che verrà revocato il diritto di concedere l'autorizzazione specificata ad altre entità. L'autorizzazione stessa non verrà revocata.  
  
> [!IMPORTANT]  
>  Se l'autorizzazione specificata è stata concessa all'entità senza l'opzione GRANT, l'autorizzazione stessa verrà revocata.  
  
 *autorizzazione*  
 Nome di un'autorizzazione. I mapping validi tra le autorizzazioni e le entità a protezione diretta sono descritti nella sezione "Osservazioni" più avanti in questo argomento.  
  
 NEL catalogo full-text **::***full text_catalog_name*  
 Specifica il catalogo full-text per cui viene revocata l'autorizzazione. Il qualificatore di ambito **::** è obbligatorio.  
  
 IN FULLTEXT STOPLIST **::***full text_stoplist_name*  
 Specifica l'elenco di parole non significative full-text per cui viene revocata l'autorizzazione. Il qualificatore di ambito **::** è obbligatorio.  
  
 *database_principal*  
 Specifica l'entità da cui viene revocata l'autorizzazione. I tipi validi sono:  
  
-   utente del database  
  
-   ruolo del database  
  
-   ruolo dell'applicazione  
  
-   utente del database sul quale viene eseguito il mapping a un account di accesso di Windows  
  
-   utente del database sul quale viene eseguito il mapping a un gruppo di Windows  
  
-   utente del database sul quale viene eseguito il mapping a un certificato  
  
-   utente del database mappato a una chiave asimmetrica  
  
-   utente del database non mappato ad alcuna entità server.  
  
 CASCADE  
 Indica che l'autorizzazione che viene revocata viene revocata anche ad altre entità a cui è stata concessa da questa entità.  
  
> [!CAUTION]  
>  La revoca propagata di un'autorizzazione concessa con WITH GRANT OPTION comporterà la revoca sia delle autorizzazioni GRANT che delle autorizzazioni DENY per tale autorizzazione.  
  
 AS *revoking_principal*  
 Specifica un'entità dalla quale l'entità che esegue la query ottiene il diritto di revocare l'autorizzazione. I tipi validi sono:  
  
-   utente del database  
  
-   ruolo del database  
  
-   ruolo dell'applicazione  
  
-   utente del database sul quale viene eseguito il mapping a un account di accesso di Windows  
  
-   utente del database sul quale viene eseguito il mapping a un gruppo di Windows  
  
-   utente del database sul quale viene eseguito il mapping a un certificato  
  
-   utente del database mappato a una chiave asimmetrica  
  
-   utente del database non mappato ad alcuna entità server.  
  
## <a name="remarks"></a>Osservazioni  
  
## <a name="fulltext-catalog-permissions"></a>Autorizzazioni FULLTEXT CATALOG  
 Un catalogo full-text è un'entità a protezione diretta a livello di database contenuta nel database padre nella gerarchia delle autorizzazioni. Nella tabella seguente sono elencate le autorizzazioni più specifiche e limitate che è possibile revocare per un catalogo full-text, insieme alle autorizzazioni più generali che le includono in modo implicito.  
  
|Autorizzazione del catalogo full-text|Autorizzazione del catalogo full-text in cui è inclusa|Autorizzazione del database in cui è inclusa|  
|-----------------------------------|----------------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY FULLTEXT CATALOG|  
|REFERENCES|CONTROL|REFERENCES|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="fulltext-stoplist-permissions"></a>Autorizzazioni FULLTEXT STOPLIST  
 Un elenco di parole non significative full-text è un'entità a protezione diretta a livello di database contenuta nel database padre nella gerarchia delle autorizzazioni. Nella tabella seguente sono elencate le autorizzazioni più specifiche e limitate che è possibile revocare per un elenco di parole non significative full-text, insieme alle autorizzazioni più generali che le includono in modo implicito.  
  
|Autorizzazione dell'elenco di parole non significative full-text|Autorizzazione dell'elenco di parole non significative full-text in cui è inclusa|Autorizzazione del database in cui è inclusa|  
|------------------------------------|-----------------------------------------------|------------------------------------|  
|ALTER|CONTROL|ALTER ANY FULLTEXT CATALOG|  
|CONTROL|CONTROL|CONTROL|  
|REFERENCES|CONTROL|REFERENCES|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'autorizzazione CONTROL per il catalogo full-text.  
  
## <a name="see-also"></a>Vedere anche  
 [CREATE APPLICATION ROLE &#40; Transact-SQL &#41;](../../t-sql/statements/create-application-role-transact-sql.md)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)   
 [CREARE il catalogo full-text &#40; Transact-SQL &#41;](../../t-sql/statements/create-fulltext-catalog-transact-sql.md)   
 [CREATE FULLTEXT STOPLIST &#40; Transact-SQL &#41;](../../t-sql/statements/create-fulltext-stoplist-transact-sql.md)   
 [Gerarchia di crittografia](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [fn_my_permissions &#40; Transact-SQL &#41;](../../relational-databases/system-functions/sys-fn-my-permissions-transact-sql.md)   
 [Autorizzazioni GRANT Full-Text &#40; Transact-SQL &#41;](../../t-sql/statements/grant-full-text-permissions-transact-sql.md)   
 [HAS_PERMS_BY_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/has-perms-by-name-transact-sql.md)   
 [Autorizzazioni &#40;motore di database&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [Entità &#40;motore di database&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [REVOKE &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-transact-sql.md)   
 [sys.fn_builtin_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-builtin-permissions-transact-sql.md)   
 [Sys. fulltext_catalogs &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-fulltext-catalogs-transact-sql.md)   
 [sys.fulltext_stoplists &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-stoplists-transact-sql.md)  
  
  
