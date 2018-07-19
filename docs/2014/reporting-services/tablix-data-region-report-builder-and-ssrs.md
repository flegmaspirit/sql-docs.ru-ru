---
title: Область данных табликса (построитель отчетов и службы SSRS) | Документы Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 99f83b32-4b86-4d40-973c-9a328d23ac8b
caps.latest.revision: 5
author: maggiesmsft
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 97336e053f4c0a9d2cd36bf381bc16f3fd28d919
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/02/2018
ms.locfileid: "37218664"
---
# <a name="tablix-data-region-report-builder-and-ssrs"></a>Область данных табликса (построитель отчетов и службы SSRS)
  Область данных табликса представляет собой обобщенный элемент макета отчета, в котором данные отчета отображаются в ячейках, упорядоченных в виде столбцов и строк. Данные отчета могут быть как подробными данными в том виде, в котором они были получены из источника данных, так и статистическими подробными данными, организованными в определенные группы. Каждая ячейка табликса может содержать любой элемент отчета, включая текстовое поле, изображение или другую область данных (например, область табликса, диаграмму или датчик). Чтобы добавить в ячейку несколько элементов отчета, сначала необходимо добавить прямоугольник, который будет выполнять роль контейнера. Затем в прямоугольник можно добавить элементы отчета.  
  
 Области данных таблицы, матрицы и списка представляются на ленте шаблонами базовой области данных табликса. При добавлении в отчет одного из этих шаблонов в действительности добавляется область данных табликса, оптимизированная для конкретного макета данных. По умолчанию шаблон таблицы отображает подробные данные в макете сетки, матрица — данные группы в макете сетки, а список — подробные данные в макете свободной формы.  
  
 По умолчанию каждая ячейка табликса в таблице или матрице содержит текстовое поле. Ячейка списка содержит прямоугольник. Элемент отчета по умолчанию можно заменить другим элементом, например изображением.  
  
 После определения групп для таблицы, матрицы или списка построитель отчетов или конструктор отчетов добавляет строки и столбцы в область данных табликса, в которой отображаются сгруппированные данные.  
  
 Для понимания принципов работы с областью данных табликса необходимо понимание следующих моментов.  
  
1.  Различия между подробными и сгруппированными данными.  
  
2.  Группы, которые упорядочены в качестве элементов иерархий групп, находятся на горизонтальной оси в качестве групп строк, а на вертикальной — в качестве групп столбцов.  
  
3.  Назначение ячеек табликса в четырех разделах области данных табликса: тело, заголовки групп строк, заголовки групп столбцов и угол.  
  
4.  Статические и динамические строки, столбцы и их связи с группами.  
  
 С помощью этих основных понятий можно распознать структуру, которую вносит построитель отчетов или конструктор отчетов при добавлении шаблонов и создании групп, и изменить ее в соответствии с потребностями. Чтобы сделать структуру области данных табликса более наглядной, построитель отчетов и конструктор отчетов предоставляют несколько визуальных признаков. Дополнительные сведения см. в разделе [Ячейки, строки и столбцы области данных табликса (построитель отчетов и службы SSRS)](report-design/tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../includes/ssrbrddup-md.md)]  
  
## <a name="understanding-detail-and-grouped-data"></a>Основные сведения о подробных и сгруппированных данных  
 Подробные данные — это все данные из набора данных отчета в том виде, в каком они получены из источника данных. По сути дела, это все, что отображается на панели результатов конструктора запросов при запуске запроса набора данных. Фактически, подробные данные включают созданные вычисляемые поля и ограничиваются фильтрами, определенными для набора данных, области данных и группы сведений. Подробные данные отображаются в строке детализации с помощью простого выражения, например [Quantity]. При запуске отчета строка детализации повторяется один раз для каждой строки результатов запроса во время выполнения.  
  
 Сгруппированные данные — это подробные данные, упорядоченные по значению, заданному в определении группы, например [SalesOrder]. Сгруппированные данные отображаются в строках и столбцах группы с помощью простых выражений, выполняющих агрегатную обработку сгруппированных данных, например [Sum(Quantity)]. Дополнительные сведения см. в разделе [Основные сведения о группах (построитель отчетов и службы SSRS)](report-design/understanding-groups-report-builder-and-ssrs.md).  
  
