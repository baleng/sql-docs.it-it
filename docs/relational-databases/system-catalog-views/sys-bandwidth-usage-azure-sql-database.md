---
title: Sys. bandwidth_usage (Database SQL di Azure) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- bandwidth_usage
- sys.bandwidth_usage
- bandwidth_usage_TSQL
- sys.bandwidth_usage_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.bandwidth_usage
- bandwidth_usage
ms.assetid: 43ed8435-f059-4907-b5c0-193a258b394a
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 5f671e8450255e9c03005c71d6f887c63559d3a7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/01/2018
ms.locfileid: "47603849"
---
# <a name="sysbandwidthusage-azure-sql-database"></a>sys.bandwidth_usage (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  **Nota: Si applica solo a [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]V11.**  
  
 Restituisce informazioni sulla larghezza di banda di rete utilizzata da ogni database in un  **[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] V11 server logico**,. In ogni riga restituita per un determinato database vengono riepilogate una direzione e una classe di utilizzo per un periodo di un'ora.  
  
 **Questa è stata deprecata in una [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] server logico versione 12.**  
  
 Il **Sys. bandwidth_usage** vista contiene le colonne seguenti.  
  
|Column Name|Description|  
|-----------------|-----------------|  
|**time**|Ora in cui la larghezza di banda è stata usata. Le righe di questa vista hanno base oraria. Ad esempio, 2009-09-19 02:00:00.000 indica che la larghezza di banda è stata usata il 19 settembre 2009 tra le 14.00 e le 3.00.|  
|**database_name**|Nome del database che ha usato la larghezza di banda.|  
|**Direzione**|Tipo di larghezza di banda usata, uno di:<br /><br /> In ingresso: I dati spostati nella [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].<br /><br /> In uscita: Dati spostati fuori il [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].|  
|**class**|Classe di larghezza di banda usata, una di:<br />Informazione interna: Dati spostati all'interno della piattaforma Azure.<br />Esterni: Dati spostati all'esterno della piattaforma Azure.<br /><br /> Questa classe viene restituita solo se il database è occupato in una relazione di copia continua tra aree ([!INCLUDE[ssGeoDR](../../includes/ssgeodr-md.md)]). Se un determinato database non partecipa ad alcuna relazione di copia continua, le righe di "interlink" non vengono restituite. Per altre informazioni, vedere la sezione "Osservazioni" più avanti in questo argomento.|  
|**time_period**|Il periodo di tempo quando si è verificato durante l'utilizzo è picco o OffPeak. L'ora Peak si basa sull'area geografica in cui è stato creato il server. Ad esempio, se un server è stato creato nell'area geografica "US_Northwest", l'ora Peak è compresa tra le 10.00 e le 18.00 PST.|  
|**Quantità**|La quantità di larghezza di banda, in kilobyte (KB), usata.|  
  
## <a name="permissions"></a>Permissions  
 In questa vista è disponibile solo nel **master** database all'account di accesso dell'entità a livello di server.  
  
## <a name="remarks"></a>Note  
  
### <a name="external-and-internal-classes"></a>Classi External e Internal  
 Per ogni database utilizzato in un determinato momento, il **Sys. bandwidth_usage** vista restituisce le righe che mostrano la classe e la direzione dell'utilizzo della larghezza di banda. Nell'esempio seguente vengono illustrati i dati che possono essere esposti per un determinato database. In questo esempio, la data e l'ora sono 2012-04-21 17:00:00, che cade nel periodo di massima attività. Il nome del database è Db1. In questo esempio **Sys. bandwidth_usage** ha restituito una riga per tutte e quattro le combinazioni di direzioni Ingress e in uscita e classi External e Internal, come indicato di seguito:  
  
|time|database_name|direction|class|time_period|quantity|  
|----------|--------------------|---------------|-----------|------------------|--------------|  
|2012-04-21 17:00:00|Db1|Ingress|External|Peak|66|  
|2012-04-21 17:00:00|Db1|Egress|External|Peak|741|  
|2012-04-21 17:00:00|Db1|Ingress|Internal|Peak|1052|  
|2012-04-21 17:00:00|Db1|Egress|Interno|Peak|3525|  
  
### <a name="interpreting-data-direction-for-includessgeodrincludesssgeodr-mdmd"></a>Interpretazione della direzione dati per [!INCLUDE[ssGeoDR](../../includes/ssgeodr-md.md)]  
 Per la [!INCLUDE[ssGeoDR](../../includes/ssgeodr-md.md)], i dati di utilizzo della larghezza di banda sono visibili nel database master logico da entrambi i lati di una relazione di copia continua. Pertanto, è necessario interpretare gli indicatori di direzione Ingress (in entrata) ed Egress (in uscita) dal punto di vista del server logico su cui viene eseguita la query. Ad esempio, considerare un flusso di replica che trasferisce 1 MB di dati dal server di origine al server di destinazione. In questo caso, nel server di origine, il MB viene conteggiato nel totale dei dati inviati mentre nel server di destinazione, il MB viene registrato come dati ricevuti.  
  
> [!NOTE]  
>  Il bulk dei dati vengono trasferiti dal server di origine al server di destinazione, nella direzione del flusso dei dati utente. Tuttavia, parte del trasferimento dei dati viene richiesto nell'altra direzione.  
  
  
