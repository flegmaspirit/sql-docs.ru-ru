---
title: Элемент DataSourceType (XML для Аналитики) | Документы Microsoft
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 015a4cfbb70ddb29216a079dffdfd928029033d3
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/04/2018
ms.locfileid: "34575676"
---
# <a name="datasourcetype-element-xmla"></a>Элемент DataSourceType (XML для аналитики)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Указывает ли [расположение](../../../analysis-services/xmla/xml-elements-properties/location-element-xmla.md) элемент, указанный для [восстановить](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md) или [Synchronize](../../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md) команда является локальным или удаленным.  
  
## <a name="syntax"></a>Синтаксис  
  
```xml  
  
<Location>  
   ...  
   <DataSourceType>...</DataSourceType>  
   ...  
</Location>  
```  
  
## <a name="element-characteristics"></a>Характеристики элемента  
  
|Характеристика|Описание|  
|--------------------|-----------------|  
|Тип данных и длина|String (перечисление)|  
|Значение по умолчанию|*удаленный*|  
|Количество элементов|0-1: необязательный элемент, который может встречаться только один раз.|  
  
## <a name="element-relationships"></a>Связи элемента  
  
|Связь|Элемент|  
|------------------|-------------|  
|Родительские элементы|[Расположение](../../../analysis-services/xmla/xml-elements-properties/location-element-xmla.md)|  
|Дочерние элементы|None|  
  
## <a name="remarks"></a>Примечания  
 Элемент **DataSourceType** определяет, содержит ли элемент **Location** локальный или удаленный источник данных. Дополнительные сведения о резервном копировании и восстановлении удаленных секций см. в разделе [резервное копирование, восстановление и синхронизация баз данных &#40;XMLA&#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md).  
  
 Значением этого элемента может быть только одна из строк в следующей таблице.  
  
|Значение|Описание|  
|-----------|-----------------|  
|*Локальные*|Элемент **Location** определяет локальный источник данных. При использовании этого значения команды **Restore** и **Synchronize** используют определенные в элементе **Location** сведения для обновления источника данных, полученного или из файлов резервной копии, заданной в элементе **File** для команды **Backup** , или из базы данных, заданной в элементе **Source** для команды **Synchronize** . Источник данных определяется элементом **DataSourceID** элемента **Location** .<br /><br /> Это значение позволяет объектам, пользующимся реляционным хранилищем OLAP (ROLAP), после восстановления или синхронизации использовать другую базу данных для хранения данных и метаданных.<br /><br /> Примечание: Данные ROLAP, например данных в таблицах измерения или таблицах обратной записи, не восстанавливаются и синхронизируются. Восстанавливаются и синхронизируются только метаданные объектов ROLAP.|  
|*удаленный*|Элемент **Location** определяет удаленный источник данных. При использовании этого значения команды **Restore** и **Synchronize** используют определенные в элементе **Location** сведения для восстановления или синхронизации в удаленном экземпляре, определенном элементом **File** элемента **Backup** , удаленных секций, полученных или из файлов резервной копии, заданной в элементе **Source** для команды **Synchronize** , или из базы данных, заданной в элементе **DataSourceID** для команды **Location** .|  
  
## <a name="see-also"></a>См. также
 [Элемент ConnectionString &#40;XML для Аналитики&#41;](../../../analysis-services/xmla/xml-elements-properties/connectionstring-element-xmla.md)   
 [Элемент DataSourceID &#40;XML для Аналитики&#41;](../../../analysis-services/xmla/xml-elements-properties/datasourceid-element-xmla.md)   
 [Свойства &#40;XML для Аналитики&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
