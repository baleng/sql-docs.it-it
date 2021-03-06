---
title: Utilizzo del Driver JDBC | Microsoft Docs
ms.custom: ''
ms.date: 07/11/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 6faaf05b-8b70-4ed2-9b44-eee5897f1cd0
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 19e1d9d72cef09c12bb00a6cdcfd2db9b9818a93
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 10/01/2018
ms.locfileid: "47845329"
---
# <a name="using-the-jdbc-driver"></a>Utilizzo del driver JDBC

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Questa sezione include istruzioni introduttive per creare una connessione semplice a un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]. Prima di connettersi a un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è innanzitutto necessario installare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nel computer locale o in un server e quindi installare il driver JDBC nel computer locale.  
  
## <a name="choosing-the-right-jar-file"></a>Scelta del file JAR corretto

Microsoft JDBC Driver fornisce diversi file con estensione jar per essere usato in corrispondenza con le impostazioni preferite di Java Runtime Environment (JRE), come in:

Microsoft JDBC Driver 7.0 per SQL Server fornisce **mssql-jdbc-7.0.0.jre8.jar**, e **mssql-jdbc-7.0.0.jre10.jar** i file di libreria di classi.

Microsoft JDBC Driver 6.4 per SQL Server fornisce **mssql-jdbc-6.4.0.jre7.jar**, **mssql-jdbc-6.4.0.jre8.jar**, e **mssql-jdbc-6.4.0.jre9.jar** libreria di classi file.

Microsoft JDBC Driver 6.2 per SQL Server fornisce **mssql-jdbc-6.2.2.jre7.jar**, e **mssql-jdbc-6.2.2.jre8.jar** i file di libreria di classi.
  
Microsoft JDBC driver 6.0 e 4.2 per SQL Server forniscono **sqljdbc41.jar**, e **sqljdbc42.jar** i file di libreria di classi.
  
Microsoft JDBC Driver 4.1 per SQL Server fornisce il **sqljdbc41.jar** file libreria di classi.

La scelta determinerà anche le funzionalità disponibili. Per altre informazioni sui file JAR da scegliere, vedere [requisiti di sistema per il Driver JDBC](../../connect/jdbc/system-requirements-for-the-jdbc-driver.md).  
  
## <a name="setting-the-classpath"></a>Impostazione del classpath

Il file con estensione jar di Microsoft JDBC driver non fanno parte di Java SDK e deve essere incluso nel Classpath dell'applicazione utente.

Se tramite JDBC Driver 4.1 o 4.2, impostare il classpath per includere **sqljdbc41.jar** oppure **sqljdbc42.jar** file dal download del driver corrispondente.

Se tramite JDBC Driver 6.2, impostare il classpath per includere il **mssql-jdbc-6.2.2.jre7.jar** oppure **mssql-jdbc-6.2.2.jre8.jar**.

Se tramite JDBC Driver 6.4, impostare il classpath per includere il **mssql-jdbc-6.4.0.jre7.jar**, * * mssql-jdbc-6.4.0.jre8.jar, o **mssql-jdbc-6.4.0.jre9.jar**.

Se tramite JDBC Driver 7.0, impostare il classpath per includere il **mssql-jdbc-7.0.0.jre8.jar** oppure **mssql-jdbc-7.0.0.jre10.jar**.

Se nel classpath manca una voce per il file con estensione Jar a destra, un'applicazione genera comune `Class not found` eccezione.  
  
### <a name="for-microsoft-jdbc-driver-70"></a>Per Microsoft JDBC Driver 7.0

Il **mssql-jdbc-7.0.0.jre8.jar** oppure **mssql-jdbc-7.0.0.jre10.jar** file vengono installati nei percorsi seguenti:

```bash
\<installation directory>\sqljdbc_<version>\<language>\mssql-jdbc-7.0.0.jre8.jar

\<installation directory>\sqljdbc_<version>\<language>\mssql-jdbc-7.0.0.jre10.jar
```

Il frammento di codice seguente è un esempio di istruzione CLASSPATH usata per un'applicazione Windows:  

`CLASSPATH =.;C:\Program Files\Microsoft JDBC Driver 7.0 for SQL Server\sqljdbc_7.0\enu\mssql-jdbc-7.0.0.jre10.jar`  
  
Il frammento di codice seguente è un esempio di istruzione CLASSPATH usata per un'applicazione Unix/Linux:  
  
`CLASSPATH =.:/home/usr1/mssqlserverjdbc/Driver/sqljdbc_7.0/enu/mssql-jdbc-7.0.0.jre10.jar`  
  
Assicurarsi che l'istruzione CLASSPATH contenga un solo [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], ad esempio uno **mssql-jdbc-7.0.0.jre8.jar** oppure **mssql-jdbc-7.0.0.jre10.jar**.

