---
title: Удаление заданий | Документация Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- delete jobs
ms.assetid: bffb915e-bc84-4417-aa35-183243ca3312
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 03e15a75d848f34fca9eab1961921ef7ff15fa0d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/01/2018
ms.locfileid: "47816224"
---
# <a name="delete-jobs"></a>удаление заданий
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> Сейчас в [управляемом экземпляре базы данных SQL Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) поддерживается большинство функций агента SQL Server (но не все). Подробные сведения см. в статье [Различия T-SQL между управляемым экземпляром базы данных SQL Azure и SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

Задание — это определенная последовательность действий, выполняемых агентом SQL Server. По умолчанию после завершения выполнения задания не удаляются. Можно удалить одно или несколько заданий агента [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , независимо от успешности завершения задания. В агенте [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] также можно настроить автоматическое удаление заданий в случае их успешного выполнения, сбоя или завершения.  
  
По умолчанию для удаления задания члены предопределенной роли сервера **sysadmin** могут выполнять хранимую системную процедуру [sp_delete_job (Transact-SQL)](http://msdn.microsoft.com/b85db6e4-623c-41f1-9643-07e5ea38db09) . Другим пользователям должна быть предоставлена одна из следующих предопределенных ролей базы данных агента [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] в базе данных **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
Дополнительные сведения о разрешениях этих ролей см. в разделе [Предопределенные роли базы данных агента SQL Server](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
Члены предопределенной роли сервера **sysadmin** с помощью процедуры **sp_delete_job** могут удалить любое задание. Пользователь, который не является членом предопределенной роли сервера **sysadmin** , может удалять только задания, принадлежащие этому пользователю.  
  
## <a name="related-tasks"></a>Связанные задачи  
  
|||  
|-|-|  
|**Описание**|**Раздел**|  
|Описывает, как удалить одно или несколько заданий агента [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|[Удаление одного или нескольких заданий](../../ssms/agent/delete-one-or-more-jobs.md)|  
|Описывает, как настроить автоматическое удаление заданий агента [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] в случае их успешного выполнения, сбоя или завершения.|[Automatically Delete a Job](../../ssms/agent/automatically-delete-a-job.md)|  
  
