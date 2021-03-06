---
title: sys.dm_db_mirroring_auto_page_repair (Transact-SQL) | Документация Майкрософт
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_db_mirroring_auto_page_repair_TSQL
- sys.dm_db_mirroring_auto_page_repair_TSQL
- sys.dm_db_mirroring_auto_page_repair
- dm_db_mirroring_auto_page_repair
dev_langs:
- TSQL
helpviewer_keywords:
- automatic page repair
- database mirroring [SQL Server], automatic page repair
- sys.dm_db_mirroring_auto_page_repair dynamic management view
ms.assetid: 49f0fc2a-e25e-47e1-a135-563adb509af1
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 976992cfe5d68659b95a62cc0b4e839f19f8cdd4
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/01/2018
ms.locfileid: "47638432"
---
# <a name="database-mirroring---sysdmdbmirroringautopagerepair"></a>Базы данных зеркальное отображение — sys.dm_db_mirroring_auto_page_repair
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Возвращает строку для каждой попытки автоматического восстановления страниц во всех зеркально отображаемых баз данных на экземпляре сервера. Представление содержит строки, связанные с последними попытками автоматического восстановления страниц в определенной зеркальной базе данных, с максимальным количеством 100 строк на каждую базу данных. По достижении максимального значения строка для следующей попытки автоматического восстановления страниц заменяет одну из существующих записей. В следующей таблице дается определение значения столбцов.  
  
|Имя столбца|Тип данных|Описание|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|Идентификатор базы данных, которой принадлежит строка.|  
|**file_id**|**int**|Идентификатор файла, в котором находится страница.|  
|**page_id**|**bigint**|Идентификатор страницы в файле.|  
|**error_type**|**int**|Тип ошибки. Допустимые значения:<br /><br /> **-** 1 = все ошибки 823 оборудования<br /><br /> 1 = 824 ошибки, кроме неверной контрольной сумме или обрыву страницы (например, неверный идентификатор страницы)<br /><br /> 2 = неверная контрольная сумма;<br /><br /> 3 = разрыв страницы.|  
|**page_status**|**int**|Состояние попытки восстановления страниц:<br /><br /> 2 = в очереди на запрос к участнику;<br /><br /> 3 = запрос отправлен участнику;<br /><br /> 4 = в очереди на автоматическое восстановление страниц (от участника получен ответ);<br /><br /> 5 = автоматическое восстановление страниц успешно завершено, и страница должна быть готова к использованию;<br /><br /> 6 = непоправимо повреждена. Во время попытки восстановления страниц произошла ошибка, например потому, что страница также повреждена на участнике, или участник не подключен, или возникли проблемы с сетью. Это состояние не окончательное: если на странице вновь встретится повреждение, она будет запрошена у участника.|  
|**modification_time**|**datetime**|Время последнего изменения состояния страницы.|  
  
## <a name="security"></a>безопасность  
  
### <a name="permissions"></a>Разрешения  
 необходимо разрешение VIEW SERVER STATE на сервере.  
  
## <a name="see-also"></a>См. также  
 [Автоматическое восстановление страниц (группы доступности: зеркальное отображение баз данных)](../../sql-server/failover-clusters/automatic-page-repair-availability-groups-database-mirroring.md)   
 [Динамические административные представления и функции (Transact-SQL)](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [suspect_pages &#40;Transact-SQL&#41;](../../relational-databases/system-tables/suspect-pages-transact-sql.md)   
 [Управление таблицей suspect_pages (SQL Server)](../../relational-databases/backup-restore/manage-the-suspect-pages-table-sql-server.md)  
  
  


