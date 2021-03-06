---
title: Release Notes (Driver ODBC per SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 07/03/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: b8459ed8-625e-4d8b-891c-e7e78c9977cc
author: MightyPen
ms.author: v-jizho2
manager: kenvh
ms.openlocfilehash: cb599d59a374fc09dbc0009f0288296cc1df9d9d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 10/01/2018
ms.locfileid: "47702070"
---
# <a name="release-notes"></a>Note sulla versione
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

  Note sulla versione per Microsoft ODBC Driver for SQL Server in Windows.  

## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-172-for-includessnoversionincludesssnoversion-mdmd-on-windows"></a>Novità di [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 17.2 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in Windows

**Funzionalità aggiunte**:

Classificazione dei dati per Database SQL di Azure e SQL Server, per altre informazioni vedere [classificazione dei dati](../data-classification.md)

Supporto per la codifica UTF-8 server

[Correzioni di bug](../bug-fixes.md)

## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-171-for-includessnoversionincludesssnoversion-mdmd-on-windows"></a>Novità di [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 17.1 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in Windows

**Funzionalità aggiunte**:

Supporto per `SQL_COPT_SS_CEKCACHETTL` e `SQL_COPT_SS_TRUSTEDCMKPATHS` attributi di connessione (per altre informazioni, vedere [utilizzo di Always Encrypted con il Driver ODBC per SQL Server](../using-always-encrypted-with-the-odbc-driver.md))
- `SQL_COPT_SS_CEKCACHETTL` Consente di controllare l'ora in cui è presente nella cache locale delle chiavi di crittografia di colonna, nonché lo scaricamento
- `SQL_COPT_SS_TRUSTEDCMKPATHS` Consente all'applicazione limitare le operazioni di Always Encrypted per usare solo l'elenco specificato di chiavi Master della colonna


Supporto dell'autenticazione interattiva di Azure Active Directory

[Correzioni di bug](../bug-fixes.md)


## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-17-for-includessnoversionincludesssnoversion-mdmd-on-windows"></a>Novità di [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 17 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in Windows

**Funzionalità aggiunte**:

Supporto per Always Encrypted per l'API BCP

Nuovo attributo di stringa di connessione UseFMTOnly fa sì che i driver per l'uso di metadati legacy in casi particolari che richiedono le tabelle temporanee.

Supporto per l'istanza gestita SQL di Azure (anteprima privata estesa). 
> [!NOTE]
> Esistono numerose differenze quando si usa l'istanza gestita:
> -   FILESTREAM non è supportato 
> -   Accesso del file System locale non è supportato, ma obbligatorio per elementi quali tracefiles 
> -   Crea tipo definito dall'utente da local path non è supportato 
> -   Non è supportata l'autenticazione integrata di Windows 
> -   DTC non è supportato 
> -   account 'sa' non è presente (l'account predefinito viene chiamato 'cloudSA')
> -   Errore di token TDS (0xAA) restituisce il nome server errato
> -   Non sono supportati i caratteri speciali nel nome del database 
> -   ALTER DATABASE [dbname1] MODIFY NAME = [dbname2] non è supportato
> -   I messaggi di errore vengono sempre visualizzati in inglese, indipendentemente dal linguaggio impostazioni (come Azure) 
  

## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-131-for-includessnoversionincludesssnoversion-mdmd-on-windows"></a>Novità di [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 13.1 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in Windows  
 ODBC Driver 13.1 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] aggiunge il supporto per [Always Encrypted](../../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md) e [Azure Active Directory](../../../connect/odbc/using-azure-active-directory.md) quando usato in combinazione con Microsoft SQL Server 2016.  Connessione corrispondente pooling le parole chiave e attributi sono descritti in [Driver Aware Connection Pooling in ODBC Driver for SQL Server](../../../connect/odbc/windows/driver-aware-connection-pooling-in-the-odbc-driver-for-sql-server.md).

 ## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-13-for-includessnoversionincludesssnoversion-mdmd-on-windows"></a>Novità di [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 13 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in Windows  
 ODBC Driver 13 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] include una funzionalità precedente da ODBC Driver 11 for SQL Server e aggiunge il supporto per Microsoft SQL Server 2016.

## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-11-for-includessnoversionincludesssnoversion-mdmd-on-windows"></a>Novità di [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 11 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in Windows  
 ODBC Driver 11 for SQL Server contiene nuove [funzionalità](./features-of-the-microsoft-odbc-driver-for-sql-server-on-windows.md), nonché tutte le funzionalità fornite con ODBC in SQL Server 2012 Native Client.  
