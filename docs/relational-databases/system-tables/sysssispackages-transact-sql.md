---
title: sysssispackages (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysdtspackages90_TSQL
- sysdtspackages90
dev_langs:
- TSQL
helpviewer_keywords:
- sysssispackages system table
ms.assetid: 66155dcd-dcdb-4e33-a242-1625828ad8d2
author: douglasl
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 7a1ab35e121683fd1c8d25dc21a2128aa3232c70
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/01/2018
ms.locfileid: "47755081"
---
# <a name="sysssispackages-transact-sql"></a>sysssispackages (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene una riga per ogni pacchetto salvato [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Questa tabella è archiviata nel **msdb** database.  
  
  
|Nome colonna|Tipo di dati|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Identificatore univoco del pacchetto.|  
|**id**|**uniqueidentifier**|GUID del pacchetto.|  
|**description**|**nvarchar**|Descrizione del pacchetto (facoltativa).|  
|**createdate**|**datetime**|Data di creazione del pacchetto.|  
|**folderid**|**uniqueidentifier**|GUID della cartella logica in cui [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] elenca il pacchetto.|  
|**ownersid**|**varbinary**|ID di sicurezza (SID) univoco dell'utente che ha creato il pacchetto.|  
|**packagedata**|**image**|Il pacchetto.|  
|**packageformat**|**int**|Formato in cui viene salvato il pacchetto.<br /><br /> Il valore 2 indica che il pacchetto viene salvato nel [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] formato.<br /><br /> Il valore 3 indica che il pacchetto viene salvato nel formato [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]o versione successiva.|  
|**packagetype**|**int**|Client che ha creato il pacchetto. I valori possibili sono i seguenti:<br /><br /> 0 (valore predefinito)<br /><br /> 1 ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] importazione / esportazione guidata)<br /><br /> 3 ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] replica)<br /><br /> 5 ([!INCLUDE[ssIS](../../includes/ssis-md.md)] progettazione)<br /><br /> 6 (Finestra di progettazione dei piani di manutenzione o procedura guidata).<br /><br /> <br /><br /> Si noti che i valori in questa colonna corrispondono al <xref:Microsoft.SqlServer.Dts.Runtime.DTSPackageType> enumerazione.|  
|**vermajor**|**int**|Versione principale più recente del pacchetto.|  
|**verssecond**|**int**|Versione secondaria più recente del pacchetto.|  
|**verbuild**|**int**|Ultima build del pacchetto.|  
|**vercomments**|**nvarchar**|Commenti sulla versione del pacchetto.|  
|**verid**|**uniqueidentifier**|GUID della versione del pacchetto.|  
|**isencrypted**|**bit**|Valore booleano che indica se un pacchetto è crittografato.|  
|**readrolesid**|**varbinary**|Ruolo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che consente di caricare i pacchetti.|  
|**writerolesid**|**varbinary**|Ruolo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che consente di salvare i pacchetti.|  
  
## <a name="see-also"></a>Vedere anche  
 [Pacchetti di Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-packages.md)  
  
  
