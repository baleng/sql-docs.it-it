---
title: Tipo di regole del cast in XQuery | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- XQuery, type casting
- casting rules [XML in SQL Server]
- explicit casting [SQL Server]
- type casting rules [XML in SQL Server]
- cast as operator
- implicit casting
ms.assetid: f2e91306-2b1b-4e1c-b6d8-a34fb9980057
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 6d85f49dcb9ab5bb0e6d5dde114d5c807a5780f5
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/15/2018
ms.locfileid: "51670280"
---
# <a name="type-casting-rules-in-xquery"></a>Regole del cast dei tipi in XQuery
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Nel diagramma seguente, relativo alle specifiche W3C XQuery 1.0 e XPath 2.0 per le funzioni e gli operatori, vengono illustrati i tipi di dati predefiniti, inclusi i tipi primitivi predefiniti e i tipi derivati predefiniti.  
  
 ![Gerarchia dei tipi XQuery 1.0](../xquery/media/xquery-typing-rules.gif "gerarchia dei tipi XQuery 1.0")  
  
 In questo argomento vengono descritte le regole del cast dei tipi applicate per il cast da un tipo all'altro tramite i metodi seguenti:  
  
-   Cast esplicito a scopo, utilizzare **sottoposto a cast come** o le funzioni costruttore del tipo (ad esempio, `xs:integer("5")`).  
  
-   Cast implicito durante la promozione dei tipi  
  
## <a name="explicit-casting"></a>Cast esplicito  
 Nella tabella seguente viene illustrato il cast dei tipi consentito tra i tipi primitivi predefiniti.  
  
 ![Descrive le regole di cast per XQuery. ](../xquery/media/casting-builtin-types.gif "Descrive le regole di cast per XQuery.")  
  
-   Per un tipo primitivo predefinito è possibile eseguire il cast a un altro tipo primitivo predefinito, in base alle regole indicate nella tabella.  
  
-   Per un tipo primitivo è possibile eseguire il cast a qualsiasi tipo derivato da tale tipo primitivo. Ad esempio, è possibile eseguire il cast da **xs: decimal** al **xs: integer**, o da **xs: decimal** al **xs: long**.  
  
-   Per un tipo derivato è possibile eseguire il cast a qualsiasi tipo che rappresenti un predecessore corrispondente nella gerarchia di tipi, fino al relativo tipo di base primitivo predefinito. Ad esempio, è possibile eseguire il cast da **xs: token** al **xs: normalizedString** o a **xs: String**.  
  
-   Per un tipo derivato è possibile eseguire il cast a un tipo primitivo a condizione di poter eseguire il cast del relativo predecessore al tipo di destinazione. Ad esempio, è possibile eseguire il cast **xs: integer**, un derivato a tipo, un **xs: String**primitivo tipo mene **xs: decimal**, **xs: integer**del predecessore primitivo, può essere convertito in **xs: String**.  
  
-   Per un tipo derivato è possibile eseguire il cast a un altro tipo derivato a condizione di poter eseguire il cast del predecessore primitivo del tipo di origine al predecessore primitivo del tipo di destinazione. Ad esempio, è possibile eseguire il cast da **xs: integer** al **xs: token**, in quanto è possibile eseguire il cast da **xs: decimal** al **xs: String**.  
  
-   Le regole per il cast di tipi definiti dall'utente a tipi predefiniti sono le stesse applicate per i tipi predefiniti. Ad esempio, è possibile definire un **myInteger** tipo derivato da **xs: integer** tipo. Quindi **myInteger** può essere eseguito il cast **xs: token**, in quanto **xs: decimal** può essere convertito in **xs: String**.  
  
 Non sono supportati i tipi di cast seguenti:  
  
-   Cast a/da tipi elenco, Questo include, ad esempio i tipi elenco definiti dall'utente e i tipi elenco predefiniti **xs: IDREFS**, **xs: Entities**, e **xs: NMTOKENS**.  
  
-   Esegue il cast da o verso **xs: QName** non è supportato.  
  
-   **xs: NOTATION** e i sottotipi di durata, completamente ordinati **xdt: yearmonthduration** e **xdt: daytimeduration**, non sono supportati. incluso di conseguenza il cast da/a questi tipi.  
  
 Negli esempi seguenti viene illustrato il cast dei tipi esplicito.  
  
### <a name="example-a"></a>Esempio A  
 Nell'esempio seguente viene eseguita una query su una variabile di tipo XML. La query restituisce una sequenza con un valore di tipo semplice tipizzato come xs:string.  
  
```  
declare @x xml  
set @x = '<e>1</e><e>2</e>'  
select @x.query('/e[1] cast as xs:string?')  
go  
```  
  
