---
title: Rendering in formato HTML (Generatore report e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 04/26/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: cf559b0a-499a-4d74-b520-b382b87e0b17
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: eea42bfc7b02c4964f34ebc6fe5f4b067a33d21e
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/02/2018
ms.locfileid: "48084541"
---
# <a name="rendering-to-html-report-builder-and-ssrs"></a>Rendering in formato HTML (Generatore report e SSRS)
  L'estensione per il rendering HTML consente di eseguire il rendering di un report in formato HTML. Può inoltre generare pagine HTML complete o frammenti di HTML da incorporare in altre pagine HTML. Tutto il codice HTML viene generato con la codifica UTF-8.  
  
 Per i report visualizzati in un browser, inclusi quelli eseguiti in Gestione report, viene utilizzata l'estensione per il rendering HTML per impostazione predefinita.  
  
 Per i report visualizzati in un browser, inclusi quelli eseguiti in Gestione report, viene utilizzata l'estensione per il rendering HTML per impostazione predefinita. L'estensione per il rendering HTML può generare frammenti HTML o documenti HTML completi. Se il codice HTML viene generato un frammento, il `HEAD`, `HTML`, e `BODY` tag del documento HTML vengono rimossi. Viene eseguito il rendering solo del contenuto del tag `BODY`. Questa funzionalità è particolarmente utile se si desidera incorporare il frammento HTML nel codice HTML prodotto da un'altra applicazione.  
  
 In alcuni scenari i parametri del report possono essere utilizzati per avviare attacchi intrusivi negli script durante il rendering di report in HTML. Per altre informazioni sulla sicurezza dei report, vedere [Garantire la sicurezza di report e risorse](../security/secure-reports-and-resources.md).  
  
 Per altre informazioni sui browser, vedere [Planning for Reporting Services e supporto Browser per Power View &#40;Reporting Services 2014&#41;](../browser-support-for-reporting-services-and-power-view.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="RenderingMHTML"></a> Rendering in formato MHTML  
 L'estensione per il rendering HTML può inoltre consentire l'esecuzione del rendering dei report in formato MHTML (MIME Encapsulation of Aggregate HTML Documents). MHTML estende HTML per incorporare oggetti codificati, ad esempio immagini, in documenti HTML. Tale estensione consente di incorporare risorse, quali immagini, documenti o altri file binari, come strutture MIME nel codice HTML del report, in un singolo file. I report MHTML sono utili anche per l'incorporamento di elementi in messaggi di posta elettronica, in quanto tutte le risorse vengono incluse nel report. Sebbene il rendering MHTML venga eseguito dall'estensione per il rendering HTML, talvolta questa funzionalità viene denominata anche estensione per il rendering MHTML.  
  
 ![Icona freccia usata con il collegamento Torna all'inizio](../../2014-toc/media/uparrow16x16.gif "Icona freccia usata con il collegamento Torna all'inizio") [Torna all'inizio](#BackToTop)  
  
##  <a name="BrowserSupport"></a> Supporto browser  
 Questa estensione per il rendering supporta le seguenti versioni di browser:  
  
-   Internet Explorer 5.5 e versioni successive  
  
-   Firefox 1.5 e versioni successive  
  
-   Safari 3.0 e versioni successive  
  
 In considerazione delle caratteristiche dei diversi browser, è possibile che il report visualizzabile sia leggermente diverso a seconda del browser. Ad esempio, la casella di testo contiene una proprietà chiamata WritingMode. non supportata in Firefox.  
  
 ![Icona freccia usata con il collegamento Torna all'inizio](../../2014-toc/media/uparrow16x16.gif "Icona freccia usata con il collegamento Torna all'inizio") [Torna all'inizio](#BackToTop)  
  
##  <a name="HTMLSpecificRenderingRules"></a> Regole di rendering specifiche di HTML  
 Durante il rendering vengono applicate le seguenti regole specifiche di HTML:  
  
-   Il renderer compila una struttura di tabella HTML in cui inserire tutti gli elementi di ogni raccolta `ReportItems`, se ne è disponibile più di una.  
  
-   Ogni elemento all'interno della struttura della tabella occupa una singola cella.  
  
-   Le celle vuote vengono compresse il più possibile per ridurre le dimensioni del codice HTML.  
  
-   Al bordo superiore viene aggiunta una riga di celle vuote, mentre a quello sinistro viene aggiunta un'altra colonna per incrementare la velocità di rendering della tabella nei browser.  
  
-   Alle righe o alle colonne della tabella che non contengono elementi, ma solo spazi tra elementi, vengono assegnate larghezze e altezze fisse.  
  
-   Le dimensioni di tutte le altre righe e colonne possono aumentare in base alle dimensioni dei singoli elementi del report.  
  
-   Tutte le coordinate e le dimensioni degli elementi del report vengono convertite in millimetri. Tutte le altre dimensioni, incluse le proprietà dello stile, mantengono le unità di misura originali. Le differenze di dimensioni e posizioni inferiori a 0,2 mm vengono considerate come 0 mm.  
  
 ![Icona freccia usata con il collegamento Torna all'inizio](../../2014-toc/media/uparrow16x16.gif "Icona freccia usata con il collegamento Torna all'inizio") [Torna all'inizio](#BackToTop)  
  
##  <a name="Interactivity"></a> Interattività  
 In HTML sono supportati alcuni elementi interattivi. Di seguito è riportata una descrizione di comportamenti specifici.  
  
### <a name="show-and-hide"></a>Elementi visualizzati e nascosti  
 Il rendering di un elemento del report la cui visibilità può essere attivata o disattivata prevede l'inclusione di un'immagine dell'elemento Toggle (+/-). Tale elemento è inoltre selezionabile con il mouse. Quando si fa clic sull'elemento, viene effettuata una nuova chiamata al server per eseguire il rendering dell'output con lo stato di visualizzazione modificato.  
  
### <a name="document-map"></a>Mappa documento  
 È possibile eseguire il rendering di etichette della mappa documento e passare a esse utilizzando la mappa documento nel controllo visualizzatore. Per le intestazioni omesse dell'area dati, il rendering delle etichette viene eseguito sulla prima cella figlio. Se non è presente alcuna cella figlio, il rendering dell'etichetta viene eseguito sull'elemento figlio che la precede.  
  
### <a name="bookmarks"></a>Segnalibri  
 I collegamenti a segnalibro vengono sottoposti a rendering e visualizzati come collegamenti ipertestuali. È possibile eseguire il rendering di destinazioni dei segnalibri e passare a esse facendo clic sui collegamenti a segnalibro. Quando si fa clic su un collegamento a un segnalibro, il report passa alla prima occorrenza dell'etichetta del segnalibro di destinazione. Se possibile, il contenuto della finestra del browser viene fatto scorrere in modo che il collegamento sia visualizzato all'inizio della finestra. Per contrassegnare le destinazioni dei segnalibri, vengono usati i tag di ancoraggio HTML (\<a>).  
  
### <a name="interactive-sorting"></a>Ordinamento interattivo  
 Se per una casella di testo è stato definito l'ordinamento dell'utente, l'estensione per il rendering HTML esegue il rendering delle icone di ordinamento nella casella di testo a destra del relativo contenuto. Se un report contiene una casella di testo in cui è stato definito l'ordinamento dell'utente, viene eseguito il rendering del codice JavaScript che provoca un postback al server quando si fa clic sull'icona di ordinamento.  
  
### <a name="hyperlinks-and-drillthrough"></a>Collegamenti ipertestuali e collegamenti drill-through  
 Il rendering di collegamenti ipertestuali e collegamenti drill-through restituisce collegamenti ipertestuali in elementi del report racchiudendo l'elemento in cui sono definiti tra tag di ancoraggio HTML (\<a>).  
  
### <a name="search"></a>Cerca  
 La caratteristica Cerca consente agli utenti di cercare una stringa di testo all'interno del report.  
  
 Ulteriori funzionalità di ricerca vengono fornite dal controllo Web Form ReportViewer.  
  
 ![Icona freccia usata con il collegamento Torna all'inizio](../../2014-toc/media/uparrow16x16.gif "Icona freccia usata con il collegamento Torna all'inizio") [Torna all'inizio](#BackToTop)  
  
##  <a name="DeviceInfo"></a> Impostazioni relative alle informazioni sul dispositivo  
 Modificando le impostazioni relative alle informazioni sul dispositivo, è possibile modificare alcune impostazioni predefinite per questo renderer, tra cui la modalità di rendering. Per altre informazioni, vedere [Impostazioni relative alle informazioni sul dispositivo HTML](../html-device-information-settings.md).  
  
 ![Icona freccia usata con il collegamento Torna all'inizio](../../2014-toc/media/uparrow16x16.gif "Icona freccia usata con il collegamento Torna all'inizio") [Torna all'inizio](#BackToTop)  
  
## <a name="see-also"></a>Vedere anche  
 [Paginazione in Reporting Services &#40;Generatore report e SSRS&#41;](../report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)   
 [Tipi di rendering &#40;Generatore report e SSRS&#41;](../report-design/rendering-behaviors-report-builder-and-ssrs.md)   
 [Funzionalità interattiva per estensioni di Rendering del Report diversi &#40;Report e SSRS&#41;](interactive-functionality-different-report-rendering-extensions.md)   
 [Rendering degli elementi del report &#40;Generatore report e SSRS&#41;](../report-design/rendering-report-items-report-builder-and-ssrs.md)   
 [Tabelle, matrici ed elenchi &#40;Generatore report e SSRS&#41;](../report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)  
  
  
