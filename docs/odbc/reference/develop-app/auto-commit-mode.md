---
title: "Modalità di Commit automatico | Documenti Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- rolling back transactions [ODBC]
- auto-commit mode [ODBC]
- transactions [ODBC], commit modes
- committing transactions [ODBC]
- commit modes [ODBC]
- transactions [ODBC], rolling back
ms.assetid: c8de5b60-d147-492d-b601-2eeae8511d00
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: fb9b6d354657578f7188481a2e7ff7566f725c80
ms.contentlocale: it-it
ms.lasthandoff: 09/09/2017

---
# <a name="auto-commit-mode"></a>La modalità autocommit
*In modalità autocommit,* ogni operazione di database è una transazione che viene eseguito il commit durante l'esecuzione. Questa modalità è adatta per molte transazioni reali che sono costituiti da una singola istruzione SQL. Non è necessario delimitare o specificare il completamento di queste transazioni. Nei database senza supporto delle transazioni, la modalità autocommit è l'unica modalità supportata. In tali database, le istruzioni vengono eseguite quando vengono eseguite e non è possibile eseguire il rollback li; sono pertanto sempre in modalità autocommit.  
  
 Se il sistema DBMS sottostante non supporta le transazioni in modalità autocommit, il driver può emulare li eseguendo manualmente il commit di ogni istruzione SQL eseguita.  
  
 Se un batch di istruzioni SQL viene eseguito in modalità autocommit, risulta specifici dell'origine dati quando le istruzioni nel batch vengono eseguito il commit. Possono essere eseguito il commit come vengono eseguiti o complessivamente dopo l'esecuzione dell'intero batch. Alcune origini dati supportino entrambi questi comportamenti e possono costituire un modo per la selezione di uno o altri utenti. In particolare, se si verifica un errore nel corso del batch, è specifici dell'origine dati se le istruzioni già eseguite sono stato eseguito il commit o rollback. Di conseguenza, applicazioni interoperabili che utilizzano batch e li richiedono per essere eseguito il commit o rollback nel suo complesso devono eseguire batch solo in modalità di commit manuale.