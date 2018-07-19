---
title: Сортировка столбцов | Документация Майкрософт
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.rep.monitor.sortcolumns.f1
ms.assetid: 66b44b6c-10a5-4e3f-a97b-7568609c88ac
caps.latest.revision: 6
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d0610b65013bce66f4ebcb6f446d63ecaf656463
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/02/2018
ms.locfileid: "37234834"
---
# <a name="sort-columns"></a>Сортировка столбцов
  Диалоговое окно **Сортировка столбцов** позволяет сортировать сетки в мониторе репликации по значению одного или нескольких столбцов. (Отсортировать по одному столбцу можно, щелкнув его заголовок в сетке монитора репликации). Например, чтобы отсортировать подписки на вкладке **Все подписки** по состоянию, а затем по типу соединения, выполните следующие действия.  
  
1.  В первой строке сетки выберите **Состояние** в столбце **Имя столбца** и значение в столбце **Порядок сортировки** .  
  
2.  Во второй строке сетки выберите **Тип соединения** в столбце **Имя столбца** и значение в столбце **Порядок сортировки** .  
  
## <a name="options"></a>Параметры  
 **Имя столбца**  
 Имя столбца, по которому нужно выполнить сортировку. Можно выполнить сортировку по одному или нескольким столбцам. Нельзя выполнить сортировку по столбцам **Текущая средняя производительность** и **Худшая производительность в данный момент** на вкладке **Публикации** из-за способа вычисления значений в этих столбцах.  
  
 **Порядок сортировки**  
 Укажите значение **По возрастанию** или **По убыванию**.  
  
 **Очистить все**  
 Удалите все строки из сетки сортировки. Для удаления одной строки выделите строку и нажмите клавишу «DELETE».  
  
## <a name="see-also"></a>См. также  
 [Наблюдение за репликацией](monitoring-replication.md)  
  
  