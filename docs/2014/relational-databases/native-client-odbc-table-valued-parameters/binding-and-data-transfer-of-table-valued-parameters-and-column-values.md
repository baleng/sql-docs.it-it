---
title: Associazione e trasferimento dati della tabella con valori di parametri e valori di colonna | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (ODBC), binding and data transfer
ms.assetid: 0a2ea462-d613-42b6-870f-c7fa086a6b42
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4ff7549e5a892f6048d6f737382f489dd0bf2ab2
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/02/2018
ms.locfileid: "48131613"
---
# <a name="binding-and-data-transfer-of-table-valued-parameters-and-column-values"></a>Associazione e trasferimento dati di valori di colonna e parametri con valori di tabella
  Analogamente agli altri parametri, i parametri con valori di tabella devono essere associati prima di poter essere passati al server. L'applicazione associa i parametri con valori di tabella esattamente come si esegue l'associazione di altri parametri: usando la funzione SQLBindParameter o chiamate equivalenti a SQLSetDescField o SQLSetDescRec. Il tipo di dati del server per un parametro con valori di tabella è SQL_SS_TABLE. Il tipo C può essere specificato come SQL_C_DEFAULT o SQL_C_BINARY.  
  
 In [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] o versioni successive, sono supportati solo parametri con valori di tabella di input. Qualsiasi tentativo di impostare SQL_DESC_PARAMETER_TYPE su un valore diverso da SQL_PARAM_INPUT restituirà, pertanto, SQL_ERROR con SQLSTATE = HY105 e il messaggio "Tipo di parametro non valido".  
  
 È possibile assegnare valori predefiniti a intere colonne dei parametri con valori di tabella utilizzando l'attributo SQL_CA_SS_COL_HAS_DEFAULT_VALUE. Valori di colonna singola di parametro con valori di tabella, tuttavia, non è possibile assegnare valori predefiniti utilizzando SQL_DEFAULT_PARAM in *StrLen_or_IndPtr* con SQLBindParameter. I parametri con valori di tabella nel suo complesso non possono essere impostati su un valore predefinito utilizzando SQL_DEFAULT_PARAM in *StrLen_or_IndPtr* con SQLBindParameter. Se queste regole non vengono seguite, SQLExecute o SQLExecDirect restituirà SQL_ERROR. Verrà generato un record di diagnostica con SQLSTATE = 07S01 e il messaggio "utilizzo valido del parametro predefinito per il parametro \<p >", dove \<p > è il numero ordinale di TVP nell'istruzione della query.  
  
 Dopo avere associato il parametro con valori di tabella, dovrà essere associata anche ogni colonna del parametro. A tale scopo, l'applicazione chiama innanzitutto SQLSetStmtAttr per impostare SQL_SOPT_SS_PARAM_FOCUS sul numero ordinale di un parametro con valori di tabella. Quindi l'applicazione associa le colonne del parametro con valori di tabella dalle chiamate alle routine seguenti: SQLBindParameter SQLSetDescRec e SQLSetDescField. L'impostazione di SQL_SOPT_SS_PARAM_FOCUS su 0 Ripristina l'effetto tipico di SQLBindParameter SQLSetDescRec e SQLSetDescField in costi operativi sui regolari parametri di livello superiore.  
  
 La ricezione e l'invio di dati effettivi non riguardano il parametro con valori di tabella stesso ma ognuna delle colonne che lo costituiscono. Poiché il parametro con valori di tabella è una pseudo colonna, vengono usati i parametri di SQLBindParameter per fare riferimento ad attributi diversi dagli altri tipi di dati, come indicato di seguito:  
  
