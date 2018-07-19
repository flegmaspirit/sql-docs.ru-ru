---
title: Редактор назначения необработанного файла (страница «Диспетчер соединений») | Документация Майкрософт
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.rawfiledestinationconnectionmanager.f1
ms.assetid: a0ec9643-3b44-4467-b855-f45ae4794f7f
caps.latest.revision: 7
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: cade93703374705e88abf136233a966e20aadfe8
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/02/2018
ms.locfileid: "37271200"
---
# <a name="raw-file-destination-editor-connection-manager-page"></a>Редактор назначения «Необработанный файл» (страница «Диспетчер соединений»)
  Для настройки назначения «Необработанный файл» на запись необработанных данных в файл используйте редактор назначения «Необработанный файл».  
  
 **Выбор действия**  
  
-   [Открытие редактора назначения «Необработанный файл»](#open)  
  
-   [Задание параметров на вкладке «Диспетчер соединений»](#connection)  
  
-   [Задание параметров на вкладке «Столбцы»](#mapping)  
  
##  <a name="open"></a> Открытие редактора назначения «Необработанный файл»  
  
1.  Добавление назначения «Необработанный файл» в пакет [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] в среде [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
2.  Щелкните правой кнопкой мыши компонент и выберите команду **Изменить**.  
  
##  <a name="connection"></a> Задание параметров на вкладке «Диспетчер соединений»  
 **Режим доступа**  
 Выберите порядок указания имени файла. Выберите пункт **Имя файла** , чтобы ввести имя файла и путь непосредственно, или пункт **Имя файла из переменной** , чтобы указать переменную, содержащую имя файла.  
  
 **Имя файла** или **Имя переменной**  
 Введите имя необработанного файла и путь к нему или выберите переменную, содержащую имя файла.  
  
 **Параметр записи**  
 Выберите метод, используемый для создания файла и записи в файл.  
  
 **Создание исходного необработанного файла**  
 Нажмите эту кнопку для создания пустого необработанного файла, который содержит только столбцы (файл только с метаданными), без необходимости запуска пакета. Файл содержит столбцы, выбранные на странице **Столбцы** окна **Редактор назначения «Необработанный файл»**. Можно указать источник «Необработанный файл» в файле, который содержит только эти метаданные.  
  
 После нажатия **Создать исходный необработанный файл**появляется окно сообщения. Щелкните **ОК** , чтобы продолжить создание файла. Щелкните **Отмена** , чтобы выбрать другой список столбцов на странице **Столбцы** .  
  
##  <a name="mapping"></a> Задание параметров на вкладке «Столбцы»  
 **Доступные входные столбцы**  
 Выберите один или несколько входных столбцов для записи в необработанный файл.  
  
 **Входной столбец**  
 Входной столбец автоматически добавляется в эту таблицу во время выбора в списке **Доступные входные столбцы**. Также можно выбрать входной столбец непосредственно в этой таблице.  
  
 **Псевдоним вывода**  
 Укажите альтернативное имя для выходного столбца.  
  
## <a name="see-also"></a>См. также  
 [Назначение «Необработанный файл»](data-flow/raw-file-destination.md)  
  
  