---
title: "sp_wait_for_database_copy_sync (база данных SQL Azure) | Документы Microsoft"
ms.custom: 
ms.date: 03/03/2017
ms.prod: 
ms.prod_service: database-engine, sql-database
ms.reviewer: 
ms.service: sql-database
ms.component: system-stored-procedures
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_wait_for_database_copy_sync_TSQL
- sp_wait_for_database_copy_sync
dev_langs: TSQL
helpviewer_keywords: sp_wait_for_database_copy_sync
ms.assetid: 7068da7f-cb74-47f2-b064-eb076a0d3885
caps.latest.revision: "13"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c7b2d41c9c87b483ab500ad351361a511ca66004
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/17/2017
---
# <a name="active-geo-replication---spwaitfordatabasecopysync"></a>Активная Георепликация - sp_wait_for_database_copy_sync
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Использование этой процедуры ограничено связью [!INCLUDE[ssGeoDR](../../includes/ssgeodr-md.md)] между источником и получателем. Вызов **sp_wait_for_database_copy_sync** приводит к подождать, пока все зафиксированные транзакции репликации и подтверждения, активная вторичная база данных приложения. Запустите **sp_wait_for_database_copy_sync** только в основной базе данных.  
  
||  
|-|  
|**Область применения**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].|  
  
## <a name="syntax"></a>Синтаксис  
  
```  
sp_wait_for_database_copy_sync [ @target_server = ] 'server_name'   
     , [ @target_database = ] 'database_name'  
```  
  
## <a name="arguments"></a>Аргументы  
 [ @target_server =] «имя_сервера»  
 Имя сервера базы данных SQL, на котором размещена активная база данных-получатель. Аргумент server_name имеет тип sysname и не имеет значения по умолчанию.  
  
 [ @target_database =] 'имя_базы_данных»  
 Имя активной базы данных-получателя. Аргумент database_name имеет тип sysname и не имеет значения по умолчанию.  
  
## <a name="return-code-values"></a>Значения кода возврата  
 Возвращает 0 при успешном завершений и номера ошибки в случае сбоя.  
  
 Наиболее вероятные условия возникновения ошибок:  
  
-   Отсутствует имя сервера или базы данных.  
  
-   Невозможно найти ссылку на заданное имя сервера или базы данных.  
  
-   Потеряно подключение к Interlink. **sp_wait_for_database_copy_sync** вернет после истечения времени ожидания соединения.  
  
## <a name="permissions"></a>Permissions  
 Эту системную хранимую процедуру может вызывать любой пользователь в базе данных-источнике. Имя входа должно быть пользователем и в базе данных-источнике, и в активной базе данных-получателе.  
  
## <a name="remarks"></a>Замечания  
 Все транзакции, зафиксированные до **sp_wait_for_database_copy_sync** вызов отправляются активную вторичную базу данных.  
  
## <a name="examples"></a>Примеры  
 В следующем примере вызывается **sp_wait_for_database_copy_sync** убедитесь, что все транзакции фиксируются в основной базе данных, db0, будут возвращены его активную вторичную базу данных на целевом сервере ubfyu5ssyt.  
  
```  
USE db0;  
GO  
EXEC sys.sp_wait_for_database_copy_sync @target_server = N'ubfyu5ssyt1', @target_database = N'db0';  
GO  
```  
  
## <a name="see-also"></a>См. также:  
 [sys.dm_continuous_copy_status &#40; База данных Azure SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-continuous-copy-status-azure-sql-database.md)   
 [Георепликация динамические административные представления и функции &#40; База данных Azure SQL &#41;](../../relational-databases/system-dynamic-management-views/geo-replication-dynamic-management-views-and-functions-azure-sql-database.md)  
  
  