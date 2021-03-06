---
title: Configurazione della modalità di invio dei valori java.sql.Time al server | Microsoft Docs
ms.custom: ''
ms.date: 07/11/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 07eb00dd-621a-46f9-a5a5-8cab4d6058b5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e0f359c66250d11fa01c74567e1faeab3ff064ac
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 11/13/2018
ms.locfileid: "51602251"
---
# <a name="configuring-how-javasqltime-values-are-sent-to-the-server"></a>Configurazione della modalità di invio dei valori java.sql.Time al server
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Se si usa un oggetto java.sql.Time o il tipo JDBC java.sql.Types.TIME per impostare un parametro, è possibile configurare la modalità di invio del valore java.sql.Time al server come tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **time** o come tipo **datetime**.  
  
 Questo scenario si applica quando si utilizza uno dei seguenti metodi:  
  
-   [SQLServerCallableStatement.registerOutParameter(int, int)](../../connect/jdbc/reference/registeroutparameter-method-int-int.md)  
  
-   [SQLServerCallableStatement.registerOutParameter(int, int, int)](../../connect/jdbc/reference/registeroutparameter-method-int-int-int.md)  
  
-   [SQLServerCallableStatement.setTime](../../connect/jdbc/reference/settime-method-sqlservercallablestatement.md)  
  
-   [SQLServerPreparedStatement.setTime](../../connect/jdbc/reference/settime-method-sqlserverpreparedstatement.md)  
  
-   [SQLServerCallableStatement.setObject](../../connect/jdbc/reference/setobject-method-sqlservercallablestatement.md)  
  
-   [SQLServerPreparedStatement.setObject](../../connect/jdbc/reference/setobject-method-sqlserverpreparedstatement.md)  
  
 La modalità di invio del valore java.sql.Time può essere configurata tramite la proprietà di connessione **sendTimeAsDatetime**. Per altre informazioni, vedere [Impostazione delle proprietà di connessione](../../connect/jdbc/setting-the-connection-properties.md).  
  
 Il valore della proprietà di connessione **sendTimeAsDatetime** può essere modificato a livello di codice con [SQLServerDataSource.setSendTimeAsDatetime](../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md).  
  
 Le versioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] precedenti a [!INCLUDE[ssKatmai](../../includes/sskatmai_md.md)] non supportano il **ora** tipo di dati, in modo che le applicazioni che utilizzano Java in genere archiviano Java valori come **datetime** o**smalldatetime** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] i tipi di dati.  
  
 Se si desidera utilizzare il **data/ora** e **smalldatetime** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipi di dati quando si lavora con i valori Java, è necessario impostare la **sendTimeAsDatetime** proprietà di connessione al **true**. Se si desidera utilizzare il **tempo** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] del tipo di dati quando si lavora con valori di Java, è consigliabile impostare il **sendTimeAsDatetime** proprietà di connessione su **false**.  
  
 Se si inviano valori java.sql.Time in un parametro il cui tipo di dati può archiviare anche la data, tali date predefinite sono diverse a seconda che il valore java.sql.Time venga inviato come valore **datetime** (1/1/1970) o **time** (1/1/1900). Per altre informazioni sulle conversioni di dati quando si inviano dati a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vedere [Uso di dati relativi a data e ora](https://go.microsoft.com/fwlink/?LinkID=145211).  
  
 Nelle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] JDBC Driver 3.0 **sendTimeAsDatetime** true per impostazione predefinita. In una versione successiva la proprietà di connessione **sendTimeAsDatetime** può essere impostata su False per impostazione predefinita.  
  
 Per assicurarsi che l'applicazione continui a funzionare come previsto, indipendentemente dal valore predefinito della proprietà di connessione **sendTimeAsDatetime**, è possibile:  
  
-   Usare java.sql.Time in caso di uso del tipo di dati **time**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Usare Java con il **data/ora**, **smalldatetime**, e **datetime2** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] i tipi di dati.  
  
SendTimeAsDatetime deve essere false per le colonne crittografate le colonne crittografate non supportano la conversione dall'ora in datetime. A partire da Microsoft JDBC Driver 6.0 per SQL Server, la classe SQLServerConnection ha i seguenti due metodi per il valore della proprietà sendTimeAsDatetime set/get.

```java
  public boolean getSendTimeAsDatetime()
  public void setSendTimeAsDatetime(boolean sendTimeAsDateTimeValue)
```
  
## <a name="see-also"></a>Vedere anche  
 [Informazioni sui tipi di dati del driver JDBC](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
  
  
