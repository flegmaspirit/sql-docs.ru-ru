---
title: 'Свойства задания: Новое задание (страница "уведомления") | Документация Майкрософт'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql12.ag.job.notifications.f1
ms.assetid: ed393cbd-4496-4399-a177-e5baa92fb689
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e5bf1005f0c8bf6717cbbf66173eee1c1aa83873
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/02/2018
ms.locfileid: "48059127"
---
# <a name="job-properties-new-job-notifications-page"></a>Свойства задания: создание задания (страница "Уведомления")
  Используйте эту страницу для установки действий агента [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], выполняемых после завершения задания.  
  
## <a name="options"></a>Параметры  
 **Электронная почта**  
 Установите этот параметр для отправки электронной почты после завершения задания. Выбрав этот параметр, выберите оператора, которому будет направлено уведомление, и состояние, вызывающее его: **При успешном завершении задания**; **При ошибке задания**или **При завершении задания**.  
  
 **Страница**  
 Установите этот параметр для отправки электронной почты на пейджер оператора после завершения задания. Выбрав этот параметр, выберите оператора, которому будет направлено уведомление, и состояние, вызывающее его: **При успешном завершении задания**, **При ошибке задания**или **При завершении задания**.  
  
 **Команда Net send**  
 Выберите этот параметр для использования команды NET SEND для оповещения оператора о завершении задания. Выбрав этот параметр, выберите оператора, которому будет направлено уведомление, и состояние, вызывающее его: **При успешном завершении задания**, **При ошибке задания**или **При завершении задания**.  
  
 **Использовать журнал событий приложений Windows**  
 Выберите этот параметр для создания записи в журнале событий приложений при завершении выполнения задания. Выбрав этот параметр, выберите состояние, вызывающее запись в журнал: **При успешном завершении задания**, **При ошибке задания**или **При завершении задания**.  
  
 **Автоматически удалить задание**  
 Выберите этот параметр для автоматического удаления задания после его завершения. Выбрав этот параметр, выберите состояние, которое вызовет удаление задания: **При успешном завершении задания**, **При ошибке задания**или **При завершении задания**.  
  
## <a name="see-also"></a>См. также  
 [Реализация заданий](implement-jobs.md)   
 [Настройка почты агента SQL Server на использование компонента Database Mail](../../relational-databases/database-mail/configure-sql-server-agent-mail-to-use-database-mail.md)  
  
  
