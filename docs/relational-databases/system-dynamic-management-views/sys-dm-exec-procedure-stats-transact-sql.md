---
title: "sys.dm_exec_procedure_stats (Transact-SQL) | Документы Microsoft"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.dm_exec_procedure_stats_TSQL
- dm_exec_procedure_stats_TSQL
- dm_exec_procedure_stats
- sys.dm_exec_procedure_stats
dev_langs: TSQL
helpviewer_keywords: sys.dm_exec_procedure_stats dynamic management view
ms.assetid: ab8ddde8-1cea-4b41-a7e4-697e6ddd785a
caps.latest.revision: "24"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: f935b0e9a4c150830a03ecb2ea1f67a4cd270d3f
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmexecprocedurestats-transact-sql"></a>sys.dm_exec_procedure_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Возвращает суммарную статистику производительности для кэшированных хранимых процедур. Это представление содержит по одной строке для каждого кэшированного плана хранимой процедуры. Время существования строки равно времени пребывания хранимой процедуры в кэше. Когда хранимая процедура удаляется из кэша, соответствующая строка исключается из представления. В этот момент возникает аналогично события трассировки SQL статистики производительности **sys.dm_exec_query_stats**.  
  
 Динамические административные представления в среде [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] не могут предоставлять информацию, которая может повлиять на автономность базы данных, или информацию о других базах данных, к которым имеет доступ пользователь. Чтобы избежать предоставления этих сведений, все строки, содержащие данные, не принадлежащие к подключенному клиенту, фильтруются.  
  
> **Примечание:** начальный запрос представления **sys.dm_exec_procedure_stats** может выдавать неточные результаты, если на сервере выполняется рабочая нагрузка. Более точные результаты могут быть получены при повторном выполнении запроса.  
  
> **Примечание для хранилища данных Azure SQL.** Вызов его из [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] или [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], используйте имя **sys.dm_pdw_nodes_exec_procedure_stats**.  
  
