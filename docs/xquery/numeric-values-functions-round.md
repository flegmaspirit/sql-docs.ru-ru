---
title: "Round-функция (XQuery) | Документы Microsoft"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
dev_langs:
- XML
helpviewer_keywords:
- fn:round function
- round function [XQuery]
ms.assetid: 320b572f-bd5b-4055-95a6-dec5718c0041
caps.latest.revision: 29
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 84815a954021f755173fefd60ef174e7a0acdcf1
ms.contentlocale: ru-ru
ms.lasthandoff: 09/01/2017

---
# <a name="numeric-values-functions---round"></a>Округление числовых значений функций-
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Возвращает ближайшее к аргументу целое значение. Если таких значений несколько, то возвращается набольшее из них. Например:  
  
 Если аргумент равен 2,5, **round()** возвращает 3.  
  
 Если аргумент является 2.4999, **round()** возвращает 2.  
  
 Если аргумент равен -2,5, **round()** возвращает значение -2.  
  
 Если аргумент представляет собой пустую последовательность, **round()** возвращает пустую последовательность.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
fn:round ( $arg as numeric?) as numeric?  
```  
  
## <a name="arguments"></a>Аргументы  
 *$arg*  
 Число, к которому применяется функция.  
  
## <a name="remarks"></a>Замечания  
 Если тип *$arg* является одним из трех базовых числовых типов, **xs: float**, **xs: double**, или **xs: decimal**, тип возвращаемого значения совпадает с *$arg* типа. Если тип *$arg* — тип, который является производным от одного из числовых типов, тип возвращаемого значения будет иметь базовый числовой тип.  
  
 Если входные данные **fn: FLOOR**, **fn: CEILING**, или **fn: Round** функции является **xdt: untypedAtomic**, нетипизированных данных, оно неявно приводится к **xs: double**.  
  
 Использование любого другого типа вызовет статическую ошибку.  
  
## <a name="examples"></a>Примеры  
 В этом разделе приведены примеры запросов XQuery к экземплярам XML, хранящимся в различных **xml** столбцов типа в базе данных AdventureWorks.  
  
 Можно использовать пример в [функция ceiling (XQuery)](../xquery/numeric-values-functions-ceiling.md) для **round()** функции языка XQuery. Все, нужно сделать, — заменить **ceiling()** функции в запрос с **round()** функции.  
  
## <a name="implementation-limitations"></a>Ограничения реализации  
 Существуют следующие ограничения:  
  
-   **Round()** функция сопоставляет целочисленные значения типу xs: decimal.  
  
-   **Round()** функция значений xs: double и xs: float в промежутке от - 0, 5e0 до - 0e0 значение 0e0 вместо - 0e0.  
  
## <a name="see-also"></a>См. также:  
 [FLOOR, функция &#40; XQuery &#41;](../xquery/numeric-values-functions-floor.md)   
 [Функция CEILING &#40; XQuery &#41;](../xquery/numeric-values-functions-ceiling.md)  
  
  