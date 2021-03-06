---
title: Uso di una stored procedure senza parametri | Microsoft Docs
ms.custom: ''
ms.date: 07/11/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: e9470a6d-a758-4c56-96ec-7b37139e36a7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5430d5bc97c91357dd0e3d756e8f28f7a813467b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 10/01/2018
ms.locfileid: "47820580"
---
# <a name="using-a-stored-procedure-with-no-parameters"></a>Utilizzo di una stored procedure senza parametri

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Il tipo più semplice di stored procedure di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che è possibile chiamare è quello che non contiene parametri e restituisce un solo set di risultati. In [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] è disponibile la classe [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) che è possibile usare per chiamare questo tipo di stored procedure ed elaborare i dati restituiti.

Quando si usa il driver JDBC per chiamare una stored procedure senza parametri, è necessario usare la sequenza di escape SQL `call`. La sintassi della sequenza di escape `call` senza parametri è la seguente:

`{call procedure-name}`

> [!NOTE]  
> Per altre informazioni sulle sequenze di escape SQL, vedere [usando le sequenze di Escape SQL](../../connect/jdbc/using-sql-escape-sequences.md).

Come esempio, viene creata la seguente stored procedure nel database di esempio [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]:

```sql
CREATE PROCEDURE GetContactFormalNames
AS  
BEGIN  
   SELECT TOP 10 Title + ' ' + FirstName + ' ' + LastName AS FormalName
   FROM Person.Contact  
END  
```

Questa stored procedure restituisce un solo set di risultati contenente una colonna di dati che corrispondono a una combinazione di titolo, nome e cognome dei primi 10 contatti presenti nella tabella Person.Contact.

Nell'esempio seguente viene passata alla funzione una connessione aperta al database di esempio [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] e viene usato il metodo [executeQuery](../../connect/jdbc/reference/executequery-method-sqlserverstatement.md) per chiamare la stored procedure GetContactFormalNames.

```java
public static void executeSprocNoParams(Connection con) throws SQLException {  
    try(Statement stmt = con.createStatement();) {  

        ResultSet rs = stmt.executeQuery("{call dbo.GetContactFormalNames}");  
        while (rs.next()) {  
            System.out.println(rs.getString("FormalName"));  
        }  
    }  
}
```

## <a name="see-also"></a>Vedere anche

[USo di istruzioni con stored procedure](../../connect/jdbc/using-statements-with-stored-procedures.md)
