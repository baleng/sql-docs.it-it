---
title: Ottimizzazione di un output degli errori con il componente script | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- transformations [Integration Services], components
- Script component [Integration Services], examples
- error outputs [Integration Services], enhancing
- Script component [Integration Services], transformation components
ms.assetid: f7c02709-f1fa-4ebd-b255-dc8b81feeaa5
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 68973d2d0464372b070667a5d59dcc4327b211bf
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52527947"
---
# <a name="enhancing-an-error-output-with-the-script-component"></a>Ottimizzazione di un output degli errori con il componente script
  Per impostazione predefinita, le due colonne supplementari in un output degli errori di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], ovvero ErrorCode e ErrorColumn, contengono solo codici numerici che rappresentano un numero di errore e l'ID della colonna in cui si è verificato l'errore. Tali valori numerici possono avere un'utilità limitata senza la descrizione dell'errore e il nome della colonna corrispondenti.  
  
 In questo argomento viene descritto come aggiungere la descrizione dell'errore e il nome della colonna ai dati dell'output degli errori esistente nel flusso di dati tramite il componente script. Nell'esempio viene aggiunta la descrizione dell'errore che corrisponde a un codice di errore specifico predefinito di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] utilizzando il metodo <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.GetErrorDescription%2A> dell'interfaccia <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100>, disponibile tramite la proprietà <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ComponentMetaData%2A> del componente script. Nell'esempio viene poi aggiunto il nome della colonna che corrisponde all'ID di derivazione acquisito tramite il metodo <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData130.GetIdentificationStringByID%2A> della stessa interfaccia.  
  
> [!NOTE]  
>  Se si desidera creare un componente da riutilizzare più facilmente con più attività Flusso di dati e più pacchetti, è possibile utilizzare il codice di questo esempio di componente script come punto iniziale per un componente del flusso di dati personalizzato. Per altre informazioni, vedere [Sviluppo di un componente del flusso di dati personalizzato](../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md).  
  
## <a name="example"></a>Esempio  
 Nell'esempio illustrato viene usato un componente script configurato come trasformazione per aggiungere la descrizione dell'errore e il nome della colonna ai dati dell'output degli errori esistente nel flusso di dati.  
  
 Per altre informazioni su come configurare il componente script per usarlo come trasformazione nel flusso di dati, vedere [Creazione di una trasformazione sincrona con il componente script](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md) e [Creazione di una trasformazione asincrona con il componente script](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-an-asynchronous-transformation-with-the-script-component.md).  
  
#### <a name="to-configure-this-script-component-example"></a>Per configurare l'esempio di componente script  
  
1.  Prima di creare il nuovo componente script, configurare un componente a monte nel flusso di dati per reindirizzare righe all'output degli errori quando si verifica un errore o un troncamento. A scopo di test, è possibile configurare un componente in modo da assicurarsi che si verificheranno errori, ad esempio configurando una trasformazione Ricerca tra due tabelle in cui la ricerca avrà esito negativo.  
  
2.  Aggiungere un nuovo componente script all'area di progettazione del flusso di dati e configurarlo come trasformazione.  
  
3.  Connettere l'output degli errori del componente a monte a questo nuovo componente script.  
  
4.  Aprire **Editor trasformazione Script** e nella pagina **Script** selezionare il linguaggio di scripting per la proprietà **ScriptLanguage**.  
  
5.  Fare clic su **Modifica script[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] per aprire l'IDE di**  [!INCLUDE[msCoName](../../includes/msconame-md.md)] Tools for Applications (VSTA) e aggiungere il codice di esempio illustrato di seguito.  
  
6.  Chiudere VSTA.  
  
7.  Nella pagina **Colonne di input** dell'Editor trasformazione Script selezionare le colonne ErrorCode e ErrorColumn.  
  
8.  Nella pagina **Input e output** aggiungere due nuove colonne.  
  
    -   Aggiungere una nuova colonna di output di tipo **Stringa** denominata **ErrorDescription**. Aumentare la lunghezza predefinita della nuova colonna fino a 255 per supportare messaggi lunghi.  
  
    -   Aggiungere un'altra nuova colonna di output di tipo **Stringa** denominata **ColumnName**. Aumentare la lunghezza predefinita della nuova colonna fino a 255 per supportare valori lunghi.  
  
9. Chiudere l'**Editor trasformazione Script.**  
  
10. Connettere l'output del componente script a una destinazione appropriata. Le destinazioni file flat sono le più facili da configurare per test ad hoc.  
  
11. Eseguire il pacchetto.  
  
```vb  
Public Class ScriptMain  
    Inherits UserComponent  
    Public Overrides Sub Input0_ProcessInputRow(ByVal Row As Input0Buffer)  
  
      Row.ErrorDescription = _  
        Me.ComponentMetaData.GetErrorDescription(Row.ErrorCode)  
  
      Dim componentMetaData130 = TryCast(Me.ComponentMetaData, IDTSComponentMetaData130)  
      If componentMetaData130 IsNot Nothing Then  
        Row.ColumnName = componentMetaData130.GetIdentificationStringByID(Row.ErrorColumn)  
         End If  
  
    End Sub  
End Class  
```  
  
```csharp  
public class ScriptMain:  
    UserComponent  
{  
    public override void Input0_ProcessInputRow(Input0Buffer Row)  
    {  
  
      Row.ErrorDescription = this.ComponentMetaData.GetErrorDescription(Row.ErrorCode);  
  
      var componentMetaData130 = this.ComponentMetaData as IDTSComponentMetaData130;  
      if (componentMetaData130 != null)  
        {  
            Row.ColumnName = componentMetaData130.GetIdentificationStringByID(Row.ErrorColumn);  
        }  
  
    }  
}  
  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Gestione degli errori nei dati](../../integration-services/data-flow/error-handling-in-data.md)   
 [Uso degli output degli errori in un componente flusso di dati](../../integration-services/extending-packages-custom-objects/data-flow/using-error-outputs-in-a-data-flow-component.md)   
 [Creazione di una trasformazione sincrona con il componente script](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md)   
  
  
