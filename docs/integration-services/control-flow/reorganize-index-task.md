---
title: Attività Riorganizza indice | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.reorganizeindextask.f1
helpviewer_keywords:
- reorganizing indexes
- Reorganize Index task [Integration Services]
- indexes [Integration Services]
ms.assetid: 9ed87861-e5c3-4fcd-8760-d112f4c0af0c
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: dc70b38e797b91f273e60489a2126e764fdf11bd
ms.sourcegitcommit: 0638b228980998de9056b177c83ed14494b9ad74
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/14/2018
ms.locfileid: "51637645"
---
# <a name="reorganize-index-task"></a>Attività Riorganizza indice
  L'attività Riorganizza indice consente di riorganizzare indici nelle tabelle e nelle viste dei database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Per altre informazioni sulla gestione degli indici, vedere [Riorganizzare e ricompilare gli indici](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md).  
  
 Tramite l'attività Riorganizza indice un pacchetto può riorganizzare indici in uno o più database. Se si utilizza l'attività per riorganizzare gli indici di un singolo database, sarà possibile scegliere le viste e le tabelle di cui riorganizzare gli indici. L'attività Riorganizza indice include anche un'opzione per la compattazione dei dati oggetto di grandi dimensioni. I dati oggetto di grandi dimensioni sono dati con il tipo **image**, **text**, **ntext**, **varchar(max)**, **nvarchar(max)**, **varbinary(max)** o **xml**. Per altre informazioni, vedere [Tipi di dati &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md).  
  
 L'attività Riorganizza indice incapsula l'istruzione Transact-SQL ALTER INDEX. Se si sceglie di compattare i dati oggetto di grandi dimensioni, l'istruzione utilizzerà la clausola REORGANIZE WITH (LOB_COMPACTION = ON), in caso contrario tale clausola verrà impostata su OFF. Per altre informazioni, vedere [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md).  
  
> [!IMPORTANT]  
>  Il tempo richiesto dall'attività per creare l'istruzione Transact-SQL da eseguire è proporzionale al numero degli indici da riorganizzare. Se l'attività è configurata per la riorganizzazione degli indici in tutte le tabelle e le viste di un database con un numero elevato di indici oppure per la riorganizzazione degli indici in più database, la generazione dell'istruzione Transact-SQL potrebbe richiedere una quantità di tempo considerevole.  
  
## <a name="configuration-of-the-reorganize-index-task"></a>Configurazione dell'attività Riorganizza indice  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] . Questa attività è disponibile nella sezione **Attività di manutenzione** della **casella degli strumenti** di Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)].  
  
 Per informazioni sulle proprietà che è possibile impostare in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] , fare clic sull'argomento seguente:  
  
-   [Attività Riorganizza indice &#40;Piano di manutenzione&#41;](../../relational-databases/maintenance-plans/reorganize-index-task-maintenance-plan.md)  
  
## <a name="related-tasks"></a>Attività correlate  
 Per altre informazioni su come impostare queste proprietà nella finestra di Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] , vedere [Impostazione delle proprietà di un'attività o di un contenitore](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b).  
  
## <a name="see-also"></a>Vedere anche  
 [Attività di Integration Services](../../integration-services/control-flow/integration-services-tasks.md)   
 [Flusso di controllo](../../integration-services/control-flow/control-flow.md)  
  
  
