---
title: Proprietà descrizione | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Error::Description
- Error::GetDescription
- Error::get_Description
helpviewer_keywords:
- Description property
ms.assetid: 4b5d6790-6c29-42aa-bf78-d9cfb8ad7965
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b9a97e1e63e3896cd451c68d6198baa991945e7a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/01/2018
ms.locfileid: "47704522"
---
# <a name="description-property"></a>Proprietà Description
Descrive un' [errore](../../../ado/reference/ado-api/error-object.md) oggetto.  
  
## <a name="return-value"></a>Valore restituito  
 Restituisce un **stringa** valore contenente una descrizione dell'errore.  
  
## <a name="remarks"></a>Note  
 Usare la **descrizione** proprietà per ottenere una breve descrizione dell'errore. Visualizzare questa proprietà per generare un avviso all'utente di un errore che non è possibile o non si desidera gestire. La stringa dipenderà da ADO o un provider.  
  
 Provider sono responsabili per il passaggio di testo dell'errore specifico per ADO. ADO aggiunge un' [errore](../../../ado/reference/ado-api/error-object.md) dell'oggetto per il **errori** raccolta per ogni provider di errore o avviso viene ricevuto. Enumerare i **errori** raccolta per individuare gli errori che il provider passa.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Error](../../../ado/reference/ado-api/error-object.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Description, HelpContext, HelpFile, NativeError, numero, origine e SQLState proprietà esempio (VB)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [Description, HelpContext, HelpFile, NativeError, numero, origine e SQLState esempio di proprietà (VC + +)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   
 [Proprietà HelpContext, HelpFile](../../../ado/reference/ado-api/helpcontext-helpfile-properties.md)   
 [Proprietà Number (ADO)](../../../ado/reference/ado-api/number-property-ado.md)   
 [Proprietà Source (errore ADO)](../../../ado/reference/ado-api/source-property-ado-error.md)
