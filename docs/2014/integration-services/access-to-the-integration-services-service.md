---
title: Servizio servizi di accesso per l'integrazione | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- SSIS packages, security
- viewing packages while running
- displaying packacges while running
- security [Integration Services], running packages
- packages [Integration Services], security
- current packages running
- Integration Services packages, security
- SQL Server Integration Services packages, security
ms.assetid: 1088aafc-14c5-4e7d-9930-606a24c3049b
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 7e9baff13c2bc368557a49b4509c6e48a444d583
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/02/2018
ms.locfileid: "48132121"
---
# <a name="access-to-the-integration-services-service"></a>Accesso al servizio Integration Services
  Tramite i livelli di protezione dei pacchetti è possibile limitare gli utenti a cui è consentito modificare ed eseguire un pacchetto. Per limitare gli utenti a cui è consentito visualizzare l'elenco di pacchetti attualmente in esecuzione in un server e arrestare i pacchetti attualmente in esecuzione in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]è necessaria una protezione aggiuntiva.  
  
 In [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] l'elenco dei pacchetti in esecuzione viene visualizzato tramite il servizio [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. I membri del gruppo Administrators di Windows possono visualizzare e arrestare tutti i pacchetti in esecuzione. Gli utenti che non appartengono a questo gruppo possono visualizzare e arrestare solo i pacchetti che hanno avviato personalmente.  
  
 È importante limitare l'accesso ai computer che eseguono un servizio [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , soprattutto se si tratta di un servizio [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] che consente l'enumerazione di cartelle remote. Gli utenti autenticati possono richiedere l'enumerazione di pacchetti. Anche se il servizio non viene individuato, le cartelle vengono comunque enumerate dal servizio. Questi nomi di cartella potrebbero essere sfruttati da un utente malintenzionato. Se un amministratore ha configurato il servizio in modo da consentire l'enumerazione di cartelle in un computer remoto, agli utenti potrebbero essere visualizzati anche i nomi di cartella in genere non visibili.  
  
  
