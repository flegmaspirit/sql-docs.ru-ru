---
title: Настройка предупреждений для уведомления администраторов политик об ошибках политик | Документация Майкрософт
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, configure alerts
ms.assetid: e8e60159-d5b0-49d5-91f3-af8e9cb994c1
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 2587224e61e79bff0606c57b6ff47c2e0c29124f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/01/2018
ms.locfileid: "47601232"
---
# <a name="configure-alerts-to-notify-policy-administrators-of-policy-failures"></a>Настройка предупреждений для уведомления администраторов политик об ошибках политик
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Если при управлении на основе политик в одном из трех автоматизированных режимов оценки возникает нарушение политики, то сообщение об этом записывается в журнал событий. Для уведомления о записи этого сообщения в журнал событий можно создать предупреждение, определяющее сообщение и выполняющее действие. Предупреждение должно определять сообщения, как показано в следующей таблице.  
  
|Режим выполнения|Номер сообщения|  
|--------------------|--------------------|  
|При изменении: запретить<br /><br /> (если авто)|34050|  
|При изменении: запретить<br /><br /> (если по запросу)|34051|  
|По расписанию|34052|  
|При изменении|34053|  
  
 Сведения о настройке предупреждений в ответ на сообщения об ошибках управления на основе политик см. в следующих разделах:  
  
-   [Создание оператора](../../ssms/agent/create-an-operator.md)  
  
-   [Создание предупреждения по номеру сообщения](../../ssms/agent/create-an-alert-using-an-error-number.md)  
  
-   [Назначение предупреждений оператору](../../ssms/agent/assign-alerts-to-an-operator.md)  
  
## <a name="permissions"></a>Разрешения  
 Когда политики вычисляются по запросу, они выполняются в контексте безопасности пользователя. Для записи в журнал ошибок пользователь должен иметь разрешения ALTER TRACE или быть членом предопределенной роли сервера sysadmin. Политики, вычисляемые пользователем, обладающим меньшими правами доступа, не регистрируются в журнале событий и не формируют предупреждений.  
  
 Автоматизированные режимы выполнения работают от имени члена роли sysadmin. Это позволяет политике регистрировать ошибки в журнале ошибок и формировать предупреждение.  
  
## <a name="additional-considerations-about-alerts"></a>Дополнительные сведения о предупреждениях  
 Примите во внимание следующие дополнительные сведения о предупреждениях.  
  
-   Предупреждения формируются только для включенных политик. Так как политики **По запросу** нельзя включить, то для них предупреждения не формируются.  
  
-   Если действие, которое необходимо предпринять, включает отправку сообщения по электронной почте, необходимо настроить учетную запись электронной почты. Рекомендуется использовать компонент Database Mail. Дополнительные сведения о настройке компонента Database Mail см. в разделе [Создание учетной записи компонента Database Mail](../../relational-databases/database-mail/create-a-database-mail-account.md).  
  
  
