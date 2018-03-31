---
title: 'Isscommandwithparameters:: Setparameterproperties (OLE DB) | Documenti Microsoft'
description: ISSCommandWithParameters::SetParameterProperties (OLE DB)
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-interfaces
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- ISSCommandWithParameters::SetParameterProperties (OLE DB)
apitype: COM
helpviewer_keywords:
- SetParameterProperties method
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a6dee4ef79b1cb8972ebe929bd087fc67f6b72fa
ms.sourcegitcommit: 9f4330a4b067deea396b8567747a6771f35e6eee
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2018
---
# <a name="isscommandwithparameterssetparameterproperties-ole-db"></a>ISSCommandWithParameters::SetParameterProperties (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Imposta le proprietà dei parametri per i singoli parametri in base al numero ordinale oppure imposta proprietà dei parametri bulk specificando una matrice di strutture SSPARAMPROPS.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
HRESULT SetParameterProperties(  
      DB_UPARAMS cParams,   
      SSPARAMPROPS rgParamProperties[]);  
```  
  
## <a name="arguments"></a>Argomenti  
 *cParams*[in]  
 Il numero di SSPARAMPROPS strutture nel *rgParamProperties* matrice. Se questo numero è zero, **isscommandwithparameters:: Setparameterproperties** eliminerà tutte le proprietà che avrebbero potuto essere specificate per tutti i parametri nel comando.  
  
 *rgParamProperties*[in]  
 Matrice di strutture SSPARAMPROPS da impostare.  
  
## <a name="return-code-values"></a>Valori restituiti  
 Il **isscommandwithparameters:: Setparameterproperties** metodo restituisce gli stessi codici di errore OLE DB principale **ICommandProperties:: SetProperties** metodo.  
  
## <a name="remarks"></a>Osservazioni  
 Impostazione delle proprietà di parametro con questo metodo è consentita in base al parametro ordinale oppure con un singolo **isscommandwithparameters:: Setparameterproperties** chiamare una volta la struttura SSPARAMPROPS è stata compilata dalla matrice di proprietà.  
  
 Il **SetParameterInfo** metodo deve essere chiamato prima di chiamare il **isscommandwithparameters:: Setparameterproperties** metodo. Se si chiama `SetParameterProperties(0, NULL)`, si cancellano tutte le proprietà di parametro specificate, mentre se si chiama `SetParameterInfo(0,NULL,NULL)`, si cancellano tutte le informazioni di parametro che includono le proprietà che potrebbero essere associate a un parametro.  
  
 La chiamata **isscommandwithparameters:: Setparameterproperties** per specificare le proprietà per un parametro che non è di tipo DBTYPE_XML o DBTYPE_UDT restituisce DB_E_ERRORSOCCURRED o DB_S_ERRORSOCCURRED e viene contrassegnato il  *dwStatus* campo di tutte le proprietà DBPROP contenute nella struttura SSPARAMPROPS per quel parametro con DBPROPSTATUS_NOTSET. È necessario attraversare la matrice DBPROP di ogni proprietà DBPROPSET contenuta nella struttura SSPARAMPROPS per individuare il parametro al quale DB_E_ERRORSOCCURRED o DB_S_ERRORSOCCURRED fa riferimento.  
  
 Se **isscommandwithparameters:: Setparameterproperties** viene chiamata per specificare le proprietà dei parametri cui informazioni non sono state impostate ancora con **SetParameterInfo**, il provider restituisce e _ PREVISTO con il messaggio di errore seguente:  
  
 Impossibile chiamare il metodo SetParameterProperties per i parametri specificati senza chiamare prima il metodo SetParameterInfo. È necessario impostare le informazioni sui parametri prima di impostare le proprietà dei parametri stessi.  
  
 Se la chiamata a **isscommandwithparameters:: Setparameterproperties** contiene alcuni parametri in cui le informazioni di parametro sono stato impostato e alcuni parametri in cui le informazioni di parametro non sono stata impostata, le proprietà dwStatus nel DBPROPSET del set di proprietà SSPARAMPROPS verranno restituite con DBSTATUS_NOTSET.  
  
 La struttura SSPARAMPROPS viene definita nel modo seguente:  
  
 `struct SSPARAMPROPS {`  
  
 `DBORDINAL iOrdinal;`  
  
 `ULONG cPropertySets;`  
  
 `DBPROPSET *rgPropertySets;`  
  
 `};`  
  
 Miglioramenti nel motore di database a partire da [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] consentire isscommandwithparameters:: Setparameterproperties ottenere descrizioni più accurate dei risultati previsti. Questi risultati più accurati differiscano dai valori restituiti da isscommandwithparameters:: Setparameterproperties nelle versioni precedenti di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Per ulteriori informazioni, vedere [Metadata Discovery](../../oledb/features/metadata-discovery.md).  
  
|Membro|Descrizione|  
|------------|-----------------|  
|*iOrdinal*|Numero ordinale del parametro passato.|  
|*cPropertySets*|Il numero di strutture DBPROPSET in *rgPropertySets*.|  
|*rgPropertySets*|Puntatore alla memoria nel quale restituire una matrice di strutture DBPROPSET.|  
  
## <a name="see-also"></a>Vedere anche  
 [OLE DB ISSCommandWithParameters &#40; &#41;](../../oledb/ole-db-interfaces/isscommandwithparameters-ole-db.md)  
  
  