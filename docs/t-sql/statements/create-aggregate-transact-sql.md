---
title: "Создание статистической функции (Transact-SQL) | Документы Microsoft"
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
- CREATE_AGGREGATE_TSQL
- CREATE AGGREGATE
- AGGREGATE_TSQL
- AGGREGATE
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE AGGREGATE statement
- aggregate functions [SQL Server], user-defined
- user-defined functions [CLR integration]
ms.assetid: 62eebc19-9f15-4245-94fa-b3fcd64a9d42
caps.latest.revision: 50
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ad5cf36e97bf3903cc9d42ec5179de6375624f95
ms.contentlocale: ru-ru
ms.lasthandoff: 09/01/2017

---
# <a name="create-aggregate-transact-sql"></a>CREATE AGGREGATE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Создает определяемую пользователем агрегатную функцию, реализация которой определена в классе сборки платформы [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]. Чтобы компонент [!INCLUDE[ssDE](../../includes/ssde-md.md)] привязал агрегатную функцию к ее реализации, содержащая реализацию сборка платформы [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] должна быть сначала передана в экземпляр [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] с помощью инструкции CREATE ASSEMBLY.  
  
 ![Значок ссылки на раздел](../../database-engine/configure-windows/media/topic-link.gif "Значок ссылки на раздел") [Синтаксические обозначения в Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
CREATE AGGREGATE [ schema_name . ] aggregate_name  
        (@param_name <input_sqltype>   
        [ ,...n ] )  
RETURNS <return_sqltype>  
EXTERNAL NAME assembly_name [ .class_name ]  
  
<input_sqltype> ::=  
        system_scalar_type | { [ udt_schema_name. ] udt_type_name }  
  
<return_sqltype> ::=  
        system_scalar_type | { [ udt_schema_name. ] udt_type_name }  
  
```  
  
## <a name="arguments"></a>Аргументы  
 *schema_name*  
 Имя схемы, которой принадлежит определяемая пользователем агрегатная функция.  
  
 *aggregate_name*  
 Имя создаваемой агрегатной функции.  
  
 **@***param_name*  
 Один или несколько параметров в определяемой пользователем статистической функции. Значение параметра должно быть задано пользователем при выполнении агрегатной функции. Определяет имя параметра, используя знак «at» (**@**) в качестве первого символа. Имя параметра должно соответствовать правилам для [идентификаторы](../../relational-databases/databases/database-identifiers.md). Параметры являются локальными для функции.  
  
 *system_scalar_type*  
 Любой из системных скалярных типов данных [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] для хранения значения входного параметра или возвращаемого значения. Все скалярные типы данных могут использоваться как параметр для определяемой пользователем статистической функции, за исключением **текст**, **ntext**, и **изображения**. Использовать нескалярные типы, такие как **курсор** и **таблицы**, не может быть указан.  
  
 *udt_schema_name*  
 Имя схемы, к которой относится пользовательский тип данных среды CLR. Если не указан, [!INCLUDE[ssDE](../../includes/ssde-md.md)] ссылки *udt_type_name* в следующем порядке:  
  
-   собственное пространство имен типов SQL;  
  
-   в установленной по умолчанию для текущего пользователя схеме в текущей базе данных;  
  
-   Схема **dbo** в текущей базе данных.  
  
 *udt_type_name*  
 Название пользовательского типа среды CLR, созданного в текущей базе данных. Если *udt_schema_name* не указан, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] предполагается, что тип принадлежит к схеме текущего пользователя.  
  
 *assembly_name* [ **.** *class_name* ]  
 Указывает сборку, с которой связывается определяемая пользователем агрегатная функция и, при необходимости, имя схемы, к которой принадлежит сборка, и имя класса в сборке, реализующего определяемую пользователем статистическую функцию. Сборка уже должна быть создана в базе данных с помощью инструкции CREATE ASSEMBLY. *class_name* должен быть допустимым [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] идентификатор и совпадать с именем класса, который существует в сборке. *class_name* может быть имя, уточненное пространством имен, если язык программирования, используемый для написания класса используются пространства имен, например C#. Если *class_name* не указан, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] оно интерпретируется таким же, как *aggregate_name*.  
  
## <a name="remarks"></a>Замечания  
 По умолчанию возможность [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] запускать код CLR отключена. Можно создавать, изменять и удалять объекты базы данных, которые ссылаются на модули управляемого кода, но код в этих модулях не будет выполняться в экземпляре [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Если [параметр clr enabled](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md) включен с помощью [sp_ Настройка](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md).  
  
 Класс сборки, указанной в *assembly_name* и его методы должны соответствовать всем требованиям для реализации определяемой пользователем статистической функции в экземпляре [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Дополнительные сведения см. в разделе [пользовательские агрегатные функции](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-aggregates.md).  
  
## <a name="permissions"></a>Permissions  
 Требует разрешения CREATE AGGREGATE и разрешения REFERENCES для сборки, указанной в предложении EXTERNAL NAME.  
  
## <a name="examples"></a>Примеры  
 В следующем примере предполагается, что образец приложения StringUtilities.csproj скомпилирован. Дополнительные сведения см. в разделе [образца программы функции строка](http://msdn.microsoft.com/library/9623013f-15f1-4614-8dac-1155e57c880c).  
  
 Пример создает статистическое выражение `Concatenate`. Перед созданием статистического выражения в локальной базе данных регистрируется сборка `StringUtilities.dll`.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @SamplesPath nvarchar(1024)  
-- You may have to modify the value of the this variable if you have  
--installed the sample some location other than the default location.  
  
SELECT @SamplesPath = REPLACE(physical_name, 'Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA\master.mdf', 'Microsoft SQL Server\130\Samples\Engine\Programmability\CLR\')   
     FROM master.sys.database_files   
     WHERE name = 'master';  
  
CREATE ASSEMBLY StringUtilities FROM @SamplesPath + 'StringUtilities\CS\StringUtilities\bin\debug\StringUtilities.dll'  
WITH PERMISSION_SET=SAFE;  
GO  
  
CREATE AGGREGATE Concatenate(@input nvarchar(4000))  
RETURNS nvarchar(4000)  
EXTERNAL NAME [StringUtilities].[Microsoft.Samples.SqlServer.Concatenate];  
GO  
```  
  
## <a name="see-also"></a>См. также:  
 [DROP AGGREGATE &#40; Transact-SQL &#41;](../../t-sql/statements/drop-aggregate-transact-sql.md)  
  
  