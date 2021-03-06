---
title: DROP ASSEMBLY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/10/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP ASSEMBLY
- DROP_ASSEMBLY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- removing assemblies
- DROP ASSEMBLY statement
- deleting assemblies
- assemblies [CLR integration], removing
- dropping assemblies
- WITH NO DEPENDENTS option
ms.assetid: 452d181a-a8e6-44a3-975d-29966d01b18d
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: f39ac767cd330bc34db8482210fab21cd29e161e
ms.sourcegitcommit: 50b60ea99551b688caf0aa2d897029b95e5c01f3
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/15/2018
ms.locfileid: "51698869"
---
# <a name="drop-assembly-transact-sql"></a>DROP ASSEMBLY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Rimuove un assembly e tutti i relativi file associati dal database corrente. Gli assembly vengono creati tramite [CREATE ASSEMBLY](../../t-sql/statements/create-assembly-transact-sql.md) e modificati tramite [ALTER ASSEMBLY](../../t-sql/statements/alter-assembly-transact-sql.md).  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
DROP ASSEMBLY [ IF EXISTS ] assembly_name [ ,...n ]  
[ WITH NO DEPENDENTS ]  
[ ; ]  
```  
  
## <a name="arguments"></a>Argomenti  
 *IF EXISTS*  
 **Si applica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (da[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] a [versione corrente](https://go.microsoft.com/fwlink/p/?LinkId=299658)).  
  
 Rimuove in modo condizionale l'assembly solo se esiste già.  
  
 *assembly_name*  
 Nome dell'assembly da eliminare.  
  
 WITH NO DEPENDENTS  
 Se viene specificato questo parametro, viene eliminato solo l'assembly definito tramite *assembly_name* e nessun assembly dipendente a cui l'assembly fa riferimento. Se viene omesso, DROP ASSEMBLY elimina l'assembly definito tramite *assembly_name* e tutti gli assembly dipendenti.  
  
## <a name="remarks"></a>Remarks  
 L'eliminazione di un assembly comporta la rimozione di un assembly e di tutti i relativi file associati, ad esempio file del codice sorgente o di debug, dal database.  
  
 Se WITH NO DEPENDENTS viene omesso, DROP ASSEMBLY elimina l'assembly definito tramite *assembly_name* e tutti gli assembly dipendenti. Se il tentativo di eliminare gli assembly dipendenti ha esito negativo, DROP ASSEMBLY restituisce un errore.  
  
 DROP ASSEMBLY restituisce un errore se all'assembly viene fatto riferimento da un altro assembly esistente nel database oppure se viene utilizzato da funzioni CLR (Common Language Runtime), procedure, trigger, tipi definiti dall'utente o funzioni di aggregazione nel database corrente.  
  
 DROP ASSEMBLY non interferisce con il codice che fa riferimento all'assembly in esecuzione. Tuttavia, dopo l'esecuzione di DROP ASSEMBLY qualsiasi tentativo di richiamare l'assembly avrà esito negativo.  
  
## <a name="permissions"></a>Permissions  
 È necessario essere il proprietario dell'assembly oppure è richiesta l'autorizzazione CONTROL per l'assembly.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente si presuppone che l'assembly `HelloWorld` sia già stato creato nell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
```  
DROP ASSEMBLY Helloworld ;  
```  
  
## <a name="see-also"></a>Vedere anche  
 [CREATE ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/create-assembly-transact-sql.md)   
 [ALTER ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-assembly-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [Recupero di informazioni sugli assembly](../../relational-databases/clr-integration/assemblies-getting-information.md)  
  
  
