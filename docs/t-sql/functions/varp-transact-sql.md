---
title: "Функция VARP (Transact-SQL) | Документы Microsoft"
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- VARP_TSQL
- VARP
dev_langs:
- TSQL
helpviewer_keywords:
- statistical variances
- expressions [SQL Server], statistical variance
- VARP function [Transact-SQL]
ms.assetid: ce5d2e32-01da-4e18-b8ed-a08b61d84456
caps.latest.revision: 40
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d27f781da75ee96b634a2ecd1239aa063807225e
ms.contentlocale: ru-ru
ms.lasthandoff: 09/01/2017

---
# <a name="varp-transact-sql"></a>VARP (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Возвращает статистическую дисперсию для заполнения всех значений в указанном выражении.  
  
 ![Значок ссылки на раздел](../../database-engine/configure-windows/media/topic-link.gif "Значок ссылки на раздел") [Синтаксические обозначения в Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Синтаксис  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
VARP ( [ ALL | DISTINCT ] expression )  
   OVER ( [ partition_by_clause ] order_by_clause )  nh  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
-- Aggregate Function Syntax   
VARP ( [ ALL | DISTINCT ] expression )  
  
-- Analytic Function Syntax  
VARP (expression) OVER ( [ partition_by_clause ] order_by_clause)  
```  
  
## <a name="arguments"></a>Аргументы  
 **ALL**  
 Применяет функцию ко всем значениям. ALL является параметром по умолчанию.  
  
 DISTINCT  
 Указывает, что учитывается каждое уникальное значение.  
  
 *expression*  
 — [Выражение](../../t-sql/language-elements/expressions-transact-sql.md) точных числовых или приблизительных числовых типа данных, за исключением **бит** тип данных. Агрегатные функции и вложенные запросы не допускаются.  
  
 НАД **(** [ *partition_by_clause* ] *order_by_clause***)**  
 *partition_by_clause* Делит результирующий набор, полученный с помощью предложения FROM, на секции, к которым применяется функция. Если этот параметр не указан, функция обрабатывает все строки результирующего набора запроса как отдельные группы. *order_by_clause* , определяет логический порядок, в котором выполняется операция. *order_by_clause* является обязательным. Дополнительные сведения см. в разделе [предложение OVER &#40; Transact-SQL &#41; ](../../t-sql/queries/select-over-clause-transact-sql.md).  
  
## <a name="return-types"></a>Типы возвращаемых значений  
 **float**  
  
## <a name="remarks"></a>Замечания  
 Если VARP используется во всех элементах в инструкции SELECT, в вычисление включаются все значения в результирующем наборе. Функция VARP может использоваться только для числовых столбцов. Значения NULL пропускаются.  
  
 VARP — это детерминированная функция, если она используется без предложений OVER и ORDER BY. Она не детерминирована при использовании с предложениями OVER и ORDER BY. Дополнительные сведения см. в разделе [Deterministic and Nondeterministic Functions](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md).  
  
## <a name="examples"></a>Примеры  
  
### <a name="a-using-varp"></a>А. Использование VARP  
 Следующий пример показывает возврат дисперсии совокупности всех дополнительных значений в таблице `SalesPerson` в базе данных [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
```  
SELECT VARP(Bonus)  
FROM Sales.SalesPerson;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Примеры: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] и[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="b-using-varp"></a>Б. Использование VARP  
 В следующем примере возвращается `VARP`значений квоты продаж в таблице `dbo.FactSalesQuota`. Первый столбец содержит дисперсию всех уникальных значений, а второй столбец содержит дисперсию всех значений, включая все повторяющиеся значения.  
  
```  
-- Uses AdventureWorks  
  
SELECT VARP(DISTINCT SalesAmountQuota)AS Distinct_Values, VARP(SalesAmountQuota) AS All_Values  
FROM dbo.FactSalesQuota;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `Distinct_Values   All_Values`  
  
 `----------------  ----------------`  
  
 `158146830494.18   157788848582.94`  
  
### <a name="c-using-varp-with-over"></a>В. Использовать функцию VARP с больше  
 В следующем примере возвращается `VARP` значений квоты продаж для каждого квартала календарного года. Обратите внимание, что предложение ORDER BY в предложении OVER упорядочивает статистическая дисперсия ORDER BY инструкции SELECT упорядочивает результирующий набор.  
  
```  
-- Uses AdventureWorks  
  
SELECT CalendarYear AS Year, CalendarQuarter AS Quarter, SalesAmountQuota AS SalesQuota,  
       VARP(SalesAmountQuota) OVER (ORDER BY CalendarYear, CalendarQuarter) AS Variance  
FROM dbo.FactSalesQuota  
WHERE EmployeeKey = 272 AND CalendarYear = 2002  
ORDER BY CalendarQuarter;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `Year  Quarter  SalesQuota              Variance`  
  
 `----  -------  ----------------------  -------------------`  
  
 `2002  1         91000.0000             0.00`  
  
 `2002  2        140000.0000             600250000.00`  
  
 `2002  3         70000.0000             860222222.22`  
  
 `2002  4        154000.0000             1185187500.00`  
  
## <a name="see-also"></a>См. также:  
 [Агрегатные функции &#40; Transact-SQL &#41;](../../t-sql/functions/aggregate-functions-transact-sql.md)   
 [ЧЕРЕЗ предложение &#40; Transact-SQL &#41;](../../t-sql/queries/select-over-clause-transact-sql.md)  
  
  

