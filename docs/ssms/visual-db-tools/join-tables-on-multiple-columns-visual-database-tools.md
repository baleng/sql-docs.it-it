---
title: Eseguire il join di tabelle su più colonne (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- multiple column joins
- joins [SQL Server], multiple columns
ms.assetid: 56a158bc-a42a-4b78-baad-4721d2d22cd3
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: fa18294f62eed2a412d3abbb5bb9d740a4364499
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/01/2018
ms.locfileid: "47685179"
---
# <a name="join-tables-on-multiple-columns-visual-database-tools"></a>Join di tabelle su più colonne (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
È possibile unire in join tabelle tramite più colonne, ossia creare una query che crei una corrispondenza tra le righe di due tabelle solo se soddisfano più condizioni. Se il database contiene una relazione di corrispondenza tra una tabella con una chiave esterna formata da più colonne e una tabella con una chiave primaria di più colonne, sarà possibile utilizzare questa relazione per creare un join a più colonne. Per informazioni dettagliate, vedere [Unione di tabelle in modo automatico &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/join-tables-automatically-visual-database-tools.md).  
  
Anche se il database non contiene relazioni di chiave esterna su più colonne, sarà possibile creare il join manualmente.  
  
### <a name="to-manually-create-a-multicolumn-join"></a>Per creare manualmente un join su più colonne  
  
1.  Aggiungere al [riquadro diagramma](../../ssms/visual-db-tools/diagram-pane-visual-database-tools.md) le tabelle da unire in join.  
  
2.  Trascinare il nome della prima colonna join nella prima finestra di tabella e rilasciarlo nella colonna correlata nella seconda finestra di tabella. Non è possibile basare un join sulle colonne text, ntext o image.  
  
    > [!NOTE]  
    > In linea generale, le colonne join devono avere tipi di dati uguali o compatibili. Se ad esempio la colonna join della prima tabella è una data, dovrà essere correlata a una colonna data nella seconda tabella. D'altra parte, se la prima colonna join contiene un valore intero, anche la colonna join correlata dovrà contenere dati di un tipo intero, anche se di dimensioni diverse. In alcuni casi, tuttavia, è possibile unire in join colonne apparentemente incompatibili tramite la conversione implicita del tipo di dati.  
    >   
    > In [Progettazione query e Progettazione viste](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md) non verranno verificati i tipi di dati delle colonne usati per creare un join, ma quando si eseguirà la query verrà visualizzato un errore qualora i tipi di dati non siano compatibili.  
  
3.  Trascinare il nome della seconda colonna join nella prima finestra di tabella e rilasciarlo nella colonna correlata nella seconda finestra di tabella.  
  
4.  Ripetere il passaggio 3 per ciascuna coppia di colonne join nelle due tabelle.  
  
5.  Consente di eseguire la query.  
  
## <a name="see-also"></a>Vedere anche  
[Eseguire query con join &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/query-with-joins-visual-database-tools.md)  
  
