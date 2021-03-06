---
title: Функция RunningValue (построитель отчетов и службы SSRS) | Документы Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 6bee2f15-0e69-49c8-9689-b04544063b1d
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: fce2675b361b3b6d4d8ffc46afdabb0b6d128cc7
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/02/2018
ms.locfileid: "48180864"
---
# <a name="runningvalue-function-report-builder-and-ssrs"></a>Функция RunningValue (построитель отчетов и службы SSRS)
  Возвращает текущий агрегат всех числовых значений, отличных от NULL, заданных выражением, вычисляемым для данной области.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
RunningValue(expression, function, scope)  
```  
  
#### <a name="parameters"></a>Параметры  
 *expression*  
 Выражение, к которому применяется статистическая обработка, например `[Quantity]`.  
  
 *function*  
 (`Enum`) Имя агрегатной функции для применения к выражению, например, `Sum`. Эта функция не может быть `RunningValue`, `RowNumber`, или `Aggregate`.  
  
 *область*  
 (`String`) Строковая константа, являющаяся именем набора данных, региона данных или группы или значением null (`Nothing` в [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]), которая определяет контекст, в котором рассчитывается агрегат. `Nothing` Указывает самый внешний контекст, обычно набор данных отчета.  
  
## <a name="return-type"></a>Тип возвращаемых данных  
 Определяется агрегатной функцией, указанной параметром *function* .  
  
## <a name="remarks"></a>Примечания  
 Значение для `RunningValue` сбрасывается в 0 для каждого нового экземпляра области. Если указано группирование, то текущее значение сбрасывается при изменении выражения группы. Если указана область данных, то текущее значение сбрасывается для каждого нового экземпляра области данных. Если указан набор данных, то текущее значение не сбрасывается по всему набору данных.  
  
 Функция `RunningValue` не может быть использована в выражении фильтра или сортировки.  
  
 Набор данных, для которого вычислено текущее значение, должен иметь такой же тип данных. Чтобы преобразовать данные, имеющие разные числовые типы в тот же тип данных, используйте функции преобразования, например `CInt`, `CDbl` или `CDec`. Дополнительные сведения см. в разделе [Функции преобразования типов](http://go.microsoft.com/fwlink/?LinkId=96142).  
  
 Значением*Scope* не может быть выражение.  
  
 *Expression* может содержать вызовы вложенных агрегатных функций со следующими условиями и исключениями.  
  
-   Область для вложенных агрегатов должна совпадать с областью внешнего агрегата или входить в нее. Одна область из всех уникальных областей в выражении должна быть дочерней относительно всех других областей.  
  
-   Область для вложенных агрегатов не может быть именем набора данных.  
  
-   *Выражение* не может содержать `First`, `Last`, `Previous`, или `RunningValue` функции.  
  
-   *Expression* не может содержать вложенные агрегаты, в которых указан параметр *recursive*.  
  
 Для вычисления текущего значения числа строк используйте функцию `RowNumber`. Дополнительные сведения см. в разделе [Функция RowNumber (построитель отчетов и службы SSRS)](report-builder-functions-rownumber-function.md).  
  
 Дополнительные сведения см. в разделах [Справочник по агрегатным функциям (построитель отчетов и службы SSRS)](report-builder-functions-aggregate-functions-reference.md) и [Область выражения для суммирования, агрегатных функций и встроенных коллекций (построитель отчетов и службы SSRS)](expression-scope-for-totals-aggregates-and-built-in-collections.md).  
  
 Дополнительные сведения о рекурсивных агрегатах см. в разделе [Создание групп рекурсивной иерархии (построитель отчетов и службы SSRS)](creating-recursive-hierarchy-groups-report-builder-and-ssrs.md).  
  
## <a name="examples"></a>Примеры  
 Следующий пример кода возвращает текущую сумму поля стоимости `Cost` в самой внешней области данных, которой является набор данных.  
  
```  
=RunningValue(Fields!Cost.Value, Sum, Nothing)  
```  
  
 Следующий пример кода выдает сумму с накоплением поля с названием `Score` в наборе данных с названием `DataSet1`.  
  
```  
=RunningValue(Fields!Score.Value,sum,"DataSet1")  
```  
  
 Следующий пример кода выдает сумму с накоплением поля с названием `Traffic Charges` во внешней области видимости.  
  
```  
=RunningValue(Fields!Traffic Charges.Value, Sum, Nothing)  
```  
  
## <a name="see-also"></a>См. также  
 [Использование выражений в отчетах &#40;построитель отчетов и службы SSRS&#41;](expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Примеры выражений (построитель отчетов и службы SSRS)](expression-examples-report-builder-and-ssrs.md)   
 [Типы данных в выражениях (построитель отчетов и службы SSRS)](expressions-report-builder-and-ssrs.md)   
 [Область выражения для суммирования, агрегатов и встроенных коллекций &#40;построитель отчетов и службы SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
