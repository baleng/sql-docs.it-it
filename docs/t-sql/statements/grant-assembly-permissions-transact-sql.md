---
title: GRANT - autorizzazioni per assembly (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/12/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- granting permissions [SQL Server], assemblies
- assemblies [CLR integration], permissions
- GRANT statement, assemblies
ms.assetid: dce1e027-f859-4967-bdda-16a95ae460d0
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 6d5c434bc9bc73b58b9b7f2cc59d32f413eef8f9
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52528998"
---
# <a name="grant-assembly-permissions-transact-sql"></a>GRANT - autorizzazioni per assembly (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Concede le autorizzazioni per un assembly.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
GRANT { permission [ ,...n ] } ON ASSEMBLY :: assembly_name  
    TO database_principal [ ,...n ]  
    [ WITH GRANT OPTION ]  
    [ AS granting_principal ]  
```  
  
## <a name="arguments"></a>Argomenti  
 *permission*  
 Specifica un'autorizzazione che può essere concessa per un assembly. Vedere l'elenco riportato di seguito.  
  
 ON ASSEMBLY **::**_assembly_name_  
 Specifica l'assembly per cui vengono concesse le autorizzazioni. Il qualificatore di ambito "::" è obbligatorio.  
  
 *database_principal*  
 Specifica l'entità a cui viene concessa l'autorizzazione. I tipi validi sono:  
  
-   utente del database  
-   ruolo del database  
-   ruolo dell'applicazione  
-   utente del database sul quale viene eseguito il mapping a un account di accesso di Windows  
-   utente del database sul quale viene eseguito il mapping a un gruppo di Windows  
-   utente del database sul quale viene eseguito il mapping a un certificato  
-   utente del database mappato a una chiave asimmetrica  
-   utente del database non mappato ad alcuna entità server.  
  
GRANT OPTION  
 Indica che l'entità potrà inoltre concedere l'autorizzazione specificata ad altre entità.  
  
AS *granting_principal*  
 Specifica un'entità dalla quale l'entità che esegue la query ottiene il diritto di concedere l'autorizzazione. I tipi validi sono:  
  
-   utente del database  
-   ruolo del database  
-   ruolo dell'applicazione  
-   utente del database sul quale viene eseguito il mapping a un account di accesso di Windows  
-   utente del database sul quale viene eseguito il mapping a un gruppo di Windows  
-   utente del database sul quale viene eseguito il mapping a un certificato  
-   utente del database mappato a una chiave asimmetrica  
-   utente del database non mappato ad alcuna entità server.  
  
## <a name="remarks"></a>Remarks  
 Un assembly è un'entità a protezione diretta a livello di database contenuta nel database padre nella gerarchia delle autorizzazioni. Di seguito sono elencate le autorizzazioni più specifiche e limitate che è possibile concedere per un assembly, insieme alle autorizzazioni più generali che le includono in modo implicito.  
  
|Autorizzazione dell'assembly|Autorizzazione dell'assembly in cui è inclusa|Autorizzazione del database in cui è inclusa|  
|-------------------------|------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY ASSEMBLY|  
|REFERENCES|CONTROL|REFERENCES|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="permissions"></a>Permissions  
 L'utente che concede le autorizzazioni (o l'entità specificata con l'opzione AS) deve disporre della relativa autorizzazione con GRANT OPTION oppure di un'autorizzazione di livello superiore che include l'autorizzazione che viene concessa.  
  
 Se si usano l'opzione AS, sono previsti questi requisiti aggiuntivi.  
  
|AS *granting_principal*|Autorizzazione aggiuntiva necessaria|  
|------------------------------|------------------------------------|  
|Utente del database|Autorizzazione IMPERSONATE per l'utente, appartenenza al ruolo predefinito del database **db_securityadmin**, appartenenza al ruolo predefinito del database **db_owner** o appartenenza al ruolo predefinito del server **sysadmin**.|  
|Utente del database di cui è stato eseguito il mapping a un account di accesso di Windows|Autorizzazione IMPERSONATE per l'utente, appartenenza al ruolo predefinito del database **db_securityadmin**, appartenenza al ruolo predefinito del database **db_owner** o appartenenza al ruolo predefinito del server **sysadmin**.|  
|Utente del database di cui è stato eseguito il mapping a un gruppo di Windows|Appartenenza al gruppo di Windows, appartenenza al ruolo predefinito del database **db_securityadmin**, appartenenza al ruolo predefinito del database **db_owner** o appartenenza al ruolo predefinito del server **sysadmin**.|  
|Utente del database di cui è stato eseguito il mapping a un certificato|Appartenenza al ruolo predefinito del database **db_securityadmin**, appartenenza al ruolo predefinito del database **db_owner** o appartenenza al ruolo predefinito del server **sysadmin**.|  
|Utente del database di cui è stato eseguito il mapping a una chiave asimmetrica|Appartenenza al ruolo predefinito del database **db_securityadmin**, appartenenza al ruolo predefinito del database **db_owner** o appartenenza al ruolo predefinito del server **sysadmin**.|  
|Utente del database di cui non è stato eseguito il mapping ad alcuna entità server|Autorizzazione IMPERSONATE per l'utente, appartenenza al ruolo predefinito del database **db_securityadmin**, appartenenza al ruolo predefinito del database **db_owner** o appartenenza al ruolo predefinito del server **sysadmin**.|  
|Ruolo del database|Autorizzazione ALTER per il ruolo, appartenenza al ruolo predefinito del database **db_securityadmin**, appartenenza al ruolo predefinito del database **db_owner** o appartenenza al ruolo predefinito del server **sysadmin**.|  
|Ruolo applicazione|Autorizzazione ALTER per il ruolo, appartenenza al ruolo predefinito del database **db_securityadmin**, appartenenza al ruolo predefinito del database **db_owner** o appartenenza al ruolo predefinito del server **sysadmin**.|  
  
 I proprietari degli oggetti possono concedere autorizzazioni per gli oggetti di cui sono proprietari. Le entità con l'autorizzazione CONTROL per un'entità a sicurezza diretta possono concedere l'autorizzazione per quella entità.  
  
 Gli utenti che dispongono dell'autorizzazione CONTROL SERVER, ad esempio i membri del ruolo predefinito del server **sysadmin**, possono concedere qualsiasi autorizzazione per qualsiasi entità a sicurezza diretta nel server. Gli utenti che dispongono dell'autorizzazione CONTROL per un database, ad esempio i membri del ruolo predefinito del database **db_owner**, possono concedere qualsiasi autorizzazione per qualsiasi entità a protezione diretta nel database. Gli utenti che dispongono dell'autorizzazione CONTROL in uno schema, possono concedere qualsiasi autorizzazione per qualsiasi oggetto all'interno dello schema.  
  
## <a name="see-also"></a>Vedere anche  
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [Autorizzazioni &#40;motore di database&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [Entità &#40;motore di database&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [CREATE APPLICATION ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-application-role-transact-sql.md)   
 [Gerarchia di crittografia](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