### <a name="example-b"></a>Esempio B  
 Nell'esempio seguente vengono eseguite query su una variabile XML tipizzata. Innanzitutto, nell'esempio viene creata una raccolta di XML Schema. e quindi viene utilizzata tale raccolta per creare una variabile XML tipizzata. Lo schema include le informazioni di tipizzazione per l'istanza XML assegnata alla variabile. Successivamente, vengono specificate le query sulla variabile.  
  
```  
create xml schema collection myCollection as N'  
<xs:schema xmlns:xs="https://www.w3.org/2001/XMLSchema">  
      <xs:element name="root">  
            <xs:complexType>  
                  <xs:sequence>  
                        <xs:element name="A" type="xs:string"/>  
                        <xs:element name="B" type="xs:string"/>  
                        <xs:element name="C" type="xs:string"/>  
                  </xs:sequence>  
            </xs:complexType>  
      </xs:element>  
</xs:schema>'  
go  
```  
  
 La query seguente restituisce un errore statico, in quanto non si conosce il numero di elementi <`root`> di livello principale inclusi nell'istanza di documento.  
  
```  
declare @x xml(myCollection)  
set @x = '<root><A>1</A><B>2</B><C>3</C></root>  
          <root><A>4</A><B>5</B><C>6</baz></C>'  
select @x.query('/root/A cast as xs:string?')  
go  
```  
  
 Se nell'espressione si specifica un elemento <`root`> singleton, la query ha esito positivo. La query restituisce una sequenza con un valore di tipo semplice tipizzato come xs:string.  
  
```  
declare @x xml(myCollection)  
set @x = '<root><A>1</A><B>2</B><C>3</C></root>  
              <root><A>4</A><B>5</B><C>6</C></root>'  
select @x.query('/root[1]/A cast as xs:string?')  
go  
```  
  
 Nell'esempio seguente, la variabile di tipo XML include una parola chiave del documento che specifica la raccolta di XML Schema. Pertanto, l'istanza XML deve essere un documento che contiene un singolo elemento di livello principale. Se si creano due elementi <`root`> nell'istanza XML, verrà restituito un errore.  
  
```  
declare @x xml(document myCollection)  
set @x = '<root><A>1</A><B>2</B><C>3</C></root>  
              <root><A>4</A><B>5</B><C>6</C></root>'  
go  
```  
  
 Per la corretta esecuzione della query, è possibile modificare l'istanza in modo che includa un unico elemento di livello principale. La query restituisce nuovamente una sequenza con un valore di tipo semplice tipizzato come xs:string.  
  
```  
declare @x xml(document myCollection)  
set @x = '<root><A>1</A><B>2</B><C>3</C></root>'  
select @x.query('/root/A cast as xs:string?')  
go  
```  
  
## <a name="implicit-casting"></a>Cast implicito  
 Il cast implicito è consentito solo per i tipi numeric e per i tipi atomici non tipizzati. Ad esempio, il seguente **min ()** funzione restituisce il numero minimo di due valori:  
  
```  
min(xs:integer("1"), xs:double("1.1"))  
```  
  
 In questo esempio, i due valori passati per la query XQuery **min ()** funzione sono di tipo diverso. Pertanto, viene eseguita la conversione implicita in cui **integer** tipo viene promosso a **double** e due **double** valori vengono confrontati.  
  
 Per la promozione dei tipi descritta in questo esempio vengono applicate le regole seguenti:  
  
-   Un tipo numeric derivato può essere promosso al tipo di base corrispondente. Ad esempio, **integer** può essere promosso al **decimale**.  
  
-   Oggetto **decimale** può essere promosso al **float** e un **float** può essere promosso al **doppie**.  
  
 Poiché il cast implicito è consentito solo per i tipi numeric, non è possibile eseguirlo nei casi seguenti:  
  
-   Non è consentito il cast implicito per i tipi string. Ad esempio, se due **stringa** tipi sono previsti e si passa un **stringa** e un **token**, il cast implicito non viene generato e viene restituito un errore.  
  
-   Non è consentito il cast implicito da tipi numeric a tipi string. Se ad esempio si passa un valore di tipo integer a una funzione che prevede un parametro di tipo string, il cast implicito non viene eseguito e viene restituito un errore.  
  
## <a name="casting-values"></a>Cast di valori  
 Durante il cast da un tipo a un altro, i valori effettivi vengono trasformati dallo spazio dei valori del tipo di origine allo spazio dei valori del tipo di destinazione. Ad esempio, il cast da un tipo xs:decimal a un tipo xs:double trasformerà il valore decimal in valore double.  
  
 Di seguito sono indicate alcune regole di trasformazione.  
  
