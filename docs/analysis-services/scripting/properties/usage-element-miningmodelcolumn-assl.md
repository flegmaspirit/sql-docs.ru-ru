---
title: "Элемент Usage (MiningModelColumn) (ASSL) | Документы Microsoft"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Usage Element (MiningModelColumn)
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- Usage
helpviewer_keywords:
- Usage element
ms.assetid: 435a857e-37a9-434e-9de1-354f1ff2993f
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: eb454a49ae0035cedca3a8ef322f5f9d13c7625e
ms.contentlocale: ru-ru
ms.lasthandoff: 09/01/2017

---
# <a name="usage-element-miningmodelcolumn-assl"></a>Элемент Usage (MiningModelColumn) (ASSL)
  Описывает способ связанного столбца в родительском объекте [MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md) используется.  
  
## <a name="syntax"></a>Синтаксис  
  
```xml  
  
<MiningModelColumn>  
   ...  
   <Usage>...</Usage>  
   ...  
</MiningModelColumn>  
```  
  
## <a name="element-characteristics"></a>Характеристики элемента  
  
|Характеристика|Описание|  
|--------------------|-----------------|  
|Тип данных и длина|String (перечисление)|  
|Значение по умолчанию|None|  
|Количество элементов|0—1: необязательный элемент, который может появляться только один раз.|  
  
## <a name="element-relationships"></a>Связи элемента  
  
|Связь|Элемент|  
|------------------|-------------|  
|Родительский элемент|[MiningModelColumn](../../../analysis-services/scripting/data-type/miningmodelcolumn-data-type-assl.md)|  
|Дочерние элементы|None|  
  
## <a name="remarks"></a>Замечания  
 Значением этого элемента может быть только одна из строк в следующей таблице.  
  
|Значение|Description|  
|-----------|-----------------|  
|*Key*|Столбец является ключевым.|  
|*Входные данные*|Столбец является входным.|  
|*Predict*|Столбец является столбцом прогноза.|  
|*PredictOnly*|Столбец является только столбцом прогноза.|  
|*None*|Столбец не используется этой моделью.<br /><br /> **\*\*Предупреждение \* \***  при Usage имеет значение «None», службы Analysis Services не отправляют никакого значения сервера по умолчанию; таким образом, атрибут Usage не включается в запрос или ответ.|  
  
 Перечисление, соответствующее разрешенным значениям для **использование** в модели объектов Analysis Management объекты AMO — <xref:Microsoft.AnalysisServices.MiningModelColumnUsages>.  
  
## <a name="see-also"></a>См. также:  
 [Свойства &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  