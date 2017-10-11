---
title: Passaggio a un Record | Documenti Microsoft
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- record jumping [ADO]
- jumping to record [ADO]
ms.assetid: 6caf6299-2eea-4d34-9b0e-b75aab07b740
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 19a4275d339132db8efd4b09a313b482fc8cb666
ms.contentlocale: it-it
ms.lasthandoff: 09/09/2017

---
# <a name="jumping-to-a-record"></a>Passaggio a un Record
Il [spostare](../../../ado/reference/ado-api/move-method-ado.md) metodo consente di spostare in avanti o indietro di **Recordset** un numero specificato di record utilizzando la sintassi seguente:  
  
```  
oRs.Move NumRecords, Start  
```  
  
## <a name="remarks"></a>Osservazioni  
 Il **spostare** metodo è supportato in tutti **Recordset** oggetti.  
  
 Se il *NumRecords* argomento è maggiore di zero, la posizione del record corrente viene spostata in avanti (verso la fine del **Recordset**). Se *NumRecords* è minore di zero, la posizione corrente si sposta all'indietro (verso l'inizio del **Recordset**).  
  
 Se il **spostare** chiamata Sposta la posizione corrente a un punto prima del primo record, ADO imposta il record corrente nella posizione precedente al primo record di **Recordset** (**BOF** è **True**). Tenta di spostarsi con le versioni precedenti quando il **BOF** proprietà è già **True** genera un errore.  
  
 Se il **spostare** chiamata Sposta la posizione corrente a un punto successivo all'ultimo record, ADO imposta il record corrente alla posizione successiva all'ultimo record nel **Recordset** (**EOF** è **True**). Tentativo di spostare in avanti quando il **EOF** proprietà è già **True** genera un errore.  
  
 La chiamata di **spostare** metodo da un oggetto vuoto **Recordset** oggetto genera un errore.  
  
 Se si passa un segnalibro nel *avviare* argomento, lo spostamento è relativo al record con il segnalibro, supponendo che il **Recordset** oggetto supporta i segnalibri. Ottenere un segnalibro utilizzando il [segnalibro](../../../ado/reference/ado-api/bookmark-property-ado.md) proprietà. Se non specificato, lo spostamento è relativo al record corrente.  
  
 Se si utilizza il **CacheSize** proprietà da memorizzare localmente i record dal provider, passando un *NumRecords* argomento che sposta la posizione corrente all'esterno del gruppo corrente di record memorizzati nella cache ADO viene forzato a recuperare un nuovo gruppo di record, a partire dal record di destinazione. Il **CacheSize** proprietà determina le dimensioni del gruppo appena recuperato e il record di destinazione è il primo record recuperato.