---
title: Столбцы данных отчетов о состоянии | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Progress Reports event category
ms.assetid: d34a6322-e26b-4454-b98f-32307d6956b5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8569f18f3838116ea5a1ed045f418602f85032c6
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/02/2018
ms.locfileid: "48171174"
---
# <a name="progress-reports-data-columns"></a>Столбцы данных отчетов о состоянии
  Категория событий «Отчеты о состоянии» имеет следующие классы событий:  
  
|**Идентификатор события**|**Имя события**|**Описание события**|  
|------------------|--------------------|---------------------------|  
|5|Начало отчета о состоянии|Начало отчета о состоянии|  
|6|Окончание отчета о состоянии|Окончание отчета о состоянии|  
|7|Текущий отчет о состоянии|Текущий отчет о состоянии|  
|8|Ошибка отчета о состоянии|Ошибка отчета о состоянии|  
  
 В следующих таблицах перечисляются столбцы данных для каждого из этих классов событий.  
  
## <a name="progress-report-begindata-columns"></a>Начало отчета о состоянии — столбцы данных  
  
|**Имя столбца**|**Идентификатор столбца**|**Тип столбца**|**Описание столбца**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|Класс событий используется для категоризации событий.|  
|EventSubclass|1|1|Подкласс событий предоставляет дополнительные сведения о каждом классе событий:<br /><br /> 1: процесс<br /><br /> 2: слияние<br /><br /> 3: удаление<br /><br /> 4: DeleteOldAggregations<br /><br /> 5: перестроить<br /><br /> 6: фиксация<br /><br /> 7: отката<br /><br /> 8: CreateIndexes<br /><br /> 9: CreateTable<br /><br /> 10: InsertInto<br /><br /> 11: транзакции<br /><br /> 12: инициализация<br /><br /> 13: дискретизации<br /><br /> 14: запрос<br /><br /> 15: создать представление<br /><br /> 16: запись данных<br /><br /> 17: ReadData<br /><br /> 18: GroupData<br /><br /> 19: GroupDataRecord<br /><br /> 20: BuildIndex<br /><br /> 21: aggregate<br /><br /> 22: BuildDecode<br /><br /> 23: WriteDecode<br /><br /> 24: BuildDMDecode<br /><br /> 25: ExecuteSQL<br /><br /> 26: ExecuteModifiedSQL<br /><br /> 27: подключение<br /><br /> 28: BuildAggsAndIndexes<br /><br /> 29: MergeAggsOnDisk<br /><br /> 30: BuildIndexForRigidAggs<br /><br /> 31: BuildIndexForFlexibleAggs<br /><br /> 32: WriteAggsAndIndexes<br /><br /> 33: WriteSegment<br /><br /> 34: DataMiningProgress<br /><br /> 35: ReadBufferFullReport<br /><br /> 36: ProactiveCacheConversion<br /><br /> 37: резервное копирование<br /><br /> 38: восстановление<br /><br /> 39: синхронизация<br /><br /> 40: создать расписание обработки<br /><br /> 41: отсоединение<br /><br /> 42: присоединение<br /><br /> 43: анализ\кодирование данных<br /><br /> 44: сжатие сегмента<br /><br /> 45: столбец таблицы записи<br /><br /> 46: Подготовка построения отношений<br /><br /> 47: построить сегмент отношений<br /><br /> 48: нагрузки<br /><br /> 49: загрузка метаданных<br /><br /> 50: загрузка данных<br /><br /> 51: Заключительная загрузка<br /><br /> 52: обход метаданных во время резервного копирования<br /><br /> 53: VertiPaq<br /><br /> 54: обработка иерархии<br /><br /> 55: переключение словаря|  
|CurrentTime|2|5|Содержит текущее время события из отчета, если доступно. Ожидаемые форматы фильтрации: «ГГГГ-ММ-ДД» и «ГГГГ-ММ-ДД ЧЧ:ММ:СС».|  
|StartTime|3|5|Содержит время начала события, если оно доступно. Ожидаемые форматы фильтрации: «ГГГГ-ММ-ДД» и «ГГГГ-ММ-ДД ЧЧ:ММ:СС».|  
|JobID|7|1|Содержит идентификатор задания, связанного с событием из отчета.|  
|SessionType|8|8|Содержит тип сеанса (сущность, вызывающую событие), связанного с событием из отчета. Доступные значения событий обработки:<br /><br /> 1 = пользователь<br /><br /> 2 = упреждающее кэширование<br /><br /> 3 = отложенная обработка|  
|ObjectID|11|8|Содержит идентификатор объекта (строку), связанного с событием из отчета.|  
|ObjectType|12|1|Содержит тип объекта.|  
|ObjectName|13|8|Содержит имя объекта, связанного с событием из отчета.|  
|ObjectPath|14|8|Содержит путь к объекту, связанному с событием из отчета, в виде списка родительских элементов с разделителями-запятыми, начинающегося с родительских элементов объекта.|  
|ObjectReference|15|8|Содержит ссылку на объект для события из отчета, созданную в виде XML-кода по всем родительским элементам и использующую теги для описания объекта.|  
|ConnectionID|25|1|Содержит уникальный идентификатор соединения, связанного с событием из отчета.|  
|DatabaseName|28|8|Содержит имя базы данных, в которой произошло событие из отчета.|  
|NTUserName|32|8|Содержит учетную запись пользователя Windows, связанную с событием из отчета.|  
|NTDomainName|33|8|Содержит учетную запись домена Windows, связанную с событием из отчета.|  
|SessionID|39|8|Содержит идентификатор сеанса, связанного с событием из отчета.|  
|NTCanonicalUserName|40|8|Имя пользователя в канонической форме. Например, engineering.microsoft.com/software/someone.|  
|SPID|41|1|Содержит идентификатор серверного процесса (SPID), уникально идентифицирующий пользовательский сеанс, связанный с событием из отчета. Идентификатор SPID напрямую соответствует идентификатору GUID сеанса, используемому XML для аналитики (XMLA).|  
|TextData|42|9|Содержит текстовые данные, связанные с событием из отчета.|  
|ServerName|43|8|Содержит имя экземпляра служб [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , на котором произошло событие из отчета.|  
  
## <a name="progress-report-enddata-columns"></a>Окончание отчета о состоянии — Столбцы данных  
  
|**Имя столбца**|**Идентификатор столбца**|**Тип столбца**|**Описание столбца**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|Класс событий используется для категоризации событий.|  
|EventSubclass|1|1|Подкласс событий предоставляет дополнительные сведения о каждом классе событий:<br /><br /> 1: процесс<br /><br /> 2: слияние<br /><br /> 3: удаление<br /><br /> 4: DeleteOldAggregations<br /><br /> 5: перестроить<br /><br /> 6: фиксация<br /><br /> 7: отката<br /><br /> 8: CreateIndexes<br /><br /> 9: CreateTable<br /><br /> 10: InsertInto<br /><br /> 11: транзакции<br /><br /> 12: инициализация<br /><br /> 13: дискретизации<br /><br /> 14: запрос<br /><br /> 15: создать представление<br /><br /> 16: запись данных<br /><br /> 17: ReadData<br /><br /> 18: GroupData<br /><br /> 19: GroupDataRecord<br /><br /> 20: BuildIndex<br /><br /> 21: aggregate<br /><br /> 22: BuildDecode<br /><br /> 23: WriteDecode<br /><br /> 24: BuildDMDecode<br /><br /> 25: ExecuteSQL<br /><br /> 26: ExecuteModifiedSQL<br /><br /> 27: подключение<br /><br /> 28: BuildAggsAndIndexes<br /><br /> 29: MergeAggsOnDisk<br /><br /> 30: BuildIndexForRigidAggs<br /><br /> 31: BuildIndexForFlexibleAggs<br /><br /> 32: WriteAggsAndIndexes<br /><br /> 33: WriteSegment<br /><br /> 34: DataMiningProgress<br /><br /> 35: ReadBufferFullReport<br /><br /> 36: ProactiveCacheConversion<br /><br /> 37: резервное копирование<br /><br /> 38: восстановление<br /><br /> 39: синхронизация<br /><br /> 40: создать расписание обработки<br /><br /> 41: отсоединение<br /><br /> 42: присоединение<br /><br /> 43: анализ\кодирование данных<br /><br /> 44: сжатие сегмента<br /><br /> 45: столбец таблицы записи<br /><br /> 46: Подготовка построения отношений<br /><br /> 47: построить сегмент отношений<br /><br /> 48: нагрузки<br /><br /> 49: загрузка метаданных<br /><br /> 50: загрузка данных<br /><br /> 51: Заключительная загрузка<br /><br /> 52: обход метаданных во время резервного копирования<br /><br /> 53: VertiPaq<br /><br /> 54: обработка иерархии<br /><br /> 55: переключение словаря|  
|CurrentTime|2|5|Содержит текущее время события из отчета, если доступно. Ожидаемые форматы фильтрации: «ГГГГ-ММ-ДД» и «ГГГГ-ММ-ДД ЧЧ:ММ:СС».|  
|StartTime|3|5|Содержит время начала события, если оно доступно. Ожидаемые форматы фильтрации: «ГГГГ-ММ-ДД» и «ГГГГ-ММ-ДД ЧЧ:ММ:СС».|  
|EndTime|4|5|Содержит время окончания события. Этот столбец не заполняется для таких классов событий запуска, как SQL:BatchStarting или SP:Starting. Ожидаемые форматы фильтрации: «ГГГГ-ММ-ДД» и «ГГГГ-ММ-ДД ЧЧ:ММ:СС».|  
|Duration|5|2|Содержит общую длительность события в миллисекундах.|  
|CPUTime|6|2|Содержит время ЦП в миллисекундах, использованного событием.|  
|JobID|7|1|Содержит идентификатор задания, связанного с событием из отчета.|  
|SessionType|8|8|Содержит тип сеанса (сущность, вызывающую событие), связанного с событием из отчета. Доступные значения событий обработки:<br /><br /> 1 = пользователь<br /><br /> 2 = упреждающее кэширование<br /><br /> 3 = отложенная обработка|  
|ProgressTotal|9|1|Содержит общий процент выполнения события из отчета.|  
|IntegerData|10|1|Содержит целочисленные данные, связанные с событием из отчета, например текущий показатель числа обработанных строк для события обработки.|  
|ObjectID|11|8|Содержит идентификатор объекта (строку), связанного с событием из отчета.|  
|ObjectType|12|1|Содержит тип объекта.|  
|ObjectName|13|8|Содержит имя объекта, связанного с событием из отчета.|  
|ObjectPath|14|8|Содержит путь к объекту, связанному с событием из отчета, в виде списка родительских элементов с разделителями-запятыми, начинающегося с родительских элементов объекта.|  
|ObjectReference|15|8|Содержит ссылку на объект для события из отчета, созданную в виде XML-кода по всем родительским элементам и использующую теги для описания объекта.|  
|Severity|22|1|Содержит степень серьезности исключения, связанного с событием из отчета. Возможны следующие значения.<br /><br /> 0 = успешное завершение<br /><br /> 1 = информационное сообщение<br /><br /> 2 = предупреждение<br /><br /> 3 = ошибка|  
|Успешно |23|1|Содержит сведения об удачной или неудачной отправке серверного события из отчета. Возможны следующие значения.<br /><br /> 0 = неуспешное завершение;<br /><br /> 1 = успешное завершение.|  
|Ошибка|24|1|Содержит номер ошибки для данного события.|  
|ConnectionID|25|1|Содержит уникальный идентификатор соединения, связанного с событием из отчета.|  
|DatabaseName|28|8|Содержит имя базы данных, в которой произошло событие из отчета.|  
|NTUserName|32|8|Содержит учетную запись пользователя Windows, связанную с событием из отчета.|  
|NTDomainName|33|8|Содержит учетную запись домена Windows, связанную с событием из отчета.|  
|SessionID|39|8|Содержит идентификатор сеанса, связанного с событием из отчета.|  
|NTCanonicalUserName|40|8|Содержит имя пользователя Windows, связанного с событием из отчета. Имя пользователя указано в канонической форме. Например, engineering.microsoft.com/software/user.|  
|SPID|41|1|Содержит идентификатор серверного процесса (SPID), уникально идентифицирующий пользовательский сеанс, связанный с событием из отчета. Идентификатор SPID напрямую соответствует идентификатору GUID сеанса, используемому XML для аналитики (XMLA).|  
|TextData|42|9|Содержит текстовые данные, связанные с событием из отчета.|  
|ServerName|43|8|Содержит имя экземпляра служб [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , на котором произошло событие из отчета.|  
  
## <a name="progress-report-currentdata-columns"></a>Текущий отчет о состоянии — Столбцы данных  
  
|**Имя столбца**|**Идентификатор столбца**|**Тип столбца**|**Описание столбца**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|Класс событий используется для категоризации событий.|  
|EventSubclass|1|1|Подкласс событий предоставляет дополнительные сведения о каждом классе событий:<br /><br /> 1: процесс<br /><br /> 2: слияние<br /><br /> 3: удаление<br /><br /> 4: DeleteOldAggregations<br /><br /> 5: перестроить<br /><br /> 6: фиксация<br /><br /> 7: отката<br /><br /> 8: CreateIndexes<br /><br /> 9: CreateTable<br /><br /> 10: InsertInto<br /><br /> 11: транзакции<br /><br /> 12: инициализация<br /><br /> 13: дискретизации<br /><br /> 14: запрос<br /><br /> 15: создать представление<br /><br /> 16: запись данных<br /><br /> 17: ReadData<br /><br /> 18: GroupData<br /><br /> 19: GroupDataRecord<br /><br /> 20: BuildIndex<br /><br /> 21: aggregate<br /><br /> 22: BuildDecode<br /><br /> 23: WriteDecode<br /><br /> 24: BuildDMDecode<br /><br /> 25: ExecuteSQL<br /><br /> 26: ExecuteModifiedSQL<br /><br /> 27: подключение<br /><br /> 28: BuildAggsAndIndexes<br /><br /> 29: MergeAggsOnDisk<br /><br /> 30: BuildIndexForRigidAggs<br /><br /> 31: BuildIndexForFlexibleAggs<br /><br /> 32: WriteAggsAndIndexes<br /><br /> 33: WriteSegment<br /><br /> 34: DataMiningProgress<br /><br /> 35: ReadBufferFullReport<br /><br /> 36: ProactiveCacheConversion<br /><br /> 37: резервное копирование<br /><br /> 38: восстановление<br /><br /> 39: синхронизация<br /><br /> 40: создать расписание обработки<br /><br /> 41: отсоединение<br /><br /> 42: присоединение<br /><br /> 43: анализ\кодирование данных<br /><br /> 44: сжатие сегмента<br /><br /> 45: столбец таблицы записи<br /><br /> 46: Подготовка построения отношений<br /><br /> 47: построить сегмент отношений<br /><br /> 48: нагрузки<br /><br /> 49: загрузка метаданных<br /><br /> 50: загрузка данных<br /><br /> 51: Заключительная загрузка<br /><br /> 52: обход метаданных во время резервного копирования<br /><br /> 53: VertiPaq<br /><br /> 54: обработка иерархии<br /><br /> 55: переключение словаря|  
|CurrentTime|2|5|Содержит текущее время события из отчета, если доступно. Ожидаемые форматы фильтрации: «ГГГГ-ММ-ДД» и «ГГГГ-ММ-ДД ЧЧ:ММ:СС».|  
|StartTime|3|5|Содержит время начала события, если оно доступно. Ожидаемые форматы фильтрации: «ГГГГ-ММ-ДД» и «ГГГГ-ММ-ДД ЧЧ:ММ:СС».|  
|JobID|7|1|Содержит идентификатор задания, связанного с событием из отчета.|  
|SessionType|8|8|Содержит тип сеанса (сущность, вызывающую событие), связанного с событием из отчета. Доступные значения событий обработки:<br /><br /> 1 = пользователь<br /><br /> 2 = упреждающее кэширование<br /><br /> 3 = отложенная обработка|  
|ProgressTotal|9|1|Содержит общий процент выполнения события из отчета.|  
|IntegerData|10|1|Содержит целочисленные данные, связанные с событием из отчета, например текущий показатель числа обработанных строк для события обработки.|  
|ObjectID|11|8|Содержит идентификатор объекта (строку), связанного с событием из отчета.|  
|ObjectType|12|1|Содержит тип объекта.|  
|ObjectName|13|8|Содержит имя объекта, связанного с событием из отчета.|  
|ObjectPath|14|8|Содержит путь к объекту, связанному с событием из отчета, в виде списка родительских элементов с разделителями-запятыми, начинающегося с родительских элементов объекта.|  
|ObjectReference|15|8|Содержит ссылку на объект для события из отчета, созданную в виде XML-кода по всем родительским элементам и использующую теги для описания объекта.|  
|ConnectionID|25|1|Содержит уникальный идентификатор соединения, связанного с событием из отчета.|  
|DatabaseName|28|8|Содержит имя базы данных, в которой произошло событие из отчета.|  
|SessionID|39|8|Содержит идентификатор сеанса, связанного с событием из отчета.|  
|SPID|41|1|Содержит идентификатор серверного процесса (SPID), уникально идентифицирующий пользовательский сеанс, связанный с событием из отчета. Идентификатор SPID напрямую соответствует идентификатору GUID сеанса, используемому XML для аналитики (XMLA).|  
|TextData|42|9|Содержит текстовые данные, связанные с событием из отчета.|  
|ServerName|43|8|Содержит имя экземпляра служб [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , на котором произошло событие из отчета.|  
  
## <a name="progress-report-errordata-columns"></a>Ошибки отчета о состоянии — Столбцы данных  
  
|**Имя столбца**|**Идентификатор столбца**|**Тип столбца**|**Описание столбца**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|Класс событий используется для категоризации событий.|  
|EventSubclass|1|1|Подкласс событий предоставляет дополнительные сведения о каждом классе событий:<br /><br /> 1: процесс<br /><br /> 2: слияние<br /><br /> 3: удаление<br /><br /> 4: DeleteOldAggregations<br /><br /> 5: перестроить<br /><br /> 6: фиксация<br /><br /> 7: отката<br /><br /> 8: CreateIndexes<br /><br /> 9: CreateTable<br /><br /> 10: InsertInto<br /><br /> 11: транзакции<br /><br /> 12: инициализация<br /><br /> 13: дискретизации<br /><br /> 14: запрос<br /><br /> 15: создать представление<br /><br /> 16: запись данных<br /><br /> 17: ReadData<br /><br /> 18: GroupData<br /><br /> 19: GroupDataRecord<br /><br /> 20: BuildIndex<br /><br /> 21: aggregate<br /><br /> 22: BuildDecode<br /><br /> 23: WriteDecode<br /><br /> 24: BuildDMDecode<br /><br /> 25: ExecuteSQL<br /><br /> 26: ExecuteModifiedSQL<br /><br /> 27: подключение<br /><br /> 28: BuildAggsAndIndexes<br /><br /> 29: MergeAggsOnDisk<br /><br /> 30: BuildIndexForRigidAggs<br /><br /> 31: BuildIndexForFlexibleAggs<br /><br /> 32: WriteAggsAndIndexes<br /><br /> 33: WriteSegment<br /><br /> 34: DataMiningProgress<br /><br /> 35: ReadBufferFullReport<br /><br /> 36: ProactiveCacheConversion<br /><br /> 37: резервное копирование<br /><br /> 38: восстановление<br /><br /> 39: синхронизация<br /><br /> 40: создать расписание обработки<br /><br /> 41: отсоединение<br /><br /> 42: присоединение<br /><br /> 43: анализ\кодирование данных<br /><br /> 44: сжатие сегмента<br /><br /> 45: столбец таблицы записи<br /><br /> 46: Подготовка построения отношений<br /><br /> 47: построить сегмент отношений<br /><br /> 48: нагрузки<br /><br /> 49: загрузка метаданных<br /><br /> 50: загрузка данных<br /><br /> 51: Заключительная загрузка<br /><br /> 52: обход метаданных во время резервного копирования<br /><br /> 53: VertiPaq<br /><br /> 54: обработка иерархии<br /><br /> 55: переключение словаря|  
|CurrentTime|2|5|Содержит текущее время события из отчета, если доступно. Ожидаемые форматы фильтрации: «ГГГГ-ММ-ДД» и «ГГГГ-ММ-ДД ЧЧ:ММ:СС».|  
|StartTime|3|5|Содержит время начала события, если оно доступно. Ожидаемые форматы фильтрации: «ГГГГ-ММ-ДД» и «ГГГГ-ММ-ДД ЧЧ:ММ:СС».|  
|EndTime|4|5|Содержит время окончания события. Этот столбец не заполняется для таких классов событий запуска, как SQL:BatchStarting или SP:Starting. Ожидаемые форматы фильтрации: «ГГГГ-ММ-ДД» и «ГГГГ-ММ-ДД ЧЧ:ММ:СС».|  
|Duration|5|2|Содержит общую длительность события в миллисекундах.|  
|JobID|7|1|Содержит идентификатор задания, связанного с событием из отчета.|  
|SessionType|8|8|Содержит тип сеанса (сущность, вызывающую событие), связанного с событием из отчета. Доступные значения событий обработки:<br /><br /> 1 = пользователь<br /><br /> 2 = упреждающее кэширование<br /><br /> 3 = отложенная обработка|  
|ProgressTotal|9|1|Содержит общий процент выполнения события из отчета.|  
|IntegerData|10|1|Содержит целочисленные данные, связанные с событием из отчета, например текущий показатель числа обработанных строк для события обработки.|  
|ObjectID|11|8|Содержит идентификатор объекта (строку), связанного с событием из отчета.|  
|ObjectType|12|1|Содержит тип объекта.|  
|ObjectName|13|8|Содержит имя объекта, связанного с событием из отчета.|  
|ObjectPath|14|8|Содержит путь к объекту, связанному с событием из отчета, в виде списка родительских элементов с разделителями-запятыми, начинающегося с родительских элементов объекта.|  
|ObjectReference|15|8|Содержит ссылку на объект для события из отчета, созданную в виде XML-кода по всем родительским элементам и использующую теги для описания объекта.|  
|Severity|22|1|Содержит степень серьезности исключения, связанного с событием из отчета. Возможны следующие значения.<br /><br /> 0 = успешное завершение<br /><br /> 1 = информационное сообщение<br /><br /> 2 = предупреждение<br /><br /> 3 = ошибка|  
|Ошибка|24|1|Содержит номер ошибки для данного события.|  
|ConnectionID|25|1|Содержит уникальный идентификатор соединения, связанного с событием из отчета.|  
|DatabaseName|28|8|Содержит имя базы данных, в которой произошло событие из отчета.|  
|SessionID|39|8|Содержит идентификатор сеанса, связанного с событием из отчета.|  
|SPID|41|1|Содержит идентификатор серверного процесса (SPID), уникально идентифицирующий пользовательский сеанс, связанный с событием из отчета. Идентификатор SPID напрямую соответствует идентификатору GUID сеанса, используемому XML для аналитики (XMLA).|  
|TextData|42|9|Содержит текстовые данные, связанные с событием из отчета.|  
|ServerName|43|8|Содержит имя экземпляра служб [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , на котором произошло событие из отчета.|  
  
## <a name="see-also"></a>См. также  
 [Категория событий «Отчеты о состоянии»](progress-reports-event-category.md)  
  
  
