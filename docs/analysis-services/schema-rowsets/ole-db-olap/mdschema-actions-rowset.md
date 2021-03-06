---
title: Набор строк схемы MDSCHEMA_ACTIONS | Документы Microsoft
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 0b2e2967b1b01c56801235b88220ea13be3b8e65
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/10/2018
---
# <a name="mdschemaactions-rowset"></a>Набор строк MDSCHEMA_ACTIONS
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Описывает действия, доступные для клиентского приложения.  
  
## <a name="rowset-columns"></a>Столбцы наборов строк  
 **MDSCHEMA_ACTIONS** набор строк содержит следующие столбцы.  
  
|Имя столбца|Индикатор типа|Длина|Описание|  
|-----------------|--------------------|------------|-----------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**||Имя базы данных.|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**||Не поддерживается. Всегда содержит **VT_NULL**.|  
|**CUBE_NAME**|**DBTYPE_WSTR**||Имя куба, которому принадлежит это действие.|  
|**ИМЯ_ДЕЙСТВИЯ**|**DBTYPE_WSTR**||Имя этого действия.|  
|**ACTION_TYPE**|**DBTYPE_I4**||Битовая карта, которая служит для задания метода срабатывания действия. В файле Msmd.h определены следующие битовые константы для этой битовой карты.<br /><br /> **MDACTION_TYPE_URL** (**0x01**)<br /><br /> **MDACTION_TYPE_HTML** (**0x02**)<br /><br /> **MDACTION_TYPE_STATEMENT** (**0x04**)<br /><br /> **MDACTION_TYPE_DATASET** (**0x08**)<br /><br /> **MDACTION_TYPE_ROWSET** (**0x10**)<br /><br /> **MDACTION_TYPE_COMMANDLINE** (**0x20**)<br /><br /> **MDACTION_TYPE_PROPRIETARY** (**0x40**)<br /><br /> **MDACTION_TYPE_REPORT** (**0x80**)<br /><br /> **MDACTION_TYPE_DRILLTHROUGH** (**0x100**)|  
|**КООРДИНАТЫ**|**DBTYPE_WSTR**||Многомерное выражение, указывающее объект или координату в многомерном пространстве, в котором выполняется действие. За передачу значения этого столбца ограничений отвечает клиентское приложение.<br /><br /> **CORDINATE** должен разрешаться в объект, указанный в **COORDINATE_TYPE**.|  
|**COORDINATE_TYPE**|**DBTYPE_I4**||Битовая карта, указывающая как **КООРДИНАЦИИ** интерпретации столбца ограничений. В файле Msmd.h определены следующие битовые константы для этой битовой карты.<br /><br /> **MDACTION_COORDINATE_CUBE** (**1**)<br /><br /> **MDACTION_COORDINATE_DIMENSION** (**2**): ссылается на иерархии измерений.<br /><br /> **MDACTION_COORDINATE_LEVEL** (**3**)<br /><br /> **MDACTION_COORDINATE_MEMBER** (**4**)<br /><br /> **MDACTION_COORDINATE_SET** (**5**)<br /><br /> **MDACTION_COORDINATE_CELL** (**6**)|  
|**ACTION_CAPTION**|**DBTYPE_WSTR**||Имя действия, если заголовок не указан и в DDL не заданы переводы.<br /><br /> Если заголовок или перевод указаны, и **CaptionIsMDX** имеет значение false, один из следующих строк:<br /><br /> -Перевод для соответствующего языка.<br /><br /> -Указанный заголовок, если для указанного языка перевод не найден.<br /><br /> -Имя действия, если перевод не найден и заголовок не указан в инструкции DDL.<br /><br /> Если заголовок или перевод указаны, и **CaptionIsMDX** имеет значение true, строка, являющаяся результатом поиска соответствующего перевода для указанного языка или указанного перевода в DDL и вычисления Формула для создания строки.<br /><br /> Если действие задано в скрипте многомерных выражений, то перевод отсутствует, а заголовок всегда рассматривается как многомерное выражение.|  
|**DESCRIPTION**|**DBTYPE_WSTR**||Понятное описание действия.|  
|**CONTENT**|**DBTYPE_WSTR**||Выражение или содержимое действия, которое должно быть запущено.|  
|**ПРИЛОЖЕНИЯ**|**DBTYPE_WSTR**||Имя приложения, используемого для запуска действия.|  
|**ВЫЗОВ**|**DBTYPE_I4**||Сведения о способе вызова действия.<br /><br /> **MDACTION_INVOCATION_INTERACTIVE** (**1**) указывает на регулярное действие, используемые во время обычной работы. Это значение по умолчанию для этого столбца.<br /><br /> **MDACTION_INVOCATION_ON_OPEN** (**2**) указывает, что действие должно выполняться при первом открытии куба.<br /><br /> **MDACTION_INVOCATION_BATCH** (**4**) указывает, что действие выполняется как часть пакетной операции или [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] задачи.<br /><br /> <br /><br /> Обратите внимание, что эти значения перечисления определены в файле Msmd.h.|  
  
 Набор строк отсортирован по **CATALOG_NAME**, **имя_схемы**, **CUBE_NAME**, **имя_действия**.  
  
