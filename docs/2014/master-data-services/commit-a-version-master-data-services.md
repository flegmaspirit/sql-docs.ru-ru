---
title: Фиксация версии (службы Master Data Services) | Документы Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- master-data-services
ms.topic: conceptual
helpviewer_keywords:
- committing versions [Master Data Services]
- versions [Master Data Services], committing
ms.assetid: 6b967a39-b333-4b84-9e5f-4fb07e156826
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 484986c617742967c41160aaf369b3562e72d938
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/02/2018
ms.locfileid: "48085790"
---
# <a name="commit-a-version-master-data-services"></a>Фиксация версии (службы Master Data Services)
  В среде [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]фиксация версии модели препятствует изменениям элементов модели и их атрибутов. Открыть зафиксированную версию нельзя.  
  
## <a name="prerequisites"></a>предварительные требования  
 Для выполнения этой процедуры:  
  
-   необходимо иметь разрешение на доступ к функциональной области **Управление версиями** ;  
  
-   необходимо быть администратором модели. Дополнительные сведения см. в статье [Administrators &#40;Master Data Services&#41;](administrators-master-data-services.md).  
  
-   Версия должна иметь состояние **Заблокирована**. Дополнительные сведения см. в статье [Lock a Version &#40;Master Data Services&#41;](../../2014/master-data-services/lock-a-version-master-data-services.md).  
  
-   Все элементы должны пройти проверку.  
  
### <a name="to-commit-a-version"></a>Фиксация версии  
  
1.  В среде [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]щелкните область **Управление версиями**.  
  
2.  На странице **Управление версиями** в строке меню щелкните **Проверить версию**.  
  
3.  На странице **Проверка версии** выберите модель и версию, которые необходимо зафиксировать.  
  
4.  Нажмите кнопку **Зафиксировать**.  
  
5.  В диалоговом окне подтверждения нажмите кнопку **ОК**.  
  
## <a name="next-steps"></a>Следующие шаги  
  
-   [Создание флага версии &#40;службы Master Data Services&#41;](../../2014/master-data-services/create-a-version-flag-master-data-services.md)  
  
-   [Назначение флага версии &#40;службы Master Data Services&#41;](../../2014/master-data-services/assign-a-flag-to-a-version-master-data-services.md)  
  
-   [Копирование версии &#40;службы Master Data Services&#41;](../../2014/master-data-services/copy-a-version-master-data-services.md)  
  
## <a name="see-also"></a>См. также  
 [Версии &#40;службы Master Data Services&#41;](../../2014/master-data-services/versions-master-data-services.md)  
  
  
