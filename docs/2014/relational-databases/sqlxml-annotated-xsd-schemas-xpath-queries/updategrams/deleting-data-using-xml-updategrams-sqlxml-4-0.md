---
title: L'eliminazione dei dati mediante Updategram XML (SQLXML 4.0) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- <after> block
- updategrams [SQLXML], deleting data
- <before> block
- mapping-schema attribute
- record deletions [SQLXML]
ms.assetid: 4fb116d7-7652-474a-a567-cb475a20765c
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 9d16d27583854988a6e937c0859239875e15616f
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/02/2018
ms.locfileid: "48220301"
---
# <a name="deleting-data-using-xml-updategrams-sqlxml-40"></a>Eliminazione di dati mediante updategram XML (SQLXML 4.0)
  Un updategram indica un'operazione di eliminazione quando un'istanza di record è presente il  **\<prima di >** blocco senza record corrispondenti nel  **\<dopo >** blocco. In questo caso, l'updategram Elimina il record nel  **\<prima di >** blocco dal database.  
  
 Di seguito viene illustrato il formato dell'updategram per un'operazione di eliminazione:  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync [mapping-schema="SampleSchema.xml"]  >  
   <updg:before>  
       <ElementName />  
      [<ElementName .../>... ]  
   </updg:before>  
    [<updg:after>  
    </updg:after>]  
  </updg:sync>  
</ROOT>  
```  
  
 È possibile omettere il  **\<dopo >** contrassegnerà se l'updategram esegue solo un'operazione di eliminazione. Se non si specifica l'opzione facoltativa `mapping-schema` attributo, il  **\<ElementName >** specificato nell'updategram esegue il mapping a una tabella di database e la mappa di elementi o attributi figlio alle colonne nella tabella.  
  
 Se un elemento specificato nell'updategram corrisponde più di una riga nella tabella o non corrisponde ad alcuna riga, l'updategram restituisce un errore e Annulla l'intera  **\<sync >** blocco. Un elemento dell'updategram può eliminare un solo record per volta.  
  
## <a name="examples"></a>Esempi  
 Negli esempi presentati in questa sezione viene utilizzato il mapping predefinito, ovvero non viene specificato alcuno schema di mapping nell'updategram. Per altri esempi di updategram che utilizzano schemi di mapping, vedere [specifica uno Schema di Mapping con annotazioni in un Updategram &#40;SQLXML 4.0&#41;](specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md).  
  
 Per creare esempi reali utilizzando gli esempi seguenti, è necessario soddisfare i requisiti specificati nelle [requisiti per l'esecuzione di esempi di SQLXML](../../sqlxml/requirements-for-running-sqlxml-examples.md).  
  
### <a name="a-deleting-a-record-by-using-an-updategram"></a>A. Eliminazione di un record mediante un updategram  
 Negli updategram seguenti vengono eliminati due record dalla tabella HumanResources.Shift.  
  
 In questi esempi l'updategram non specifica uno schema di mapping, pertanto utilizza il mapping predefinito nel quale il nome dell'elemento esegue il mapping a un nome di tabella e gli attributi o i sottoelementi eseguono il mapping alle colonne.  
  
 Questo primo updategram è incentrato sugli attributi e identifica due turni (giorno-sera e sera-notte) nel  **\<prima di >** blocco. Poiché non vi è alcun record corrispondente nel  **\<dopo >** blocco, si tratta di un'operazione di eliminazione.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:sync >  
  <updg:before>  
       <HumanResources.Shift ShiftID="4"  
                        Name="Day-Evening"  
                        StartTime="1900-01-01 11:00:00.000"  
                        EndTime="1900-01-01 19:00:00.000"  
                        ModifiedDate="2004-01-01 00:00:00.000" />  
       <HumanResources.Shift ShiftID="5"  
                        Name="Evening-Night"  
                        StartTime="1900-01-01 19:00:00.000"  
                        EndTime="1900-01-01 03:00:00.000"  
                        ModifiedDate="2004-01-01 00:00:00.000" />  
  </updg:before>  
  <updg:after>  
  </updg:after>  
</updg:sync>  
</ROOT>  
```  
  
##### <a name="to-test-the-updategram"></a>Per testare l'updategram  
  
1.  Completare l'esempio B ("inserimento di più record mediante un updategram") nella [inserimento di dati mediante Updategram XML &#40;SQLXML 4.0&#41;](inserting-data-using-xml-updategrams-sqlxml-4-0.md).  
  
2.  Copiare l'updategram sopra indicato in blocco note e salvarlo Updategram-removeshifts nella stessa cartella utilizzata per il completamento ("inserimento di più record mediante un updategram") nella [inserimento di dati mediante Updategram XML &#40;SQLXML 4.0&#41; ](inserting-data-using-xml-updategrams-sqlxml-4-0.md).  
  
3.  Creare e utilizzare lo script di test SQLXML 4.0 (Sqlxml4test.vbs) per eseguire l'updategram.  
  
     Per altre informazioni, vedere [utilizzo di ADO per eseguire query di SQLXML 4.0](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Considerazioni sulla sicurezza degli updategram &#40;SQLXML 4.0&#41;](../security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