### <a name="for-microsoft-jdbc-driver-64"></a>Per Microsoft JDBC Driver 6.4

Il **mssql-jdbc-6.4.0.jre7.jar**, * * mssql-jdbc-6.4.0.jre8.jar, o **mssql-jdbc-6.4.0.jre9.jar** file vengono installati nel percorso seguente:  

```bash  
\<installation directory>\sqljdbc_<version>\<language>\mssql-jdbc-6.4.0.jre7.jar
  
\<installation directory>\sqljdbc_<version>\<language>\mssql-jdbc-6.4.0.jre8.jar

\<installation directory>\sqljdbc_<version>\<language>\mssql-jdbc-6.4.0.jre9.jar
```

Il frammento di codice seguente è un esempio di istruzione CLASSPATH usata per un'applicazione Windows:  
  
`CLASSPATH =.;C:\Program Files\Microsoft JDBC Driver 6.4 for SQL Server\sqljdbc_6.4\enu\mssql-jdbc-6.4.0.jre9.jar`  
  
Il frammento di codice seguente è un esempio di istruzione CLASSPATH usata per un'applicazione Unix/Linux:  
  
`CLASSPATH =.:/home/usr1/mssqlserverjdbc/Driver/sqljdbc_6.4/enu/mssql-jdbc-6.4.0.jre9.jar`  
  
Assicurarsi che l'istruzione CLASSPATH contenga un solo [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], ad esempio uno **mssql-jdbc-6.4.0.jre7.jar**, * * mssql-jdbc-6.4.0.jre8.jar, o **mssql-jdbc-6.4.0.jre9.jar**.

### <a name="for-microsoft-jdbc-driver-62"></a>Per Microsoft JDBC Driver 6.2

Il **mssql-jdbc-6.2.2.jre7.jar** oppure **mssql-jdbc-6.2.2.jre8.jar** file vengono installati nei percorsi seguenti:

```bash
\<installation directory>\sqljdbc_<version>\<language>\mssql-jdbc-6.2.2.jre7.jar
  
\<installation directory>\sqljdbc_<version>\<language>\mssql-jdbc-6.2.2.jre8.jar
```

Il frammento di codice seguente è un esempio di istruzione CLASSPATH usata per un'applicazione Windows:  
  
`CLASSPATH =.;C:\Program Files\Microsoft JDBC Driver 6.2 for SQL Server\sqljdbc_6.2\enu\mssql-jdbc-6.2.2.jre8.jar`  
  
Il frammento di codice seguente è un esempio di istruzione CLASSPATH usata per un'applicazione Unix/Linux:  
  
`CLASSPATH =.:/home/usr1/mssqlserverjdbc/Driver/sqljdbc_6.2/enu/mssql-jdbc-6.2.2.jre8.jar`  
  
Assicurarsi che l'istruzione CLASSPATH contenga solo un [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], ad esempio mssql-jdbc-6.2.2.jre7.jar o mssql-jdbc-6.2.2.jre8.jar.  

### <a name="for-microsoft-jdbc-driver-41-42-and-60"></a>Per Microsoft JDBC Driver 6.0, 4.2 e 4.1

I file sqljdbc.jar, sqljdbc4.jar, sqljdbc41.jar e sqljdbc42.jar vengono installati nei percorsi seguenti:  

```bash
\<installation directory>\sqljdbc_<version>\<language>\sqljdbc.jar  
  
\<installation directory>\sqljdbc_<version>\<language>\sqljdbc4.jar  
  
\<installation directory>\sqljdbc_<version>\<language>\sqljdbc41.jar  
  
\<installation directory>\sqljdbc_<version>\<language>\sqljdbc42.jar  
```

Il frammento di codice seguente è un esempio di istruzione CLASSPATH usata per un'applicazione Windows:  
  
`CLASSPATH =.;C:\Program Files\Microsoft JDBC Driver 6.0 for SQL Server\sqljdbc_4.2\enu\sqljdbc42.jar`  
  
Il frammento di codice seguente è un esempio di istruzione CLASSPATH usata per un'applicazione Unix/Linux:  

`CLASSPATH =.:/home/usr1/mssqlserverjdbc/Driver/sqljdbc_4.2/enu/sqljdbc42.jar`  
  
Verificare che l'istruzione CLASSPATH contenga solo un [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], ad esempio sqljdbc.jar, sqljdbc4.jar, sqljdbc41.jar o sqljdbc42.jar.  
  
