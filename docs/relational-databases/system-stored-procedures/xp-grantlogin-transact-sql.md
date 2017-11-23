---
title: "xp_grantlogin (Transact-SQL) | Документы Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- xp_grantlogin
- xp_grantlogin_TSQL
dev_langs: TSQL
helpviewer_keywords: xp_grantlogin
ms.assetid: c851c1ab-3b29-4b99-9902-78c2665a844b
caps.latest.revision: "25"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 401ec8c4b43bf95de2b7d7a6b9cadaa3d3a038f2
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/21/2017
---
# <a name="xpgrantlogin-transact-sql"></a>xp_grantlogin (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Предоставляет группе или пользователю Windows доступ к [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]Используйте [CREATE LOGIN](../../t-sql/statements/create-login-transact-sql.md) вместо него.  
  
||  
|-|  
|**Область применения**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (с[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] до [текущей версии](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
 ![Значок ссылки на раздел](../../database-engine/configure-windows/media/topic-link.gif "Значок ссылки на раздел") [Синтаксические обозначения в Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
xp_grantlogin {[@loginame = ] 'login'} [,[@logintype = ] 'logintype']  
```  
  
## <a name="arguments"></a>Аргументы  
 [  **@loginame =** ] **"***входа***"**  
 Имя добавляемого пользователя или группы Windows. Пользователь или группа Windows должны быть дополнены именем домена Windows в виде *домена*\\*пользователя*. *Имя входа* — **sysname**, не имеет значения по умолчанию.  
  
 [  **@logintype =** ] **"***logintype***"**  
 Уровень безопасности входного имени, которому предоставляется доступ. *logintype* — **varchar(5)**, значение по умолчанию NULL. Только **администратора** можно указать. Если **администратора** указано, *входа* предоставляется доступ к [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]и добавлен в качестве члена **sysadmin** предопределенной роли сервера.  
  
## <a name="return-code-values"></a>Значения кода возврата  
 0 (успешное завершение) или 1 (неуспешное завершение)  
  
## <a name="remarks"></a>Замечания  
 **xp_grantlogin** теперь системной хранимой процедурой, а не расширенной хранимой процедуры. **xp_grantlogin** вызовы **sp_grantlogin** и **sp_addsrvrolemember**.  
  
## <a name="permissions"></a>Permissions  
 Требуется членство в **securityadmin** предопределенной роли сервера. При изменении *logintype*, требуется членство в **sysadmin** предопределенной роли сервера.  
  
## <a name="see-also"></a>См. также:  
 [Хранимая процедура sp_denylogin (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-denylogin-transact-sql.md)   
 [Хранимая процедура sp_grantlogin (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [Системные хранимые процедуры (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Общие расширенные хранимые процедуры &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql.md)   
 [xp_enumgroups &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/xp-enumgroups-transact-sql.md)   
 [xp_loginconfig &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/xp-loginconfig-transact-sql.md)   
 [xp_logininfo &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/xp-logininfo-transact-sql.md)   
 [sp_revokelogin &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-revokelogin-transact-sql.md)  
  
  