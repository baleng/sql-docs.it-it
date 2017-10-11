---
title: 'Passaggio 1: Creazione di cartelle di lavoro e le variabili di ambiente | Documenti Microsoft'
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
ms.assetid: 45091ba2-ea3d-4399-9814-489d812b42cc
caps.latest.revision: 19
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: de69cfa9d63daa6cd5638774aba2540fd2ffdbaa
ms.contentlocale: it-it
ms.lasthandoff: 09/26/2017

---
# <a name="lesson-1-1---creating-working-folders-and-environment-variables"></a>Lezione 1-1-Creazione di cartelle di lavoro e le variabili di ambiente
In questa attività si procederà alla creazione della cartella di lavoro C:\DeploymentTutorial e delle nuove variabili di ambiente`DataTransfer` e `LoadXMLData`che verranno utilizzate nelle attività successive dell'esercitazione.  
  
La cartella di lavoro si trova nella radice dell'unità C. È comunque possibile utilizzare un'unità o un percorso diverso, se necessario. In questo caso, sarà tuttavia necessario prendere nota del percorso e quindi utilizzarlo ogni volta che nell'esercitazione si fa riferimento al percorso della cartella di lavoro DeploymentTutorial.  
  
In una lezione successiva i pacchetti salvati nel file system verranno distribuiti nella tabella sysssispackages del database msdb di[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . La situazione ideale è quella in cui i pacchetti di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] vengono distribuiti in un altro computer. In caso contrario, è comunque possibile acquisire una notevole familiarità con le procedure illustrate in questa esercitazione distribuendo i pacchetti in un'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] sul computer locale. Alle variabili di ambiente utilizzate nel computer locale e in quello di destinazione vengono assegnati i medesimi nomi, ma valori diversi. Nel computer locale il valore della variabile di ambiente `DataTransfer` fa ad esempio riferimento alla cartella C:\DeploymentTutorial, mentre in quello di destinazione la stessa variabile `DataTransfer` fa riferimento alla cartella C:\DeploymentTutorialInstall.  
  
Se si prevede di eseguire la distribuzione nel computer locale, è necessario creare un unico set di variabili di ambiente. Per poter eseguire la distribuzione locale sarà comunque necessario impostare le variabili di ambiente sui valori appropriati.  
  
Se si prevede di distribuire i pacchetti in un altro computer, è necessario creare due set di variabili di ambiente, uno per il computer locale e uno per quello di destinazione. È possibile creare subito le variabili per il computer di origine e successivamente quelle per il computer di destinazione. Per poter installare i pacchetti nel computer di destinazione, è tuttavia necessario che in quest'ultimo siano disponibili la cartella e le variabili di ambiente.  
  
### <a name="to-create-the-local-working-folder"></a>Per creare la cartella di lavoro locale  
  
1.  Fare clic con il pulsante destro del mouse sul menu Start e quindi scegliere Esplora.  
  
2.  Fare clic su **Disco locale (C:)**.  
  
3.  Scegliere **Nuovo** dal menu **File**e fare clic su **Cartella**.  
  
4.  Assegnare a Nuova cartella il nome **DeploymentTutorial**.  
  
### <a name="to-create-local-environment-variables"></a>Per creare le variabili di ambiente locali  
  
1.  Fare clic sul menu **Start** e scegliere **Pannello di controllo**.  
  
2.  In Pannello di controllo fare doppio clic su **Sistema**.  
  
3.  Nella finestra di dialogo **Proprietà del sistema** fare clic sulla scheda **Avanzate** e quindi fare clic **su Variabili d'ambiente**.  
  
4.  Nel riquadro **Variabili di sistema** della finestra di dialogo **Variabili d'ambiente** fare clic su **Nuova**.  
  
5.  Nella finestra di dialogo **Nuova variabile di sistema** digitare **DataTransfer** nella casella **Nome variabile** e **C:\DeploymentTutorial\datatransferconfig.dtsconfig** nella casella **Valore variabile** .  
  
6.  Scegliere **OK**.  
  
7.  Fare nuovamente clic su **Nuova** e digitare **LoadXMLData** nella casella **Nome variabile** e **C:\DeploymentTutorial\loadxmldataconfig.dtsconfig** nella casella **Valore variabile** .  
  
8.  Fare clic su **OK** per chiudere la finestra di dialogo **Variabili d'ambiente** .  
  
9. Fare clic su **OK** per chiudere la finestra di dialogo **Proprietà del sistema** .  
  
10. Facoltativamente, riavviare il computer. Se non si riavvia il computer, il nome della nuova variabile non verrà visualizzato nella Configurazione guidata pacchetto, ma sarà comunque possibile utilizzarla.  
  
### <a name="to-create-destination-environment-variables"></a>Per creare le variabili d'ambiente di destinazione  
  
1.  Fare clic sul menu **Start** e scegliere **Pannello di controllo**.  
  
2.  In Pannello di controllo fare doppio clic su **Sistema**.  
  
3.  Nella finestra di dialogo **Proprietà del sistema** fare clic sulla scheda **Avanzate** e quindi fare clic **su Variabili d'ambiente**.  
  
4.  Nel riquadro **Variabili di sistema** della finestra di dialogo **Variabili d'ambiente** fare clic su **Nuova**.  
  
5.  Nella finestra di dialogo **Nuova variabile di sistema** digitare **DataTransfer** nella casella **Nome variabile** e **C:\DeploymentTutorialInstall\datatransferconfig.dtsconfig** nella casella **Valore variabile** .  
  
6.  Scegliere **OK**.  
  
7.  Fare nuovamente clic su **Nuova** e digitare **LoadXMLData** nella casella **Nome variabile** e **C:\DeploymentTutorialInstall\loadxmldataconfig.dtsconfig** nella casella **Valore variabile** .  
  
8.  Fare clic su **OK** per chiudere la finestra di dialogo **Variabili d'ambiente** .  
  
9. Fare clic su **OK** per chiudere la finestra di dialogo **Proprietà del sistema** .  
  
10. Facoltativamente, riavviare il computer.  
  
## <a name="next-task-in-lesson"></a>Attività successiva della lezione  
[Passaggio 2: Creazione del progetto di distribuzione](../integration-services/lesson-1-2-creating-the-deployment-project.md)  
  
  
  
