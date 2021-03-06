---
title: Настройка веб-части "Средство просмотра отчетов" | Документы Майкрософт
ms.date: 09/25/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-server-sharepoint
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.openlocfilehash: cbbc8331699121acaf526e257fd926542c894824
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/01/2018
ms.locfileid: "47770792"
---
# <a name="customize-the-report-viewer-web-part"></a>Настройка веб-части "Средство просмотра отчетов"

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

Веб-часть "Средство просмотра отчетов" можно использовать для просмотра отчетов, которые создаются на сервере отчетов, настроенном для работы в режиме интеграции с SharePoint. Отчеты, которые можно отобразить, включают файлы определений отчета (файлы с расширением RDL) и отчеты построителя отчетов. Отчеты автоматически открываются в веб-части "Средство просмотра отчетов" на новой странице, но веб-часть "Средство просмотра отчетов" можно добавить и на существующую веб-страницу или сайт, если на этой странице необходимо постоянно отображать определенный отчет.

> [!NOTE]
> Несмотря на одинаковое имя, веб-часть "Средство просмотра отчетов", устанавливаемая как надстройка служб [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], и веб-часть "Средство просмотра отчетов", которая находится в файле RSWebParts.cab, отличаются. Инструкции в этом разделе относятся к веб-части "Средство просмотра отчетов", которая устанавливается в составе надстройки служб [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].

 Веб-часть средства "Средство просмотра отчетов" можно настроить следующими способами:  
  
-   Изменить внешний вид веб-части путем задания ее свойств.  
  
-   Выбрать функции интерактивного создания отчетов, доступные на панели инструментов отчета.  
  
-   Указать, какие области доступны для просмотра. Веб-часть "Средство просмотра отчетов" состоит из области просмотра отчетов, области параметров и области учетных данных.  
  
 Веб-часть "Средство просмотра отчетов" нельзя расширить для поддержки других типов файлов. Кроме того, нельзя заменить панель инструментов отчета на другую или добавить функциональность в существующую панель. Если необходимо изменить эти стандартные функции, потребуется создать настраиваемую веб-часть.  

## <a name="setting-web-part-properties"></a>Настройка свойств веб-части

 Веб-часть имеет несколько пользовательских свойств, используемых для настройки определенных функций. Веб-часть имеет также общие свойства, стандартные для каждой веб-части.  
  
### <a name="change-default-properties"></a>Изменение значений свойств по умолчанию

 Веб-часть "Средство просмотра отчетов" имеет свойства по умолчанию, идеально подходящие для открытия отчетов по запросу из библиотеки или папки. По умолчанию на панели инструментов отображаются все доступные элементы управления, а высота и ширина задаются так, чтобы использовалось все доступное пространство веб-страницы. Если необходимо изменить свойства по умолчанию, настроить веб-часть можно с помощью диалогового окна **Настройки веб-сайта**.  
  
1.  В меню **Действия сайта** выберите пункт **Настройки веб-сайта**.  
  
2.  В разделе "Коллекции" выберите **Веб-части**.  
  
3.  Щелкните файл **ReportViewer.dwp**.  
  
4.  Откройте панель средств и установите свойства, которые необходимо использовать.  
  
### <a name="customize-an-embedded-report-viewer-in-a-web-page"></a>Настройка средства просмотра отчетов, внедренного в веб-страницу

 Можно задать свойства так, чтобы средство просмотра отчетов уместилось на веб-странице. Средство просмотра отчетов может использовать те же стили и цвета, что и содержащая его страница. Можно скрыть целиком или частично панель инструментов, схему документа и область параметров, чтобы максимально увеличить область просмотра отчетов в пределах выделенного пространства. Отчет всегда использует стили, определенные при его создании. После опубликования отчета в библиотеке SharePoint изменить его внешний вид невозможно.  
  
 Если веб-часть "Средство просмотра отчетов" внедряется в веб-страницу, необходимо задать в качестве значения свойства **URL-адрес отчета** адрес определенного отчета. Если этого не сделать, средство просмотра отчетов отобразит инструкции для установления связи с отчетом. Изменить или удалить эти инструкции нельзя.  
  
### <a name="custom-properties-of-the-report-viewer-web-part"></a>Пользовательские свойства веб-части "Средство просмотра отчетов"

 При задании значений пользовательских свойств учтите, что некоторые свойства используются только при внедрении веб-части "Средство просмотра отчетов" в страницу. Среди них «Заголовок», «Высота», «Ширина», «Стиль рамки» и «Зона». Другие свойства, такие как настройки панели инструментов и настройки параметров, используются вне зависимости от того, появляется ли средство просмотра отчетов внутри страницы или в полностраничном режиме.  
  
 Ниже перечислены пользовательские свойства веб-части "Средство просмотра отчетов".  
  
