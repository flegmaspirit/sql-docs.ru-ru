---
title: Производительность служб SQL Server R - результаты и ресурсы | Документы Microsoft
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: ce5fb99b3808b9da0d32bee48ff31f6e0b2dae95
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/16/2018
ms.locfileid: "31204116"
---
# <a name="performance-for-r-services-results-and-resources"></a>Производительность служб R: результаты и ресурсы
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Эта статья содержит четвертый и последний ряда, описывающий оптимизации производительности для служб R. В этой статье приведена сводка методов, результаты и выводы из двух практические примеры, которые проверены различные методы оптимизации.

Примеры использования двух имели различные задачи:

+ Первый пример внедрения, группа разработчиков служб R, поиск для оценки влияния конкретного пути оптимизации
+ Второй пример использования группой специалист по анализу данных поэкспериментировали с несколько методов, чтобы определить лучшие показатели оптимизации для конкретного сценария оценки большого объема.

В этом разделе перечислены сведения о результатах первый пример внедрения. Для второго примера реализации сводку описывает общую результатов проверки. В конце этого раздела приведены ссылки на все сценарии и образец данных и ресурсы, используемые авторов оригинала.

## <a name="performance-case-study-airline-dataset"></a>Производительность практический пример: авиакомпании набора данных

В данном практическом группа разработчиков SQL Server R Services тестировать влияние различные оптимизации. Была создана модель одного rxLogit и оценки выполняемого авиакомпании набора данных. Оптимизация были применены во время обучения и оценки процессов, чтобы оценить влияние отдельных.

- Github: [образцы данных и сценариев](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/PerfTuning) для изучения оптимизации SQL Server

### <a name="test-methods"></a>Методы теста

1. Набор данных авиакомпании состоит 10 млн строк одной таблицы. Он был загружен и массовой загрузки в SQL Server.
2. Шесть копий таблицы были внесены изменения.
3. Различные изменения были применены к копий таблицы, чтобы проверить компоненты SQL Server, такие как сжатие page, сжатие row, индексирование по столбцам данных хранилища и т. д.
4. Производительность измерялась до и после каждого оптимизации была применена.

| Имя таблицы| Описание|
|------|------|
| *airline* | Данные, преобразованные из исходного XDF-файла с использованием `rxDataStep`.|                          |
| *airlineWithIntCol*   | Параметр *DayOfWeek*, преобразованный в целое число, а не в строку. Эта таблица также добавляет столбец *rowNum*.|
| *airlineWithIndex*    | Здесь содержатся те же данные, что и в таблице *airlineWithIntCol*, но с одним кластеризованным индексом с применением столбца *rowNum*.|
| *airlineWithPageComp* | Здесь содержатся те же данные, что и в таблице *airlineWithIndex*, но с включенным сжатием страниц. Эта таблица также добавляет два столбца, *CRSDepHour* и *Late*, которые вычисляются из параметров *CRSDepTime* и *ArrDelay*. |
| *airlineWithRowComp*  | Здесь содержатся те же данные, что и в таблице *airlineWithIndex*, но с включенным сжатием строк. Эта таблица также добавляет два столбца, *CRSDepHour* и *Late*, которые вычисляются из параметров *CRSDepTime* и *ArrDelay*. |
| *airlineColumnar*     | Хранилище столбцов с одним кластеризованным индексом. Эта таблица заполняется данными из очищенного CSV-файла.|

Каждый тест включал следующие действия:

1. Перед выполнением каждого теста вызывалась сборка мусора R.
2. Модель логистической регрессии был создан на основе данных таблицы. Для параметра *rowsPerRead* каждого теста было задано значение 500 000.
3. Показатели, созданные с помощью обученной модели
4. Каждого теста в шесть раз. Время первого запуска («холодный запуск») был удален. Чтобы предусмотреть случайные выброс **максимальное** времени между оставшиеся пять запусков также был удален. На основе среднего значения продолжительности четырех оставшихся выполнений вычислено среднее значение времени, затраченного на выполнение каждого теста.
5. Были выполнены тесты с помощью *reportProgress* параметр со значением 3 (= временные параметры отчета и ход выполнения). Каждый выходной файл содержит сведения о времени, затраченного на операции ввода-ВЫВОДА, время перехода и время вычисления. Эти значения полезны для устранения неполадок и диагностики.
6. Выходные данные в консоли также был направлен в файл в выходной каталог.
7. Тестовые скрипты обработки значения времени в этих файлах для вычисления среднего времени по запусков.

