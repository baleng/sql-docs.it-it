---
title: Funzionamento Stored procedure estese | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- extended stored procedures [SQL Server], about extended stored procedures
ms.assetid: 6e946d8c-3268-4b59-8a1c-1637909cd701
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 118603088f1cad1ee612f7e4035dc69ba66bc860
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/01/2018
ms.locfileid: "47838319"
---
# <a name="how-extended-stored-procedures-work"></a>Funzionamento delle stored procedure estese
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Utilizzare invece la funzionalità di integrazione con CLR.  
  
 Il funzionamento di una stored procedure estesa è il seguente:  
  
1.  Quando un client esegue una stored procedure estesa, la richiesta viene trasmessa in flusso di dati tabulare (TDS) o formato SOAP Simple Object Access Protocol () dall'applicazione client per [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
2.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esegue la ricerca della DLL associata alla stored procedure estesa e, se non è già caricata, la carica.  
  
3.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] chiama la stored procedure estesa richiesta (implementata come funzione all'interno della DLL).  
  
4.  La stored procedure estesa passa set di risultati e restituisce parametri al server mediante l'API Stored procedure estesa.  
  
## <a name="see-also"></a>Vedere anche  
 [Programmazione di stored procedure estese del motore di database](../../relational-databases/database-engine-extended-stored-procedure-programming.md)  
  
  