|Parametro|Attributo correlato per i tipi di parametro non con valori di tabella, incluse le colonne|Attributo correlato per i parametri con valori di tabella|  
|---------------|--------------------------------------------------------------------------------|----------------------------------------------------|  
|*InputOutputType*|SQL_DESC_PARAMETER_TYPE in IPD.<br /><br /> Per le colonne dei parametri con valori di tabella, deve corrispondere all'impostazione per il parametro con valori di tabella stesso.|SQL_DESC_PARAMETER_TYPE in IPD.<br /><br /> Deve essere SQL_PARAM_INPUT.|  
|*ValueType*|SQL_DESC_TYPE, SQL_DESC_CONCISE_TYPE in APD.|SQL_DESC_TYPE, SQL_DESC_CONCISE_TYPE in APD.<br /><br /> Deve essere SQL_C_DEFAULT o SQL_C_BINARY.|  
|*ParameterType*|SQL_DESC_TYPE, SQL_DESC_CONCISE_TYPE in IPD.|SQL_DESC_TYPE, SQL_DESC_CONCISE_TYPE in IPD.<br /><br /> Deve essere SQL_SS_TABLE.|  
|*ColumnSize*|SQL_DESC_LENGTH o SQL_DESC_PRECISION in IPD.<br /><br /> Ciò dipende dal valore della *ParameterType*.|SQL_DESC_ARRAY_SIZE<br /><br /> Può essere impostato anche utilizzando SQL_ATTR_PARAM_SET_SIZE quando lo stato attivo del parametro è impostato sul parametro con valori di tabella.<br /><br /> Per un parametro con valori di tabella, è il numero di righe nei buffer delle colonne dei parametri con valori di tabella.|  
|*DecimalDigits*|SQL_DESC_PRECISION o SQL_DESC_SCALE in IPD.|Non utilizzato. Deve essere 0.<br /><br /> Se questo parametro è non verrà SQLBindParameter 0, verrà generato restituito SQL_ERROR e un record di diagnostica con SQLSTATE = HY104 e il messaggio "precisione non è valida o la scala".|  
|*ParameterValuePtr*|SQL_DESC_DATA_PTR in APD.|SQL_CA_SS_TYPE_NAME.<br /><br /> Questo parametro è facoltativo per le chiamate di stored procedure ed è possibile specificare NULL se non è richiesto. Deve essere specificato per le istruzioni SQL che non sono chiamate di stored procedure.<br /><br /> Questo parametro serve anche come valore univoco utilizzabile dall'applicazione per identificare il parametro con valori di tabella quando viene utilizzata l'associazione variabile di righe. Per ulteriori informazioni, vedere la sezione "Associazione variabile di righe di parametri con valori di tabella" più avanti n questo argomento.<br /><br /> Quando in una chiamata a SQLBindParameter viene specificato un nome di tipo di parametro con valori di tabella, è necessario specificarlo come valore Unicode, anche nelle applicazioni compilate come applicazioni ANSI. Il valore usato per il parametro *StrLen_or_IndPtr* deve essere SQL_NTS oppure la lunghezza della stringa del nome moltiplicata per sizeof (WCHAR).|  
|*BufferLength*|SQL_DESC_OCTET_LENGTH in APD.|Lunghezza del nome del tipo di parametro con valori di tabella espressa in byte.<br /><br /> Può essere SQL_NTS, se il nome del tipo è con terminazione Null oppure 0 se il nome del tipo di parametro con valori di tabella non è richiesto.|  
|*StrLen_or_IndPtr*|SQL_DESC_OCTET_LENGTH_PTR in APD.|SQL_DESC_OCTET_LENGTH_PTR in APD.<br /><br /> Per i parametri con valori di tabella è un conteggio di righe anziché una lunghezza di dati.|  
  
 Sono supportate due modalità di trasferimento dati per i parametri con valori di tabella: associazione di righe fissa e variabile.  
  
## <a name="fixed-table-valued-parameter-row-binding"></a>Associazione fissa di righe di parametri con valori di tabella  
 Per l'associazione fissa di righe, un'applicazione alloca i buffer (o le matrici di buffer) di dimensioni sufficienti a contenere tutti i possibili valori delle colonne di input. L'applicazione effettua quanto segue:  
  
1.  Associa tutti i parametri utilizzando SQLBindParameter, SQLSetDescRec o SQLSetDescField chiamate.  
  
    1.  Imposta SQL_DESC_ARRAY_SIZE sul numero massimo di righe che possono essere trasferite per ogni parametro con valori di tabella. Questa operazione può essere eseguita nella chiamata di SQLBindParameter.  
  
2.  Chiama la funzione SQLSetStmtAttr per impostare SQL_SOPT_SS_PARAM_FOCUS sul numero ordinale di ogni parametro con valori di tabella.  
  
    1.  Per ogni parametro con valori di tabella, associa le colonne dei parametri con valori di tabella utilizzando SQLBindParameter, SQLSetDescRec o SQLSetDescField chiamate.  
  
    2.  Per ogni colonna di parametri con valori di tabella che deve avere i valori predefiniti, chiama SQLSetDescField per impostare SQL_CA_SS_COL_HAS_DEFAULT_VALUE su 1.  
  
3.  Chiama la funzione SQLSetStmtAttr per impostare SQL_SOPT_SS_PARAM_FOCUS su 0. Questa operazione deve essere eseguita prima SQLExecute o SQLExecDirect viene chiamata. In caso contrario, viene restituito SQL_ERROR e vengono generati un record di dati diagnostici con SQLSTATE=HY024 e il messaggio "Valore attributo non valido, SQL_SOPT_SS_PARAM_FOCUS (deve essere zero in fase di esecuzione)."  
  
4.  Set *StrLen_or_IndPtr* o SQL_DESC_OCTET_LENGTH_PTR su SQL_DEFAULT_PARAM per un parametro con valori di tabella senza righe o il numero di righe da trasferire nella chiamata successiva di SQLExecute o SQLExecDirect se i valori di tabella parametro contiene righe. *StrLen_or_IndPtr* o non può essere impostato SQL_DESC_OCTET_LENGTH_PTR su SQL_NULL_DATA per un parametro con valori di tabella come i parametri con valori di tabella non sono nullable (anche se le colonne che costituiscono parametri con valori di tabella possono essere nullable). Se è impostato su un valore non valido, SQLExecute o SQLExecDirect restituisce SQL_ERROR e viene generato un record di diagnostica con SQLSTATE = SQLSTATE=hy090 e il messaggio "lunghezza di stringa o buffer non valida per il parametro \<p >", dove p è il numero di parametro.  
  
