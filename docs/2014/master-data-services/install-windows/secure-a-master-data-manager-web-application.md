---
title: Обеспечение безопасности веб-приложения диспетчера основных данных | Документы Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: e360ba3a-e96b-4f85-b588-ed1f767fa973
caps.latest.revision: 8
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 3316a5469e6b5420178ae34a40ae4e2f9f0abd70
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/02/2018
ms.locfileid: "37231344"
---
# <a name="secure-a-master-data-manager-web-application"></a>Обеспечение безопасности веб-приложения диспетчера основных данных
  Веб-приложение [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] можно обезопасить с помощью протокола HTTPS.  
  
> [!NOTE]  
>  Веб-приложение [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] может использовать протокол HTTP или HTTPS, но не оба.  
  
## <a name="prerequisites"></a>предварительные требования  
 Выполнение процедуры  
  
-   На веб-сервере, где установлен экземпляр служб [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] , нужно обладать правами администратора.  
  
-   Службы MDS должны быть установлены на веб-сервере, а веб-приложение должно существовать. Дополнительные сведения см. в статьях [Установка служб Master Data Services](install-master-data-services.md) и [Create a Master Data Manager Web Application &#40;Master Data Services&#41;](create-a-master-data-manager-web-application-master-data-services.md).  
  
### <a name="to-secure-the-master-data-manager-web-application-with-https"></a>Обеспечение безопасности веб-приложения диспетчера основных данных с помощью протокола HTTPS  
  
1.  После подтверждения того, что веб-приложение [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] имеет верные настройки протокола HTTP, создайте сертификат на сервере служб IIS. Дополнительные сведения см. в разделе [Настройка сертификатов сервера IIS 7](http://technet.microsoft.com/library/cc732230\(WS.10\).aspx).  
  
2.  На панели **Соединения** на вкладке **Сайты**щелкните сайт, на котором размещено веб-приложение [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] .  
  
3.  На панели **Действия** щелкните **Привязки**.  
  
4.  Нажмите кнопку **Добавить**.  
  
5.  Выберите **https**из списка.  
  
6.  Выберите SSL-сертификат.  
  
7.  Нажмите кнопку **ОК**.  
  
8.  Необязательный параметр. Чтобы удалить из списка протокол HTTP, разрешив доступ к сайту только по протоколу HTTPS, щелкните строку **http**. Нажмите кнопку **Удалить** и в диалоговом окне подтверждения выберите **Да**.  
  
    > [!IMPORTANT]  
    >  Необходимо изменить настройки basicHttp и wsHttpBinding после удаления HTTP.  
  
9. Чтобы закрыть диалоговое окно **Привязки сайтов** , нажмите кнопку **Закрыть**.  
  
10. Теперь откройте файл web.config из *диск*: \Program Files\Microsoft SQL Server\120\Master Data Services\WebApplication.  
  
11. Найдите строку `<security mode="Message">` и измените ее на строку `<security mode="Transport">`.  
  
12. Сохраните файл и закройте его. Если возникает ошибка, это происходит из-за включенного контроля учетных записей. Дополнительные сведения см. в разделе [Отключение контроля учетных записей](http://technet.microsoft.com/library/cc709691\(WS.10\).aspx). Теперь пользователи могут использовать для доступа к сайту протокол HTTPS.  
  
## <a name="see-also"></a>См. также  
 [Создание веб-приложения диспетчера основных данных (службы Master Data Services)](create-a-master-data-manager-web-application-master-data-services.md)  
  
  