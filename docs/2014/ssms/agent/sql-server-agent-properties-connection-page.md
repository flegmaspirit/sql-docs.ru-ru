---
title: Свойства агента SQL Server (страница "Подключение") | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql12.ag.agent.connection.f1
ms.assetid: d6a677ff-60ad-47ba-a0cb-df4193b165e0
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: db643175e7965f82f9c6741b22e09387dc893dff
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/02/2018
ms.locfileid: "48176054"
---
# <a name="sql-server-agent-properties-connection-page"></a>Свойства агента SQL Server (страница «Соединение»)
  Эта страница используется для просмотра и изменения настроек соединения службы агента [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] к [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="options"></a>Параметры  
 **Псевдоним локального сервера**  
 Указывает псевдоним, который применяется для подключения к локальному экземпляру [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Если невозможно использовать параметры соединения для агента [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] по умолчанию, определите псевдоним для экземпляра и укажите здесь псевдоним.  
  
 **Использовать проверку подлинности Windows**  
 В качестве метода проверки подлинности, используемого для подключения к экземпляру [!INCLUDE[msCoName](../../includes/msconame-md.md)] , устанавливается проверка подлинности [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Windows. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] подключается как учетная запись, под которой работает служба агента [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 **Использовать проверку подлинности SQL Server**  
 В качестве метода проверки подлинности, используемого для подключения к экземпляру сервера [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , устанавливается проверка подлинности [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] поддерживается для обратной совместимости. Для повышения безопасности, по возможности, используйте проверку подлинности Windows.  
  
 **Имя входа**  
 Указывается имя входа, используемое для подключения к [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **Пароль**  
 Указывается пароль, используемый для подключения к [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
  