|Свойство|Описание|  
|--------------|-----------------|  
|Отчет|Полный путь к отчету, находящемуся на текущем сайте SharePoint или на сайте того же веб-приложения или фермы. Для получения оптимальных результатов при установке дополнительных свойств после указания URL-адреса отчета нажмите кнопку «Применить».|  
|Назначение гиперссылки|Стандартный код HTML, который определяет целевой фрейм, предназначенный для отображения связанного содержимого в текущем документе. Для отчетов, содержащих гиперссылки на внешние веб-сайты, можно указать, открывается ли целевой документ поверх существующего отчета в текущем окне или в новом окне браузера. Допустимые значения: **_Top**, **_Blank**и **_Self**. **_Top** использует текущее окно, **_Blank** загружает документ в новое окно браузера, а **_Self** открывает документ в текущем фрейме. Хотя **_Parent** является допустимым значением атрибута Target в HTML, не используйте это значение для веб-части "Средство просмотра отчетов", внедренной в страницу.|  
|Автоматическое формирование заголовка веб-части|Формируемый заголовок, который содержит имя веб-части "Средство просмотра отчетов" и имя отчета, разделенные дефисом. Если у отчета нет заголовка, используется имя файла отчета. Этот заголовок виден при добавлении веб-части на страницу. Если этот флажок установлен, то заголовок формируется каждый раз при обновлении страницы.|  
|Автоматическое формирование подробной ссылки для заголовка веб-части|Формируемая гиперссылка, которая отображается над веб-частью. Можно щелкнуть эту ссылку, чтобы открыть отчет на новой странице в полностраничном режиме.|  
|Отображение элемента меню построителя отчетов|Показывает или скрывает элемент меню **Действия** , который позволяет открыть построитель отчетов.|  
|Отображение элемента меню подписок|Показывает или скрывает элемент меню **Действия** , предназначенный для создания подписки на отчет.|  
|Отображение элемента меню печати|Показывает или скрывает элемент меню **Действия** , предназначенный для печати отчета.|  
|Отображение элемента меню экспорта|Показывает или скрывает элемент меню **Действия** , предназначенный для экспорта отчета.|  
|Отображение кнопки обновления|Показывает или скрывает кнопку обновления на панели инструментов.|  
|Отображение элементов управления навигацией по страницам|Показывает или скрывает кнопки навигации по отчету на панели инструментов. Этот параметр отвечает за отображение всех элементов управления навигацией.|  
|Отображение кнопки «Назад»|Показывает или скрывает кнопку «Назад» на панели инструментов.|  
|Отображение элементов управления поиском|Показывает или скрывает элементы управления поиском на панели инструментов. Элементы управления поиском позволяют пользователю искать текст в готовом для просмотра отчете. Этот параметр изменяет видимость всех элементов управления поиском.|  
|Отображение элемента управления масштабированием|Показывает или скрывает элемент управления масштабированием на панели инструментов.|  
|Отображение кнопки веб-канала ATOM|Показывает или скрывает кнопку веб-канала ATOM на панели инструментов.<br /><br /> ![htmlviewer_datafeed](../../reporting-services/media/htmlviewer-datafeed.gif "htmlviewer_datafeed")|  
|Расположение панели инструментов|Определяет расположение панели инструментов в средстве просмотра отчетов. Допустимые значения включают **Top** и **Bottom**.|  
|Область приглашений|Допустимыми значениями являются **Displayed**, **Collapsed**и **Hidden**. **Displayed** отображает область параметров для отчетов с параметризованными значениями, которые пользователь должен ввести до выполнения отчета. Значение **Hidden** используется, если все параметры отчета заданы и область параметров нужно скрыть.|  
|Ширина области параметров|Можно выбрать единицу измерения и значение. Значение по умолчанию — 200 пикселей. Единственным требованием для этого свойства является значение больше нуля.|  
|Схема документа|Элемент управления навигацией по отчету, который определен в отчете и используется для предоставления доступа к конкретным разделам отчета с помощью одного щелчка мышью. Она доступна в HTML-отчетах. Схема документа отображается в сворачиваемой области рядом с областью просмотра отчета. Допустимыми значениями являются **Displayed**, **Collapsed**и **Hidden**. Если для отчета определена схема документа, то область разворачивается по умолчанию, только если она не помечена в свойствах веб-части как скрытая или свернутая. Если схема документа свернута, можно щелкнуть эту стрелку, чтобы развернуть ее.|  
|Ширина области схемы документа|Можно выбрать единицу измерения и значение. Значение по умолчанию — 200 пикселей. Единственным требованием для этого свойства является значение больше нуля.|  
|Загрузка параметров|Получите свойства параметров отчета. Не все отчеты имеют параметры. Если в отчете нет параметров, значения не возвращаются. При установке свойств только что переданного отчета можно получить ошибку, которая указывает, что соединение с источником данных удалено. В этом случае восстановите соединение и завершите настройку свойств параметров. Дополнительные сведения о настройке соединения см. в разделе [Создание общих источников данных и управление ими (службы Reporting Services в режиме интеграции с SharePoint)](http://msdn.microsoft.com/library/2d3428e4-a810-4e66-a287-ff18e57fad76).<br /><br /> Для получения наилучших результатов нажмите кнопку **Применить** перед тем, как нажать кнопку «Загрузка параметров».<br /><br /> После загрузки свойств параметров можно установить их тем же способом, что и на странице свойств параметров в отчете. Дополнительные сведения о задании параметров см. в разделе [Настройка параметров опубликованного отчета (службы Reporting Services в режиме интеграции с SharePoint)](../../reporting-services/report-design/set-parameters-on-a-published-report-sharepoint-integrated-mode.md).|  

## <a name="customizing-the-toolbar"></a>Настройка панели инструментов

 Панель инструментов отображается под заголовком и занимает верхнюю часть отчета. Панель инструментов содержит элементы меню **Действия** , элементы для перемещения по страницам для отчетов, разбитых на страницы, обновления и изменения масштаба. Она включает управление схемой документа для отчетов, содержащих схему документа. Меню **Действия** содержит команды для экспорта отчетов, поиска текста и чисел в отчете, печати отчета, а также для открытия отчета в построителе отчетов.  
  
 В меню  **Действия** нельзя добавлять новые команды, но его можно настраивать, изменяя список команд, которые видит пользователь. Чтобы изменить видимость кнопок и элементов управления на панели инструментов, необходимо внести изменения в параметры раздела **Видимость элементов панели инструментов** веб-части. Можно также удалить только команду **Печать** или конкретные форматы экспорта, сделав эти функции недоступными на сервере отчетов. Элементы управления для перемещения по страницам доступны для отчетов, содержащих разрывы страниц; в ином случае отчет является целой страницей переменной длины. Действие**Обновить** приводит к повторной обработке отчета с использованием параметров, которые являются текущими для отчета. Для отображения всех элементов управления в одной строке общая ширина веб-части должна составлять не менее 400 пикселей.  

## <a name="customizing-the-viewing-area"></a>Настройка области просмотра

 Область просмотра используется для отображения отчетов. Внутри области просмотра отчета расположены также области «Параметры» и «Учетные данные», если они используются. Если необходимы учетные данные, то рядом с пустой областью просмотра отчета отображается область «Учетные данные». Область «Учетные данные» исчезает после того, как пользователь предоставит учетные данные и запустит отчет. Чтобы настроить текст приглашения, которое запрашивает у пользователей учетные данные, измените свойства соединения с источником данных. Дополнительные сведения см. в разделе [Создание общих источников данных и управление ими (службы Reporting Services в режиме интеграции с SharePoint)](http://msdn.microsoft.com/library/2d3428e4-a810-4e66-a287-ff18e57fad76).  
  
 Область «Параметры» предоставляет поля для ввода значений перед выполнением отчета. Она используется только в том случае, если определение отчета содержит параметры. Если отображается любая из областей "Параметры" или "Учетные данные", то представление отчета занимает оставшуюся ширину веб-части. Вы можете задать свойства веб-части, чтобы настроить ширину области "Параметры". Можно также определить метки, которые появляются рядом с конкретными параметрами страницы. Дополнительные сведения об изменении меток параметров см. в разделе [Настройка параметров опубликованного отчета (службы Reporting Services в режиме интеграции с SharePoint)](../../reporting-services/report-design/set-parameters-on-a-published-report-sharepoint-integrated-mode.md).  
  
## <a name="see-also"></a>См. также раздел

 [Веб-часть "Средство просмотра отчетов" на сайте SharePoint](../../reporting-services/report-server-sharepoint/report-viewer-web-part-on-a-sharepoint-site.md)   
 [Добавление на страницу веб-части средства просмотра отчетов](../../reporting-services/report-server-sharepoint/add-the-report-viewer-web-part-to-a-web-page.md)  

Остались вопросы? [Посетите форум служб Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231).
