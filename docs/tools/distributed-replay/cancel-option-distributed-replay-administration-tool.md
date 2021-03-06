---
title: Opzione Annulla (strumento di amministrazione Riesecuzione distribuita) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
ms.assetid: fea376de-307a-4b45-b7e2-37df88f3681a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 34e0cbc518044d5bc3a18b754d8146af8fca1462
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52524215"
---
# <a name="cancel-option-distributed-replay-administration-tool"></a>Opzione cancel (strumento di amministrazione Distributed Replay)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Lo strumento di amministrazione Riesecuzione distribuita di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , **DReplay.exe**, è uno strumento da riga di comando che consente di comunicare con il controller di Riesecuzione distribuita. Questo argomento descrive l'opzione della riga di comando **cancel** e la sintassi corrispondente.  
  
 L'opzione **cancel** annulla l'operazione corrente in esecuzione nel controller.  
  
 ![Icona di collegamento all'argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento all'argomento")Per altre informazioni sulle convenzioni relative alla sintassi dello strumento di amministrazione, vedere [Convenzioni della sintassi Transact-SQL &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
dreplay cancel [-m controller] [-q]   
```  
  
#### <a name="parameters"></a>Parametri  
 **Controller** *-m*  
 Nome computer del controller. È possibile utilizzare "`localhost`" o "`.`" per fare riferimento al computer locale.  
  
 Se il parametro **-m** non è specificato, viene usato il computer locale.  
  
 **-q**  
 Modalità non interattiva. Non viene richiesta alcuna conferma da parte dell'utente.  
  
 Il parametro **-q** è facoltativo.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene inviata una richiesta di annullamento in modalità non interattiva. Il valore `localhost` indica che il servizio controller viene eseguito nello stesso computer dello strumento di amministrazione.  
  
```  
dreplay cancel -m localhost -q  
```  
  
## <a name="permissions"></a>Permissions  
 È necessario eseguire lo strumento di amministrazione come utente interattivo, scegliendo tra utente locale e account utente di dominio. Per utilizzare un account utente locale, lo strumento di amministrazione e il controller devono essere eseguiti nello stesso computer.  
  
 Per altre informazioni, vedere [Sicurezza di Distributed Replay](../../tools/distributed-replay/distributed-replay-security.md).  
  
## <a name="see-also"></a>Vedere anche  
 [SQL Server Distributed Replay](../../tools/distributed-replay/sql-server-distributed-replay.md)  
  
  