Например следующие результаты являются время в интервале от одного теста. Нам нужны значения **общего времени чтения** (время ввода-вывода) и **времени перехода** (дополнительное время на настройку процессов для вычисления).

**Временные параметры образца**

```
Running IntCol Test. Using airlineWithIntCol table.
run 1 took 3.66 seconds
run 2 took 3.44 seconds
run 3 took 3.44 seconds
run 4 took 3.44 seconds
run 5 took 3.45 seconds
run 6 took 3.75 seconds
  
Average Time: 3.4425
metric time pct
1 Total time 3.4425 100.00
2 Overall compute time 2.8512 82.82
3 Total read time 2.5378 73.72
4 Transition time 0.5913 17.18
5 Total non IO time 0.3134 9.10
```

Рекомендуется загрузить и изменить скрипты тестов для устранения проблем со службами R Services или функции RevoScaleR.

### <a name="test-results-all"></a>(Все) результаты теста

В этом разделе сравниваются до и после результаты за каждым из тестов.

#### <a name="data-size-with-compression-and-a-columnar-table-store"></a>Размер данных со сжатием и хранилища столбцов таблицы

Первый тест сравнивается использование сжатия данных и один столбец таблицы для уменьшения объема данных.

| Имя таблицы            | Строки     | Зарезервировано   | Данные        | index_size | Не используется  | Процент сохранения (зарезервировано) |
|-----------------------|----------|------------|------------|------------|---------|---------------------|
| *airlineWithIndex*    | 10 000 000 | 2 978 816 КБ | 2 972 160 КБ | 6128 КБ    | 528 КБ  | 0                   |
| *airlineWithPageComp* | 10 000 000 | 625 784 КБ  | 623 744 КБ  | 1352 КБ    | 688 КБ  | 79 %                 |
| *airlineWithRowComp*  | 10 000 000 | 1 262 520 КБ | 1 258 880 КБ | 2552 КБ    | 1088 КБ | 58 %                 |
| *airlineColumnar*     | 9 999 999  | 201 992 КБ  | 201 624 КБ  | н/д        | 368 КБ  | 93 %                 |

**Выводы**

Наибольшее благодаря сокращению объема данных было достигнуто путем применения индекса columnstore, а затем на странице сжатия.

#### <a name="effects-of-compression"></a>Влияние сжатия

Этот тест по сравнению с преимуществами сжатия строк, сжатие страниц и отсутствие сжатия. Обучении модели использовались `rxLinMod` на данные из трех таблиц данных. Для всех таблиц использованы те же формулы и запросы.

| Имя таблицы            | Имя теста       | numTasks | Среднее время |
|-----------------------|-----------------|----------|--------------|
| *airlineWithIndex*    | NoCompression   | 1        | 5,6775       |
|                       | NoCompression - parallel| 4        | 5,1775       |
| *airlineWithPageComp* | PageCompression | 1        | 6,7875       |
|                       | PageCompression - parallel | 4        | 5,3225       |
| *airlineWithRowComp*  | RowCompression  | 1        | 6,1325       |
|                       | RowCompression - parallel  | 4        | 5,2375       |

**Выводы**

Сжатие сама по себе не помогут. В этом примере выполняется увеличение ЦП для обработки сжатия компенсирует уменьшение времени ввода-ВЫВОДА.

Однако при выполнении теста в параллельном режиме (для параметра *numTasks* задано значение 4) значение среднего времени сокращается.

Для более крупных наборов данных влияние сжатия может быть более заметным. Сжатие зависит от набора данных и значений. Поэтому, чтобы определить, как сжатие влияет на ваш набор данных, нужно поэкспериментировать.

### <a name="effect-of-windows-power-plan-options"></a>Влияние варианта схемы управления питанием Windows

В этом эксперименте параметр `rxLinMod` использовался с таблицей *airlineWithIntCol*. Схема управления питанием Windows был задан либо **Сбалансированный** или **высокая производительность**. Для всех тестов для параметра *numTasks* было задано значение 1. Тест был запущен в шесть раз и была выполнена два раза в обоих параметры электропитания для изучения особенностей результатов.

