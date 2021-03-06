---
title: Методы (XMLA) | Документы Microsoft
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 15f930695e13d824e70da748dad20cf574e9bc38
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/04/2018
ms.locfileid: "34579146"
---
# <a name="xml-elements---methods"></a>Элементы XML - методы
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Протокол XML для аналитики (XMLA) используется два метода, **Discover** и **Execute**, которые предлагают стандартный способ для приложений для доступа к данным в экземпляре служб Analysis Services. Поскольку эти методы вызываются при помощи протокола SOAP, они получают входные данные и предоставляют результаты в формате XML. Службы Analysis Services реализует оба метода в соответствии со спецификацией XML для аналитики 1.1.  
  
## <a name="in-this-section"></a>В этом разделе  
 Ниже описываются методы XML для Аналитики, реализованные в службы Analysis Services.  
  
|Метод|Описание|  
|------------|-----------------|  
|[Метод Discover &#40;XML для Аналитики&#41;](../../analysis-services/xmla/xml-elements-methods-discover.md)|Получает сведения, такие как список доступных баз данных или сведений о конкретном объекте от экземпляра служб Analysis Services. Данные, полученные с помощью метода **Discover** , зависят от значений параметров, переданных этому методу.|  
|[Метод Execute &#40;XML для Аналитики&#41;](../../analysis-services/xmla/xml-elements-methods-execute.md)|Отправляет команды XML для Аналитики в экземпляр служб Analysis Services. Сюда входят запросы, связанные с передачей данных, например извлечение или обновление данных на сервере.|  
  
## <a name="see-also"></a>См. также
 [XML-элементы &#40;XML для Аналитики&#41;](http://msdn.microsoft.com/library/40ab2360-efb6-4ba6-bf23-e84964e51008)   
 [Типы данных XML &#40;XML для Аналитики&#41;](../../analysis-services/xmla/xml-data-types/xml-data-types-xmla.md)   
 [XML-элементы &#40;XML для Аналитики&#41;](http://msdn.microsoft.com/library/40ab2360-efb6-4ba6-bf23-e84964e51008)  
  
  
