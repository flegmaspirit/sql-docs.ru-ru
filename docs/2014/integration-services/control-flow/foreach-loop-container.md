---
title: Контейнер "Цикл по каждому элементу" | Документы Майкрософт
ms.custom: ''
ms.date: 08/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.foreachloopcontainer.f1
helpviewer_keywords:
- repeating control flow
- Foreach Loop containers
- foreach enumerators [Integration Services]
- containers [Integration Services], Foreach Loop
ms.assetid: dd6cc2ba-631f-4adf-89dc-29ef449c6933
caps.latest.revision: 75
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 47318402206bc0a11ce943d74df8a612acd5f128
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/02/2018
ms.locfileid: "37280430"
---
# <a name="foreach-loop-container"></a>Контейнер «цикл по каждому элементу»
  Контейнер «цикл по каждому элементу» определяет повторяющийся поток управления в пакете. Реализация цикла схожа с циклической структурой **Foreach** в языках программирования. Организация цикла в пакете происходит с помощью перечислителя Foreach.  Контейнер «цикл по каждому элементу» повторяет операции потока управления для каждого члена заданного перечислителя.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] доступны следующие типы перечислителей:  
  
-   Перечислитель ADO по каждой строке для перечисления строк в таблицах. Например, можно получить все строки в наборе записей ADO.  
  
     Recordset destination сохраняет данные в памяти в наборе записей, который хранится в переменной пакета `Object` тип данных. Как правило, используется контейнер «цикл по каждому элементу» с перечислителем ADO по каждой строке для обработки одной строки набора записей за раз. Переменная, указанная для перечислителя ADO по каждой строке, должна иметь тип данных Object. Дополнительные сведения о назначении «Набор записей» см. в разделе [Use a Recordset Destination](../data-flow/recordset-destination.md).  
  
-   Перечислитель набора строк схемы ADO.NET для перечисления сведений схемы об источнике данных. Например, можно перечислить таблицы базы данных [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] и вывести их список.  
  
-   Перечислитель с циклом по каждому файлу для перечисления файлов в папке. Перечислитель может просматривать вложенные папки. Например, можно считать все файлы с расширением *.LOG, находящиеся в папке Windows и всех вложенных в нее папках.  
  
-   Перечислитель по объекту из переменной для перечисления объектов, содержащихся в заданной переменной. Перечисляемым объектом может быть массивом, ADO.NET `DataTable`, [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] перечислителя и т. д. Например, можно перечислить значения массива, в которых содержатся имена серверов.  
  
-   Перечислитель Foreach Item для перечисления элементов коллекций. Например, можно перечислить имена исполняемых объектов и рабочие каталоги, используемые задачей «Выполнение процесса».  
  
-   Перечислитель по набору узлов для перечисления результирующего набора выражения XPath. Например, указанное выражение может перечислить и вывести список всех авторов классического периода: `/authors/author[@period='classical']`.  
  
-   Перечислитель по объектам SMO для перечисления объектов служб [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] SMO. Например, можно перечислить представления в базе данных [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] и вывести их список.  
  
-   Перечислитель по большим двоичным объектам Azure Foreach для перечисления больших двоичных объектов в контейнере больших двоичных объектов в службе хранилища Azure.  
  
-   Перечислитель с циклом по каждому файлу ADLS для перечисления файлов в каталоге ADLS.
  
 На приведенной ниже диаграмме представлен контейнер «цикл по каждому элементу», в котором содержится задача «Файловая система». В цикле «по каждому элементу» используется перечислитель с циклом по каждому файлу, а задача «Файловая система» настроена для копирования файла. В заданной перечислителем папке цикл повторяется четыре раза и копирует четыре файла.  
  
 ![Контейнер цикла Foreach, перечисляющий папку](../media/ssis-foreachloop.gif "Контейнер цикла Foreach, перечисляющий папку")  
  
 Для обновления свойства объекта в пакете, соответствующего значению коллекции перечислителя, можно использовать сочетание переменных и выражений для свойств. Вначале необходимо сопоставить значение коллекции с пользовательской переменной, а затем задать выражение для свойства, которое использует указанную переменную. Например, значение коллекции в перечислителе с циклом по каждому файлу сопоставляется с переменной с именем `MyFile` и переменная затем используется в выражении для свойства Subject задачи "Отправка почты". Во время выполнения пакета свойству Subject присваивается имя файла на каждой итерации цикла. Дополнительные сведения см. в разделе [Использование выражений свойств в пакетах](../expressions/use-property-expressions-in-packages.md).  
  
 Переменные, сопоставленные со значением коллекции в перечислителе, также могут использоваться в выражениях и скриптах.  
  
 Контейнер «цикл по каждому элементу» может включать в себя несколько задач и контейнеров, однако в нем может использоваться только один тип перечислителя. В случае если контейнер «цикл по каждому элементу» включает в себя несколько задач, можно связывать значение коллекции в перечислителе с несколькими свойствами каждой задачи.  
  
 Чтобы определить преобразование для подмножества потока управления пакета, можно задать атрибуты преобразования для контейнера «цикл по каждому элементу». Таким образом, процесс настройки преобразований происходит на уровне контейнера «цикл по каждому элементу», а не на уровне пакета. Например, в случае когда контейнер «цикл по каждому элементу» выполняет поток управления, обновляющий измерения и таблицы фактов в схеме «звезда», можно настроить преобразование таким образом, чтобы каждый раз проводилась проверка обновлений всех таблиц фактов. Дополнительные сведения см. в разделе [Транзакции служб Integration Services](../integration-services-transactions.md).  
  
