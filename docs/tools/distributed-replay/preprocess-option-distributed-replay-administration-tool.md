---
title: Opzione preprocess (strumento di amministrazione Riesecuzione distribuita) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
ms.assetid: 9b5012fd-233e-4a25-a2e1-585c63b70502
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: cb0411323de64747c4b142fc4eda1882aceae010
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52502707"
---
# <a name="preprocess-option-distributed-replay-administration-tool"></a>Opzione preprocess (strumento di amministrazione Distributed Replay)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Lo strumento di amministrazione Riesecuzione distribuita di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , **DReplay.exe**, è uno strumento da riga di comando che consente di comunicare con il controller di Riesecuzione distribuita. Questo argomento descrive l'opzione della riga di comando **preprocess** e la sintassi corrispondente.  
  
 L'opzione **preprocess** avvia la fase di pre-elaborazione. Durante questa fase il controller prepara i dati di traccia di input per la riproduzione sul server di destinazione.  
  
 ![Icona di collegamento all'argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento all'argomento")Per altre informazioni sulle convenzioni relative alla sintassi dello strumento di amministrazione, vedere [Convenzioni della sintassi Transact-SQL &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
dreplay preprocess [-m controller] -i input_trace_file  
    -d controller_working_dir [-c config_file] [-f status_interval]  
```  
  
#### <a name="parameters"></a>Parametri  
 **Controller** *-m*  
 Specifica il nome computer del controller. È possibile utilizzare "`localhost`" o "`.`" per fare riferimento al computer locale.  
  
 Se il parametro **-m** non è specificato, viene usato il computer locale.  
  
 **-i** *input_trace_file*  
 Specifica il percorso completo del file di traccia di input nel controller, ad esempio `D:\Mytrace.trc`. Il parametro **-i** è obbligatorio.  
  
 Se nella stessa directory sono presenti file di rollover, questi verranno caricati e utilizzati automaticamente. I file devono rispettare la convenzione di denominazione per il rollover dei file, ad esempio `Mytrace.trc`, `Mytrace_1.trc`, `Mytrace_2.trc`, `Mytrace_3.trc`, ... `Mytrace_n.trc`.  
  
> [!NOTE]  
>  Se si utilizza lo strumento di amministrazione in un computer diverso dal controller, sarà necessario copiare i file di traccia di input nel controller in modo da poter utilizzare un percorso locale per questo parametro.  
  
 **-d** *controller_working_dir*  
 Specifica la directory nel controller in cui verrà archiviato il file intermedio. Il parametro **-d** è obbligatorio.  
  
 Di seguito vengono indicati i requisiti per questo parametro:  
  
-   La directory deve trovarsi nel controller.  
  
-   È necessario specificare il percorso completo, che inizia con una lettera di unità, ad esempio `c:\WorkingDir`.  
  
-   Il percorso non deve terminare con una barra rovesciata "`\`".  
  
-   I percorsi UNC non sono supportati.  
  
 **-c** *config_file*  
 È il percorso completo del file di configurazione della pre-elaborazione. Viene utilizzato per specificare il percorso del file di configurazione della pre-elaborazione quando tale file viene archiviato in una posizione diversa. Questo parametro può essere un percorso UNC o un percorso locale nel computer in cui viene eseguito lo strumento di amministrazione.  
  
 Il parametro **-c** non è obbligatorio se non è necessario applicare filtri o non si vuole modificare il tempo massimo di inattività.  
  
 Senza il parametro **-c**, viene usato il file di configurazione della pre-elaborazione predefinito, ovvero `DReplay.exe.preprocess.config`.  
  
 *intervallo_stato***-f**  
 Specifica la frequenza in secondi in base alla quale visualizzare messaggi di stato.  
  
 Se **-f** non è specificato, l'intervallo predefinito è 30 secondi.  
  
## <a name="examples"></a>Esempi  
 In questo esempio la fase di pre-elaborazione viene avviata con tutte le impostazioni predefinite. Il valore `localhost` indica che il servizio controller viene eseguito nello stesso computer dello strumento di amministrazione. Il parametro *input_trace_file* specifica il percorso dei dati di traccia di input, ad esempio `c:\mytrace.trc`. Il file di traccia non viene filtrato, quindi è necessario specificare il parametro **-c** .  
  
```  
dreplay preprocess -m localhost -i c:\mytrace.trc -d c:\WorkingDir  
```  
  
 In questo esempio viene avviata la fase di pre-elaborazione e viene specificato un file di configurazione della pre-elaborazione modificato. A differenza dell'esempio precedente, il parametro **-c** viene usato per puntare al file di configurazione modificato, se è stato archiviato in un percorso diverso. Ad esempio  
  
```  
dreplay preprocess -m localhost -i c:\mytrace.trc -d c:\WorkingDir -c c:\DReplay.exe.preprocess.config  
```  
  
 Nel file di configurazione della pre-elaborazione modificato, viene aggiunta una condizione di filtro per filtrare le sessioni di sistema durante la riproduzione distribuita. Il filtro viene aggiunto modificando l'elemento `<PreprocessModifiers>` nel file di configurazione della pre-elaborazione `DReplay.exe.preprocess.config`.  
  
 Nell'esempio seguente viene illustrato un file di configurazione modificato:  
  
```  
<?xml version='1.0'?>  
<Options>  
    <PreprocessModifiers>  
        <IncSystemSession>No</IncSystemSession>  
        <MaxIdleTime>-1</MaxIdleTime>  
    </PreprocessModifiers>  
</Options>  
```  
  
## <a name="permissions"></a>Permissions  
 È necessario eseguire lo strumento di amministrazione come utente interattivo, scegliendo tra utente locale e account utente di dominio. Per utilizzare un account utente locale, lo strumento di amministrazione e il controller devono essere eseguiti nello stesso computer.  
  
 Per altre informazioni, vedere [Sicurezza di Distributed Replay](../../tools/distributed-replay/distributed-replay-security.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Preparazione dei dati di traccia di input](../../tools/distributed-replay/prepare-the-input-trace-data.md)   
 [SQL Server Distributed Replay](../../tools/distributed-replay/sql-server-distributed-replay.md)   
 [Configurare Riesecuzione distribuita](../../tools/distributed-replay/configure-distributed-replay.md)  
  
  