## <a name="understanding-group-hierarchies"></a>Основные сведения об иерархиях групп  
 Группы упорядочиваются как элементы иерархий групп. Хотя иерархия групп строк и иерархия групп столбцов лежат на разных осях, они представляют собой идентичные структуры. Если представить страницу, то группы строк развертываются вдоль страницы, а группы столбцов — поперек.  
  
 Древовидная структура представляет вложенные группы строк и столбцов, имеющие связь типа «родители-потомки», например категории с подкатегориями. Родительская группа является корневым элементом дерева, а дочерние группы — ветвями. Группы могут также иметь независимую связь с соседними элементами, например продажи по территориям и продажи по годам. Несколько несвязанных древовидных иерархий называются лесом. Группы строк и группы столбцов в области данных табликса по отдельности представляются в виде независимого леса. Дополнительные сведения см. в разделе [Основные сведения о группах (построитель отчетов и службы SSRS)](report-design/understanding-groups-report-builder-and-ssrs.md).  
  
## <a name="understanding-tablix-data-region-areas"></a>Основные сведения о разделах области данных табликса  
 Область данных табликса состоит из четырех областей: угла табликса, иерархии групп строк табликса, иерархии групп столбцов табликса и тела табликса. Тело табликса существует всегда. Другие разделы являются необязательными.  
  
 Ячейки в области тела табликса отображают подробные данные и данные группы.  
  
 Ячейки в разделе «Группы строк» создаются автоматически при создании группы строки. Они представляют собой верхний колонтитул группы строк и отображают значения экземпляра группы строк по умолчанию. Например, при группировании по значению [SalesOrder] значения экземпляров группы являются отдельными заказами на продажу, по которым производится группирование.  
  
 Ячейки в разделе «Группы столбцов» создаются автоматически при создании группы столбцов. Они представляют собой верхний колонтитул группы столбцов и отображают значения экземпляра группы столбцов по умолчанию. Например, при группировании по значению [Year] значения экземпляров группы являются отдельными годами, по которым производится группирование.  
  
 Ячейки в разделе «Угол табликса» создаются автоматически при определении обоих групп строк и столбцов. В этих ячейках могут отображаться метки, либо можно выполнить их слияние и создать заголовок.  
  
 Дополнительные сведения см. в разделе [Области данных табликса &#40;построитель отчетов и службы SSRS&#41;](report-design/tablix-data-region-areas-report-builder-and-ssrs.md).  
  
## <a name="understanding-static-and-dynamic-rows-and-columns"></a>Основные сведения о статических и динамических строках и столбцах  
 В области данных табликса ячейки упорядочены в строки и столбцы, связанные с группами. Структура групп строк идентична структуре групп столбцов. В этом примере используются группы строк, но эти же принципы можно применить к группам столбцов.  
  
 Строка может быть либо статической, либо динамической. Статическая строка не связана с группой. При запуске отчета статическая строка подготавливается к просмотру один раз. Верхние и нижние колонтитулы таблицы являются статическими строками. Статические строки отображают метки и итоговые данные. Ячейки в статической строке относятся к области данных.  
  
 Динамическая строка связана с одной или несколькими группами. Динамическая строка подготавливается к просмотру по одному разу для каждого из уникальных значений группы самой внутренней группы. Ячейки в динамической строке относятся к самой внутренней группе строк и столбцов, которой принадлежит ячейка.  
  
 Динамические строки детализации связаны с группой сведений, которая создается автоматически при добавлении таблицы или списка в область конструктора. По определению группа сведений является самой внутренней группой области данных табликса. Ячейки отображают в строках детализации подробные данные.  
  
 Динамические строки группы создаются при добавлении группы строк или столбцов к существующей области данных табликса. Ячейки в динамических строках группы отображают статистические значения для области по умолчанию.  
  
 Функция «Добавить итог» автоматически создает строку за пределами текущей группы, в которой отображаются значения, относящиеся к группе. Можно также вручную добавлять статические и динамические строки. Визуальные индикаторы помогают определить, какие строки являются статическими, а какие — динамическими. Дополнительные сведения см. в разделе [Ячейки, строки и столбцы области данных табликса (построитель отчетов и службы SSRS)](report-design/tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>См. также  
 [Связывание нескольких областей данных с одним набором данных (построитель отчетов и службы SSRS)](report-design/linking-multiple-data-regions-to-the-same-dataset-report-builder-and-ssrs.md)   
 [Управление отображением области данных табликса на странице отчетов (построитель отчетов и службы SSRS)](report-design/controlling-the-tablix-data-region-display-on-a-report-page.md)   
 [Изучение возможностей области данных табликса (построитель отчетов и службы SSRS)](report-design/exploring-the-flexibility-of-a-tablix-data-region-report-builder-and-ssrs.md)   
 [Таблицы, матрицы и списки (построитель отчетов и службы SSRS)](report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)  
  
  