##### <a name="casting-a-value-from-a-string-or-untypedatomic-type"></a>Cast di un valore da un tipo string o untypedAtomic  
 Il valore di cui viene eseguito il cast a un tipo string o untypedAtomic viene trasformato con le stesse modalità applicate per la convalida del valore in base alle regole del tipo di destinazione, che includono l'eventuale pattern e le regole di elaborazione degli spazi vuoti. Ad esempio, l'operazione seguente avrà esito positivo e genererà il valore double 1.1e0:  
  
 `xs:double("1.1")`  
  
 Nel caso del cast a tipi binari quali xs:base64Binary o xs:hexBinary da un tipo string o untypedAtomic, per i valori di input deve essere utilizzato rispettivamente il formato di codifica base64 o hex.  
  
##### <a name="casting-a-value-to-a-string-or-untypedatomic-type"></a>Cast di un valore a un tipo string o untypedAtomic  
 Il cast a un tipo string o untypedAtomic trasforma il valore nella relativa rappresentazione lessicale canonica XQuery. In particolare, è possibile che un valore conforme a un pattern specifico o a un altro vincolo durante l'input non venga rappresentato in base a tale vincolo.  Per notificare agli utenti, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] contrassegna i tipi in cui il vincolo di tipo può rappresentare un problema, visualizzando un avviso quando tali tipi vengono caricati nella raccolta di schemi.  
  
 Nel cast di un valore di tipo xs:float o xs:double o di uno qualsiasi dei relativi sottotipi a un tipo string o untypedAtomic, il valore viene rappresentato nella notazione scientifica, ma solo se il valore assoluto del valore è minore di 1.0E-6 oppure maggiore o uguale a 1.0E6. Per tale motivo, 0 viene serializzato nella notazione scientifica come 0.0E0.  
  
 Ad esempio `xs:string(1.11e1)` restituirà il valore stringa `"11.1"`, mentre `xs:string(-0.00000000002e0)` restituirà il valore stringa `"-2.0E-11"`.  
  
 Nel cast di tipi binari quali xs:base64Binary o xs:hexBinary a tipo string o untypedAtomic, i valori binari verranno rappresentati rispettivamente nel formato di codifica base64 o hex.  
  
##### <a name="casting-a-value-to-a-numeric-type"></a>Cast di un valore a un tipo numeric  
 Nel cast di un valore di un tipo numeric a un valore di un altro tipo numeric, viene eseguito il mapping del valore da uno spazio dei possibili valori a un altro senza eseguire la serializzazione della stringa. Se il valore non soddisfa il vincolo di un tipo di destinazione, vengono applicate le regole seguenti:  
  
-   Nel caso in cui il valore di origine sia già di tipo numeric e il tipo di destinazione sia xs:float o un relativo sottotipo che consente valori -INF o INF e il cast del valore numeric di origine restituisca un overflow, viene eseguito il mapping tra il valore e INF se il valore è positivo oppure tra il valore e -INF se il valore è negativo. Se il tipo di destinazione non consente INF o -INF e si verifica un overflow, il cast ha esito negativo e il risultato in questa versione di SQL Server è la sequenza vuota.  
  
-   Se il valore di origine è già di tipo numeric, il tipo di destinazione è un tipo numeric che include 0, -0e0 o 0e0 nel relativo intervallo di valori accettati e il cast del valore numeric di origine restituisce un underflow, viene eseguito il mapping del valore nei seguenti modi:  
  
    -   Per un tipo di destinazione decimal, viene eseguito il mapping tra il valore e 0.  
  
    -   Se il valore è un underflow negativo, viene eseguito il mapping tra il valore e -0e0.  
  
    -   Se il valore è un underflow positivo per un tipo di destinazione float o double, viene eseguito il mapping tra il valore e 0e0.  
  
     Se il tipo di destinazione non include zero nel relativo spazio dei valori, il cast ha esito negativo e il risultato è la sequenza vuota.  
  
     Si noti che il cast di un valore a un tipo a virgola mobile binario, ad esempio xs:float, xs:double o uno qualsiasi dei relativi sottotipi, può perdere la precisione.  
  
## <a name="implementation-limitations"></a>Limitazioni di implementazione  
 Limitazioni:  
  
-   Non è supportato il valore a virgola mobile NaN.  
  
-   I valori di cui è possibile eseguire il cast sono limitati dalle restrizioni di implementazione dei tipi di destinazione. Ad esempio, non è possibile convertire una stringa di data con un anno negativo in **xs: date**. Tali cast genereranno la sequenza vuota se il valore è fornito in fase di esecuzione (anziché generare un errore di runtime).  
  
## <a name="see-also"></a>Vedere anche  
 [Definire la serializzazione di dati XML](../relational-databases/xml/define-the-serialization-of-xml-data.md)  
  
  
