---
title: Преобразование "Соединение слиянием" | Документы Майкрософт
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.mergejointrans.f1
helpviewer_keywords:
- datasets [Integration Services]
- Merge Join transformation
- datasets [Integration Services], joining
- joining datasets [Integration Services]
- joins [SQL Server], SSIS
ms.assetid: cd8b0412-f83b-4bd2-b227-e53dcfd941a8
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 0620aec0c710e513115455388276c72cc4371e9a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/02/2018
ms.locfileid: "48171046"
---
# <a name="merge-join-transformation"></a>преобразование «Соединение слиянием»
  Преобразование «Соединение слиянием» предоставляет выход, формируемый объединением двух отсортированных наборов данных при помощи соединения FULL, LEFT или INNER. Например, соединение LEFT может использоваться для объединения таблицы, содержащей данные о товарах, с таблицей, в которой перечисляются страны или регионы, в которых эти товары были произведены. Результатом является таблица, в которой перечисляются все товары и страны или регионы их происхождения.  
  
 Настройка преобразования «Соединение слиянием» может производиться следующими способами.  
  
-   Задайте соединение как соединение FULL, LEFT или INNER.  
  
-   Задайте столбцы, которые использует соединение.  
  
-   Укажите, обрабатывает ли преобразование значения NULL как равные другим значениям NULL.  
  
    > [!NOTE]  
    >  Если значения NULL не интерпретируются как равные значения, преобразование обрабатывает значения NULL аналогично тому, как это делает компонент SQL Server Database Engine.  
  
 Это преобразование имеет два входа и один выход. Вывод ошибок не поддерживается.  
  
## <a name="input-requirements"></a>Требования к входным данным  
 Преобразованию «Соединение слиянием» необходимы отсортированные входные данные. Дополнительные сведения об этом важном требовании см. в статье [Сортировка данных для преобразований "Слияние" и "Соединение слиянием"](sort-data-for-the-merge-and-merge-join-transformations.md).  
  
## <a name="join-requirements"></a>Требования к соединению  
 Преобразование «Соединение слиянием» требует, чтобы соединяемые столбцы имели совпадающие метаданные. Например, нельзя соединить столбец, содержащий числовые данные, со столбцом с символьными данными. Если данные представляют собой тип строковых данных, длина столбца при вторичном входе должна быть меньше или равна длине столбца при первичном входе, с которым происходит слияние.  
  
## <a name="buffer-throttling"></a>Регулировка количества буферов  
 Больше не нужно настроить значение `MaxBuffersPerInput` свойство так, как корпорация Майкрософт внесла изменения, которые уменьшили риск, что преобразования «Соединение слиянием» будет потреблять чрезмерный объем памяти. Эта проблема иногда возникает, если несколько входов операции «Соединение слиянием» производят данные с различной скоростью.  
  
## <a name="related-tasks"></a>Связанные задачи  
 Свойства могут устанавливаться через конструктор служб [!INCLUDE[ssIS](../../../includes/ssis-md.md)] или с помощью программных средств.  
  
 Дополнительные сведения об установке свойств этого преобразования см. в следующих разделах:  
  
-   [Расширение набора данных с помощью преобразования "Соединение слиянием"](merge-join-transformation.md)  
  
-   [Установление свойств компонента потока данных](../set-the-properties-of-a-data-flow-component.md)  
  
-   [Сортировка данных для преобразований "Слияние" и "Соединение слиянием"](sort-data-for-the-merge-and-merge-join-transformations.md)  
  
## <a name="see-also"></a>См. также  
 [Редактор преобразования соединения слиянием](../../merge-join-transformation-editor.md)   
 [Преобразование «Слияние»](merge-transformation.md)   
 [UNION All Transformation](union-all-transformation.md)   
 [Преобразования служб Integration Services](integration-services-transformations.md)  
  
  
