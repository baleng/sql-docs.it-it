---
title: Account di accesso, utenti e ruoli di database (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology:
- master-data-services
ms.topic: conceptual
helpviewer_keywords:
- security [Master Data Services], database roles
- database [Master Data Services], users
- security [Master Data Services], database users
- database [Master Data Services], roles
- database [Master Data Services], logins
- security [Master Data Services], database logins
ms.assetid: 72ee383e-a619-461b-9f9d-1cac162ab0c5
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: ed15741a0565cda9735b4e2d851e1b025deea224
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/01/2018
ms.locfileid: "47607349"
---
# <a name="database-logins-users-and-roles-master-data-services"></a>Account di accesso, utenti e ruoli di database (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] sono inclusi account di accesso, utenti e ruoli installati automaticamente nell'istanza del [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] in cui è ospitato il database [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] . Questi account di accesso, utenti e ruoli non devono essere modificati.  
  
## <a name="logins"></a>Logins  
  
|Account di accesso|Descrizione|  
|-----------|-----------------|  
|**mds_dlp_login**|Consente la creazione di assembly UNSAFE. Per altre informazioni, vedere [Creating an Assembly](../relational-databases/clr-integration/assemblies/creating-an-assembly.md).<br /><br /> - Account di accesso disabilitato con password generata casualmente.<br /><br /> - Esegue il mapping a dbo per il database [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .<br /><br /> - Per msdb, mds_clr_user esegue il mapping a questo account di accesso.|  
|**mds_email_login**|Account di accesso abilitato utilizzato per le notifiche.<br /><br /> Per msdb e il database [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] , mds_email_user esegue il mapping a questo account di accesso.|  
  
## <a name="msdb-users"></a>Utenti di msdb  
  
|Utente|Descrizione|  
|----------|-----------------|  
|**mds_clr_user**|Non usato. Esegue il mapping a mds_dlp_login.|  
|**mds_email_user**|Utilizzato per le notifiche.<br /><br /> - Esegue il mapping a mds_email_login.<br /><br /> - È un membro del ruolo DatabaseMailUserRole.|  
  
## <a name="master-data-services-database-users"></a>Utenti del database Master Data Services  
  
|Utente|Descrizione|  
|----------|-----------------|  
|**mds_email_user**|Utilizzato per le notifiche.<br /><br /> - Dispone dell'autorizzazione SELECT per lo schema mdm.<br /><br /> - Dispone dell'autorizzazione EXECUTE per il tipo di tabella mdm.MemberGetCriteria definito dall'utente.<br /><br /> - Dispone dell'autorizzazione EXECUTE per la stored procedure mdm.udpNotificationQueueActivate.|  
|**mds_schema_user**|È proprietario degli schemi mdm e mdq. Lo schema predefinito è mdm.<br /><br /> Non disporre di un account di accesso di cui è stato eseguito il mapping.|  
|**mds_ssb_user**|Utilizzato per eseguire attività di Service Broker.<br /><br /> -Ha le autorizzazioni DELETE, INSERT, REFERENCES, SELECT e UPDATE per tutti gli schemi.<br /><br /> - Non ha un account di accesso a cui è stato eseguito il mapping.|  
  
## <a name="master-data-services-database-role"></a>Ruolo del database Master Data Services  
  
|Role|Descrizione|Permissions|  
|----------|-----------------|-----------------|  
|**mds_exec**|Il ruolo contiene l'account impostato in [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] quando si crea un'applicazione Web [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] e si definisce un account per il pool di applicazioni.|Autorizzazione EXECUTE per tutti gli schemi.<br /><br /> <br /><br /> Autorizzazioni ALTER, INSERT e SELECT per queste tabelle:<br /><br /> mdm.tblStgMember<br /><br /> mdm.tblStgMemberAttribute<br /><br /> mdm.tbleStgRelationship<br /><br /> <br /><br /> Autorizzazione SELECT per queste tabelle:<br /><br /> mdm.tblUser<br /><br /> mdm.tblUserGroup<br /><br /> mdm.tblUserPreference<br /><br /> <br /><br /> Autorizzazione SELECT per queste viste:<br /><br /> mdm.viw_SYSTEM_SECURITY_NAVIGATION<br /><br /> mdm.viw_SYSTEM_SECURITY_ROLE_ACCCESSCONTROL<br /><br /> mdm.viw_SYSTEM_SECURITY_ROLE_ACCCESSCONTROL_MEMBER<br /><br /> mdm.viw_SYSTEM_SECURITY_USER_MODEL|  
  
## <a name="schemas"></a>Schemi  
  
|Role|Descrizione|  
|----------|-----------------|  
|**mdm**|Contiene tutti gli oggetti di database [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] e Service Broker diversi dalle funzioni contenute nello schema mdq.|  
|**mdq**|Sono contenute le funzioni del database [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] relative al filtro dei risultati dei membri in base a espressioni regolari o somiglianza e per la formattazione di messaggi di posta elettronica di notifica.|  
|**stg**|Contiene tabelle di database [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] , stored procedure e viste correlate al processo di gestione temporanea. Non eliminare alcun oggetto. Per altre informazioni sul processo di gestione temporanea, vedere [Panoramica: Importazione di dati da tabelle &#40;Master Data Services&#41;](../master-data-services/overview-importing-data-from-tables-master-data-services.md).|  
  
## <a name="see-also"></a>Vedere anche  
 [Sicurezza di oggetti di database &#40;Master Data Services&#41;](../master-data-services/database-object-security-master-data-services.md)  
  
  
