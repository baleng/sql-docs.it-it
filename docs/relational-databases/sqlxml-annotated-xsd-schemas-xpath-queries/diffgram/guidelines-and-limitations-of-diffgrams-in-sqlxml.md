---
title: Linee guida e le limitazioni di DiffGram SQLXML | Documenti di Microsoft
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- DiffGrams [SQLXML], about DiffGrams
ms.assetid: cf8689c4-2a63-4d05-b202-21b5ff187d7f
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d30c7a93906f9de5fb3826ac4d8a8e1f845f1693
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/01/2018
ms.locfileid: "47779169"
---
# <a name="guidelines-and-limitations-of-diffgrams-in-sqlxml"></a>Linee guida e limitazioni per i Diffgram in SQLXML
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Quando si utilizzano Diffgram con SQLXML 4.0, tenere presenti le considerazioni seguenti:  
  
-   I tipi di oggetto binario di grandi dimensioni (BLOB), ad esempio **text/ntext** e le immagini non devono essere utilizzati nel  **\<diffgr: prima >** bloccare quando si utilizzano DiffGram, perché in questo caso verrà inclusi per l'utilizzo in controllo della concorrenza. Ciò può provocare problemi con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a causa delle limitazioni applicate al confronto per i tipi BLOB. Ad esempio, viene usata la parola chiave LIKE nella clausola WHERE per il confronto tra le colonne del **testo** del tipo di dati; tuttavia, i confronti avrà esito negativo nel caso dei tipi BLOB in cui la dimensione dei dati è maggiore di 8 KB.  
  
-   Caratteri speciali nei **ntext** dati possono causare problemi con SQLXML 4.0 a causa delle limitazioni applicate al confronto per i tipi BLOB. Ad esempio, l'utilizzo di "[Serializable]" nel  **\<diffgr: prima >** blocco di un DiffGram se utilizzato nel controllo della concorrenza di una colonna di **ntext** tipo avrà esito negativo con il provider SQLOLEDB seguente Descrizione dell'errore:  
  
    ```  
    Empty update, no updatable rows found   Transaction aborted  
    ```  
  
  
