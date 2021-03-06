---
title: Configurare Windows Firewall per consentire l'accesso a SQL Server |Microsoft Docs
ms.custom: ''
ms.date: 05/17/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- Windows Firewall ports
- WMI firewall ports
- Windows Firewall [Database Engine]
- firewall systems, configuring
- advfirewall
- firewall systems
- rules firewall
- firewall systems, overview and port list
- 1433 TCP port
- portopening using netsh
- ports [SQL Server], TCP
- netsh to open firewall ports
ms.assetid: f55c6a0e-b6bd-4803-b51a-f3a419803024
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f82ce2b0d3ec19dea48f99634a5c5c9936f25ef9
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/27/2018
ms.locfileid: "52408468"
---
# <a name="configure-the-windows-firewall-to-allow-sql-server-access"></a>Configure the Windows Firewall to Allow SQL Server Access
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

> [!div class="nextstepaction"]
> [Contribuisci a migliorare la documentazione di SQL Server](https://80s3ignv.optimalworkshop.com/optimalsort/36yyw5kq-0)

I sistemi firewall contribuiscono a impedire l'accesso non autorizzato alle risorse del computer. Se un firewall viene abilitato ma non configurato correttamente, i tentativi di connessione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] potrebbero essere bloccati.  
  
Per accedere a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] attraverso un firewall, è necessario configurare il firewall nel computer in cui viene eseguito [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Il firewall è un componente di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows. È possibile anche installare un firewall di un altro produttore. Questo articolo illustra come configurare Windows Firewall, ma i principi di base si applicano anche ad altri programmi firewall.  
  
> [!NOTE]  
>  Questo articolo offre una panoramica della configurazione del firewall e riepiloga le informazioni utili a un amministratore di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per ulteriori informazioni sul firewall, vedere la documentazione di riferimento, ad esempio [Windows Firewall with Advanced Security and IPSec](https://go.microsoft.com/fwlink/?LinkID=116904).  
  
 Gli utenti che già conoscono l'elemento **Windows Firewall** del Pannello di controllo e lo snap-in MMC Windows Firewall con sicurezza avanzata e che sanno quali impostazioni configurare, possono passare direttamente agli articoli elencati di seguito:  
  
-   [Configurazione di Windows Firewall per l'accesso al Motore di database](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)  
  
-   [Configurare Windows Firewall per consentire l'accesso ad Analysis Services](../../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)  
  
-   [Configurare un firewall per l'accesso al server di report](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md)  
  
##  <a name="BKMK_basic"></a> Informazioni di base sul firewall  
 Il meccanismo alla base del funzionamento dei firewall è il controllo dei pacchetti in ingresso seguito dal confronto rispetto a un set di regole. Se le regole consentono il pacchetto, esso viene passato al protocollo TCP/IP per un'elaborazione ulteriore. Se non lo consentono, il pacchetto viene ignorato e, se la registrazione è abilitata, viene creata una voce nel file di registrazione del firewall.  
  
 L'elenco del traffico consentito viene creato in uno dei modi seguenti:  
  
-   Quando il computer che include il firewall abilitato avvia la comunicazione, il firewall crea una voce nell'elenco in modo da consentire la risposta. La risposta in ingresso è considerata traffico richiesto e non è necessario effettuare alcuna configurazione.  
  
-   Le eccezioni per il firewall vengono configurate dall'amministratore. In questo modo è possibile accedere a programmi specificati in esecuzione o a porte di connessione specificate nel computer. In questo caso, il computer accetta il traffico in ingresso non richiesto quando svolge le funzioni di server, listener o peer. Questo è il tipo di configurazione che è necessario completare per connettersi a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 La scelta del tipo di firewall più adatto alle proprie esigenze non si limita alla decisione relativa alla necessità di aprire o chiudere una determinata porta e presuppone che vengano prese in considerazione tutte le regole e le opzioni di configurazione disponibili. Questo articolo non prende in esame tutte le opzioni possibili del firewall. Si consiglia di consultare i documenti seguenti:  
  
 [Guida introduttiva a Windows Firewall con sicurezza avanzata](https://go.microsoft.com/fwlink/?LinkId=116080)  
  
 [Pagina concernente la guida alla progettazione di Windows Firewall con sicurezza avanzata](https://go.microsoft.com/fwlink/?LinkId=116904)  
  
 [Pagina concernente l'introduzione all'isolamento di dominio e server](https://go.microsoft.com/fwlink/?LinkId=116081)  
  
##  <a name="BKMK_default"></a> Impostazioni del firewall predefinite  
 Il primo passaggio della pianificazione della configurazione del firewall consiste nel determinare lo stato corrente del firewall per il sistema operativo in uso. Se quest'ultimo è stato aggiornato da una versione precedente, è possibile che le impostazioni del firewall siano state conservate o che siano state modificate da un altro amministratore o da Criteri di gruppo nel dominio.  
  
> [!NOTE]  
>  L'attivazione del firewall influisce su altri programmi a cui è consentito l'accesso al computer, ad esempio la condivisione di file e stampanti e le connessioni desktop remoto. Prima di modificare le impostazioni del firewall, gli amministratori devono tener conto di tutte le applicazioni in esecuzione nel computer.  
  
##  <a name="BKMK_programs"></a> Programmi di configurazione del firewall  
Configurare le impostazioni di Windows Firewall con **Microsoft Management Console** o **netsh**.  

-  **Microsoft Management Console (MMC)**  
  
     Lo snap-in MMC Windows Firewall con sicurezza avanzata consente di configurare impostazioni del firewall più avanzate. Questo snap-in presenta la maggior parte delle opzioni di firewall in una modalità di facile utilizzo e presenta tutti i profili firewall. Per altre informazioni, vedere [Utilizzo dello snap-in Windows Firewall con sicurezza avanzata](#BKMK_WF_msc) più avanti in questo articolo.  
  
-   **netsh**  
  
     Lo strumento **netsh.exe** può essere usato da un amministratore per configurare e monitorare i computer basati su Windows in un prompt dei comandi o con un file batch **.** Usando lo strumento **netsh** è possibile indirizzare i comandi contestuali all'helper adatto per far sì che questo esegua il comando desiderato. Un helper è un file DLL (Dynamic Link Library, libreria di collegamento dinamico) che estende la funzionalità dello strumento **netsh** e fornisce configurazione, monitoraggio e supporto per uno o più servizi, utilità o protocolli. Tutti i sistemi operativi che supportano [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dispongono di un helper del firewall. [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)] ha anche un helper del firewall avanzato denominato **advfirewall**. I dettagli sull'uso di **netsh** non vengono trattati in questo articolo. Tuttavia, molte delle opzioni di configurazione descritte possono essere configurate con **netsh**. Ad esempio, eseguire lo script seguente al prompt dei comandi per aprire la porta TCP 1433:  
  
    ```  
    netsh firewall set portopening protocol = TCP port = 1433 name = SQLPort mode = ENABLE scope = SUBNET profile = CURRENT  
    ```  
  
     Esempio simile utilizzando l'helper Windows Firewall con sicurezza avanzata:  
  
    ```  
    netsh advfirewall firewall add rule name = SQLPort dir = in protocol = tcp action = allow localport = 1433 remoteip = localsubnet profile = DOMAIN  
    ```  
  
     Per altre informazioni su **netsh**, vedere i collegamenti seguenti:  
  
    -   [Utilizzo dello strumento Netsh.exe e parametri della riga di comando](https://support.microsoft.com/kb/242468)  
  
    -   [Utilizzo del contesto "netsh advfirewall firewall" anziché del contesto "netsh firewall" per controllare il comportamento di Windows Firewall in Windows Server 2008 e in Windows Vista](https://support.microsoft.com/kb/947709)  
  
    -   [Pagina relativa alla mancata configurazione del profilo pubblico in un computer basato su Windows Vista qualora il comando "netsh firewall" venga utilizzato con il parametro "profile=all"](https://support.microsoft.com/kb/947213)  
  
## <a name="ports-used-by-includessnoversionincludesssnoversion-mdmd"></a>Porte utilizzate da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 Le tabelle seguenti consentono di identificare le porte utilizzate da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
###  <a name="BKMK_ssde"></a> Ports Used By the Database Engine  
 Nella tabella seguente sono indicate le porte più utilizzate dal [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
|Scenario|Port|Commenti|  
|--------------|----------|--------------|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in esecuzione su TCP|Porta TCP 1433|Si tratta della porta più comune consentita dal firewall. Viene utilizzata nelle connessioni di routine all'installazione predefinita del [!INCLUDE[ssDE](../../includes/ssde-md.md)]o a un'istanza denominata che rappresenta l'unica istanza in esecuzione nel computer. Le istanze denominate presuppongo alcune considerazioni speciali. Vedere [Porte dinamiche](#BKMK_dynamic_ports) più avanti in questo articolo.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nella configurazione predefinita|La porta TCP è una porta dinamica determinata all'avvio del [!INCLUDE[ssDE](../../includes/ssde-md.md)] .|Vedere la discussione che segue nella sezione [Porte dinamiche](#BKMK_dynamic_ports). La porta UDP 1434 potrebbe essere richiesta per il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser durante l'utilizzo di istanze denominate.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] quando vengono configurate per l'utilizzo di una porta fissa|Il numero di porta configurato dall'amministratore.|Vedere la discussione che segue nella sezione [Porte dinamiche](#BKMK_dynamic_ports).|  
|Dedicated Admin Connection|Porta TCP 1434 per l'istanza predefinita. Per le istanze denominate vengono utilizzate altre porte. Per informazioni sul numero di porta, controllare il log degli errori.|Per impostazione predefinita, le connessioni amministrative dedicate (DAC, Dedicated Administrator Connection) remote non sono abilitate. Per abilitare le connessioni DAC remote, utilizzare il facet Configurazione superficie di attacco. Per ulteriori informazioni, vedere [Surface Area Configuration](../../relational-databases/security/surface-area-configuration.md).|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser|Porta UDP 1434|Il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser è in attesa delle connessioni in ingresso a un'istanza denominata e fornisce al client il numero di porta TCP corrispondente. In genere il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser viene avviato ogni volta che si usano istanze denominate del [!INCLUDE[ssDE](../../includes/ssde-md.md)] . Non è necessario avviare il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser se il client è configurato per la connessione alla porta specifica dell'istanza denominata.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in esecuzione su un endpoint HTTP.|Può essere specificata quando viene creato un endpoint HTTP. Le impostazioni predefinite sono la porta TCP 80 per il traffico CLEAR_PORT e la porta 443 per il traffico SSL_PORT.|Utilizzata per una connessione HTTP tramite un URL.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in esecuzione su un endpoint HTTPS.|Porta TCP 443|Utilizzata per una connessione HTTPS tramite un URL. HTTPS è una connessione HTTP che utilizza il protocollo SSL (Secure Sockets Layer).|  
|[!INCLUDE[ssSB](../../includes/sssb-md.md)]|Porta TCP 4022. Per verificare la porta utilizzata, eseguire la query seguente:<br /><br /> `SELECT name, protocol_desc, port, state_desc`<br /><br /> `FROM sys.tcp_endpoints`<br /><br /> `WHERE type_desc = 'SERVICE_BROKER'`|Per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssSB](../../includes/sssb-md.md)]non sono disponibili porte predefinite, ma questa è la configurazione convenzionale usata negli esempi della documentazione online.|  
|Mirroring del database|Porta scelta dall'amministratore. Per determinare la porta, eseguire la query seguente:<br /><br /> `SELECT name, protocol_desc, port, state_desc FROM sys.tcp_endpoints`<br /><br /> `WHERE type_desc = 'DATABASE_MIRRORING'`|Per il mirroring del database non sono disponibili porte predefinite, tuttavia negli esempi della documentazione online viene usata la porta TCP 5022 o 7022. È molto importante evitare di interrompere un endpoint del mirroring in uso, soprattutto in modalità a protezione elevata con failover automatico. La configurazione del firewall deve evitare di interrompere il quorum. Per altre informazioni, vedere [Specificare un indirizzo di rete del server &#40;Mirroring del database&#41;](../../database-engine/database-mirroring/specify-a-server-network-address-database-mirroring.md).|  
|Replica|Per le connessioni di replica a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vengono utilizzate le tipiche porte standard del [!INCLUDE[ssDE](../../includes/ssde-md.md)] (porta TCP 1433 per l'istanza predefinita e così via).<br /><br /> La sincronizzazione Web e l'accesso FTP/UNC per snapshot di replica richiedono l'apertura di porte aggiuntive sul firewall. Per trasferire lo schema e i dati iniziali da una posizione all'altra, per la replica possono essere utilizzati il protocollo FTP (porta TCP 21), la sincronizzazione su HTTP (porta TCP 80) o la condivisione di file. Nella condivisione di file vengono utilizzate le porte UDP 137 e 138 a la porta TCP 139 in caso di utilizzo di NetBios. La condivisione file utilizza la porta TCP 445.|Per la sincronizzazione su HTTP, la replica utilizza l'endpoint IIS, ovvero le porte per le quali è configurabile, anche se la porta 80 rappresenta l'impostazione predefinita, ma il processo IIS si connette a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di back-end tramite le porte standard (1433 per l'istanza predefinita).<br /><br /> Durante la sincronizzazione Web tramite FTP, il trasferimento FTP avviene tra IIS e il server di pubblicazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , non tra il sottoscrittore e IIS.|  
|[!INCLUDE[tsql](../../includes/tsql-md.md)] debugger|Porta TCP 135<br /><br /> Vedere [Considerazioni speciali per la porta 135](#BKMK_port_135)<br /><br /> Potrebbe essere necessaria anche l'eccezione [IPsec](#BKMK_IPsec) .|Se si utilizza [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)], nel computer host di [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] , è necessario aggiungere anche **Devenv.exe** all'elenco di eccezioni e aprire la porta TCP 135.<br /><br /> Se si utilizza [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], nel computer host di [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] , è necessario aggiungere anche **ssms.exe** all'elenco di eccezioni e aprire la porta TCP 135. Per altre informazioni, vedere [Configurare le regole del firewall prima di eseguire il debugger TSQL](../../relational-databases/scripting/configure-firewall-rules-before-running-the-tsql-debugger.md).|  
  
 Per istruzioni dettagliate sulla configurazione di Windows Firewall per il [!INCLUDE[ssDE](../../includes/ssde-md.md)], vedere [Configurazione di Windows Firewall per l'accesso al Motore di database](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md).  
  
####  <a name="BKMK_dynamic_ports"></a> Porte dinamiche  
 Per impostazione predefinita, per le istanze denominate, inclusa [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)], vengono utilizzate porte dinamiche. Ciò significa che ogni volta che il [!INCLUDE[ssDE](../../includes/ssde-md.md)] viene avviato, identifica una porta disponibile e ne utilizza il numero. Se l'istanza denominata è l'unica istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)] installata, è probabile che venga utilizzata la porta TCP 1433. Se sono installate altre istanze del [!INCLUDE[ssDE](../../includes/ssde-md.md)] , è probabile che venga utilizzata una porta TCP diversa. Poiché la porta selezionata potrebbe cambiare ogni volta che il [!INCLUDE[ssDE](../../includes/ssde-md.md)] viene avviato, è difficile configurare il firewall per abilitare l'accesso al numero di porta corretto. Pertanto, se si utilizza un firewall, è consigliabile riconfigurare il [!INCLUDE[ssDE](../../includes/ssde-md.md)] affinché utilizzi ogni volta lo stesso numero di porta. In questi casi si parla quindi di porta fissa o porta statica. Per altre informazioni, vedere [Configurazione di un server per l'attesa su una porta TCP specifica &#40;Gestione configurazione SQL Server&#41;](../../database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port.md).  
  
 Un'alternativa alla configurazione di un'istanza denominata in modo che si metta in attesa su una porta fissa consiste nel creare un'eccezione nel firewall per un programma di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ad esempio **sqlservr.exe** per il [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Anche se può risultare utile, il numero di porta non verrà visualizzato nella colonna **Porta locale** della pagina **Regole in entrata** quando si usa lo snap-in MMC Windows Firewall con sicurezza avanzata. Questa operazione può rendere più difficile il controllo delle porte aperte. Tenere anche presente che un Service Pack o un aggiornamento cumulativo può modificare il percorso del file eseguibile di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , rendendo non valida la regola del firewall.  
  
##### <a name="to-add-a-program-exception-to-the-firewall-using-windows-firewall-with-advanced-security"></a>Per aggiungere un'eccezione del programma al firewall usando Windows Firewall con protezione avanzata
  
1. Dal menu Start digitare *wf.msc*. Fare clic su **Windows Firewall con sicurezza avanzata**.

1. Nel riquadro sinistro fare clic su **Regole connessioni in entrata**.

1. Nel riquadro destro, in **Azioni** fare clic su **Nuova regola**. Verrà aperta la **Creazione guidata nuova regola connessioni in entrata**.

1. In **Tipo di regola** fare clic su **Programma**. Scegliere **Avanti**.

1. In **Programma** fare clic su **Percorso programma**. Fare clic su **Sfoglia** per individuare l'istanza di SQL Server. Il programma è chiamato sqlservr.exe e in genere si trova in:

   `C:\Program Files\Microsoft SQL Server\MSSQL13.<InstanceName>\MSSQL\Binn\sqlservr.exe`

   Scegliere **Avanti**.

1. In **Operazione** fare clic su **Consenti la connessione**.  

1. In Profilo includere tutti e tre i profili. Scegliere **Avanti**.

1. In **Nome** digitare un nome per la regola. Fare clic su **Fine**.

Per altre informazioni sugli endpoint, vedere [Configurazione del Motore di database per l'attesa su più porte TCP](../../database-engine/configure-windows/configure-the-database-engine-to-listen-on-multiple-tcp-ports.md) e [Viste del catalogo degli endpoint &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/endpoints-catalog-views-transact-sql.md). 
  
###  <a name="BKMK_ssas"></a> Porte utilizzate da Analysis Services  
 Nella tabella seguente sono indicate le porte più utilizzate da [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
|Funzionalità|Port|Commenti|  
|-------------|----------|--------------|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|Porta TCP 2383 per l'istanza predefinita|La porta standard per l'istanza predefinita di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser|Porta TCP 2382 necessaria solo per un'istanza denominata di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|Le richieste di connessione client per un'istanza denominata di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] che non specificano un numero di porta vengono indirizzate alla porta 2382, ovvero la porta su cui è in attesa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser la richiesta viene quindi reindirizzata alla porta utilizzata dall'istanza denominata.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] configurato per l'uso tramite IIS/HTTP<br /><br /> Il Servizio PivotTable® utilizza HTTP o HTTPS|Porta TCP 80|Utilizzata per una connessione HTTP tramite un URL.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] configurato per l'uso tramite IIS/HTTPS<br /><br /> Il Servizio PivotTable® utilizza HTTP o HTTPS|Porta TCP 443|Utilizzata per una connessione HTTPS tramite un URL. HTTPS è una connessione HTTP che utilizza il protocollo SSL (Secure Sockets Layer).|  
  
 Se gli utenti accedono a [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] tramite IIS e Internet, è necessario aprire la porta su cui IIS è in attesa e specificare la porta nella stringa di connessione client. In questo caso, non è necessario aprire alcuna porta per l'accesso diretto ad [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. È consigliabile limitare la porta predefinita 2389 e la porta 2382 insieme a tutte le altre porte non necessarie.  
  
 Per istruzioni dettagliate su come configurare Windows Firewall per [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], vedere [Configurare Windows Firewall per consentire l'accesso ad Analysis Services](../../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md).  
  
###  <a name="BKMK_ssrs"></a> Porte utilizzate da Reporting Services  
Nella tabella seguente sono indicate le porte più utilizzate da [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
|Funzionalità|Port|Commenti|  
|-------------|----------|--------------|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Servizi Web|Porta TCP 80|Utilizzata per una connessione HTTP a [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] tramite un URL. È consigliabile non usare la regola preconfigurata **Servizi Web (HTTP)**. Per ulteriori informazioni, vedere la sezione [Interazione con altre regole del firewall](#BKMK_other_rules) più avanti.|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] configurato per l'utilizzo tramite HTTPS|Porta TCP 443|Utilizzata per una connessione HTTPS tramite un URL. HTTPS è una connessione HTTP che utilizza il protocollo SSL (Secure Sockets Layer). È consigliabile non usare la regola preconfigurata **Servizi Web protetti (HTTP)**. Per ulteriori informazioni, vedere la sezione [Interazione con altre regole del firewall](#BKMK_other_rules) più avanti.|  
  
Quando [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] si connette a un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)] o di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], è necessario aprire anche le porte adatte per quei servizi. Per istruzioni dettagliate su come configurare Windows Firewall per [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], vedere [Configurare un firewall per l'accesso al server di report](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md).  
  
###  <a name="BKMK_ssis"></a> Porte utilizzate da Integration Services  
 Nella tabella seguente sono indicate le porte utilizzate dal servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
|Funzionalità|Port|Commenti|  
|-------------|----------|--------------|  
|[!INCLUDE[msCoName](../../includes/msconame-md.md)] Remote Procedure Call (MS RPC)<br /><br /> Utilizzate dal runtime di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .|Porta TCP 135<br /><br /> Vedere [Considerazioni speciali per la porta 135](#BKMK_port_135)|Il servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] utilizza il protocollo DCOM sulla porta 135. Gestione controllo servizi utilizza la porta 135 per eseguire operazioni come l'avvio e l'arresto del servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e la trasmissione di richieste di controllo al servizio in esecuzione. Il numero di porta non può essere modificato.<br /><br /> Questa porta deve essere aperta solo se si sta effettuando la connessione a un'istanza remota del servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] da [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] o da un'applicazione personalizzata.|  
  
Per istruzioni dettagliate su come configurare Windows Firewall per [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], vedere [Integration Services Service &#40;SSIS Service&#41;](../../integration-services/service/integration-services-service-ssis-service.md) (Servizio Integration Services - Servizio SSIS).  
  
###  <a name="BKMK_additional_ports"></a> Porte e servizi aggiuntivi  
Nella tabella riportata di seguito sono elencati i servizi e le porte da cui potrebbe dipendere [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
|Scenario|Port|Commenti|  
|--------------|----------|--------------|  
|Strumentazione gestione Windows (WMI)<br /><br /> Per ulteriori informazioni su Strumentazione gestione Windows (WMI), vedere [WMI Provider for Configuration Management Concepts](../../relational-databases/wmi-provider-configuration/wmi-provider-for-configuration-management.md).|WMI viene eseguito come parte di un host del servizio condiviso con porte assegnate tramite DCOM e potrebbe utilizzare la porta TCP 135.<br /><br /> Vedere [Considerazioni speciali per la porta 135](#BKMK_port_135)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizza WMI per elencare e gestire servizi. È consigliabile usare il gruppo di regole preconfigurate **Strumentazione gestione Windows (WMI)**. Per ulteriori informazioni, vedere la sezione [Interazione con altre regole del firewall](#BKMK_other_rules) più avanti.|  
|[!INCLUDE[msCoName](../../includes/msconame-md.md)] Distributed Transaction Coordinator (MS DTC)|Porta TCP 135<br /><br /> Vedere [Considerazioni speciali per la porta 135](#BKMK_port_135)|Se l'applicazione utilizza transazioni distribuite, può essere necessario configurare il firewall in modo da consentire il flusso del traffico di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Distributed Transaction Coordinator (MS DTC) tra istanze MS DTC separate e tra MS DTC e strumenti di gestione delle risorse come [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. È consigliabile utilizzare il gruppo di regole preconfigurato **Distributed Transaction Coordinator** .<br /><br /> Quando è configurato un solo oggetto MS DTC condiviso per l'intero cluster in un gruppo di risorse distinto, è necessario aggiungere sqlservr.exe come eccezione al firewall.|  
|Il pulsante Sfoglia in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] utilizza il protocollo UDP per connettersi al servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser. Per altre informazioni, vedere [Servizio SQL Server Browser &#40;Motore database e SSAS&#41;](../../database-engine/configure-windows/sql-server-browser-service-database-engine-and-ssas.md).|Porta UDP 1434|UDP è un protocollo senza connessione.<br /><br /> Il firewall include un'impostazione, denominata [UnicastResponsesToMulticastBroadcastDisabled Property of the INetFwProfile Interface](https://go.microsoft.com/fwlink/?LinkId=118371) che controlla il comportamento del firewall relativamente alle risposte unicast a una richiesta UDP di trasmissione (o multicast).  Sono possibili due comportamenti:<br /><br /> Se l'impostazione è TRUE, non sono consentite risposte unicast a una trasmissione. I servizi di enumerazione non possono essere eseguiti correttamente.<br /><br /> Se l'impostazione è FALSE (impostazione predefinita), le risposte unicast sono consentite per 3 secondi. La durata non è configurabile. In una rete congestionata o ad alta latenza o nei server con carico elevato i tentativi di enumerazione delle istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] potrebbero restituire un elenco parziale e fuorviante per gli utenti.|  
|<a name="BKMK_IPsec"></a> Traffico IPsec|Porta UDP 500 e porta UDP 4500|Se i criteri di dominio richiedono che le comunicazioni di rete vengano eseguite tramite IPsec, è necessario aggiungere anche le porte UDP 4500 e UDP 500 all'elenco delle eccezioni. IPsec è un'opzione che usa la **Creazione guidata nuova regola connessioni in entrata** nello snap-in Windows Firewall. Per altre informazioni, vedere [Utilizzo dello snap-in Windows Firewall con sicurezza avanzata](#BKMK_WF_msc) più avanti.|  
|Utilizzo dell'autenticazione di Windows con domini trusted|Per consentire le richieste di autenticazione, è necessario configurare i firewall.|Per ulteriori informazioni, vedere [Configurazione di un firewall per domini e trust](https://support.microsoft.com/kb/179442/).|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e servizio cluster di Windows|Il clustering richiede porte aggiuntive non direttamente correlate a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|Per ulteriori informazioni, vedere [Enable a network for cluster use](https://go.microsoft.com/fwlink/?LinkId=118372).|  
|Spazi dei nomi URL riservati in HTTP Server API (HTTP.SYS)|Probabilmente la porta TCP 80, ma può essere configurata su altre porte. Per informazioni generali, vedere [Configuring HTTP and HTTPS](https://go.microsoft.com/fwlink/?LinkId=118373).|Per informazioni specifiche [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sulla prenotazione di un endpoint HTTP.SYS usando HttpCfg.exe, vedere [Informazioni su prenotazioni e registrazione URL &#40;Gestione configurazione SSRS&#41;](../../reporting-services/install-windows/about-url-reservations-and-registration-ssrs-configuration-manager.md).|  
  
##  <a name="BKMK_port_135"></a> Considerazioni speciali per la porta 135  
 Quando si utilizza RPC con TCP/IP o UDP/IP come trasporto, le porte in ingresso spesso vengono assegnate dinamicamente ai servizi di sistema, se necessario. Vengono utilizzate le porte TCP/IP e UDP/IP che sono più grandi della porta 1024 e spesso vengono definite in modo informale "porte RPC casuali". In questi casi, i client RPC si basano sul mapper di endpoint RPC per indicare le porte dinamiche assegnate al server. Per alcuni servizi basati su RPC è possibile configurare una porta specifica anziché consentire a RPC un'assegnazione dinamica. È inoltre possibile limitare l'intervallo di porte assegnate dinamicamente da RPC a un piccolo intervallo, indipendentemente dal servizio. Poiché la porta 135 viene utilizzata per molti servizi, viene attaccata di frequente da utenti malintenzionati. Quando si apre la porta 135, limitare l'ambito della regola del firewall.  
  
 Per ulteriori informazioni sulla porta 135, consultare i riferimenti seguenti:  
  
-   [Panoramica dei servizi e requisiti per le porte di rete per il sistema server Windows](https://support.microsoft.com/kb/832017)  
  
-   [Troubleshooting RPC Endpoint Mapper errors using the Windows Server 2003 Support Tools from the product CD](https://support.microsoft.com/kb/839880)  
  
-   [Remote procedure call (RPC)](https://go.microsoft.com/fwlink/?LinkId=118375)  
  
-   [Configurazione dell'allocazione delle porte dinamiche RPC perché funzionino con i firewall](https://support.microsoft.com/kb/154596/)  
  
##  <a name="BKMK_other_rules"></a> Interazione con altre regole del firewall  
 Per effettuare la configurazione di Windows Firewall, è necessario utilizzare regole e gruppi di regole. Ogni regola o gruppo di regole in genere è associato a un particolare programma o un servizio ed è possibile che tale programma o servizio modifichi o elimini la regola all'insaputa dell'utente. I gruppi di regole **Servizi Web (HTTP)** e **Servizi Web (HTTPS)** , ad esempio, sono associati a IIS. L'abilitazione di queste due regole comporterà l'apertura delle porte 80 e 443 e l'attivazione delle funzionalità di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che dipendono da tali porte. È tuttavia possibile che gli amministratori che configurano IIS le modifichino o disabilitino. Pertanto, se si utilizza la porta 80 o la porta 443 per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è necessario creare una regola o un gruppo di regole personalizzate che mantenga la configurazione delle porte desiderata, indipendentemente dalle altre regole IIS.  
  
 Lo snap-in MMC Windows Firewall con sicurezza avanzata consente tutto il traffico che corrisponde alle regole di concessione applicabili. Pertanto, se esistono due regole applicabili entrambe alla porta 80 (con parametri diversi), il traffico che corrisponde all'una o all'altra verrà consentito. Se una regola consente il traffico sulla porta 80 da una subnet locale e l'altra il traffico da qualsiasi indirizzo, l'effetto finale è che tutto il traffico verso la porta 80 verrà consentito, indipendentemente dall'origine. Per gestire efficacemente l'accesso a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], gli amministratori devono verificare periodicamente tutte le regole del firewall abilitate sul server.  
  
##  <a name="BKMK_profiles"></a> Panoramica sui profili del firewall  
 I profili del firewall vengono illustrati in [Guida introduttiva a Windows Firewall con sicurezza avanzata](https://go.microsoft.com/fwlink/?LinkId=116080) nella sezione relativa al **firewall host con riconoscimento del percorso di rete**. Per riepilogare, i sistemi operativi sono in grado di identificare e memorizzare ciascuna delle reti alle quali si connettono per tutto quello che riguarda la connettività, le connessioni e la categoria.  
  
 Sono disponibili tre tipi di percorsi di rete in Windows Firewall con sicurezza avanzata:  
  
-   Dominio. Windows può autenticare l'accesso al controller di dominio per il dominio al quale il computer viene unito.  
  
-   Pubblica. Ad eccezione di quelle del dominio, tutte le reti sono inizialmente classificate come pubbliche. Le reti che rappresentano connessioni dirette a Internet o che si trovano in luoghi pubblici, ad esempio aeroporti e Internet caffè, dovrebbero essere sempre pubbliche.  
  
-   Privata. Una rete identificata da un utente o da un'applicazione come privata. Solo le reti attendibili devono essere identificate come reti private. In genere gli utenti desiderano identificare come private le reti domestiche o di piccole aziende.  
  
 L'amministratore può creare un profilo per ogni tipo di percorso di rete, contenente diversi criteri del firewall. È possibile applicare un solo profilo alla volta. L'ordine di applicazione è il seguente:  
  
1.  Se tutte le interfacce vengono autenticate nel controller di dominio per il dominio del quale il computer è membro, il profilo del dominio viene applicato.  
  
2.  Se tutte le interfacce sono autenticate nel controller di dominio o sono connesse a reti classificate come percorsi di rete privati, viene applicato il profilo privato.  
  
3.  In caso contrario, viene applicato il profilo pubblico.  
  
 Utilizzare lo snap-in MMC Windows Firewall con sicurezza avanzata per visualizzare e configurare tutti i profili del firewall. L'elemento **Windows Firewall** del Pannello di controllo configura solo il profilo corrente.  
  
##  <a name="BKMK_additional_settings"></a> Impostazioni aggiuntive del firewall mediante l'elemento Windows Firewall del Pannello di controllo  
 Le eccezioni aggiunte al firewall possono limitare l'apertura della porta alle connessioni in ingresso da computer specifici o dalla subnet locale. Questa restrizione dell'ambito di apertura della porta è consigliata e può ridurre il livello di esposizione del computer agli utenti malintenzionati.  
  
> [!NOTE]  
>  L'uso dell'elemento **Windows Firewall** del Pannello di controllo configura solo il profilo del firewall corrente.  
  
### <a name="to-change-the-scope-of-a-firewall-exception-using-the-windows-firewall-item-in-control-panel"></a>Per modificare l'ambito dell'eccezione di un firewall mediante l'elemento Windows Firewall del Pannello di controllo  
  
1.  Nell'elemento **Windows Firewall** del Pannello di controllo selezionare un programma o una porta nella scheda **Eccezioni** , quindi fare clic su **Proprietà** o **Modifica**.  
  
2.  Nella finestra di dialogo **Modifica programma** o **Modifica porta** fare clic su **Cambia ambito**.  
  
3.  Selezionare una delle opzioni seguenti:  
  
    -   **Tutti i computer (compresi quelli in Internet)**  
  
         Non consigliata. Questa opzione consente a tutti i computer che riescono a comunicare con il computer dell'utente di connettersi al programma o alla porta specificata. Questa impostazione potrebbe essere necessaria per consentire la presentazione delle informazioni a utenti anonimi su Internet, ma aumenta l'esposizione a utenti malintenzionati. L'esposizione può essere ulteriormente aumentata se insieme a questa impostazione viene abilitato anche l'attraversamento NAT (Network Address Translation), ad esempio l'opzione Consenti attraversamento confini.  
  
    -   **Solo la rete (subnet) locale**  
  
         Questa impostazione offre una protezione maggiore rispetto a **Tutti i computer**. Solo i computer che si trovano nella subnet locale della rete possono connettersi al programma o alla porta.  
  
    -   **Elenco personalizzato:**  
  
     Solo i computer che dispongono degli indirizzi IP elencati possono connettersi. Questa opzione offre un livello di protezione ancora più elevato di **Solo la rete (subnet) locale**, anche se i computer client che usano DHCP possono modificare occasionalmente l'indirizzo IP. Pertanto il computer desiderato non sarà in grado di connettersi. Un altro computer, a cui non è stata concessa l'autorizzazione, potrebbe accettare l'indirizzo IP elencato ed essere in grado di connettersi. L'opzione **Elenco personalizzato** può risultare adatta per elencare altri server configurati per l'utilizzo di un indirizzo IP fisso anche se gli indirizzi IP possono essere soggetti a spoofing da parte di un intruso. L'efficacia delle regole di limitazione del firewall equivale solo a quella dell'infrastruttura di rete.  
  
##  <a name="BKMK_WF_msc"></a> Utilizzo dello snap-in Windows Firewall con sicurezza avanzata  
 È possibile configurare impostazioni del firewall avanzate aggiuntive tramite lo snap-in MMC Windows Firewall con sicurezza avanzata. Lo snap-in include una procedura guidata di creazione delle regole ed espone impostazioni aggiuntive non disponibili nell'elemento **Windows Firewall** del Pannello di controllo. Sono incluse le seguenti impostazioni:  
  
-   Impostazioni di crittografia  
  
-   Restrizioni dei servizi  
  
-   Restrizione delle connessioni per i computer in base al nome  
  
-   Restrizione delle connessioni a utenti o profili specifici  
  
-   Attraversamento dei confini che consente al traffico di ignorare i router NAT (Network Address Translation)  
  
-   Configurazione di regole in uscita  
  
-   Configurazione di regole di sicurezza  
  
-   Richiesta di IPsec per le connessioni in ingresso  
  
### <a name="to-create-a-new-firewall-rule-using-the-new-rule-wizard"></a>Per creare una nuova regola del firewall utilizzando la Creazione guidata nuova regola connessioni in entrata  
  
1.  Nel menu Start, scegliere **Esegui**, digitare **WF.msc**e quindi fare clic su **OK**.  
  
2.  In **Windows Firewall con sicurezza avanzata**, nel riquadro sinistro, fare clic con il pulsante destro del mouse su **Regole in entrata**, quindi scegliere **Nuova regola**.  
  
3.  Completare la **Creazione guidata nuova regola connessioni in entrata** utilizzando le impostazioni desiderate.  
  
##  <a name="BKMK_troubleshooting"></a> Risoluzione dei problemi relativi alle impostazioni del firewall  
 Le tecniche e gli strumenti illustrati di seguito possono risultare utili per la risoluzione dei problemi del firewall.  
  
-   Lo stato della porta più efficace è l'unione di tutte le regole relative alla porta. Quando si tenta di bloccare l'accesso attraverso una porta, può essere utile verificare tutte le regole in cui viene citato il numero della porta. A questo scopo, utilizzare lo snap-in MMC Windows Firewall con sicurezza avanzata e ordinare le regole in entrata e in uscita in base al numero della porta.  
  
-   Verificare le porte attive nel computer su cui è in esecuzione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Questo processo di verifica include l'individuazione delle porte TCP/IP in attesa, nonché dello stato delle porte.  
  
     Per verificare quali porte siano in attesa, usare l'utilità da riga di comando **netstat** . Oltre alle connessioni TCP attive, l'utilità **netstat** visualizza anche un'ampia gamma di statistiche e informazioni relative al protocollo IP.  
  
    #### <a name="to-list-which-tcpip-ports-are-listening"></a>Per elencare le porte TCP/IP in attesa  
  
    1.  Aprire una finestra del prompt dei comandi.  
  
    2.  Al prompt dei comandi digitare **netstat -n -a**.  
  
         L'opzione **-n** indica a **netstat** di visualizzare in valori numerici l'indirizzo e il numero di porta delle connessioni TCP attive. L'opzione **-a** indica a **netstat** di visualizzare le porte TCP e UDP su cui è in attesa il computer.  
  
-   L'utilità **PortQry** può essere usata per indicare lo stato delle porte TCP/IP come in attesa, non in attesa o filtrato. Uno stato filtrato non indica se la porta è o non è in attesa, bensì che l'utilità non ha ricevuto alcuna risposta dalla porta. È possibile scaricare l'utilità **PortQry** dalla pagina relativa nell' [area download Microsoft](https://go.microsoft.com/fwlink/?LinkId=28590).  
  
## <a name="see-also"></a>Vedere anche  
 [Panoramica dei servizi e requisiti per le porte di rete per il sistema server Windows](https://support.microsoft.com/kb/832017)   
 [Procedura: Configurare le impostazioni del firewall (database SQL di Azure)](https://azure.microsoft.com/documentation/articles/sql-database-configure-firewall-settings/)  
  
  
