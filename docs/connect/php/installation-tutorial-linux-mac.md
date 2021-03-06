---
title: Linux e macOS esercitazione sull'installazione per Microsoft Drivers per PHP per SQL Server | Microsoft Docs
ms.date: 07/20/2018
ms.prod: sql
ms.prod_service: connectivity
ms.custom: ''
ms.technology: connectivity
ms.topic: conceptual
author: ulvii
ms.author: v-ulibra
manager: v-mabarw
ms.openlocfilehash: af05ede442133465e7f268665bac4cd11a17f653
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 11/13/2018
ms.locfileid: "51604601"
---
# <a name="linux-and-macos-installation-tutorial-for-the-microsoft-drivers-for-php-for-sql-server"></a>Linux e macOS esercitazione sull'installazione per Microsoft Drivers per PHP per SQL Server
Le istruzioni seguenti si presuppongono un ambiente pulito e mostrano come installare PHP 7.x, il driver ODBC di Microsoft, Apache e Microsoft Drivers per PHP per SQL Server in Ubuntu 16.04, 17.10 e 18.04, 7 RedHat, Debian 8 e 9, Suse 12 e macOS 10.11 , 10.12 e 10.13. Queste istruzioni è consigliabile installare i driver tramite PECL, ma è anche possibile scaricare i file binari precompilati dal [Microsoft Drivers per PHP per SQL Server](https://github.com/Microsoft/msphpsql/releases) Github pagina project e installarli seguendo le istruzioni [ Caricamento del driver Microsoft per PHP per SQL Server](../../connect/php/loading-the-php-sql-driver.md). Per una spiegazione del caricamento di estensione e il motivo per cui non è aggiungere le estensioni di PHP. ini, vedere la sezione sul [caricamento del driver](../../connect/php/loading-the-php-sql-driver.md##loading-the-driver-at-php-startup).

Installare queste istruzioni PHP 7.2 per impostazione predefinita, vedere le note all'inizio di ogni sezione per installare PHP 7.0 o 7.1.

## <a name="contents-of-this-page"></a>Contenuto di questa pagina:

- [Installare i driver in Ubuntu 16.04 e 17.10 18.04](#installing-the-drivers-on-ubuntu-1604-1710-and-1804)
- [Installazione dei driver in Red Hat 7](#installing-the-drivers-on-red-hat-7)
- [Installazione dei driver in Debian 8 e 9](#installing-the-drivers-on-debian-8-and-9)
- [Installare i driver in Suse 12](#installing-the-drivers-on-suse-12)
- [Installare i driver in macOS El Capitan e Sierra o High Sierra](#installing-the-drivers-on-macos-el-capitan-sierra-and-high-sierra)

## <a name="installing-the-drivers-on-ubuntu-1604-1710-and-1804"></a>Installare i driver su Ubuntu 16.04 17.10 e 18.04

> [!NOTE]
> Per installare PHP 7.0 o 7.1, sostituire 7.2 con 7.0 o 7.1 nei comandi seguenti.
> Per Ubuntu 18.04, il passaggio per aggiungere il repository ondrej non è obbligatorio a meno che non è necessario PHP 7.0 o 7.1. Tuttavia, l'installazione di PHP 7.0 o 7.1 in Ubuntu 18.04 potrebbe non funzionare come pacchetti dal repository ondrej forniti con dipendenze che possono entrare in conflitto con una base installare 18.04 Ubuntu.

### <a name="step-1-install-php"></a>Passaggio 1. Installare PHP
```
sudo su
add-apt-repository ppa:ondrej/php -y
apt-get update
apt-get install php7.2 php7.2-dev php7.2-xml -y --allow-unauthenticated
```
### <a name="step-2-install-prerequisites"></a>Passaggio 2. Prerequisiti di installazione
Installare il driver ODBC per Ubuntu seguendo le istruzioni nella [pagina di installazione di Linux e macOS](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md).

### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>Passaggio 3. Installare i driver PHP per Microsoft SQL Server
```
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
sudo su
echo extension=pdo_sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/30-pdo_sqlsrv.ini
echo extension=sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/20-sqlsrv.ini
exit
```
### <a name="step-4-install-apache-and-configure-driver-loading"></a>Passaggio 4. Installare Apache e configurare il caricamento del driver
```
sudo su
apt-get install libapache2-mod-php7.2 apache2
a2dismod mpm_event
a2enmod mpm_prefork
a2enmod php7.2
echo "extension=pdo_sqlsrv.so" >> /etc/php/7.2/apache2/conf.d/30-pdo_sqlsrv.ini
echo "extension=sqlsrv.so" >> /etc/php/7.2/apache2/conf.d/20-sqlsrv.ini
exit
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>Passaggio 5. Riavviare Apache e testare lo script di esempio
```
sudo service apache2 restart
```
Per testare l'installazione, vedere [Testing dell'installazione](#testing-your-installation) alla fine di questo documento.

## <a name="installing-the-drivers-on-red-hat-7"></a>Installazione dei driver in Red Hat 7

> [!NOTE]
> Per installare PHP 7.0 o 7.1, sostituire remi php72 con remi php70 o remi-php71 rispettivamente nei comandi seguenti.

### <a name="step-1-install-php"></a>Passaggio 1. Installare PHP

```
sudo su
wget https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
wget https://rpms.remirepo.net/enterprise/remi-release-7.rpm
rpm -Uvh remi-release-7.rpm epel-release-latest-7.noarch.rpm
subscription-manager repos --enable=rhel-7-server-optional-rpms
yum-config-manager --enable remi-php72
yum update
yum install php php-pdo php-xml php-pear php-devel re2c gcc-c++ gcc
```
### <a name="step-2-install-prerequisites"></a>Passaggio 2. Prerequisiti di installazione
Installare il driver ODBC per Red Hat 7 seguendo le istruzioni nella [pagina di installazione di Linux e macOS](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md).

La compilazione i driver di PHP PECL con PHP 7.2 richiede GCC una più recente rispetto al valore predefinito:
```
sudo yum-config-manager --enable rhel-server-rhscl-7-rpms
sudo yum install devtoolset-7
scl enable devtoolset-7 bash
```
### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>Passaggio 3. Installare i driver PHP per Microsoft SQL Server
```
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
sudo su
echo extension=pdo_sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/30-pdo_sqlsrv.ini
echo extension=sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/20-sqlsrv.ini
exit
```
Un problema in PECL potrebbe impedire l'installazione corretta dell'ultima versione dei driver anche se è stato aggiornato GCC. Per installare, scaricare i pacchetti e compilare manualmente (una procedura simile per pdo_sqlsrv):
```
pecl download sqlsrv
tar xvzf sqlsrv-5.3.0.tgz
cd sqlsrv-5.3.0/
phpize
./configure --with-php-config=/usr/bin/php-config
make
sudo make install
```
In alternativa è possibile scaricare i file binari precompilati dal [pagina del progetto Github](https://github.com/Microsoft/msphpsql/releases), oppure installare dal repository Remi:
```
sudo yum install php-sqlsrv php-pdo_sqlsrv
```
### <a name="step-4-install-apache"></a>Passaggio 4. Installare Apache
```
sudo yum install httpd
```
SELinux viene installato per impostazione predefinita e viene eseguito in modalità applica. Per consentire di Apache per connettersi ai database tramite SELinux, eseguire il comando seguente:
```
sudo setsebool -P httpd_can_network_connect_db 1
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>Passaggio 5. Riavviare Apache e testare lo script di esempio
```
sudo apachectl restart
```
Per testare l'installazione, vedere [Testing dell'installazione](#testing-your-installation) alla fine di questo documento.

## <a name="installing-the-drivers-on-debian-8-and-9"></a>Installazione dei driver in Debian 8 e 9

> [!NOTE]
> Sostituisci 7.2 nei comandi seguenti per installare PHP 7.0 o 7.1, 7.0 o 7.1.

### <a name="step-1-install-php"></a>Passaggio 1. Installare PHP
```
sudo su
apt-get install curl apt-transport-https
wget -O /etc/apt/trusted.gpg.d/php.gpg https://packages.sury.org/php/apt.gpg
echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" > /etc/apt/sources.list.d/php.list
apt-get update
apt-get install -y php7.2 php7.2-dev php7.2-xml
```
### <a name="step-2-install-prerequisites"></a>Passaggio 2. Prerequisiti di installazione
Installare il driver ODBC per Debian seguendo le istruzioni nella [pagina di installazione di Linux e macOS](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md). 

È necessario anche generare le impostazioni locali corrette per ottenere un output PHP per visualizzare correttamente in un browser. Ad esempio, per le impostazioni locali UTF-8 it_IT, eseguire i comandi seguenti:
```
sudo su
sed -i 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/g' /etc/locale.gen
locale-gen
```

### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>Passaggio 3. Installare i driver PHP per Microsoft SQL Server
```
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
sudo su
echo extension=pdo_sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/30-pdo_sqlsrv.ini
echo extension=sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/20-sqlsrv.ini
exit
```
### <a name="step-4-install-apache-and-configure-driver-loading"></a>Passaggio 4. Installare Apache e configurare il caricamento del driver
```
sudo su
apt-get install libapache2-mod-php7.2 apache2
a2dismod mpm_event
a2enmod mpm_prefork
a2enmod php7.2
echo "extension=pdo_sqlsrv.so" >> /etc/php/7.2/apache2/conf.d/30-pdo_sqlsrv.ini
echo "extension=sqlsrv.so" >> /etc/php/7.2/apache2/conf.d/20-sqlsrv.ini
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>Passaggio 5. Riavviare Apache e testare lo script di esempio
```
sudo service apache2 restart
```
Per testare l'installazione, vedere [Testing dell'installazione](#testing-your-installation) alla fine di questo documento.

## <a name="installing-the-drivers-on-suse-12"></a>Installare i driver in Suse 12

> [!NOTE]
> Per installare PHP 7.0, ignora il comando seguente aggiungendo il repository - 7.0 è l'impostazione predefinita PHP in suse 12.
> Per installare PHP 7.1, sostituire l'URL del repository di seguito con l'URL seguente: `https://download.opensuse.org/repositories/devel:/languages:/php:/php71/SLE_12/devel:languages:php:php71.repo`

### <a name="step-1-install-php"></a>Passaggio 1. Installare PHP
```
sudo su
zypper -n ar -f https://download.opensuse.org/repositories/devel:languages:php/SLE_12/devel:languages:php.repo
zypper --gpg-auto-import-keys refresh
zypper -n install php7 php7-pear php7-devel
```
### <a name="step-2-install-prerequisites"></a>Passaggio 2. Prerequisiti di installazione
Installare il driver ODBC per Suse 12, seguendo le istruzioni [pagina di installazione di Linux e macOS](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md).

### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>Passaggio 3. Installare i driver PHP per Microsoft SQL Server
```
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
sudo su
echo extension=pdo_sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/pdo_sqlsrv.ini
echo extension=sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/sqlsrv.ini
exit
```
### <a name="step-4-install-apache-and-configure-driver-loading"></a>Passaggio 4. Installare Apache e configurare il caricamento del driver
```
sudo su
zypper install apache2 apache2-mod_php7
a2enmod php7
echo "extension=sqlsrv.so" >> /etc/php7/apache2/php.ini
echo "extension=pdo_sqlsrv.so" >> /etc/php7/apache2/php.ini
exit
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>Passaggio 5. Riavviare Apache e testare lo script di esempio
```
sudo systemctl restart apache2
```
Per testare l'installazione, vedere [Testing dell'installazione](#testing-your-installation) alla fine di questo documento.

## <a name="installing-the-drivers-on-macos-el-capitan-sierra-and-high-sierra"></a>Installare i driver in macOS El Capitan e Sierra o High Sierra

Se non è già stata, installare brew come indicato di seguito:
```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

> [!NOTE]
> Per installare PHP 7.0 o 7.1, sostituire php@7.2 con php@7.0 o php@7.1 rispettivamente nei comandi seguenti.

### <a name="step-1-install-php"></a>Passaggio 1. Installare PHP

```
brew tap
brew tap homebrew/core
brew install php@7.2
```
PHP dovrebbe ora essere nel proprio percorso: eseguire `php -v` per verificare che sia in esecuzione la versione corretta di PHP. Se PHP non sia presente nel percorso o non è la versione corretta, eseguire il comando seguente:
```
brew link --force --overwrite php@7.2
```

### <a name="step-2-install-prerequisites"></a>Passaggio 2. Prerequisiti di installazione
Installare il driver ODBC per macOS, seguendo le istruzioni [pagina di installazione di Linux e macOS](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md). 

Inoltre, si potrebbe essere necessario installare gli strumenti di creazione GNU:
```
brew install autoconf automake libtool
```

### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>Passaggio 3. Installare i driver PHP per Microsoft SQL Server
```
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
```
### <a name="step-4-install-apache-and-configure-driver-loading"></a>Passaggio 4. Installare Apache e configurare il caricamento del driver
```
brew install apache2
```
Per trovare il file di configurazione per l'installazione di Apache Apache, eseguire 
```
apachectl -V | grep SERVER_CONFIG_FILE
``` 
e sostituire il percorso `httpd.conf` nei comandi seguenti:
```
echo "LoadModule php7_module /usr/local/opt/php@7.2/lib/httpd/modules/libphp7.so" >> /usr/local/etc/httpd/httpd.conf
(echo "<FilesMatch .php$>"; echo "SetHandler application/x-httpd-php"; echo "</FilesMatch>";) >> /usr/local/etc/httpd/httpd.conf
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>Passaggio 5. Riavviare Apache e testare lo script di esempio
```
sudo apachectl restart
```
Per testare l'installazione, vedere [Testing dell'installazione](#testing-your-installation) alla fine di questo documento.

## <a name="testing-your-installation"></a>Test dell'installazione

Per testare questo esempio di script, creare un file denominato testsql.php nella radice del documento del sistema. Si tratta `/var/www/html/` su Red Hat, Ubuntu e Debian `/srv/www/htdocs` in SUSE o `/usr/local/var/www` in macOS. Copiare lo script seguente, sostituendo il server, database, nome utente e password in modo appropriato.
```
<?php
$serverName = "yourServername";
$connectionOptions = array(
    "database" => "yourDatabase",
    "uid" => "yourUsername",
    "pwd" => "yourPassword"
);

// Establishes the connection
$conn = sqlsrv_connect($serverName, $connectionOptions);
if ($conn === false) {
    die(formatErrors(sqlsrv_errors()));
}

// Select Query
$tsql = "SELECT @@Version AS SQL_VERSION";

// Executes the query
$stmt = sqlsrv_query($conn, $tsql);

// Error handling
if ($stmt === false) {
    die(formatErrors(sqlsrv_errors()));
}
?>

<h1> Results : </h1>

<?php
while ($row = sqlsrv_fetch_array($stmt, SQLSRV_FETCH_ASSOC)) {
    echo $row['SQL_VERSION'] . PHP_EOL;
}

sqlsrv_free_stmt($stmt);
sqlsrv_close($conn);

function formatErrors($errors)
{
    // Display errors
    echo "Error information: <br/>";
    foreach ($errors as $error) {
        echo "SQLSTATE: ". $error['SQLSTATE'] . "<br/>";
        echo "Code: ". $error['code'] . "<br/>";
        echo "Message: ". $error['message'] . "<br/>";
    }
}
?>
```
Inserire nel browser https://localhost/testsql.php (https://localhost:8080/testsql.php in macOS). È ora deve essere in grado di connettersi a SQL Server/database SQL di Azure.

## <a name="see-also"></a>Vedere anche  
[Introduzione a Microsoft Drivers per PHP per SQL Server](../../connect/php/getting-started-with-the-php-sql-driver.md)

[Caricamento dei Driver Microsoft per PHP per SQL Server](../../connect/php/loading-the-php-sql-driver.md)

[Requisiti di sistema dei driver Microsoft per PHP per SQL Server](../../connect/php/system-requirements-for-the-php-sql-driver.md)
