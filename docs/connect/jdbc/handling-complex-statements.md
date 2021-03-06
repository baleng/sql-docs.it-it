---
title: Gestione delle istruzioni complesse | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 6b807a45-a8b5-4b1c-8b7b-d8175c710ce0
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d44f2c229755c742d5481f3ca427f11fb5586c2c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 10/01/2018
ms.locfileid: "47623929"
---
# <a name="handling-complex-statements"></a>Gestione delle istruzioni complesse
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Quando si usa [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], può essere necessario gestire istruzioni complesse, incluse le istruzioni generate dinamicamente in fase di esecuzione. Le istruzioni complesse eseguono spesso varie attività, inclusi aggiornamenti, inserimenti ed eliminazioni. Questi tipi di istruzioni potrebbero inoltre restituire più set di risultati e parametri di output. In questi casi, nel codice Java che consente di eseguire le istruzioni non sarà possibile stabilire in anticipo i tipi e il numero degli oggetti e dei dati restituiti.  
  
 Per elaborare le istruzioni complesse in modo efficace, il driver JDBC offre vari metodi che consentono di eseguire query sugli oggetti e sui dati restituiti, in modo che l'applicazione utilizzata possa elaborarli correttamente. Il metodo [execute](../../connect/jdbc/reference/execute-method-sqlserverstatement.md) della classe [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) è fondamentale per l'elaborazione delle istruzioni complesse. Questo metodo restituisce un **booleana** valore. Quando il valore è true, il primo risultato restituito dalle istruzioni è un set di risultati. Quando il valore è false, il primo risultato restituito è un conteggio di aggiornamento.  
  
 Se il tipo di oggetto o di dati restituiti è noto, è possibile usare il metodo [getResultSet](../../connect/jdbc/reference/getresultset-method-sqlserverstatement.md) o il metodo [getUpdateCount](../../connect/jdbc/reference/getupdatecount-method-sqlserverstatement.md) per l'elaborazione dei dati. Per passare all'oggetto o ai dati successivi restituiti dall'istruzione complessa, chiamare il metodo [getMoreResults](../../connect/jdbc/reference/getmoreresults-method.md).  
  
 Nell'esempio seguente viene passata alla funzione una connessione aperta al database di esempio [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)], viene creata un'istruzione complessa che combina una chiamata di stored procedure con un'istruzione SQL, le istruzioni vengono eseguite e quindi viene usato un ciclo `do` per elaborare tutti i set di risultati e i conteggi di aggiornamento che sono stati restituiti.  
  
 [!code[JDBC#HandlingComplexStatements1](../../connect/jdbc/codesnippet/Java/handling-complex-statements_1.java)]  
  
## <a name="see-also"></a>Vedere anche  
 [Uso delle istruzioni con il driver JDBC](../../connect/jdbc/using-statements-with-the-jdbc-driver.md)  
  
  
