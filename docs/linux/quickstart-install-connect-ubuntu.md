---
title: Introduzione a SQL Server su Ubuntu | Microsoft Docs
description: Questa Guida introduttiva illustra come installare SQL Server 2017 o SQL Server 2019 in Ubuntu e quindi creare ed eseguire query di un database con sqlcmd.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 07/16/2018
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: 31c8c92e-12fe-4728-9b95-4bc028250d85
ms.openlocfilehash: 917e43dd6a9c78e5199967df58a2d46c4843cf13
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/15/2018
ms.locfileid: "51677949"
---
# <a name="quickstart-install-sql-server-and-create-a-database-on-ubuntu"></a>Guida introduttiva: Installare SQL Server e creare un database in Ubuntu

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

In questa Guida introduttiva, si installa SQL Server 2017 o SQL Server 2019 preview su Ubuntu 16.04. Quindi Connettiti **sqlcmd** per creare il primo database ed eseguire query.

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

In questa Guida introduttiva è installare SQL Server 2019 preview su Ubuntu 16.04. Quindi Connettiti **sqlcmd** per creare il primo database ed eseguire query.

::: moniker-end

> [!TIP]
> Questa esercitazione richiede l'input dell'utente e una connessione a internet. Se è interessati al [automatica](sql-server-linux-setup.md#unattended) oppure [offline](sql-server-linux-setup.md#offline) procedure di installazione, vedere [informazioni aggiuntive sull'installazione per SQL Server in Linux](sql-server-linux-setup.md).

## <a name="prerequisites"></a>Prerequisiti

È necessario disporre di un computer con Ubuntu 16.04 **almeno 2 GB** di memoria.

Per installare Ubuntu nel proprio computer, visitare [ https://www.ubuntu.com/download/server ](https://www.ubuntu.com/download/server). È anche possibile creare macchine virtuali Ubuntu in Azure. Visualizzare [creare e gestire VM Linux con l'interfaccia della riga di comando Azure](https://docs.microsoft.com/azure/virtual-machines/linux/tutorial-manage-vm).

> [!NOTE]
> A questo punto, il [sottosistema Windows per Linux](https://msdn.microsoft.com/commandline/wsl/about) per Windows 10 non è supportato come destinazione di installazione.

Per altri requisiti di sistema, vedere [requisiti di sistema per SQL Server in Linux](sql-server-linux-setup.md#system).

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

## <a id="install"></a>Installare SQL Server

Per configurare SQL Server in Ubuntu, eseguire i comandi seguenti in un terminale per installare il **mssql-server** pacchetto.

1. Importare le chiavi GPG repository pubblico:

   ```bash
   wget -qO- https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

2. Registrare il repository di Microsoft SQL Server Ubuntu:

   ```bash
   sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017.list)"
   ```

   > [!TIP]
   > Se si vuole provare 2019 di SQL Server, è necessario registrare invece le **Preview (2019)** repository. Usare il comando seguente per le installazioni di SQL Server 2019:
   >
   > ```bash
   > sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-preview.list)"
   > ```

3. Eseguire i comandi seguenti per installare SQL Server:

   ```bash
   sudo apt-get update
   sudo apt-get install -y mssql-server
   ```

4. Dopo il completamento dell'installazione del pacchetto, eseguire **mssql-conf setup** e seguire le istruzioni per impostare la password account SA e scegliere l'edizione.

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

   > [!TIP]
   > Le seguenti edizioni di SQL Server 2017 sono concessa in licenza gratuitamente: Evaluation, Developer ed Express.

   > [!NOTE]
   > Assicurarsi di specificare una password complessa per l'account SA (caratteri di lunghezza 8 minimo, incluse le lettere maiuscole e lettere minuscole, cifre in base 10 e/o i simboli non alfanumerici).

5. Al termine della configurazione, verificare che il servizio sia in esecuzione:

   ```bash
   systemctl status mssql-server
   ```

6. Se si prevede di connettersi in remoto, si potrebbe essere necessario anche aprire la porta TCP di SQL Server (valore predefinito 1433) nel firewall.

A questo punto, SQL Server è in esecuzione nel computer Ubuntu ed è pronto per l'uso.

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

## <a id="install"></a>Installare SQL Server

Per configurare SQL Server in Ubuntu, eseguire i comandi seguenti in un terminale per installare il **mssql-server** pacchetto.

1. Importare le chiavi GPG repository pubblico:

   ```bash
   wget -qO- https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

2. Registrare il repository di Microsoft SQL Server Ubuntu per l'anteprima di SQL Server 2019:

   ```bash
   sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-preview.list)"
   ```

3. Eseguire i comandi seguenti per installare SQL Server:

   ```bash
   sudo apt-get update
   sudo apt-get install -y mssql-server
   ```

4. Dopo il completamento dell'installazione del pacchetto, eseguire **mssql-conf setup** e seguire le istruzioni per impostare la password account SA e scegliere l'edizione.

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

   > [!NOTE]
   > Assicurarsi di specificare una password complessa per l'account SA (caratteri di lunghezza 8 minimo, incluse le lettere maiuscole e lettere minuscole, cifre in base 10 e/o i simboli non alfanumerici).

5. Al termine della configurazione, verificare che il servizio sia in esecuzione:

   ```bash
   systemctl status mssql-server
   ```

6. Se si prevede di connettersi in remoto, si potrebbe essere necessario anche aprire la porta TCP di SQL Server (valore predefinito 1433) nel firewall.

A questo punto, anteprima di SQL Server 2019 è in esecuzione nel computer Ubuntu e sia pronto per l'uso.

::: moniker-end

## <a id="tools"></a>Installare gli strumenti da riga di comando di SQL Server

Per creare un database, è necessario connettersi con uno strumento che è possibile eseguire istruzioni Transact-SQL in SQL Server. La procedura seguente installa gli strumenti da riga di comando di SQL Server: [sqlcmd](../tools/sqlcmd-utility.md) e [bcp](../tools/bcp-utility.md).

Usare la procedura seguente per installare il **mssql-tools** in Ubuntu. 

1. Importare le chiavi GPG repository pubblico.

   ```bash
   curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

1. Registrare il repository Microsoft Ubuntu.

   ```bash
   curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list | sudo tee /etc/apt/sources.list.d/msprod.list
   ```

1. Aggiornare l'elenco delle origini ed eseguire il comando di installazione con il pacchetto di sviluppo unixODBC.

   ```bash
   sudo apt-get update 
   sudo apt-get install mssql-tools unixodbc-dev
   ```

   > [!Note] 
   > Eseguire l'aggiornamento alla versione più recente di **mssql-tools** eseguire i comandi seguenti:
   >    ```bash
   >   sudo apt-get update 
   >   sudo apt-get install mssql-tools 
   >   ```

1. **Facoltativo**: aggiungere `/opt/mssql-tools/bin/` per il **percorso** variabile di ambiente in una shell bash.

   Per rendere **sqlcmd/bcp** accessibile da shell di bash per sessioni di accesso, modificare le **PATH** nel **~/.bash_profile** file con il comando seguente:

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
   ```

   Per rendere **sqlcmd/bcp** accessibile da shell di bash per le sessioni interattive/senza accesso, modificare il **PATH** nel **~/.bashrc** file con il comando seguente:

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
   source ~/.bashrc
   ```

[!INCLUDE [Connect, create, and query data](../includes/sql-linux-quickstart-connect-query.md)]
