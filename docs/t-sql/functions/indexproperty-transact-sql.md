---
title: "INDEXPROPERTY (Transact-SQL) | Документы Microsoft"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- INDEXPROPERTY
- INDEXPROPERTY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- INDEXPROPERTY function
- indexes [SQL Server], viewing
- indexes [SQL Server], properties
ms.assetid: 998d5788-4871-44a8-8125-0d9390868b84
caps.latest.revision: 56
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: cbd10b32ee6b2d88a97222c3a970452a4a628b83
ms.contentlocale: ru-ru
ms.lasthandoff: 09/01/2017

---
# <a name="indexproperty-transact-sql"></a>INDEXPROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Возвращает значение свойства именованного индекса или статистики для указанного идентификационного номера таблицы, имени индекса или статистики, а также имени свойства. Возвращает NULL для XML-индексов.  
  
 ![Значок ссылки на раздел](../../database-engine/configure-windows/media/topic-link.gif "Значок ссылки на раздел") [Синтаксические обозначения в Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Синтаксис  
  
```  
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
INDEXPROPERTY ( object_ID , index_or_statistics_name , property )   
```  
  
## <a name="arguments"></a>Аргументы  
 *object_id*  
 Выражение, которое содержит идентификационный номер объекта таблицы или индексированного представления, для которого предоставляются сведения о свойстве индекса. *object_id* — **int**.  
  
 *index_or_statistics_name*  
 Выражение, которое содержит имя индекса или статистики, для которой возвращаются сведения о свойстве. *index_or_statistics_name* — **nvarchar(128)**.  
  
 *Свойство*  
 Выражение, которое содержит имя возвращаемого свойства базы данных. *Свойство* — **varchar(128)**, и может принимать одно из следующих значений.  
  
> [!NOTE]  
>  Если не указано иное, значение NULL возвращается, когда *свойство* не является допустимым именем свойства, *object_ID* не является допустимым Идентификатором объекта, *object_ID* является неподдерживаемым типом объекта для Указанное свойство или вызывающий объект не имеет разрешения на просмотр метаданных объекта.  
  
|Свойство|Description|Значение|  
|--------------|-----------------|-----------|  
|**IndexDepth**|Глубина индекса.|Количество уровней индекса.<br /><br /> NULL = Неверный XML-индекс или вход.|  
|**IndexFillFactor**|Значение коэффициента заполнения, использованное при создании индекса или при его последней перестройке.|Коэффициент заполнения.|  
|**IndexID**|Идентификатор индекса указанной таблицы или индексированного представления.|Идентификатор индекса.|  
|**IsAutoStatistics**|Статистики были сформированы параметром AUTO_CREATE_STATISTICS инструкции ALTER DATABASE.|1 = True<br /><br /> 0 = False или XML-индекс.|  
|**IsClustered**|Кластеризованный индекс.|1 = True<br /><br /> 0 = False или XML-индекс.|  
|**IsDisabled**|Индекс отключен.|1 = True<br /><br /> 0 = False.<br /><br /> NULL = Введенные значения недопустимы.|  
|**IsFulltextKey**|Индекс является ключом для полнотекстового и семантического индексирования таблицы.|**Область применения**: начиная с [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] до [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> 1 = True<br /><br /> 0 = False или XML-индекс.<br /><br /> NULL = Введенные значения недопустимы.|  
|**IsHypothetical**|Индекс является гипотетическим и не может использоваться напрямую в качестве пути доступа к данным. Гипотетические индексы содержат статистики уровня столбца и управляются и используются помощником по настройке ядра СУБД.|1 = True<br /><br /> 0 = False или XML-индекс.<br /><br /> NULL = Введенные значения недопустимы.|  
|**IsPadIndex**|Индекс задает пространство, которое должно оставаться открытым на каждом внутреннем узле.|**Область применения**: начиная с [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] до [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> 1 = True<br /><br /> 0 = False или XML-индекс.|  
|**IsPageLockDisallowed**|Значение блокировки страницы, установленное параметром ALLOW_PAGE_LOCKS инструкции ALTER INDEX.|**Область применения**: начиная с [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] до [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> 1 = Блокировка страниц запрещена;<br /><br /> 0 = Page разрешены блокировки.<br /><br /> NULL = Введенные значения недопустимы.|  
|**IsRowLockDisallowed**|Значение блокировки строк, установленное параметром ALLOW_ROW_LOCKS инструкции ALTER INDEX.|**Область применения**: начиная с [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] до [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> 1 = Блокировка строк запрещена;<br /><br /> 0 = Блокировка строк разрешена.<br /><br /> NULL = Введенные значения недопустимы.|  
|**IsStatistics**|*index_or_statistics_name* — статистика, созданная с помощью инструкции CREATE STATISTICS или параметром AUTO_CREATE_STATISTICS инструкции ALTER DATABASE.|1 = True<br /><br /> 0 = False или XML-индекс.|  
|**IsUnique**|Индекс является уникальным.|1 = True<br /><br /> 0 = False или XML-индекс.|  
|**IsColumnstore**|Оптимизированный для памяти xVelocity индекс columnstore.|**Область применения**: начиная с [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] до [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> 1 = True<br /><br /> 0 = False.|  
  
## <a name="return-types"></a>Типы возвращаемых значений  
 **int**  
  
## <a name="exceptions"></a>Исключения  
 Возвращает значение NULL в случае ошибки или если участник не имеет разрешений для просмотра объекта.  
  
 Пользователь может просматривать только метаданные защищаемых объектов, которыми он владеет или на которые пользователю были предоставлены разрешения. Это означает, что создающие метаданные встроенные функции, такие как INDEXPROPERTY могут вернуть значение NULL в случае, если пользователь не имеет разрешений на объект. Дополнительные сведения см. в разделе [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="examples"></a>Примеры  
 В следующем примере возвращается значения для **IsClustered**, **IndexDepth**, и **IndexFillFactor** свойства `PK`_`Employee` \_ `BusinessEntityID` индекс `Employee` в таблицу [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] базы данных.  
  
```  
SELECT   
    INDEXPROPERTY(OBJECT_ID('HumanResources.Employee'),  
        'PK_Employee_BusinessEntityID','IsClustered')AS [Is Clustered],  
    INDEXPROPERTY(OBJECT_ID('HumanResources.Employee'),  
        'PK_Employee_BusinessEntityID','IndexDepth') AS [Index Depth],  
    INDEXPROPERTY(OBJECT_ID('HumanResources.Employee'),  
        'PK_Employee_BusinessEntityID','IndexFillFactor') AS [Fill Factor];  
  
```  
  
 Результирующий набор:  
  
```  
Is Clustered Index Depth Fill Factor   
------------ ----------- -----------   
1            2           0  
  
(1 row(s) affected)  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Примеры: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] и[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 В следующем примере рассматривается свойства индексы на `FactResellerSales` таблицы.  
  
```  
-- Uses AdventureWorks  
  
SELECT   
INDEXPROPERTY(OBJECT_ID('dbo.FactResellerSales'),  
    'ClusteredIndex_6d10fa223e5e4c1fbba087e29e16a7a2','IsClustered') AS [Is Clustered],  
INDEXPROPERTY(OBJECT_ID('dbo.FactResellerSales'),  
    'ClusteredIndex_6d10fa223e5e4c1fbba087e29e16a7a2','IsColumnstore') AS [Is Columnstore Index],  
INDEXPROPERTY(OBJECT_ID('dbo.FactResellerSales'),  
    'ClusteredIndex_6d10fa223e5e4c1fbba087e29e16a7a2','IndexFillFactor') AS [Fill Factor];  
GO  
```  
  
## <a name="see-also"></a>См. также:  
 [CREATE INDEX (Transact-SQL)](../../t-sql/statements/create-index-transact-sql.md)   
 [Статистика](../../relational-databases/statistics/statistics.md)   
 [sys.indexes (Transact-SQL)](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.index_columns (Transact-SQL)](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)   
 [sys.stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md)   
 [sys.stats_columns &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-stats-columns-transact-sql.md)  
  
  

