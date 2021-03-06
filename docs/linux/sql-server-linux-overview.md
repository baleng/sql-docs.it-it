---
title: Panoramica di SQL Server in Linux | Microsoft Docs
description: Questo articolo descrive come SQL Server viene eseguito in Linux e fornisce informazioni su come per altre informazioni.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 09/25/2018
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: 9dcc6a90-0add-42c2-815b-862e4e2a21ac
ms.openlocfilehash: bf1d3b2b494377eb964f4a30ea97a48bd1dfcff7
ms.sourcegitcommit: a2be75158491535c9a59583c51890e3457dc75d6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/07/2018
ms.locfileid: "51269525"
---
# <a name="sql-server-on-linux"></a>SQL Server in Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

::: moniker range="= sql-server-2017 || = sqlallproducts-allversions"
A partire da SQL Server 2017, viene eseguito SQL Server in Linux. È lo stesso motore di database di SQL Server, con molti servizi indipendentemente dal sistema operativo e le funzionalità di simile.
::: moniker-end

::: moniker range=">= sql-server-ver15 || >= sql-server-linux-ver15"
Anteprima di SQL Server 2019 viene eseguito su Linux. È lo stesso motore di database di SQL Server, con molti servizi indipendentemente dal sistema operativo e le funzionalità di simile. Per altre informazioni su questa versione, vedere [nuove funzionalità di anteprima di SQL Server 2019 per Linux](../sql-server/what-s-new-in-sql-server-ver15.md#sqllinux).
::: moniker-end

::: moniker range="= sql-server-2017"
> [!TIP]
> [Anteprima di SQL Server 2019](sql-server-linux-overview.md?view=sql-server-ver15) è stato rilasciato! Per scoprire quali sono le novità nella versione più recente per Linux, vedere [nuove funzionalità di anteprima di SQL Server 2019 per Linux](../sql-server/what-s-new-in-sql-server-ver15.md?view=sql-server-ver15#sqllinux).
::: moniker-end

::: moniker range="= sql-server-linux-2017"
> [!TIP]
> [Anteprima di SQL Server 2019](sql-server-linux-overview.md?view=sql-server-linux-ver15) è stato rilasciato! Per scoprire quali sono le novità nella versione più recente per Linux, vedere [nuove funzionalità di anteprima di SQL Server 2019 per Linux](../sql-server/what-s-new-in-sql-server-ver15.md?view=sql-server-linux-ver15#sqllinux).
::: moniker-end

::: moniker range="= sqlallproducts-allversions"
> [!TIP]
> Anteprima di SQL Server 2019 è stato rilasciato! Per scoprire quali sono le novità nella versione più recente per Linux, vedere [nuove funzionalità di anteprima di SQL Server 2019 per Linux](../sql-server/what-s-new-in-sql-server-ver15.md#sqllinux).
::: moniker-end

## <a name="install"></a>Install

Per iniziare, installare SQL Server in Linux con una delle seguenti esercitazioni di avvio rapido:

- [Installare in Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md)
- [Installare in SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
- [Installazione in Ubuntu](quickstart-install-connect-ubuntu.md)
- [Esecuzione in Docker](quickstart-install-connect-docker.md)
- [Eseguire il provisioning di una macchina virtuale SQL in Azure](/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=%2fsql%2flinux%2ftoc.json)

> [!NOTE]
> Docker stesso viene eseguito su più piattaforme, il che significa che è possibile eseguire l'immagine Docker in Linux, Mac e Windows.

## <a name="connect"></a>Connect

Dopo l'installazione, connettersi all'istanza di SQL Server nel computer Linux. È possibile connettersi in locale o in modalità remota e con un'ampia gamma di strumenti e driver. Le guide rapide viene illustrato come usare il [sqlcmd](sql-server-linux-setup-tools.md) lo strumento da riga di comando. Altri strumenti includono:

| Strumento | Esercitazione |
|-----|-----|
| Visual Studio Code (VS Code) | [Usare Visual Studio Code con SQL Server in Linux](sql-server-linux-develop-use-vscode.md) |
| SQL Server Management Studio (SSMS) | [Usare SSMS in Windows per connettersi a SQL Server in Linux](sql-server-linux-manage-ssms.md) |
| SQL Server Data Tools (SSDT) | [Usare SSDT con SQL Server in Linux](sql-server-linux-develop-use-ssdt.md) |

## <a name="explore"></a>Esplora

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

In tutte le piattaforme supportate, tra cui Linux, SQL Server 2017 offre lo stesso motore di database sottostante. Di conseguenza, molte funzionalità e le funzionalità esistenti funzionano nello stesso modo in Linux. In questa area della documentazione di espone alcune di queste funzionalità da una prospettiva di Linux. Chiama anche le aree che presentano requisiti specifici in Linux.

Se ha già familiarità con SQL Server, consultare il [note sulla versione](sql-server-linux-release-notes.md) per linee guida generali e i problemi noti per questa versione. Quindi esaminare [novità di SQL Server in Linux](sql-server-linux-whats-new.md) nonché [novità di SQL Server 2017 complessiva](../sql-server/what-s-new-in-sql-server-2017.md).

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15"

[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] in tutte le piattaforme supportate, tra cui Linux, ha lo stesso motore di database sottostante. Di conseguenza, molte funzionalità e le funzionalità esistenti funzionano nello stesso modo in Linux. In questa area della documentazione di espone alcune di queste funzionalità da una prospettiva di Linux. Chiama anche le aree che presentano requisiti specifici in Linux.

Se ha già familiarità con SQL Server in Linux, vedere la [note sulla versione](sql-server-linux-release-notes-2019.md) per linee guida generali e i problemi noti per questa versione. Quindi esaminare [nuove funzionalità per l'anteprima di SQL Server 2019 in Linux](../sql-server/what-s-new-in-sql-server-ver15.md?view=sql-server-ver15).

::: moniker-end

<!--SQL Server All Versions-->
::: moniker range="=sqlallproducts-allversions"

SQL Server 2017 e [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] hanno lo stesso motore di database sottostanti in tutte le piattaforme supportate, tra cui Linux. Di conseguenza, molte funzionalità e le funzionalità esistenti funzionano nello stesso modo in Linux. In questa area della documentazione di espone alcune di queste funzionalità da una prospettiva di Linux. Chiama anche le aree che presentano requisiti specifici in Linux.

Se ha già familiarità con SQL Server in Linux, consultare le note sulla versione:

- [Note sulla versione di SQL Server 2017](sql-server-linux-release-notes.md)
- [Note sulla versione di anteprima di SQL Server 2019](sql-server-linux-release-notes-2019.md)

Quindi è Esaminiamo novità recenti:

- [Novità di SQL Server 2017](sql-server-linux-whats-new.md)
- [Novità per SQL Server 2019 anteprima in Linux](../sql-server/what-s-new-in-sql-server-ver15.md#sqllinux)

::: moniker-end

> [!TIP]
> Per le risposte alle domande più frequenti, vedere la [SQL Server in Linux FAQ](sql-server-linux-faq.md).

[!INCLUDE[Get Help Options](../includes/paragraph-content/get-help-options.md)]

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]