> [!NOTE]  
> Nei sistemi Windows i nomi di directory con lunghezza superiore a quella della convenzione 8.3 o i nomi delle cartelle con spazi possono causare problemi con i classpath. In questo caso si consiglia di spostare provvisoriamente il file sqljdbc.jar file, sqljdbc4.jar file o sqljdbc41.jar in un nome di directory semplice, ad esempio `C:\Temp`, modificare il classpath e verificare se in questo modo il problema è stato risolto.  
  
### <a name="applications-that-are-run-directly-at-the-command-prompt"></a>Applicazioni eseguite direttamente dal prompt dei comandi

Il classpath è configurato nel sistema operativo. Accodare sqljdbc.jar, sqljdbc4.jar o sqljdbc41.jar al classpath del sistema. In alternativa, specificare il classpath nella riga di comando Java che esegue l'applicazione usando l'opzione `java -classpath`.  
  
### <a name="applications-that-run-in-an-ide"></a>Applicazioni eseguite in un IDE  

Ogni fornitore IDE offre un metodo diverso per impostare il classpath nel proprio IDE. La semplice impostazione del classpath nel sistema operativo non funzionerà. È necessario aggiungere sqljdbc.jar, sqljdbc4.jar o sqljdbc41.jar al classpath IDE.  
  
### <a name="servlets-and-jsps"></a>Servlet e JSP  

Servlet e JSP vengono eseguiti in un motore servlet/JSP, ad esempio Tomcat. Il classpath deve essere impostato in base alla documentazione del motore del servlet/JSP. La semplice impostazione del classpath nel sistema operativo non funzionerà. Alcuni motori del servlet/JSP offrono schermate di installazione utilizzabili per impostare il classpath del motore. In questo caso è necessario accodare il file JDBC Driver JAR corretto al classpath del motore esistente e riavviare il motore. In altri casi è possibile distribuire il driver copiando il file sqljdbc.jar, sqljdbc4.jar o sqljdbc41.jar in una directory specifica, ad esempio lib, durante l'installazione del motore. Il classpath del driver del motore può anche essere indicato in un file di configurazione specifico.  
  
### <a name="enterprise-java-beans"></a>Enterprise Java Beans  

Le piattaforme Enterprise Java Beans (EJB) vengono eseguite in un contenitore EJB. I contenitori EJB provengono da vari fornitori. Le applet Java vengono eseguite in un browser ma scaricate da un server Web. Copiare il file sqljdbc.jar, sqljdbc4.jar o sqljdbc41.jar nella radice del server Web e specificare il nome del file JAR nella scheda di archiviazione HTML dell'applet, ad esempio `<applet ... archive=mssql-jdbc-***.jar>`.  
  
## <a name="making-a-simple-connection-to-a-database"></a>Creazione di una connessione semplice a un database

Se si utilizza la libreria di classi sqljdbc.jar, le applicazioni devono innanzitutto registrare il driver, come indicato di seguito:  
  
`Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");`  

Quando viene caricato il driver, è possibile stabilire una connessione tramite un URL di connessione e al metodo getConnection della classe DriverManager:

```java
String connectionUrl = "jdbc:sqlserver://localhost:1433;" +  
   "databaseName=AdventureWorks;user=MyUserName;password=*****;";  
Connection con = DriverManager.getConnection(connectionUrl);  
```

A partire dall'API di JDBC 4.0 il metodo `DriverManager.getConnection()` è stato ottimizzato in modo da consentire il caricamento automatico dei driver JDBC. Le applicazioni non devono pertanto chiamare il metodo `Class.forName` per registrare o caricare il driver quando si usano librerie jar del driver.  
  
Quando viene chiamato il metodo getConnection della classe DriverManager, un driver appropriato viene individuato il set di driver JDBC registrati. il file sqljdbc4.jar, sqljdbc41.jar o sqljdbc42.jar include il file "META-INF/services/java.sql.Driver", che contiene il **sqlserverdriver** come driver registrato. Le applicazioni esistenti, che attualmente caricano i driver usando il metodo Class.forName, continueranno a funzionare senza alcuna modifica.  
  
> [!NOTE]  
> la libreria di classi sqljdbc4.jar, sqljdbc41.jar o sqljdbc42.jar non può essere utilizzata con le versioni precedenti di Java Runtime Environment (JRE). Visualizzare [requisiti di sistema per il Driver JDBC](../../connect/jdbc/system-requirements-for-the-jdbc-driver.md) per l'elenco di versioni JRE supportate dal [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)].  

Per altre informazioni su come connettersi con origini dati e usare un URL di connessione, vedere [Building the Connection URL](../../connect/jdbc/building-the-connection-url.md) e [impostando le proprietà di connessione](../../connect/jdbc/setting-the-connection-properties.md).  
  
## <a name="see-also"></a>Vedere anche  

[Panoramica del driver JDBC](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