5.  SQLExecute chiamate o SQLExecDirect.  
  
 Immettere i valori di colonna di parametri con valori di tabella possono essere passati in parti se *StrLen_or_IndPtr* è impostato su SQL_LEN_DATA_AT_EXEC (*lunghezza*) o SQL_DATA_AT_EXEC per la colonna. Si tratta di una procedura analoga a quella utilizzata per passare i valori in parti quando vengono utilizzate matrici di parametri. Come con tutti i parametri data-at-execution, SQLParamData indica per quale riga della matrice il driver richiede dati; l'applicazione deve risolvere questo problema. L'applicazione non può prevedere l'ordine con il quale il driver richiederà i valori.  
  
## <a name="variable-table-valued-parameter-row-binding"></a>Associazione variabile di righe di parametri con valori di tabella  
 Per l'associazione variabile di righe, le righe vengono trasferite in batch in fase di esecuzione e l'applicazione passa le righe al driver su richiesta. Si tratta di una procedura simile al data-at-execution per i valori di parametri singoli. Per l'associazione variabile di righe, l'applicazione effettua quanto segue:  
  
1.  Associa i parametri e le colonne di parametri con valori di tabella come descritto nei passaggi da 1 a 3 della sezione precedente, "Associazione fissa di righe di parametri con valori di tabella".  
  
2.  Set *StrLen_or_IndPtr* o SQL_DESC_OCTET_LENGTH_PTR per qualsiasi parametro con valori di tabella che devono essere passati in fase di esecuzione a SQL_DATA_AT_EXEC. Se non sono impostati valori, il parametro verrà elaborato come descritto nella sezione precedente.  
  
3.  SQLExecute chiamate o SQLExecDirect. Verrà restituito SQL_NEED_DATA se sono presenti parametri SQL_PARAM_INPUT o SQL_PARAM_INPUT_OUTPUT da gestire come parametri data-at-execution. In questo caso, l'applicazione effettua quanto segue:  
  
    -   Chiama la funzione SQLParamData. Restituisce il *ParameterValuePtr* valore per un parametro data-at-execution e un codice restituito di SQL_NEED_DATA. Quando tutti i dati dei parametri è stato passato al driver, SQLParamData restituisce SQL_SUCCESS, SQL_SUCCESS_WITH_INFO o SQL_ERROR. Per i parametri data-at-execution *ParameterValuePtr*, che corrisponde al descrittore di campo SQL_DESC_DATA_PTR, può essere considerato come un token per identificare in modo univoco un parametro per il quale è richiesto un valore. Tale "token" viene passato dall'applicazione al driver in fase di associazione, quindi viene passato nuovamente all'applicazione in fase di esecuzione.  
  
4.  Per inviare dati di riga di parametro con valori di tabella per i parametri con valori di tabella null, se il parametro con valori di tabella non è presenti righe, un'applicazione chiama con SQLPutData *StrLen_or_Ind* impostato su SQL_DEFAULT_PARAM.  
  
     Per i TVP non Null, un'applicazione:  
  
    -   Set *Str_Len_or_Ind* per tutte le colonne di parametri con valori di tabella sui valori appropriati e popola i buffer dei dati per le colonne di parametri con valori di tabella che non devono essere parametri data-at-execution. È possibile utilizzare la funzionalità data-at-execution per le colonne di parametri con valori di tabella seguendo procedure analoghe a quelle necessarie per passare in parti i parametri ordinari al driver.  
  
    -   Viene chiamato con SQLPutData *Str_Len_or_Ind* impostato sul numero di righe da inviare al server. I valori esterni all'intervallo compreso tra 0 e SQL_DESC_ARRAY_SIZE o SQL_DEFAULT_PARAM sono un errore e restituiranno SQLSTATE HY090, con il messaggio "Lunghezza di stringa o di buffer non valida". 0 indica che tutte le righe sono state inviate e non sono più disponibili dati per un parametro con valori di tabella (come indicato nel secondo punto elenco). SQL_DEFAULT_PARAM può essere utilizzato solo la prima volta che il driver richiede dati per un parametro con valori di tabella (come descritto nel primo punto elenco).  
  
5.  Quando tutte le righe sono state inviate, chiama SQLPutData per il parametro con valori di tabella con una *Str_Len_or_Ind* pari a 0, quindi procede al passaggio 3a.  
  
6.  Chiama la funzione SQLParamData nuovamente. Se sono presenti parametri data-at-execution tra le colonne di parametri con valori di tabella, questi verranno identificati dal valore *ValuePtrPtr* restituito da SQLParamData. Quando sono disponibili tutti i valori di colonna, SQLParamData restituirà nuovamente il *ParameterValuePtr* valore per il parametro con valori di tabella e l'applicazione viene avviata nuovamente.  
  
## <a name="see-also"></a>Vedere anche  
 [I parametri con valori di tabella &#40;ODBC&#41;](table-valued-parameters-odbc.md)  
  
  
