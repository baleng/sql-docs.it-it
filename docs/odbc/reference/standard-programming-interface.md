---
title: Interfaccia di programmazione standard | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC [ODBC], database access
- SQL [ODBC], database access
- database access [ODBC]
- standardizing database access [ODBC], programming interface
- programming interface standardization [ODBC]
ms.assetid: a2fa727e-51f2-4123-ae25-0ee28e611231
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b02b5a907fc134e04a4c78cda2448c128178585a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/01/2018
ms.locfileid: "47622559"
---
# <a name="standard-programming-interface"></a>Interfaccia di programmazione standard
L'interfaccia di programmazione è probabilmente il più ovvio candidato per la standardizzazione. Infatti, quando viene sviluppata ODBC, ANSI e ISO già fornito standard per embedded SQL e SQL moduli. Anche se non gli standard esistevano per un database della riga di comando, il gruppo di accesso SQL, ovvero un consorzio di settore di fornitori di database, è stata valuta l'opportunità di creare una volta; parti di ODBC in un secondo momento è diventato la base per il proprio lavoro.  
  
 Uno dei requisiti per ODBC è che una singola applicazione binaria doveva usare più DBMS. È per questo motivo che ODBC non utilizza linguaggi embedded SQL o un modulo. Anche se il linguaggio nelle lingue SQL e il modulo incorporate è standardizzato, ognuna è associata a precompilers specifici del DBMS. Di conseguenza, è necessario ricompilare le applicazioni per ogni sistema DBMS e i file binari risultanti funzionano solo con un singolo DBMS. Sebbene questo sia accettabile per le applicazioni con volumi contenuti disponibili nei mondi minicomputer e mainframe, non è accettabile nel mondo personal computer. In primo luogo, è un vero incubo logistico recapitare più versioni di software preconfezionato con volumi elevati di clienti. in secondo luogo, le applicazioni di personal computer devono spesso accedere simultaneamente più DBMS.  
  
 D'altra parte, è possibile implementare un'interfaccia a livello di chiamata tramite librerie o driver di database, che si trovano in ogni computer locale; un driver diverso è necessario per ogni sistema DBMS. Poiché i sistemi operativi moderni possono caricare tali librerie (ad esempio, librerie a collegamento dinamico nel sistema operativo Microsoft® Windows®) in fase di esecuzione, una singola applicazione possa accedere ai dati da diversi DBMS senza ricompilazione e può anche accedere ai dati da più database contemporaneamente. Man mano che diventano disponibili nuovi driver di database, gli utenti possono semplicemente installarli sui propri computer senza dover modificare, compilare o ricollegare le applicazioni di database. Inoltre, un'interfaccia a livello di chiamata è un buon candidato per ODBC perché Windows, ovvero la piattaforma per cui è stato originariamente sviluppato ODBC, già massiccio tali librerie.
