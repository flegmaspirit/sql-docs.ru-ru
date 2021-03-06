---
title: Шаг 2. Проверка пакета развертывания | Документы Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
ms.assetid: 6c13f5c9-c75e-4e52-94dc-2d2db2c578fe
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 5a9f5ef250617b445ce30624537f715be73b3d2f
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/02/2018
ms.locfileid: "48102124"
---
# <a name="step-2-verifying-the-deployment-bundle"></a>Этап 2. Проверка пакета развертывания
  На занятии 1 был создан проект учебного развертывания и в него добавлены пакеты и вспомогательные файлы; в предыдущей задаче была построена программа развертывания для проекта.  
  
 В этой задаче будет проверено содержимое пакета развертывания. Пакет развертывания представляет собой папку, которая будет скопирована на целевой компьютер и использована для установки пакетов. Если было использовано значение по умолчанию — bin\Deployment — в качестве местонахождения для программы развертывания, пакетом развертывания будет папка Bin\Deployment в папке Deployment Tutorial в проекте [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
### <a name="to-verify-the-content-of-deployment-bundle"></a>Проверка содержимого пакета развертывания  
  
1.  Выберите папку bin\Deployment.  
  
2.  Проверьте наличие в папке следующих файлов:  
  
    -   DataTransfer.dtsx  
  
    -   datatransferconfig.dtsconfig  
  
    -   Deployment Tutorial.SSISDeploymentManifest  
  
    -   LoadXMLData.dtsx  
  
    -   loadxmldataconfig.dtsconfig  
  
    -   NewCustomers.txt  
  
    -   orders.xml  
  
    -   orders.xsd  
  
    -   Readme.txt  
  
3.  Щелкните правой кнопкой файл Deployment Tutorial.SSISDeploymentManifest, наведите указатель на пункт **Открыть с помощью**и выберите пункт **Internet Explorer**. Файл также можно открыть в текстовом редакторе, например в приложении «Блокнот». Код XML в файле должен быть таким:  
  
     `<?xml version="1.0"?><DTSDeploymentManifest GeneratedBy="Domain\UserName" GeneratedFromProjectName="Deployment Tutorial" GeneratedDate="2006-02-24T13:29:02.6537669-08:00" AllowConfigurationChanges="true"><Package>DataTransfer.dtsx</Package><Package>LoadXMLData.dtsx</Package><ConfigurationFile>datatransferconfig.dtsconfig</ConfigurationFile><ConfigurationFile>loadxmldataconfig.dtsconfig</ConfigurationFile><MiscellaneousFile>Readme.txt</MiscellaneousFile><MiscellaneousFile>orders.xml</MiscellaneousFile><MiscellaneousFile>NewCustomers.txt</MiscellaneousFile><MiscellaneousFile>orders.xsd</MiscellaneousFile></DTSDeploymentManifest>`  
  
4.  Убедитесь, что значение `AllowConfigurationChanges` атрибут **true** а XML включает `Package` элемент для каждого из двух пакетов, `MiscellaneousFile` элемент для каждого из четырех непакетных файлов и `ConfigurationFile` элемент для каждого из двух XML-файлов конфигурации.  
  
5.  Закройте обозреватель Internet Explorer или текстовый редактор.  
  
## <a name="next-lesson"></a>Следующее занятие  
 [Занятие 3. Установка пакетов](../integration-services/lesson-3-install-ssis-package.md)  
  
![Значок служб Integration Services (маленький)](media/dts-16.gif "значок служб Integration Services (маленький)")**оставаться до даты со службами Integration Services** <br /> Чтобы загрузить новейшую документацию, статьи, образцы и видеоматериалы корпорации Майкрософт, а также лучшие решения участников сообщества, посетите страницу служб [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] на сайте MSDN:<br /><br /> [Посетите страницу служб Integration Services на сайте MSDN](http://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Чтобы получать автоматические уведомления об этих обновлениях, подпишитесь на RSS-каналы, предлагаемые на этой странице.  
  
  