**Высокая производительность** power параметр:

| Имя теста | Выполнить \# | Истекшее время | Среднее время |
|-----------|--------|--------------|--------------|
| IntCol    | 1      | 3,57 с |              |
|           | 2      | 3,45 с |              |
|           | 3      | 3,45 с |              |
|           | 4      | 3,55 с |              |
|           | 5      | 3,55 с |              |
|           | 6      | 3,45 с |              |
|           |        |              | 3.475        |
|           | 1      | 3,45 с |              |
|           | 2      | 3,53 с |              |
|           | 3      | 3,63 с |              |
|           | 4      | 3,49 с |              |
|           | 5      | 3,54 с |              |
|           | 6      | 3,47 с |              |
|           |        |              | 3,5075       |

Вариант **сбалансированного** электропитания:

| Имя теста | Выполнить \# | Истекшее время | Среднее время |
|-----------|--------|--------------|--------------|
| IntCol    | 1      | 3,89 с |              |
|           | 2      | 4,15 с |              |
|           | 3      | 3,77 с |              |
|           | 4      | 5 с    |              |
|           | 5      | 3,92 с |              |
|           | 6      | 3,8 с  |              |
|           |        |              | 3,91         |
|           | 1      | 3,82 с |              |
|           | 2      | 3,84 с |              |
|           | 3      | 3,86 с |              |
|           | 4      | 4,07 с |              |
|           | 5      | 4,86 с |              |
|           | 6      | 3,75 с |              |
|           |        |              | 3,88         |

**Выводы**

Время выполнения более согласованное и быстрее при использовании Windows **высокая производительность** схемы управления питанием.

#### <a name="using-integer-vs-strings-in-formulas"></a>Используя целое число или строки в формулах

Этот тест оценить влияние изменения кода R, чтобы избежать общая проблема с строка факторов. В частности, обучении модели использовались `rxLinMod` с помощью двух таблиц: в первом факторов хранятся в виде строки, во второй таблице факторов хранятся как целые числа.

+ Для *авиакомпании* таблица, столбец [DayOfWeek] содержит строки. _ColInfo_ параметр использовался для определения уровней, коэффициент (понедельник, Вторник,...)

+  Для *airlineWithIndex* таблицы [DayOfWeek] должно быть целым числом. _ColInfo_ не указан.

+ В обоих случаях использовалась одна формула: `ArrDelay ~ CRSDepTime + DayOfWeek`.

| Имя таблицы          | Имя теста   | Среднее время |
|---------------------|-------------|--------------|
| *Авиакомпании*           | *FactorCol* | 10,72        |
| *airlineWithIntCol* | *IntCol*    | 3,4475       |

**Выводы**

Нет явное преимущество при использовании целых чисел, а не строк для факторов.

### <a name="avoiding-transformation-functions"></a>Предотвращение функции преобразования

В этом тесте обучении модели использовались `rxLinMod`, но между двумя выполнениями был изменен код:

+ При первом запуске функцию преобразования был применен как часть построения модели. 
+ Во время выполнения второй значения компонента были предварительно вычисляемые и доступных, чтобы функция преобразования не требовалось.

| Имя теста             | Среднее время |
|-----------------------|--------------|
| WithTransformation    | 5,1675       |
| WithoutTransformation | 4,7          |

**Выводы**

Время на обучение был короче Если **не** с помощью функции преобразования. Другими словами в обучении модели быстрее при использовании столбцов, которые предварительно вычисляются и сохраняются в таблице.

Экономия места должно быть больше, если отсутствуют многие дополнительные преобразования, и были большего набора данных (\> 100 МБ).

### <a name="using-columnar-store"></a>Использование хранилища столбцов

Этот тест оценить производительность преимущества использования хранилища по столбцам данных и индекс. В одном обучении модели с помощью `rxLinMod` и без преобразования данных.

+ При первом запуске таблица данных используется хранилище стандартных строк.
+ Во время выполнения второй использовался хранилища столбцов.

| Имя таблицы         | Имя теста | Среднее время |
|--------------------|-----------|--------------|
| *airlineWithIndex* | RowStore  | 4,67         |
| *airlineColumnar*  | ColStore  | 4,555        |