|Имя столбца|Тип данных|Description|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|Идентификатор базы данных, в которой находится хранимая процедура.|  
|**object_id**|**int**|Идентификатор объекта хранимой процедуры.|  
|**type**|**char(2)**|Тип объекта:<br /><br /> P = хранимая процедура SQL<br /><br /> PC = хранимая процедура сборки (среда CLR)<br /><br /> X = расширенная хранимая процедура|  
|**type_desc**|**nvarchar(60)**|Описание типа объекта:<br /><br /> SQL_STORED_PROCEDURE<br /><br /> CLR_STORED_PROCEDURE<br /><br /> EXTENDED_STORED_PROCEDURE|  
|**sql_handle**|**varbinary(64)**|Это может использоваться для корреляции с запросами в **sys.dm_exec_query_stats** , которые выполнялись из этой хранимой процедуры.|  
|**plan_handle**|**varbinary(64)**|Идентификатор плана в оперативной памяти. Этот идентификатор является временным и константным, только пока план сохраняется в кэше. Это значение может использоваться с **sys.dm_exec_cached_plans** динамическое административное представление.<br /><br /> Значение всегда равно 0x000, если скомпилированная в собственном коде хранимая процедура запрашивает оптимизированную для памяти таблицу.|  
|**cached_time**|**datetime**|Время добавления хранимой процедуры в кэш.|  
|**last_execution_time**|**datetime**|Время последнего выполнения хранимой процедуры.|  
|**execution_count**|**bigint**|Количество выполнений хранимой процедуры с момента последней компиляции.|  
|**total_worker_time**|**bigint**|Общее время ЦП в микросекундах, при выполнении этой хранимой процедуры с момента его компиляции.<br /><br /> Для скомпилированных в собственном коде хранимых процедур функция **total_worker_time** может быть неточной, если за время меньше миллисекунды выполняется большое количество хранимых процедур.|  
|**last_worker_time**|**bigint**|Время ЦП, затраченное на последнее выполнение хранимой процедуры, в микросекундах. <sup>1</sup>|  
|**min_worker_time**|**bigint**|Минимальное время ЦП (в микросекундах), которое эта хранимая процедура когда-либо затрачивала на одно выполнение. <sup>1</sup>|  
|**max_worker_time**|**bigint**|Максимальное время ЦП (в микросекундах), которое эта хранимая процедура когда-либо затрачивала на одно выполнение. <sup>1</sup>|  
|**total_physical_reads**|**bigint**|Общее количество операций физического считывания при выполнении хранимой процедуры с момента ее компиляции.<br /><br /> Значение всегда равно 0 при запросе оптимизированной для памяти таблицы.|  
|**last_physical_reads**|**bigint**|Количество операций физического считывания за время последнего выполнения хранимой процедуры.<br /><br /> Значение всегда равно 0 при запросе оптимизированной для памяти таблицы.|  
|**min_physical_reads**|**bigint**|Минимальное количество операций физического считывания за одно выполнение хранимой процедуры.<br /><br /> Значение всегда равно 0 при запросе оптимизированной для памяти таблицы.|  
|**max_physical_reads**|**bigint**|Максимальное количество операций физического считывания за одно выполнение хранимой процедуры.<br /><br /> Значение всегда равно 0 при запросе оптимизированной для памяти таблицы.|  
|**total_logical_writes**|**bigint**|Общее количество операций логической записи при выполнении хранимой процедуры с момента ее компиляции.<br /><br /> Значение всегда равно 0 при запросе оптимизированной для памяти таблицы.|  
|**last_logical_writes**|**bigint**|Количество страниц в буферном пуле, загрязненных во время последнего выполнения плана. Если страница уже является «грязной» (т. е. измененной), операции записи не учитываются.<br /><br /> Значение всегда равно 0 при запросе оптимизированной для памяти таблицы.|  
|**min_logical_writes**|**bigint**|Минимальное количество операций логической записи за одно выполнение хранимой процедуры.<br /><br /> Значение всегда равно 0 при запросе оптимизированной для памяти таблицы.|  
|**max_logical_writes**|**bigint**|Максимальное количество операций логической записи за одно выполнение хранимой процедуры.<br /><br /> Значение всегда равно 0 при запросе оптимизированной для памяти таблицы.|  
|**total_logical_reads**|**bigint**|Общее количество операций логического чтения при выполнении хранимой процедуры с момента ее компиляции.<br /><br /> Значение всегда равно 0 при запросе оптимизированной для памяти таблицы.|  
|**last_logical_reads**|**bigint**|Количество операций логического чтения за время последнего выполнения хранимой процедуры.<br /><br /> Значение всегда равно 0 при запросе оптимизированной для памяти таблицы.|  
|**min_logical_reads**|**bigint**|Минимальное количество операций логического чтения за одно выполнение хранимой процедуры.<br /><br /> Значение всегда равно 0 при запросе оптимизированной для памяти таблицы.|  
|**max_logical_reads**|**bigint**|Максимальное количество операций логического чтения за одно выполнение хранимой процедуры.<br /><br /> Значение всегда равно 0 при запросе оптимизированной для памяти таблицы.|  
|**total_elapsed_time**|**bigint**|Общее время, затраченное на выполнение хранимой процедуры, в микросекундах.|  
|**last_elapsed_time**|**bigint**|Время, затраченное на последнее выполнение хранимой процедуры, в микросекундах.|  
|**min_elapsed_time**|**bigint**|Минимальное время, затраченное на одно выполнение хранимой процедуры, в микросекундах.|  
|**max_elapsed_time**|**bigint**|Максимальное время, затраченное на одно выполнение хранимой процедуры, в микросекундах.|  
|**pdw_node_id**|**int**|**Применяется к**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)],[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> Идентификатор для узла, это распределение.|  
  
 <sup>1</sup> для скомпилированных в собственном коде хранимых процедур при включении сбора статистики времени рабочей роли собираются в миллисекундах. Если запрос выполняется за время меньше миллисекунды, это значение будет равно 0.  
  
## <a name="permissions"></a>Permissions  
На [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], требуется `VIEW SERVER STATE` разрешение.   
На [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] уровней Premium необходимо `VIEW DATABASE STATE` разрешений в базе данных. На [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] уровней Standard и Basic, требует **администратор сервера** или **администратора Azure Active Directory** учетной записи. 
  
## <a name="remarks"></a>Замечания  
 Статистика в представлении обновляется после завершения выполнения хранимой процедуры.  
  
## <a name="examples"></a>Примеры  
 В следующем примере возвращаются сведения о 10 первых хранимых процедурах, идентифицируемых по среднему затраченному времени.  
  
```  
SELECT TOP 10 d.object_id, d.database_id, OBJECT_NAME(object_id, database_id) 'proc name',   
    d.cached_time, d.last_execution_time, d.total_elapsed_time,  
    d.total_elapsed_time/d.execution_count AS [avg_elapsed_time],  
    d.last_elapsed_time, d.execution_count  
FROM sys.dm_exec_procedure_stats AS d  
ORDER BY [total_worker_time] DESC;  
```  
  
## <a name="see-also"></a>См. также:  
 [&#40; динамические административные представления и функции, связанные с выполнением Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [sys.dm_exec_sql_text &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)   
 [sys.dm_exec_query_stats (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)   
 
 [sys.dm_exec_trigger_stats &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-trigger-stats-transact-sql.md)  
  
  