## <a name="enumerator-types"></a>Типы перечислителей  
 Перечислители являются настраиваемыми. Для настройки необходимо предоставлять различные сведения в зависимости от перечислителя.  
  
 В приведенной ниже таблице перечисляются все типы сведений для разных типов перечислителей.  
  
|Перечислитель|Требования настройки|  
|----------------|--------------------------------|  
|Перечислитель ADO по каждой строке|Задайте исходную переменную для объекта ADO, а также режим перечислителя. Переменная должна иметь тип Object.|  
|Перечислитель по набору строк схемы ADO.NET|Задайте соединение с базой данных, а также перечисляемую схему.|  
|Перечислитель с циклом по каждому файлу|Задайте папку и файлы для перечисления, формат имен полученных файлов, а также укажите, нужно ли просматривать вложенные папки.|  
|Перечислитель по объекту из переменной|Задайте переменную, которая содержит объекты перечисления.|  
|Перечислитель по каждому элементу|Задайте элементы в коллекции перечислителя по каждому элементу, включая столбцы и типы данных в них.|  
|Перечислитель по набору узлов|Задайте источник XML-документа, а также настройте операцию XPath.|  
|Перечислитель по объектам SMO|Задайте соединение с базой данных, а также перечисляемые объекты SMO.|  
|Большой двоичный объект Azure Foreach|Укажите контейнер больших двоичных объектов Azure, который содержит большие двоичные объекты, которые необходимо перечислить.|  
|Файл ADLS по циклу Foreach|Укажите каталог ADLS, который содержит файлы, которые необходимо перечислить, а также некоторые фильтры.|
  
## <a name="property-expressions-in-foreach-loop-containers"></a>Выражения свойств в контейнерах «Цикл по каждому элементу»  
 Пакеты можно настроить на одновременный запуск нескольких исполняемых объектов. Такую конфигурацию следует использовать с осторожностью, если пакет содержит контейнер «цикл по каждому элементу», в котором реализованы выражения свойств.  
  
 Часто в реализации выражения свойства полезно устанавливать значение свойства ConnectionString диспетчера соединений, которое используют перечислители контейнера "цикл по каждому элементу". Выражение свойства ConnectionString устанавливается переменной, которая сопоставляется со значением коллекции перечислителя и обновляется при каждом повторении цикла.  
  
 Пакет необходимо настроить на запуск только одного исполняемого объекта в каждый момент времени. Это позволит избежать негативного влияния неопределенности временных рамок действий, присущей параллельному выполнению задач в цикле. Например, если пакет может одновременно запускать несколько задач, то контейнер «цикл по каждому элементу», который перечисляет файлы в папке, получает имена файлов и затем использует для вставки имен файлов в таблицу задачу «Выполнение SQL», может вызывать конфликт операций записи, если два экземпляра задачи «Выполнение SQL» предпримут попытку записи в одно и то же время. Дополнительные сведения см. в разделе [Использование выражений свойств в пакетах](../expressions/use-property-expressions-in-packages.md).  
  
## <a name="related-tasks"></a>Related Tasks  
 Значения свойств можно задавать с помощью конструктора [!INCLUDE[ssIS](../../../includes/ssis-md.md)] или программными средствами.  
  
 Дополнительные сведения о задании этих свойств в конструкторе служб [!INCLUDE[ssIS](../../../includes/ssis-md.md)] см. в следующих разделах:  
  
-   [Настройка контейнера "цикл по каждому элементу"](foreach-loop-container.md)  
  
-   [Задание свойств задач или контейнеров](../set-the-properties-of-a-task-or-container.md)  
  
 Сведения о задании этих свойств программными средствами см. в следующем разделе:  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.ForEachLoop>  
  
## <a name="related-content"></a>См. также  
 Запись в блоге [Службы SSIS для перечислителя по набору узлов](http://go.microsoft.com/fwlink/?LinkId=220671)на сайте bidn.com.  
  
## <a name="see-also"></a>См. также  
 [Поток управления](control-flow.md)   
 [Контейнеры служб Integration Services](integration-services-containers.md)  
  
  