---
title: "ALTER SERVICE MASTER KEY (Transact-SQL) | Документы Microsoft"
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
- ALTER_SERVICE_MASTER_KEY_TSQL
- ALTER SERVICE MASTER KEY
dev_langs:
- TSQL
helpviewer_keywords:
- REGENERATE phrase
- FORCE option
- ALTER SERVICE MASTER KEY statement
- cryptography [SQL Server], Service Master Key
- modifying Service Master Key
- decryption [SQL Server], Service Master Key
- encryption [SQL Server], Service Master Key
- service master key [SQL Server], modifying
ms.assetid: a1e9be0e-4115-47d8-9d3a-3316d876a35e
caps.latest.revision: 41
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4ee9fd8a888ed796b4d01b007aec5f8217cce5d9
ms.contentlocale: ru-ru
ms.lasthandoff: 09/01/2017

---
# <a name="alter-service-master-key-transact-sql"></a>ALTER SERVICE MASTER KEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Изменяет главный ключ службы экземпляра [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Значок ссылки на раздел](../../database-engine/configure-windows/media/topic-link.gif "Значок ссылки на раздел") [Синтаксические обозначения в Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
ALTER SERVICE MASTER KEY   
    [ { <regenerate_option> | <recover_option> } ] [;]  
  
<regenerate_option> ::=  
    [ FORCE ] REGENERATE  
  
<recover_option> ::=  
    { WITH OLD_ACCOUNT = 'account_name' , OLD_PASSWORD = 'password' }  
    |      
    { WITH NEW_ACCOUNT = 'account_name' , NEW_PASSWORD = 'password' }  
```  
  
## <a name="arguments"></a>Аргументы  
 FORCE  
 Указывает, что главный ключ службы должен быть принудительно создан повторно, даже если это может привести к потере данных. Дополнительные сведения см. в разделе [изменение учетной записи службы SQL Server](#_changing) далее в этом разделе.  
  
 REGENERATE  
 Указывает, что главный ключ службы должен быть создан повторно.  
  
 OLD_ACCOUNT **= "***account_name***"**  
 Указывает имя старой учетной записи службы Windows.  
  
> [!WARNING]  
>  Данный параметр является устаревшим. Не используйте. Взамен используйте диспетчер конфигурации [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 OLD_PASSWORD **= "***пароль***"**  
 Указывает пароль старой учетной записи службы Windows.  
  
> [!WARNING]  
>  Данный параметр является устаревшим. Не используйте. Взамен используйте диспетчер конфигурации [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 NEW_ACCOUNT **= "***account_name***"**  
 Указывает имя новой учетной записи службы Windows.  
  
> [!WARNING]  
>  Данный параметр является устаревшим. Не используйте. Взамен используйте диспетчер конфигурации [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Новый_пароль **= "***пароль***"**  
 Указывает пароль новой учетной записи службы Windows.  
  
> [!WARNING]  
>  Данный параметр является устаревшим. Не используйте. Взамен используйте диспетчер конфигурации [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="remarks"></a>Замечания  
 Главный ключ службы автоматически создается в первый раз, когда он требуется для шифрования пароля связанного сервера, учетных данных или главного ключа базы данных. Главный ключ службы шифруется с помощью ключа локального компьютера или интерфейса API защиты данных Windows. Этот API использует ключ, получаемый из учетных данных Windows, которые соответствуют учетной записи службы для [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] использует для защиты главного ключа службы и главного ключа базы данных алгоритм шифрования AES. AES - это новый алгоритм шифрования, отличный от алгоритма 3DES, используемого в более ранних версиях. После обновления экземпляра компонента [!INCLUDE[ssDE](../../includes/ssde-md.md)] до [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] необходимо заново сформировать главный ключ службы и главный ключ базы данных, чтобы обновить главные ключи до алгоритма AES. Дополнительные сведения о повторном создании главного ключа базы данных см. в статье [ALTER MASTER KEY (Transact-SQL)](../../t-sql/statements/alter-master-key-transact-sql.md).  
  
##  <a name="_changing"></a>Изменение учетной записи службы SQL Server  
 Чтобы изменить учетную запись службы [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], используйте диспетчер конфигурации [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Для управления учетной записью службы и изменения записи [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] хранит дополнительную копию главного ключа службы, защищенную учетной записью компьютера, которая обладает необходимыми разрешениями, предоставляемыми группе служб [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Если выполняется перестроение компьютера, то главный ключ службы может быть восстановлен тем же пользователем домена, который раньше использовался учетной записью службы. Это не работает с локальные учетные записи или учетные записи локальной системы, локальной службы или сетевой службы. Если производится обновление [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] на другой компьютер, выполните миграцию главного ключа службы с помощью резервного копирования и восстановления.  
  
 Фраза REGENERATE повторно создает главный ключ службы. При повторном создании главного ключа службы [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] расшифровывает все ключи, которые были зашифрованы главным ключом, а затем шифрует их новым главным ключом службы. Эта операция требовательна к вычислительным ресурсам. Рекомендуется назначать ее выполнение на периоды низкой загрузки системы, кроме случаев получения несанкционированного доступа к ключу. В случае ошибки любой из операций дешифрования выполнение инструкции в целом также завершается ошибкой.  
  
 Установка параметра FORCE вызывает продолжение процесса повторного создания ключа даже в том случае, когда не удается получить текущий главный ключ или расшифровать все зашифрованные им закрытые ключи. Используйте параметр FORCE, только в том случае, если восстановление завершается ошибкой и невозможно восстановить главный ключ службы с помощью [RESTORE SERVICE MASTER KEY](../../t-sql/statements/restore-service-master-key-transact-sql.md) инструкции.  
  
> [!CAUTION]  
>  Главный ключ службы является корнем иерархии шифрования [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Главный ключ службы прямо или непрямо защищает все другие ключи и секретные данные в иерархии шифрования. Если зависящий от него ключ не удастся расшифровать во время принудительного повторного создания главного ключа, то защищаемые этим ключом данные будут потеряны.  
  
 При перемещении SQL на другой компьютер следует использовать одну и ту же учетную запись службы для дешифрования главного ключа службы — SQL Server фиксирует шифрование учетной записи компьютера автоматически.  
  
## <a name="permissions"></a>Permissions  
 Необходимо разрешение CONTROL SERVER на сервер.  
  
## <a name="examples"></a>Примеры  
 Следующий пример иллюстрирует повторное создание главного ключа службы.  
  
```  
ALTER SERVICE MASTER KEY REGENERATE;  
GO  
```  
  
## <a name="see-also"></a>См. также:  
 [ВОССТАНОВЛЕНИЕ главного ключа службы &#40; Transact-SQL &#41;](../../t-sql/statements/restore-service-master-key-transact-sql.md)   
 [Резервная копия главного ключа службы &#40; Transact-SQL &#41;](../../t-sql/statements/backup-service-master-key-transact-sql.md)   
 [Иерархия шифрования](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  