---
title: Интеграция служб Reporting Services в приложения | Документы Майкрософт
ms.date: 09/18/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: application-integration
ms.topic: reference
author: markingmyname
ms.author: maghan
monikerRange: = sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: f68945ab92db13f80236cfa900067a7d38533849
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/01/2018
ms.locfileid: "47614122"
---
# <a name="integrating-reporting-services-into-applications"></a>Интеграция служб Reporting Services в приложения

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-not-2017](../../includes/ssrs-appliesto-not-2017.md)] [!INCLUDE [ssrs-appliesto-not-pbirs](../../includes/ssrs-appliesto-not-pbirs.md)]

  Службы [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] представляют собой открытую и расширяемую платформу создания отчетов, которая позволяет предоставить разработчикам всеобъемлющий набор API для разработки решений.

> [!NOTE]
> Начиная с SQL Server 2017 Reporting Services, для разработки решений используется доступ через API REST. Доступ через API SOAP является нерекомендуемым. Дополнительные сведения см. в разделе [Разработка с помощью API REST для служб Reporting Services](../developer/rest-api.md).
  
 Предусмотрены три способа интеграции служб [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] в пользовательские приложения: веб-служба сервера отчетов, которую также называют SOAP API [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], элементы управления средства просмотра отчетов для [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] и средства доступа по URL-адресу. В каждом из этих вариантов реализуется отдельный подход к интеграции служб [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] в приложения.
  
## <a name="report-server-web-service"></a>Веб-служба сервера отчетов

 Веб-служба сервера отчетов является основным интерфейсом разработки приложений служб [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Эта веб-служба предоставляет все необходимые методы для интеграции служб [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] в приложения, независимо от того, ведется ли разработка кода для управления каталогом отчетов или для подготовки отчетов в поддерживаемом формате. Примером такого приложения может служить диспетчер отчетов, входящий в комплект поставки службы [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]; в нем веб-служба используется для управления базой данных сервера отчетов.  
  
## <a name="report-viewer-controls-for-visual-studio"></a>Элементы управления средства просмотра отчетов для Visual Studio

 Элементы управления средства просмотра отчетов, включенные в состав [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)], используются для интеграции средств просмотра отчетов в приложения. Имеется два элемента управления: один для приложений на основе Windows Forms, а другой — для приложений Web Forms. Каждый элемент управления обеспечивает возможность просмотра отчетов, развернутых на сервере отчетов, а также возможность отображения отчетов, существующих в среде, где сервер отчетов пока еще не установлен.  
  
## <a name="url-access"></a>доступ по URL-адресу  
 Доступ по URL-адресу представляет собой еще один метод интеграции средств просмотра отчетов в приложения; он используется в случаях, когда применение элементов управления средства просмотра отчетов не представляется возможным. Метод доступа по URL-адресу также позволяет отправлять пользователям ссылки на отчеты по электронной почте.  
  
## <a name="in-this-section"></a>В этом разделе

 [Интеграция служб Reporting Services с использованием протокола SOAP](../../reporting-services/application-integration/integrating-reporting-services-using-soap.md)  
 Описывает способ интеграции средств навигации по отчетам и управления отчетами служб [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] в существующие бизнес-приложения с помощью веб-службы сервера отчетов.  
  
 [Интеграция служб Reporting Services с помощью элементов управления средства просмотра отчетов](../../reporting-services/application-integration/integrating-reporting-services-using-reportviewer-controls.md)  
 Описывает способ интеграции средств просмотра отчетов в существующие приложения с помощью элементов управления средства просмотра отчетов.  
  
 [Интеграция служб Reporting Services с использованием URL-адресов](../../reporting-services/application-integration/integrating-reporting-services-using-url-access.md)  
 Описывает способ интеграции средств навигации по отчетам служб [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] в существующие бизнес-приложения с помощью доступа по URL-адресу.  
  
## <a name="next-steps"></a>Следующие шаги

Сведения о выборе между доступом по URL-адресу или API-интерфейсами SOAP см. в разделе [Выбор между доступом по URL-адресу и протоколом SOAP в службах Reporting Services](choosing-between-url-access-and-soap.md).

Сведения об API REST в SQL Server 2017 Reporting Services см. в разделе [Разработка с помощью API REST для служб Reporting Services](../developer/rest-api.md).

Остались вопросы? [Посетите форум служб Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231).
