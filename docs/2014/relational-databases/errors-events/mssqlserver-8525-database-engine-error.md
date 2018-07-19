---
title: MSSQLSERVER_8525 | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- "8525"
helpviewer_keywords:
- 8525 (Database Engine error)
ms.assetid: 297867c1-691e-4d6b-a3be-a7575015ecfa
caps.latest.revision: 9
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: adf88cf5e9982c3b02516cd69c186c2ac449f7cf
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/03/2018
ms.locfileid: "37425343"
---
# <a name="mssqlserver8525"></a>MSSQLSERVER_8525
    
## <a name="details"></a>Сведения  
  
|||  
|-|-|  
|Название продукта|SQL Server|  
|Идентификатор события|8525|  
|Источник события|MSSQLSERVER|  
|Компонент|SQLEngine|  
|Символическое имя||  
|Текст сообщения|Распределенная транзакция завершена. Прикрепите этот сеанс к новой транзакции или транзакции NULL.|  
  
## <a name="explanation"></a>Объяснение  
 Модель программирования, применяемая в координаторе распределенных транзакций с [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], требует, чтобы приложения явно прикреплялись к распределенным транзакциям и исключались из них.  
  
 Это происходит, если выполняются перечисленные ниже условия.  
  
-   Приложение прикреплено к распределенной транзакции.  
  
-   Транзакция завершилась фиксацией или откатом по любой причине.  
  
-   Приложение пользователя не отключилось явным образом от распределенной транзакции, либо не было явно прикреплено к новой.  
  
-   Приложение пытается выполнить транзакционную операцию, которая не является отключением от существующей распределенной транзакции или прикреплением к новой, например выполняет запрос или запускает локальную транзакцию.  
  
 Состояние ошибки 1 используется в тех случаях, когда приложение выполняет операцию, создающую локальные транзакции, а состояние 2 — когда приложение пытается прикрепиться к связанному сеансу.  
  
## <a name="user-action"></a>Действие пользователя  
 После того как приложение прикрепится к распределенной транзакции, оно должно явным образом отключиться от распределенной транзакции или присоединиться к другой распределенной транзакции. Это приведет к неявному отключению от предыдущей прикрепленной транзакции. Точный синтаксис отключения от распределенной транзакции или прикрепления к ней см. в руководстве по программному интерфейсу для приложения.  
  
  