---
title: Finestra di dialogo Confronto (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdt.dlgbox.definecolumncollation
- vdtsql.chm:65561
ms.assetid: e4020f79-7abf-4839-b9b2-984ef7049817
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3876b59b4ca11bb81d590e4f5941be7da0c497e5
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52505274"
---
# <a name="collation-dialog-box-visual-database-tools"></a>Finestra di dialogo Confronto (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Questa finestra di dialogo consente di specificare una sequenza di confronto per la colonna. La sequenza di confronto di una colonna viene utilizzata nelle operazioni in cui i valori della colonna vengono confrontati con quelli di un'altra colonna o rispetto a valori costanti. Influisce inoltre sul comportamento di alcune funzioni stringa, quali SUBSTRING e CHARINDEX. Per un elenco completo degli effetti dell'impostazione di confronto di una colonna, vedere la documentazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
Questa finestra di dialogo viene visualizzata quando si eseguono le operazioni seguenti:  
  
-   Se si specifica un nome di confronto non valido nel campo **Confronto** della scheda **Proprietà colonne** .  
  
-   Se si fa clic nel campo **Confronto** della scheda **Proprietà colonne** e sui puntini di sospensione (**...**) a destra del campo.  
  
## <a name="options"></a>Opzioni  
**Confronto SQL**  
Consente di scegliere tra le sequenze di confronto definite da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e disponibili nell'elenco a discesa.  
  
**Confronto Windows**  
Consente di scegliere tra le sequenze di confronto definite da Windows e disponibili nell'elenco a discesa.  
  
**Ordinamento binario**  
Consente di selezionare i codici binari dei valori di tipo carattere per i confronti. Se si seleziona questa opzione, alcune opzioni di confronto alfabetico non saranno più disponibili. I confronti senza distinzione fra maiuscole e minuscole, ad esempio, non saranno disponibili poiché le lettere maiuscole e le lettere minuscole hanno codifiche binarie diverse. È disponibile solo se si seleziona **Confronto Windows**.  
  
**Ordinamento dizionario**  
Consente di utilizzare le opzioni di confronto alfabetico. È disponibile solo se si seleziona **Confronto Windows**. Le opzioni di confronto alfabetico sono le seguenti:  
  
-   **Distinzione maiuscole/minuscole** Selezionare questa opzione se si vuole che per i confronti venga fatta distinzione tra maiuscole e minuscole.  
  
-   **Distinzione caratteri accentati/non accentati** Selezionare questa opzione se si vuole che per i confronti venga fatta distinzione tra lettere accentate e lettere non accentate. Selezionando questa opzione, anche le lettere accentate in modo diverso verranno considerate come lettere diverse.  
  
-   **Distinzione Kana** Selezionare questa opzione se si vuole che per i confronti venga fatta distinzione tra le sillabe giapponesi katakana e hiragana.  
  
-   **Distinzione larghezza** Selezionare questa opzione se si vuole che per i confronti venga fatta distinzione tra caratteri a byte singolo e a byte doppio.  
  
**Pulsante Ripristina**  
Applica alla colonna la sequenza di confronto predefinita per il database.  
  
## <a name="see-also"></a>Vedere anche  
[Utilizzo di colonne in query di aggregazione &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/work-with-columns-in-aggregate-queries-visual-database-tools.md)  
  