> [!NOTE]  
>  Действия **MDACTION_TYPE_PROPRIETARY** тип должен предоставить значение для **приложения** столбца.  
  
## <a name="restriction-columns"></a>Столбцы ограничений  
 **MDSCHEMA_ACTIONS** строк может быть ограничен столбцами, перечисленными в следующей таблице.  
  
|Имя столбца|Индикатор типа|Состояние ограничения|  
|-----------------|--------------------|-----------------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|Необязательно|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**|Необязательно|  
|**CUBE_NAME**|**DBTYPE_WSTR**|Обязательный|  
|**ИМЯ_ДЕЙСТВИЯ**|**DBTYPE_WSTR**|Необязательно|  
|**ACTION_TYPE**|**DBTYPE_I4**|Необязательно|  
|**КООРДИНАТЫ**|**DBTYPE_WSTR**|Обязательный|  
|**COORDINATE_TYPE**|**DBTYPE_I4**|Обязательный|  
|**ВЫЗОВ**|**DBTYPE_I4**|(Необязательно) **ВЫЗОВ** столбца ограничений по умолчанию используется значение **MDACTION_INVOCATION_INTERACTIVE**. Получить все действия с помощью **MDACTION_INVOCATION_ALL** значение в **ВЫЗОВ** столбец ограничений.|  
|**CUBE_SOURCE**|**DBTYPE_UI2**|(Необязательно) Ограничение по умолчанию имеет значение 1. Битовая карта с одним из следующих допустимых значений:<br /><br /> 1 CUBE<br /><br /> 2 DIMENSION|  
  
> [!IMPORTANT]  
>  **ВЫЗОВ** столбца ограничений имеет значение по умолчанию **MDACTION_INVOCATION_INTERACTIVE**. Набор строк схемы, который не задает явным образом значения для этого столбца, содержит только строки с этим значением. Строк, который должен содержать весь набор действий, используйте **MDACTION_INVOCATION_ALL** константы в **ВЫЗОВ** столбец ограничений.  
  
 Клиентские приложения могут определить несколько **ACTION_TYPE** с помощью оператора OR.  
  
## <a name="remarks"></a>Примечания  
 В следующей таблице перечислены допустимые **КООРДИНАЦИИ** и **COORDINATE_TYPE** комбинации.  
  
|Тип объекта COORDINATE|COORDINATE_TYPE|  
|----------------------------|----------------------|  
|**Cube**|**MDACTION_COORDINATE_CUBE**|  
|**Измерения**|**MDACTION_COORDINATE_DIMENSION**<br /><br /> **MDACTION_COORDINATE_LEVEL**<br /><br /> **MDACTION_COORDINATE_MEMBER**<br /><br /> **MDACTION_COORDINATE_SET**<br /><br /> **MDACTION_COORDINATE_CELL**|  
|**Иерархия**|**MDACTION_COORDINATE_DIMENSION**|  
|**Level**|**MDACTION_COORDINATE_LEVEL**|  
|**Член**|**MDACTION_COORDINATE_MEMBER**|  
|**Набор**|**MDACTION_COORDINATE_SET**|  
|**Ячейки**|**MDACTION_COORDINATE_CELL**|  
  
## <a name="see-also"></a>См. также  
 [OLE DB для OLAP наборы строк схемы](../../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)  
  
  