**Выводы**

Производительность повышается в хранилище столбцов чем с магазином стандартной строки. В более крупных наборов данных могут возникать значительные различия в производительности (\> 100 МБ).

### <a name="effect-of-using-the-cube-parameter"></a>Результат использования параметра куба

Назначение этого теста было определить, является ли в RevoScaleR вариант использования предварительно вычисляемых **куба** может повысить производительность. Обучении модели использовались `rxLinMod`, с помощью этой формулы:

```R
ArrDelay ~ Origin:DayOfWeek + Month + DayofMonth + CRSDepTime
```

В таблице факторов *DayOfWeek* хранится в виде строки.

| Имя теста     | Параметр куба | numTasks | Среднее время | Однострочный прогнозирования (ArrDelay_Pred) |
|---------------|----------------|----------|--------------|---------------------------------|
| CubeArgEffect | `cube = F`     | 1        | 91,0725      | 9,959204                        |
|               |                | 4        | 44,09        | 9,959204                        |
|               | `cube = T`     | 1        | 21,1125      | 9,959204                        |
|               |                | 4        | 8,08         | 9,959204                        |

**Выводы**

Использование аргумента параметр куба четко повышает производительность.

### <a name="effect-of-changing-maxdepth-for-rxdtree-models"></a>Эффект от изменения maxDepth для моделей rxDTree

В этом эксперименте `rxDTree` алгоритмов был использован для создания модели на *airlineColumnar* таблицы. Для этого теста для параметра *numTasks* задано значение 4. Различными значениями для *maxDepth* были использованы, чтобы продемонстрировать, как изменение глубина дерева влияет на время выполнения.

| Имя теста       | maxDepth | Среднее время |
|-----------------|----------|--------------|
| TreeDepthEffect | 1        | 10,1975      |
|                 | 2        | 13,2575      |
|                 | 4        | 19,27        |
|                 | 8        | 45,5775      |
|                 | 16       | 339,54       |

**Выводы**

При увеличении глубины дерева, общее число узлов экспоненциально. Значительно также увеличивается время, прошедшее для создания модели.

### <a name="prediction-on-a-stored-model"></a>Прогноз на хранимые модели

Назначение этого теста было определение воздействие на производительность на оценки при обученная модель сохраняется в таблицу SQL Server, а не создается как часть текущим исполняемым кодом. Для оценки, хранимую модель загружается из базы данных и прогнозы создаются с помощью кадра одной строки данных в памяти (Локальный Контекст вычислений).

Результаты теста показано время сохранения модели и время, необходимое для загрузки модели и прогнозирования.

| Имя таблицы | Имя теста | Среднее время (для обучения модели) | Время сохранения и загрузки модели|
|------------|------------|------------|------------|
| airline    | SaveModel| 21,59| 2,08|
| airline    | LoadModelAndPredict | | 2,09 (со временем для прогнозирования) |

**Выводы**

Загрузка обученной модели из таблицы — это именно более быстрый способ сделать прогноз. Рекомендуется избегать создания модели и выполнении оценки в тот же скрипт.

## <a name="case-study-optimization-for-the-resume-matching-task"></a>Практический пример: оптимизация для соответствия resume задачи

Модель сопоставления resume был разработан специалистами по анализу данных Microsoft Ke Huang для тестирования производительности кода R в SQL Server и выполнив так справки данных, специалистов по анализу создавать масштабируемые, корпоративные решения.

### <a name="methods"></a>Методы

Пакеты MicrosoftML и RevoScaleR, использованных для обучения прогнозной модели в сложные решения R, с большими наборами данных. Запросы SQL и код R были одинаковыми во всех тестов. Тесты проводились на одной виртуальной Машины Azure с установленным сервером SQL Server. Автор затем сравнивается оценки времени с и без следующие оптимизации, предоставляемые SQL Server:

- Таблицы в памяти
- Soft-NUMA
- Регулятор ресурсов

Чтобы оценить влияние на выполнение скрипта R программной архитектуры NUMA, команды обработки и анализа данных тестировать решение на виртуальной машине Azure с 20 физических ядер. На этих физических ядер на четыре программной архитектуры NUMA были созданы автоматически, таким образом, что каждый узел содержит пять ядер.

