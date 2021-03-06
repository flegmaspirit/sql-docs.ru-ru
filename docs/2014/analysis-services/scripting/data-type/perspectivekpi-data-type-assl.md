---
title: Тип данных PerspectiveKpi (ASSL) | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- PerspectiveKpi Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- PerspectiveKpi
helpviewer_keywords:
- PerspectiveKpi data type
ms.assetid: e8d19ec8-70d3-4947-904a-fb81fcac9afd
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 72917af7fc4bf24ab9b1e76e70fe6339638336e3
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/02/2018
ms.locfileid: "48076234"
---
# <a name="perspectivekpi-data-type-assl"></a>Тип данных PerspectiveKpi (ASSL)
  Определяет тип-примитив, представляющий сведения о ключевой показатель эффективности (KPI) в [перспективы](../objects/perspective-element-assl.md) элемент.  
  
## <a name="syntax"></a>Синтаксис  
  
```xml  
  
<PerspectiveKpi>  
   <KpiID>...</KpiID>  
   <Annotations>...</Annotations>  
</PerspectiveKpi>  
```  
  
## <a name="data-type-characteristics"></a>Характеристики типа данных  
  
|Характеристика|Описание|  
|--------------------|-----------------|  
|Базовые типы данных|None|  
|Производные типы данных|None|  
  
## <a name="data-type-relationships"></a>Связи типа данных  
  
|Связь|Элемент|  
|------------------|-------------|  
|Родительские элементы|None|  
|Дочерние элементы|[Заметки](../collections/annotations-element-assl.md), [KpiID](../properties/id-element-assl.md)|  
|Производные элементы|[Ключевой показатель эффективности](../objects/kpi-element-assl.md) ([ключевые показатели эффективности](../collections/kpis-element-assl.md) коллекцию [перспективы](../objects/perspective-element-assl.md))|  
  
## <a name="remarks"></a>Примечания  
 Соответствующий элемент в модели объектов объекты управления Analysis AMO — это <xref:Microsoft.AnalysisServices.PerspectiveKpi>.  
  
## <a name="see-also"></a>См. также  
 [Типы данных XML в языке сценариев служб аналитики &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
