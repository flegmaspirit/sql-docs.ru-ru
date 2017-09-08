---
title: "Параметры сортировки | Документы Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- COLLATE
- COLLATE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- collations [SQL Server], COLLATE clause
- COLLATE clause
ms.assetid: 76763ac8-3e0d-4bbb-aa53-f5e7da021daa
caps.latest.revision: 25
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9154d293ca5b7737a9c80fef0754dcec6e461a46
ms.contentlocale: ru-ru
ms.lasthandoff: 09/01/2017

---
# <a name="collations"></a>Параметры сортировки
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Предложение, которое может применяться к определению базы данных или столбца для определения параметров сортировки, а также к выражению символьной строки, чтобы применить приведение параметров сортировки.  
  
 ![Значок ссылки на раздел](../../database-engine/configure-windows/media/topic-link.gif "Значок ссылки на раздел") [Синтаксические обозначения в Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
COLLATE { <collation_name> | database_default }  
<collation_name> :: =   
     { Windows_collation_name } | { SQL_collation_name }  
```  
  
## <a name="arguments"></a>Аргументы  
 *collation_name*  
 Имя параметров сортировки, применяемых к выражению, определению столбца или определению базы данных. *collation_name* может быть только указанным *Windows_collation_name* или *SQL_collation_name*. *collation_name* должно быть литеральное значение. *collation_name* не может быть представлен переменной или выражением.  
  
 *Windows_collation_name* имя параметров сортировки для [имя параметров сортировки Windows](../../t-sql/statements/windows-collation-name-transact-sql.md).  
  
 *SQL_collation_name* имя параметров сортировки для [имя параметров сортировки SQL Server](../../t-sql/statements/sql-server-collation-name-transact-sql.md).  
  
 При применении параметров сортировки на уровне определения базы данных параметры сортировки Windows «Только для Юникода» нельзя использовать с предложением COLLATE.  
  
 **database_default**  
 Заставляет предложение COLLATE наследовать параметры сортировки текущей базы данных.  
  
## <a name="remarks"></a>Замечания  
 Предложение COLLATE можно указывать на нескольких уровнях. следующие основные параметры.  
  
1.  Создание или изменение базы данных.  
  
     Предложение COLLATE можно использовать в инструкциях CREATE DATABASE и ALTER DATABASE для указания параметров сортировки по умолчанию для базы данных. Можно также задать параметры сортировки при создании базы данных с помощью среды [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Если не указывать параметры сортировки, базе данных присваиваются параметры сортировки по умолчанию для экземпляра [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
    > [!NOTE]  
    >  Параметры сортировки Windows только для Юникода могут использоваться только с предложением COLLATE для применения параметров сортировки для **nchar**, **nvarchar**, и **ntext** типов данных на уровне столбцов и выражение уровня данных. они не может использоваться с предложением COLLATE для изменения параметров сортировки экземпляра базы данных или сервера.  
  
2.  Создание или изменение столбца таблицы.  
  
     Параметры сортировки можно указать для каждого столбца символьной строки с помощью предложения COLLATE в инструкциях CREATE TABLE и ALTER TABLE. Можно также задать параметры сортировки при создании таблицы с помощью среды [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Если не указывать параметры сортировки, столбцу присваиваются параметры сортировки по умолчанию для базы данных.  
  
     Можно также использовать `database_default` параметр в предложении COLLATE, чтобы указать, что столбец временной таблицы использует по умолчанию параметры сортировки текущей базы данных пользователя для соединения, а не **tempdb**.  
  
3.  Приведение параметров сортировки выражения.  
  
     Предложение COLLATE можно использовать для применения символьного выражения к определенным параметрам сортировки. Символьным литералам и переменным присваиваются параметры сортировки по умолчанию для текущей базы данных. Ссылкам столбцов присваивается определение параметров сортировки для столбца.  
  
 Параметры сортировки идентификатора зависят от уровня, для которого определен этот идентификатор. К идентификаторам объектов на уровне экземпляров, таких как имена входа и имена базы данных, применяются параметры сортировки по умолчанию для экземпляра. К идентификаторам объектов внутри базы данных, таких как таблицы, представления и имена столбцов, применяются параметры сортировки, используемые по умолчанию для базы данных. Например: две таблицы, имена которых отличаются только регистром, можно создать в базе данных с параметрами сортировки, учитывающими регистр букв, но нельзя создать в базе данных с параметрами сортировки без учета регистра. Дополнительные сведения см. в разделе [Database Identifiers](../../relational-databases/databases/database-identifiers.md).  
  
 Переменные, метки GOTO, временные хранимые процедуры и временные таблицы можно создавать, если контекст соединения связан с одной базой данных, и ссылка на которую сохраняется, когда контекст переключается на другую базу данных. Идентификаторы переменных, меток GOTO, временных хранимых процедур и временных таблиц имеют параметры сортировки по умолчанию для экземпляра сервера.  
  
 Предложение COLLATE применяется только к **char**, **varchar**, **текст**, **nchar**, **nvarchar** , и **ntext** типов данных.  
  
 Предложение COLLATE использует *collate_name* для ссылки на имя параметров сортировки SQL Server или параметры сортировки Windows для применения к выражению, определению столбца или определению базы данных. *collation_name* может быть только указанным *Windows_collation_name* или *SQL_collation_name* и этот параметр должен содержать литеральное значение. *collation_name* не может быть представлен переменной или выражением.  
  
 Параметры сортировки обычно определяются по имени, за исключением программы установки. В программе установки вместо имени указывается обозначение базовых параметров сортировки (локали параметров сортировки) для параметров сортировки Windows, а затем определяются настройки сортировки с учетом или без учета регистра или диакритических знаков.  
  
 Можно выполнить системную функцию [fn_helpcollations](../../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md) для получения списка всех допустимых имен параметров сортировки параметров сортировки Windows и параметры сортировки SQL Server:  
  
```  
SELECT name, description  
FROM fn_helpcollations();  
```  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] поддерживает только кодовые страницы, существующие в базовой операционной системе. При выполнении операции, зависящей от параметров сортировки, используемых ссылочным объектом, параметры сортировки [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] должны использовать кодовую страницу, которая поддерживается работающей на компьютере операционной системой. Эти операции могут включать:  
  
-   указание параметров сортировки по умолчанию для базы данных при ее создании или изменении;  
  
-   указание параметров сортировки для столбца при создании или изменении таблицы;  
  
-   При восстановлении или присоединении базы данных, параметры сортировки базы данных по умолчанию и параметры сортировки любого **char**, **varchar**, и **текст** столбцов или параметров в базе данных должны поддерживаться операционной системой.  
  
     Поддерживаемые преобразования кодовых страниц для **char** и **varchar** типы данных, но не для **текст** тип данных. Сообщения о потере данных во время преобразования кодовых страниц не выводятся.  
  
 Если параметры сортировки, заданные или параметры сортировки, используемые объектом по ссылке, используют кодовую страницу, не поддерживаемую Windows, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] выводит сообщение об ошибке.  
  
## <a name="examples"></a>Примеры  
  
### <a name="a-specifying-collation-during-a-select"></a>A. Указание параметров сортировки во время выбора  
 В следующем примере создается простая таблица, а затем вставляются четыре строки. Затем в примере применяются два параметра сортировки при выборе данных из таблицы, при этом демонстрируется, что `Chiapas` сортируется по-разному.  
  
```tsql  
CREATE TABLE Locations  
(Place varchar(15) NOT NULL);  
GO  
INSERT Locations(Place) VALUES ('Chiapas'),('Colima')  
                             , ('Cinco Rios'), ('California');  
GO  
--Apply an typical collation  
SELECT Place FROM Locations  
ORDER BY Place  
COLLATE Latin1_General_CS_AS_KS_WS ASC;  
GO  
-- Apply a Spanish collation  
SELECT Place FROM Locations  
ORDER BY Place  
COLLATE Traditional_Spanish_ci_ai ASC;  
GO  
```  
  
 Ниже приведены результаты первого запроса.  
  
 `Place`  
  
 `-------------`  
  
 `California`  
  
 `Chiapas`  
  
 `Cinco Rios`  
  
 `Colima`  
  
 Ниже приведены результаты второго запроса.  
  
 `Place`  
  
 `-------------`  
  
 `California`  
  
 `Cinco Rios`  
  
 `Colima`  
  
 `Chiapas`  
  
### <a name="b-additional-examples"></a>Б. Дополнительные примеры  
 Дополнительные примеры использования **COLLATE**, в разделе [CREATE DATABASE &#40; Transact SQL Server-SQL &#41; ](../../t-sql/statements/create-database-sql-server-transact-sql.md) пример **ж. Создание базы данных и назначение имени и параметров сортировки**, и [ALTER TABLE &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-table-transact-sql.md) пример **ф. Изменение параметров сортировки столбца**.  
  
## <a name="see-also"></a>См. также:  
 [ALTER TABLE (Transact-SQL)](../../t-sql/statements/alter-table-transact-sql.md)   
 [Поддержка параметров сортировки и Юникода](../../relational-databases/collations/collation-and-unicode-support.md)   
 [Очередность параметров сортировки (Transact-SQL)](../../t-sql/statements/collation-precedence-transact-sql.md)   
 [Константы &#40; Transact-SQL &#41;](../../t-sql/data-types/constants-transact-sql.md)   
 [CREATE DATABASE (SQL Server Transact-SQL)](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [CREATE TABLE (Transact-SQL)](../../t-sql/statements/create-table-transact-sql.md)   
 [DECLARE @local_variable (Transact-SQL)](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
 [Таблица &#40; Transact-SQL &#41;](../../t-sql/data-types/table-transact-sql.md)  
  
  