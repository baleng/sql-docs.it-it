---
title: 'Attività 2: Caricamento dei dati fornitore in MDS utilizzando il componente aggiuntivo MDS per Excel | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.topic: conceptual
ms.assetid: 598deb57-e0cc-4e0a-aeb1-94432c094c67
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 36e50a34f708bc13da489591d73ca0521cdb5a6b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/02/2018
ms.locfileid: "48101211"
---
# <a name="task-2-uploading-supplier-data-to-mds-using-mds-add-in-for-excel"></a>Attività 2: Caricamento dei dati fornitore in MDS utilizzando il componente aggiuntivo MDS per excel
  In questa attività si pubblicano i dati puliti e fornitore **MDS** usando la **il componente aggiuntivo MDS per Excel**. Creare un'entità denominata **Supplier** nel **Suppliers** modello creato nella lezione precedente. All'entità sarà associato un attributo per ogni colonna nel file di Excel. Gli attributi Name e Code dell'entità Supplier corrispondono per la **SupplierID** e **Supplier Name** colonne in Excel.  
  
1.  Aprire **puliti e Matched Suppliers. xls** nelle **Excel**.  
  
2.  Premere **CTRL + A** per selezionare tutti i dati. Si tratta **importante** di selezionare tutti i dati nel foglio di calcolo.  
  
3.  Fare clic su **dati Master** nella barra dei menu.  
  
4.  Fare clic su **Crea entità** pulsante della barra multifunzione.  
  
     ![Excel - scheda dati Master - pulsante Crea entità](../../2014/tutorials/media/et-ulingsdtomdsusingmdsaddinforexcel-01.jpg "Excel - scheda dati Master - pulsante Crea entità")  
  
5.  Nelle **Gestisci connessioni** finestra di dialogo, se non è possibile visualizzare la connessione al **server MDS locale** sotto **connessioni esistenti**, eseguire le operazioni seguenti:  
  
    1.  Selezionare **creare una nuova connessione**, fare clic su **New** pulsante.  
  
    2.  Nel **Aggiungi nuova connessione** finestra di dialogo, digitare **Server MDS locale** per **descrizione** e **http://localhost/MDS** per  **Indirizzo server MDS**, fare clic su **OK** per chiudere la finestra di dialogo.  
  
6.  Nelle **Gestisci connessioni** finestra di dialogo **Server MDS locale** (http://localhost/MDS), fare clic su **testare** per testare la connessione. Fare clic su **OK** nella finestra di messaggio.  
  
7.  Fare clic su **Connect** per connettersi al server MDS.  
  
8.  Nel **Crea entità** finestra di dialogo **Suppliers** per il **modello**.  
  
9. Assicurarsi che **VERSION_1** sia selezionata per **versione**.  
  
10. Immettere **Supplier** per **Nome nuova entità**.  
  
11. Selezionare **SupplierID** per **la colonna che contiene un identificatore univoco** campo (è anche possibile generare un codice automaticamente). Essenzialmente esegue il mapping del **SupplierID** colonna **Excel** per il **codice** attributo del **Supplier** entità.  
  
12. Selezionare **Supplier Name** per **la colonna che contiene i nomi** campo. Essenzialmente esegue il mapping del **Supplier Name** colonna **Excel** per il **nome** attributo del **Supplier** entità. Il **codice** e **nome** gli attributi sono attributi obbligatori per un'entità in MDS.  
  
     ![Creare la finestra di dialogo Entity](../../2014/tutorials/media/et-ulingsdtomdsusingmdsaddinforexcel-02.jpg "dialogo Crea entità")  
  
13. Fare clic su **OK** per creare l'entità in MDS, pubblicare i dati master all'entità e chiudere **Crea entità** nella finestra di dialogo.  
  
14. Ora, verrà visualizzato un nuovo foglio denominato **Supplier**, ovvero il nome dell'entità, aggiunto al foglio di calcolo di Excel e nella parte superiore del foglio di lavoro si dovrebbe vedere che il foglio di lavoro è connesso al server MDS. Si noti che il foglio di lavoro originale (intitolata **Sheet1**) esiste ancora.  
  
     ![Excel - schede fornitore e Foglio1](../../2014/tutorials/media/et-ulingsdtomdsusingmdsaddinforexcel-03.jpg "Excel - schede fornitore e Foglio1")  
  
     ![Excel - visualizzazione Dettagli connessione MDS](../../2014/tutorials/media/et-ulingsdtomdsusingmdsaddinforexcel-04.jpg "Excel - visualizzazione Dettagli connessione MDS")  
  
15. Mantieni **Excel** aprire.  
  
## <a name="next-task"></a>Attività successiva  
 [Attività 3: Verifica dei dati in Gestione dati master](../../2014/tutorials/task-3-verifying-the-data-in-master-data-manager.md)  
  
  