В случае соответствия resume для оценки влияния на заданий R была применена сопоставить ЦП. Четыре **пулы ресурсов SQL** и четыре **внешних пулов ресурсов** были созданы, чтобы убедиться, что в каждом узле, будет использоваться тот же набор процессоров указан процессоров.

Каждый из пулов ресурсов был назначен различные группы рабочей нагрузки, чтобы оптимизировать использование оборудования. Причина заключается в Soft-NUMA и сходство ЦП невозможно разделить физической памяти в физических узлов NUMA; Таким образом по определению все, основанных на одном физическом узле NUMA узлов NUMA мягкой необходимо использовать память в одном блоке памяти операционной системы. Другими словами является без сходства процессора и памяти.

Процесс был использован для создания такой конфигурации:

1. Сократите объем памяти по умолчанию для SQL Server.

2. Создайте четыре новые пулы для выполнения заданий R в параллельном режиме.

3. Таким образом, что каждая группа рабочей нагрузки связана с пулом ресурсов, создайте четыре группы рабочей нагрузки.

4. Перезапустите регулятора ресурсов с новой группы рабочей нагрузки и назначений.

5. Создайте функцию-классификатор, определяемые пользователем (UDF) для назначения различных задач на группы другой рабочей нагрузки.

6. Обновите конфигурацию регулятора ресурсов для использования функции для группы рабочей нагрузки.

### <a name="results"></a>Результаты

Конфигурации, существовавшей наилучшей производительности при сопоставлении resume изучения имел следующий вид:

-   Четыре внутренние пулы ресурсов (для SQL Server)

-   Четыре внешних пулов ресурсов (для внешних скриптов заданий)

-   Каждый пул ресурсов связан с конкретной группе рабочей нагрузки

-   Назначенный каждого пула ресурсов для разных процессоров

-   Максимальный объем памяти для внутреннего использования (для SQL Server) = 30%

-   Максимальный объем памяти для использования сеансов R = 70%

Для модели сопоставления resume использования внешнего скрипта было активно и возникли другие базы данных под управлением службы ядра СУБД. Таким образом ресурсы, выделенные для внешних скриптов, была увеличена до 70%, которая оказалась оптимальные для производительности сценария.

Эта конфигурация была полученных в процессе экспериментов с разными значениями. Если используется другое оборудование или другого решения оптимальной конфигурации могут быть иными. Всегда экспериментируйте с целью поиска оптимальной конфигурации для вашего случая!

В оптимизированном решении в течение 8,5 секунд на компьютере 20 ядрами рейтинги 1.1 миллионов строк данных (с помощью функций, 100). Оптимизация значительно улучшена производительность с точки зрения времени оценки.

Также рекомендуется результаты **число функций** был значительное влияние на время оценки. Улучшение были более наглядными дополнительные возможности были использованы в модели прогнозирования.

Рекомендуется ознакомиться с этой статье блога и сопутствующие учебника подробное описание.

