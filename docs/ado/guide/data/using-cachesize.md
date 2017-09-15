---
title: "С помощью CacheSize | Документы Microsoft"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- locks [ADO], CacheSize property
- CacheSize property [ADO]
ms.assetid: ca1c3422-b6a4-4ba6-af55-54f975b698b1
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 74ec85c5907485edc5ad8dbcb6c24826fc21ccf3
ms.contentlocale: ru-ru
ms.lasthandoff: 09/09/2017

---
# <a name="using-cachesize"></a>С помощью CacheSize
Используйте **CacheSize** свойства, сколько записей следует извлекать за один раз в локальную память от поставщика. Например если **CacheSize** равно 10, после первого открытия **записей** объекта, поставщик возвращает первые 10 записей в локальную память. При перемещении по **записей** объекта, поставщик возвращает данные из буфера локальной памяти. После перемещения за последней записью в кэше, поставщик извлекает следующие 10 записей из источника данных в кэш.  
  
> [!NOTE]
>  **CacheSize** на основе **максимальное число открытых строк** свойства поставщика (в **свойства** коллекцию **записей** объекта). Не удается задать **CacheSize** больше, чем значение **максимальное число открытых строк.** Чтобы изменить число строк, которые можно открыть поставщиком, задайте **максимальное число открытых строк**.  
  
 Значение **CacheSize** может настраиваться в течение жизни **записей** объект, но изменить это значение влияет только на число записей в кэше после последующих получений из источника данных. Изменение значения свойства сама по себе не повлияет на текущее содержимое кэша.  
  
 Если меньше записей для извлечения чем **CacheSize** указывает поставщик возвращает оставшиеся записи и ошибка не возникает.  
  
 Объект **CacheSize** значение 0 не разрешается и возвращает сообщение об ошибке.  
  
 Записей, полученных из кэша не отражают параллельных изменений, внесенных другими пользователями в исходных данных. Чтобы принудительно обновить кэшированные данные, используйте [Resync](../../../ado/reference/ado-api/resync-method.md) метод.  
  
 Если **CacheSize** задано значение больше 1, методы навигации ([переместить](../../../ado/reference/ado-api/move-method-ado.md), [MoveFirst, MoveLast, MoveNext и MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)) может привести к переходу для удаленной запись, если происходит удаление после записи были получены. После первоначальной fetch последующих операций удаления не отразится в кэше данных до попытки получить доступ к значению данных из удаленной строки. Однако задание **CacheSize** 1 устраняет эту проблему, так как удаленные строки не могут быть выбраны.