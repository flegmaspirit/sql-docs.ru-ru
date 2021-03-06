---
title: Администрирование серверов при помощи среды SQL Server Management Studio | Документация Майкрософт
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Management Studio [SQL Server], servers
- servers [SQL Server], administering
ms.assetid: 938bb035-e07a-4082-9f93-229d9feb6b06
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: de4714d28808bc208154abbfba400f3ece888642
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/02/2018
ms.locfileid: "48196524"
---
# <a name="administer-servers-with-sql-server-management-studio"></a>Администрирование серверов при помощи среды SQL Server Management Studio
  [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] является функционально насыщенные, интегрированные административным клиентом, разработанным для решения задач [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] требования к управлению администратора сервера. В среде [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]задачи администрирования выполняются при помощи обозревателя объектов, который позволяет подключиться к любому серверу семейства [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] и просматривать его содержимое при помощи графических средств. Сервер может быть экземпляром компонента [!INCLUDE[ssDE](../includes/ssde-md.md)], службами [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] или службами [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)], [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].  
  
 В число средств среды [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] входят зарегистрированные серверы, обозреватель объектов, обозреватель решений, обозреватель шаблонов, страница сводки и окно документа. Чтобы отобразить средство, в меню **Вид** выберите его название. Для отображения редактора запросов нажмите кнопку **Создать запрос** на панели инструментов.  
  
> [!IMPORTANT]  
>  По умолчанию сетевой трафик между [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] и [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] не шифруется. Не работайте в среде [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] с конфиденциальными данными (включая пароли), не установив шифруемого соединения. Дополнительные сведения см. в разделе [Включение шифрования соединений в компоненте Database Engine (диспетчер конфигураций SQL Server)](../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md).  
  
 Используйте среду [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] для выполнения следующих действий:  
  
-   регистрации серверов;  
  
-   соединения с экземпляром компонента [!INCLUDE[ssDE](../includes/ssde-md.md)], службами [!INCLUDE[ssAS](../includes/ssas-md.md)], службами [!INCLUDE[ssRS](../includes/ssrs.md)] или службами [!INCLUDE[ssIS](../includes/ssis-md.md)];  
  
-   настройки свойств сервера;  
  
-   управления объектами базы данных и службами [!INCLUDE[ssAS](../includes/ssas-md.md)] , такими как кубы, измерения и сборки;  
  
-   создания таких объектов, как базы данных, таблицы, кубы, пользователи базы данных и имена входа;  
  
-   управления файлами и группами файлов;  
  
-   присоединения или отсоединения баз данных;  
  
-   запуска средств для работы со сценариями;  
  
-   управления безопасностью;  
  
-   просмотра системных журналов;  
  
-   контроля текущей активности;  
  
-   настройки репликации;  
  
-   управления полнотекстовыми индексами.  
  
 Для запуска и остановки [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] или агента [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] следует использовать диспетчер конфигурации [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
## <a name="see-also"></a>См. также  
 [Использование среды SQL Server Management Studio](../database-engine/use-sql-server-management-studio.md)   
 [Просмотр или изменение свойств сервера (SQL Server)](../database-engine/configure-windows/view-or-change-server-properties-sql-server.md)  
  
  