-   [Оптимизация советы и рекомендации для машинного обучения в SQL Server](https://azure.microsoft.com/blog/optimization-tips-and-tricks-on-azure-sql-server-for-machine-learning-services/)

Многие пользователи заметить, что производится небольшой паузы в первый раз после загрузки среды выполнения R (или Python). По этой причине как описано в этих тестах времени при первом запуске часто определяется но позднее удаляется. Кэширование может привести к производительности важные различия между первой и второй запускает. Также есть некоторые издержки при перемещении данных между SQL Server и внешних среды выполнения, особенно в том случае, если данные, передаваемые по сети, а не загружаемых непосредственно из SQL Server.

По этим причинам нет не одно решение по снижению рисков в настоящее время начальной загрузки как влияние на производительность существенно изменяется в зависимости от задачи. Например кэширование выполняется для одной строки оценки в пакетах; Таким образом последовательных операций оценки выполняется гораздо быстрее и среды выполнения R, ни модели перезагружается. Можно также использовать [оценки собственного](../sql-native-scoring.md) следует избегать загрузки среды выполнения R полностью.

Для больших моделей обучения или оценки в больших пакетов, издержки могут быть минимальные по сравнению с выигрыш без перемещения данных или потоковой передачи и параллельной обработки. См. эти последние блоги и примеры, руководство по производительности:

+ [Кредитов классификацию, использование служб R SQL Server 2016](https://blogs.msdn.microsoft.com/microsoftrservertigerteam/2016/09/27/loan-classification-using-sql-server-2016-r-services/)
+ [Взаимодействий раннее клиентов со службами R Services](https://blogs.msdn.microsoft.com/sqlcat/2016/06/16/early-customer-experiences-with-sql-server-r-services/)
+ [С помощью R обнаружения мошенничества в 1 миллиона транзакций в секунду](http://blog.revolutionanalytics.com/2016/09/fraud-detection.html/)

## <a name="resources"></a>Ресурсы

Ниже приведены ссылки на сведения, инструменты и скрипты, используемые в разработке таких тестов.

+ Тестирование сценариев и ссылки на данные производительности: [образцы данных и скриптов для изучения оптимизации SQL Server](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/PerfTuning)

+ Статья о решения соответствия resume: [советы по оптимизации и рекомендации для SQL Server R Services](https://azure.microsoft.com/blog/optimization-tips-and-tricks-on-azure-sql-server-for-machine-learning-services/)

+ Скрипты, используемые в оптимизации SQL для соответствия resume решения: [репозитории GitHub](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/SQLOptimizationTips)

### <a name="learn-about-windows-server-management"></a>Дополнительные сведения об управлении сервером Windows

+ [Как определить размер файла подкачки для 64-разрядных версий Windows](https://support.microsoft.com/kb/2860880)

+ [Основные сведения о NUMA](https://technet.microsoft.com/library/ms178144.aspx)

+ [Как SQL Server поддерживает архитектуру NUMA](https://technet.microsoft.com/library/ms180954.aspx)

+ [Программная архитектура NUMA](https://docs.microsoft.com/sql/database-engine/configure-windows/soft-numa-sql-server)

### <a name="learn-about-sql-server-optimizations"></a>Дополнительные сведения об оптимизации SQL Server

+ [Реорганизация и перестроение индексов](../../relational-databases\indexes\reorganize-and-rebuild-indexes.md)

+ [Введение в таблицы, оптимизированные для памяти](https://docs.microsoft.com/sql/relational-databases/in-memory-oltp/introduction-to-memory-optimized-tables)

+ [Демонстрация: Улучшение производительности выполняющейся в памяти OLTP](https://docs.microsoft.com/sql/relational-databases/in-memory-oltp/demonstration-performance-improvement-of-in-memory-oltp)

+ [Сжатие данных](../../relational-databases/data-compression/data-compression.md)

+ [Включение сжатия таблицы или индекса](../../relational-databases/data-compression/enable-compression-on-a-table-or-index.md)

+ [Отключение сжатия таблицы или индекса](../../relational-databases/data-compression/disable-compression-on-a-table-or-index.md)

### <a name="learn-about-managing-sql-server"></a>Дополнительные сведения об управлении SQL Server

+ [Наблюдение и настройка производительности](../../relational-databases/performance/monitor-and-tune-for-performance.md)

+ [регулятор ресурсов](../../relational-databases/resource-governor/resource-governor.md)

+ [Знакомство с регулятором ресурсов](https://technet.microsoft.com/library/bb895232.aspx)

+ [Управление ресурсами для служб R](resource-governance-for-r-services.md)

+ [Создание пула ресурсов для R](how-to-create-a-resource-pool-for-r.md)

+ [Пример настройки регулятора ресурсов](https://blog.sqlauthority.com/2012/06/04/sql-server-simple-example-to-configure-resource-governor-introduction-to-resource-governor/)

### <a name="tools"></a>Средства

+ [Генератор загрузки хранилища DISKSPD. Тестовое средство производительности](https://github.com/microsoft/diskspd)

+ [Fsutil](https://technet.microsoft.com/library/cc753059.aspx)


## <a name="other-articles-in-this-series"></a>Другие статьи в этой серии

[Производительность помощник по настройке для R — введение](sql-server-r-services-performance-tuning.md)

[Настройка производительности для R - конфигурации SQL Server](sql-server-configuration-r-services.md)

[Настройка производительности для R - R оптимизации кода и данных](r-and-data-optimization-r-services.md)

[Помощник по настройке производительности - пример использования результатов](performance-case-study-r-services.md)
