---
title: MSSQLSERVER_2570 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 2570 (Database Engine error)
ms.assetid: 29800aa9-81aa-4371-992c-487dbb617f46
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1f996df18335b0444e2efe530870d952634c3e82
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/15/2018
ms.locfileid: "51677330"
---
# <a name="mssqlserver2570"></a>MSSQLSERVER_2570
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|2570|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|DBCC_COLUMN_VALUE_OUT_OF_RANGE|  
|Testo del messaggio|Pagina P_ID, slot S_ID nell'oggetto con ID O_ID, ID di indice I_ID, ID di partizione PN_ID, ID di unità di allocazione A_ID (tipo TYPE). Il valore della colonna COLUMN_NAME non è compreso nell'intervallo consentito per il tipo di dati "DATATYPE". Aggiornare la colonna a un valore valido.|  
  
## <a name="explanation"></a>Spiegazione  
Il valore contenuto nella colonna specificata non è compreso nell'intervallo dei valori possibili per il tipo di dati della colonna.  
  
## <a name="user-action"></a>Azione dell'utente  
L'errore non è reversibile. Aggiornare la colonna a un valore compreso nell'intervallo consentito per il tipo di dati della colonna ed eseguire di nuovo il comando.  Per altre informazioni, vedere l'articolo [923247](https://support.microsoft.com/kb/923247) della Knowledge Base.  
  
## <a name="see-also"></a>Vedere anche  
[UPDATE &#40;Transact-SQL&#41;](~/t-sql/queries/update-transact-sql.md)  
[Tipi di dati &#40;Transact-SQL&#41;](~/t-sql/data-types/data-types-transact-sql.md)  
  
