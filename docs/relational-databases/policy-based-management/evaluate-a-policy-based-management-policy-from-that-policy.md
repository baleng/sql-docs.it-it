---
title: Valutare i criteri della gestione basata su criteri da quei criteri | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, evaluate policy
ms.assetid: 0b3214bd-d0ab-45ab-9281-3d95507abe54
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 29db8b510faecc2b9006cba0bfec995ec78d8beb
ms.sourcegitcommit: ef6e3ec273b0521e7c79d5c2a4cb4dcba1744e67
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/10/2018
ms.locfileid: "51512162"
---
# <a name="evaluate-a-policy-based-management-policy-from-that-policy"></a>Valutare i criteri della gestione basata su criteri da quei criteri
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  In questo argomento verrà descritto come valutare i criteri utilizzandoli in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 **Contenuto dell'argomento**  
  
-   **Prima di iniziare:**  
  
     [Security](#Security)  
  
-   **Per valutare i criteri tramite:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Permissions  
 È necessaria l'appartenenza al ruolo PolicyAdministratorRole nel database msdb.  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-evaluate-a-policy"></a>Per valutare i criteri  
  
1.  In **Esplora oggetti**fare clic sul segno più per espandere il server contenente i criteri da valutare.  
  
2.  Fare clic sul segno più per espandere la cartella **Gestione** .  
  
3.  Fare clic sul segno più per espandere la cartella **Gestione criteri**.  
  
4.  Fare clic sul segno più per espandere la cartella **Criteri** .  
  
5.  Fare clic con il pulsante destro del mouse sui criteri da valutare e scegliere **Valuta**.  
  
6.  Nella finestra di dialogo **Risultati valutazione**  verranno visualizzati i risultati della valutazione dei criteri. Per le destinazioni non conformi ai criteri e con proprietà che possono essere riconfigurate tramite gestione basata su criteri, è possibile applicare la conformità facendo clic su **Applica**. Per ulteriori informazioni sulle opzioni disponibili nella finestra di dialogo **Valuta criteri** , vedere [Evaluate Policies Dialog Box, Policy Selection Page](../../relational-databases/policy-based-management/evaluate-policies-dialog-box-policy-selection-page.md) e [Evaluate Policies Dialog Box, Evaluation Results Page](../../relational-databases/policy-based-management/evaluate-policies-dialog-box-evaluation-results-page.md).  
  
7.  Al termine, fare clic su **Chiudi**.  
  
  
