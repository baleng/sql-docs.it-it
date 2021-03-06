---
title: Creare una struttura di Data Mining relazionale | Documenti Microsoft
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: fe3958698c41cc54b6606255ced3a79133c66320
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/10/2018
ms.locfileid: "34017259"
---
# <a name="create-a-relational-mining-structure"></a>Creare una struttura di data mining relazionale
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  La maggior parte dei modelli di data mining sono basati su origini dati relazionali. La creazione di un modello di data mining relazionale offre il vantaggio di poter assemblare dati ad hoc e aggiornare ed eseguire il training di un modello evitando la complessità di dover creare un cubo.  
  
 Una struttura di data mining relazionale può ottenere dati da origini disparate. È possibile archiviare i dati non elaborati in sistemi di tabelle, file o database relazionali, purché i dati possano essere definiti come parte di una vista origine dati. Ad esempio, è necessario utilizzare una struttura di data mining relazionale se i dati sono in Excel, in un data warehouse di SQL Server o in un database di report di SQL Server oppure in origini esterne cui si accede tramite provider OLE DB o ODBC.  
  
 In questo argomento vengono forniti cenni preliminari sull'utilizzo di Creazione guidata modello di data mining per creare una struttura di data mining relazionale.  
  
 [Requisiti](#BKMK_Relational_Structure)  
  
 [Processo di creazione di una struttura di data mining relazionale](#BKMK_Relational_Structure)  
  
 [Come scegliere le origini dati](#BKMK_ChooseRelData)  
  
 [Come specificare il tipo di contenuto e di dati](#bkmk_ContentDataType)  
  
 [Come creare un set di dati di controllo e perché](#bkmk_Holdout)  
  
 [Come abilitare il drill-through e perché](#BKMK_DrillThru)  
  
## <a name="requirements"></a>Requisiti  
 Innanzitutto, è necessario disporre di un'origine dati esistente. È possibile utilizzare Progettazione origine dati per impostare un'origine dati, se non esiste già. Per altre informazioni, vedere [Creare un'origine dati &#40;SSAS - multidimensionale&#41;](../../analysis-services/multidimensional-models/create-a-data-source-ssas-multidimensional.md).  
  
 Successivamente, utilizzare la Creazione guidata vista origine dati per assemblare i dati richiesti in una sola vista origine dati. Per altre informazioni sulla modalità di selezione, trasformazione, filtro o gestione dei dati con le viste origine dati, vedere [Viste origine dati in modelli multidimensionali](../../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md).  
  
##  <a name="BKMK_Relational_Structure"></a> Panoramica del processo  
 Avviare la Creazione guidata modello di data mining facendo clic con il pulsante destro del mouse sul nodo **Strutture di data mining** in Esplora soluzioni e scegliendo **Aggiungi nuova struttura di data mining**. La procedura guidata consente di eseguire in modo semplificato i passaggi indicati di seguito per la creazione della struttura di un nuovo modello di data mining relazionale:  
  
1.  **Selezione metodo di definizione**: consente di selezionare un tipo di origine dati e scegliere **Da database relazionale o data warehouse**.  
  
2.  **Crea la struttura di data mining**: consente di determinare se verrà compilata solo una struttura o una struttura con un modello di data mining.  
  
     Scegliere inoltre un algoritmo appropriato per il modello iniziale. Per indicazioni sugli algoritmi ottimali per attività specifiche, vedere [Algoritmi di data mining &#40;Analysis Services - Data mining&#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md).  
  
3.  **Selezione vista origine dati**: scegliere una vista origine dati da usare per il training del modello. La vista origine dati può inoltre contenere dati utilizzati per il test o dati non correlati. Scegliere quali dati verranno effettivamente utilizzati nella struttura e nel modello. È inoltre possibile applicare filtri ai dati in un secondo momento.  
  
4.  **Impostazione tipi di tabelle**: selezionare la tabella che contiene i case usati per l'analisi. Per alcuni set di dati, in particolare quelli utilizzati per la compilazione di modelli di analisi di mercato su acquisti, può essere necessario includere anche una tabella correlata, da utilizzare come tabella nidificata.  
  
     Per ogni tabella, è necessario specificare la chiave, per consentire all'algoritmo di identificare un record univoco e i record correlati, se è stata aggiunta una tabella nidificata.  
  
     Per altre informazioni, vedere [Mining Structure Columns](../../analysis-services/data-mining/mining-structure-columns.md).  
  
5.  **Impostazione dati di training**: in questa pagina, si sceglie la *tabella del case*, ovvero la tabella che contiene i dati più importanti per l'analisi.  
  
     Per alcuni set di dati, in particolare quelli utilizzati per la compilazione di modelli di analisi di mercato su acquisti, può essere necessario includere anche una tabella correlata. I valori in tale tabella nidificata verranno gestiti come più valori tutti correlati a una sola riga (o case) nella tabella principale.  
  
6.  **Impostazione tipo di contenuto e dati delle colonne**: per ogni colonna usata nella struttura è necessario scegliere sia un *tipo di dati* che un *tipo di contenuto*.  
  
     Con la procedura guidata vengono automaticamente rilevati i tipi di dati possibili, ma non è necessario utilizzare il tipo di dati consigliato dalla procedura guidata. Ad esempio, anche se i dati contengono numeri, potrebbero essere rappresentativi di dati di categoria. Alle colonne specificate come chiavi viene assegnato automaticamente il tipo di dati corretto per tale tipo di modello particolare. Per altre informazioni, vedere [Colonne del modello di data mining](../../analysis-services/data-mining/mining-model-columns.md) e [Tipi di dati &#40;data mining&#41;](../../analysis-services/data-mining/data-types-data-mining.md).  
  
     Il *tipo di contenuto* scelto per ogni colonna utilizzata nel modello indica all'algoritmo in che modo devono essere elaborati i dati.  
  
     Ad esempio, è possibile decidere di discretizzare i numeri, anziché utilizzare valori continui. È inoltre possibile utilizzare l'algoritmo per rilevare automaticamente il tipo di contenuto migliore per la colonna. Per altre informazioni, vedere [Tipi di contenuto &#40;Data mining&#41;](../../analysis-services/data-mining/content-types-data-mining.md).  
  
7.  **Crea set di testing**: in questa pagina è possibile definire nella procedura guidata la quantità di dati da mettere da parte durante il test del modello. Se i dati supporteranno più modelli, è consigliabile creare un set di dati di controllo, in modo da poter eseguire il test di tutti i modelli sugli stessi dati.  
  
     Per altre informazioni, vedere [Test e convalida &#40;Data mining&#41;](../../analysis-services/data-mining/testing-and-validation-data-mining.md).  
  
8.  **Completamento procedura guidata**: in questa pagina si assegna un nome alla nuova struttura di data mining e al modello di data mining associato, quindi si salvano struttura e modello.  
  
     È inoltre possibile impostare alcune opzioni importanti, a seconda del tipo di modello. Ad esempio, è possibile abilitare il drill-through sulla struttura.  
  
     In questa fase la struttura di data mining e il modello sono esclusivamente metadati; sarà necessario elaborarli entrambi per ottenere risultati.  
  
##  <a name="BKMK_ChooseRelData"></a> Come scegliere i dati relazionali  
 Le strutture di data mining relazionali possono essere basate sui dati disponibili tramite un'origine dei dati OLE DB. Se i dati di origine sono contenuti all'interno di più tabelle, si utilizza una vista origine dati per assemblare le tabelle e le colonne necessarie in una sola posizione.  
  
 Se le tabelle includono relazioni uno-a-molti, se ad esempio si dispone di più record di acquisto per ogni cliente che si desidera analizzare, è possibile aggiungere entrambe le tabelle e utilizzarne una come tabella del case, collegando i dati del lato molti della relazione come tabella nidificata.  
  
 I dati di una struttura di data mining derivano dal contenuto all'interno della vista origine dati esistente. È possibile modificare dati secondo le esigenze all'interno della vista origine dati, aggiungendo relazioni o colonne derivate che potrebbero non essere presenti nei dati relazionali sottostanti. È inoltre possibile creare calcoli o aggregazioni denominati all'interno della vista origine dati. Queste funzionalità sono molto utili se non è possibile controllare la disposizione dei dati nell'origine dati o se si desidera sperimentare diverse aggregazioni di dati per i modelli di data mining.  
  
 Non è necessario utilizzare tutti i dati disponibili; è possibile scegliere quali colonne includere nella struttura di data mining. Tutti i modelli basati su tale struttura possono quindi usare tali colonne o è possibile contrassegnare determinate colonne per **ignorarle** per un particolare modello. È inoltre possibile consentire agli utenti di un modello di data mining di eseguire il drill-down a partire dai risultati del modello per visualizzare colonne della struttura di data mining aggiuntive non incluse nel modello di data mining stesso.  
  
##  <a name="bkmk_ContentDataType"></a> Come specificare il tipo di contenuto e di dati  
 Il tipo di dati è molto simile ai tipi di dati specificati in SQL Server o nelle interfacce di altre applicazioni: date e ore, numeri di dimensioni diverse, valori booleani, testo e altri dati discreti.  
  
 Tuttavia, i tipi di contenuto sono importanti per il data mining e influiscono sul risultato dell'analisi. Il tipo di contenuto indica all'algoritmo come procedere con i dati: i numeri devono essere considerati su scala continua o suddivisi in contenitori? Quanti valori potenziali sono presenti? Ogni valore è distinto? Se il valore è una chiave, che tipo di chiave è? Indica un valore data/ora, una sequenza o un altro tipo di chiave?  
  
 Si noti che la scelta del tipo di dati può limitare la scelta dei tipi di contenuto. Ad esempio, non è possibile discretizzare valori non numerici. Se il tipo di contenuto desiderato non è visibile, fare clic su **Indietro** per tornare alla pagina del tipo di dati e provarne uno diverso.  
  
 Non è importante preoccuparsi di evitare di ottenere il tipo di contenuto errato. È molto facile creare un nuovo modello e modificare il tipo di contenuto all'interno del modello, purché il nuovo tipo di contenuto sia supportato dal tipo di dati impostato nella struttura di data mining. È inoltre molto comune creare più modelli con tipi di contenuto diversi, come esperimento o per soddisfare i requisiti di un algoritmo diverso.  
  
 Ad esempio, se i dati contengono una colonna del reddito, è possibile creare due modelli diversi quando si utilizza l'algoritmo Microsoft Decision Trees e configurare la colonna alternativamente come numeri continui o intervalli discreti. Tuttavia, se è stato aggiunto un modello utilizzando l'algoritmo Microsoft Naive Bayes, sarebbe necessario impostare la colonna solo sui valori discretizzati, perché tale algoritmo non supporta i numeri continui.  
  
##  <a name="bkmk_Holdout"></a> Come suddividere i dati in set di training e in set di testing e perché  
 Verso la fine della procedura guidata è necessario decidere se partizionare i dati in set di training e di testing. La possibilità di fornire una parte dei dati campionati in modo casuale per eseguire il testing è molto utile e consente di garantire che un set coerente di dati di test sia disponibile per essere utilizzato con tutti i modelli di data mining associati alla nuova struttura.  
  
> [!WARNING]  
>  Si noti che questa opzione non è disponibile per tutti i tipi di modelli. Ad esempio, se si crea un modello di previsione, non sarà possibile utilizzare dati di controllo, perché l'algoritmo Time Series non accetta lacune nei dati. Per un elenco dei tipi di modelli che supportano i set di dati di controllo, vedere [Set di dati di training e di testing](../../analysis-services/data-mining/training-and-testing-data-sets.md).  
  
 Per creare questo set di dati di controllo, specificare la percentuale dei dati che si desidera utilizzare per il test. Tutti i dati rimanenti saranno utilizzati per il training. Facoltativamente, è possibile impostare un numero massimo di case da utilizzare per i test o impostare un valore di inizializzazione da utilizzare per avviare il processo di selezione casuale.  
  
 La definizione del set di test di dati di controllo viene archiviata con la struttura di data mining, in modo che tutte le volte in cui si crea un nuovo modello basato sulla struttura, il set di dati di testing sarà disponibile per valutarne l'accuratezza. Se si elimina la cache della struttura di data mining, verranno anche eliminate le informazioni sui case utilizzati per il training e su quelli utilizzati per i test.  
  
##  <a name="BKMK_DrillThru"></a> Come abilitare il drill-through e perché  
 Nella parte conclusiva della procedura guidata, è possibile scegliere di abilitare il *drill-through*. È facile non notare questa opzione, che è importante. Il drill-through consente di visualizzare i dati di origine nella struttura di data mining eseguendo una query sul modello di data mining.  
  
 Perché è utile? Si supponga di visualizzare i risultati di un modello di clustering e di voler vedere i clienti inseriti in un cluster specifico. Tramite il drill-through, è possibile visualizzare dettagli quali le informazioni di contatto.  
  
> [!WARNING]  
>  Per utilizzare il drill-through è necessario abilitarlo durante la creazione della struttura di data mining. È possibile abilitare il drill-through sui modelli in un secondo momento, impostando una proprietà sul modello, ma per le strutture di data mining questa opzione deve essere impostata all'inizio. Per altre informazioni, vedere [Query drill-through &#40;Data mining&#41;](../../analysis-services/data-mining/drillthrough-queries-data-mining.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Progettazione di Data Mining](../../analysis-services/data-mining/data-mining-designer.md)   
 [Creazione guidata di Data Mining & #40; Analysis Services - Data Mining & #41;](../../analysis-services/data-mining/data-mining-wizard-analysis-services-data-mining.md)   
 [Proprietà modello di data mining](../../analysis-services/data-mining/mining-model-properties.md)   
 [Proprietà per la struttura di Data Mining e le colonne della struttura](../../analysis-services/data-mining/properties-for-mining-structure-and-structure-columns.md)   
 [Data mining struttura attività e procedure](../../analysis-services/data-mining/mining-structure-tasks-and-how-tos.md)  
  
  
