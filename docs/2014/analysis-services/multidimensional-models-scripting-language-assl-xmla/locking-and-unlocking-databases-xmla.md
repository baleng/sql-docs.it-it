---
title: Blocco e sblocco di database (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- locking [XML for Analysis]
- XML for Analysis, locking
- XMLA, locking
- unlocking objects
ms.assetid: 451afa58-ce03-4ecc-8dd3-9e7e8559b5f1
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e1f518f846a6e0bb87f858d7a5798eb9a7e9c8d0
ms.sourcegitcommit: 7fe14c61083684dc576d88377e32e2fc315b7107
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/26/2018
ms.locfileid: "50146276"
---
# <a name="locking-and-unlocking-databases-xmla"></a>Blocco e sblocco di database (XMLA)
  È possibile bloccare e sbloccare database utilizzando, rispettivamente, il [Lock](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/lock-element-xmla) e [Unlock](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/lock-element-xmla) comandi XML for Analysis (XMLA). In genere, gli altri comandi XMLA bloccano e sbloccano automaticamente gli oggetti in base alle esigenze per completare il comando durante l'esecuzione. In modo esplicito è possibile bloccare o sbloccare un database per eseguire più comandi all'interno di una singola transazione, ad esempio un [Batch](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/batch-element-xmla) comando, impedendo ad altre applicazioni dal commit di una transazione di scrittura al database.  
  
## <a name="locking-databases"></a>Blocco di database  
 Il comando `Lock` blocca un oggetto, per utilizzo condiviso o esclusivo, all'interno del contesto della transazione attualmente attiva. Un blocco su un oggetto impedisce alle transazioni di eseguire il commit finché non viene rimosso. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] supporta due tipi di blocchi, blocchi condivisi e blocchi esclusivi. Per altre informazioni sui tipi di blocco supportati da [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], vedere [modalità elemento &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/mode-element-xmla).  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] consente solo che i database vengano bloccati. Il [oggetti](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla) elemento deve contenere un riferimento a un [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] database. Se l'elemento `Object` non viene specificato oppure fa riferimento a un oggetto diverso da un database `Object`, si verifica un errore.  
  
> [!IMPORTANT]  
>  Solo amministratori del database o amministratori del server possono eseguire in modo esplicito un comando `Lock`.  
  
 Gli altri comandi eseguono implicitamente un comando `Lock` su un database [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Qualsiasi operazione che legge dati o metadati da un database, ad esempio qualsiasi [Discover](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-discover) metodo o un' [Execute](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-execute) metodo in esecuzione un [istruzione](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/statement-element-xmla) comando, applica implicitamente un condiviso bloccare il database. Qualsiasi transazione che esegue il commit delle modifiche nei dati o metadati per un oggetto in un [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] database, ad esempio un `Execute` metodo in esecuzione un' [Alter](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/alter-element-xmla) comando, applica implicitamente un blocco esclusivo sul database.  
  
## <a name="unlocking-objects"></a>Sblocco di oggetti  
 Il comando `Unlock` rimuove un blocco applicato all'interno del contesto della transazione attualmente attiva.  
  
> [!IMPORTANT]  
>  Solo gli amministratori del database o gli amministratori del server possono eseguire in modo esplicito un comando `Unlock`.  
  
 Tutti i blocchi sono contenuti nel contesto della transazione corrente. Quando viene eseguito il commit oppure il rollback della transazione corrente, tutti i blocchi definiti all'interno della transazione vengono rilasciati automaticamente.  
  
## <a name="see-also"></a>Vedere anche  
 [Bloccare l'elemento &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/lock-element-xmla)   
 [Elemento Unlock &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/lock-element-xmla)   
 [Sviluppo con XMLA in Analysis Services](developing-with-xmla-in-analysis-services.md)  
  
  
