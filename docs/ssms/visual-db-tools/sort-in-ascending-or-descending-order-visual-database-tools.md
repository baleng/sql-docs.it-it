---
title: Ordinare in modo crescente o decrescente (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- descending sorts
- ascending sorts
ms.assetid: d61cc55b-9ee8-4ecf-a32f-6459ae43910b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 37e81aef5c27f6302bfec677fdeff44ad2d59acb
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/01/2018
ms.locfileid: "47612961"
---
# <a name="sort-in-ascending-or-descending-order-visual-database-tools"></a>Ordinamento in modo crescente o decrescente (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
È possibile ordinare i risultati di una query in modo crescente o decrescente in base a una o più colonne del set di risultati usando la parola chiave **ASC** o **DESC** con la clausola **ORDER BY** .  
  
> [!NOTE]  
> Il criterio di ordinamento è determinato in parte dalla sequenza di confronto della colonna. Per cambiare la sequenza di confronto, è possibile usare la [finestra di dialogo Regole di confronto](../../ssms/visual-db-tools/collation-dialog-box-visual-database-tools.md).  
  
Nella procedura riportata di seguito si presuppone che in Progettazione query e Progettazione viste sia aperta una query in cui viene utilizzata la clausola ORDER BY per ordinare una o più colonne.  
  
### <a name="to-specify-or-change-the-order-in-which-results-are-sorted"></a>Per impostare o cambiare il criterio di ordinamento dei risultati  
  
1.  Nel [riquadro Criteri](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md)fare clic sul campo **Tipo ordinamento** relativo alla colonna che si vuole riordinare.  
  
2.  Selezionare **Crescente** o **Decrescente** per specificare il criterio di ordinamento per la colonna.  
  
Quando si utilizza il riquadro Criteri, la clausola UNION della query cambia in base alle azioni più recenti.  
  
> [!NOTE]  
> Per ordinare i risultati in base a più colonne, utilizzare la colonna Ordinamento per specificare l'ordine in cui deve essere effettuata la ricerca nelle diverse colonne. Per altre informazioni, vedere [Ordinare più colonne nelle query &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/sort-multiple-columns-in-queries-visual-database-tools.md).  
  
## <a name="see-also"></a>Vedere anche  
[Ordinare e raggruppare i risultati delle query &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)  
[Creare un riepilogo dei risultati di query &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/summarize-query-results-visual-database-tools.md)  
[Procedure per la progettazione di query e viste &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
