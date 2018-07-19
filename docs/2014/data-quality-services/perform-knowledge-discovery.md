---
title: Обнаружение набора знаний | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.dqs.kb.kbanalyze.f1
- sql12.dqs.kb.viewselectcd.f1
- sql12.dqs.kb.kbmap.f1
- sql12.dqs.kb.kbterms.f1
ms.assetid: 34a0ea16-02e6-46ed-90bc-dede68687f63
caps.latest.revision: 37
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 172dfee131d4452e2d3adae7a3e8854591a8c0a1
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/02/2018
ms.locfileid: "37206184"
---
# <a name="perform-knowledge-discovery"></a>Обнаружение набора знаний
  В этом разделе описывается создание базы знаний посредством обнаружения набора знаний. В процессе обнаружения службы [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) анализируют данные из образца данных источника данных посредством автоматизированного процесса и добавляют обнаруженные знания в базу знаний. Эти наборы знаний можно изменять и расширять на шаге **Управление значениями домена** действия обнаружения набора знаний или в действии управления доменами.  
  
 Обнаружение знаний — это управляемый мастером процесс из трех шагов, каждый из которых обязателен для выполнения.  
  
##  <a name="BeforeYouBegin"></a> Перед началом  
  
###  <a name="Prerequisites"></a> Предварительные требования  
 На компьютере с [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] должна быть установлена программа Microsoft Excel, если исходные данные, для которых производится обнаружение, содержатся в файле Excel. В противном случае на стадии сопоставления невозможно будет выбрать файл Excel. Файлы, созданные Microsoft Excel, могут иметь расширение XLSX, XLS или CSV. При использовании 64-разрядной версии Excel поддерживаются только файлы Excel 2003 (.xls), файлы Excel 2007 и 2010 (.xlsx) не поддерживаются. При использовании 64-разрядной версии Excel 2007 или 2010 сохраните файл как XLS- или CSV-файл либо вместо этого установите 32-разрядную версию Excel.  
  
###  <a name="Security"></a> безопасность  
  
####  <a name="Permissions"></a> Permissions  
 Для создания базы знаний необходима роль dqs_kb_editor или dqs_administrator в базе данных DQS_MAIN.  
  
##  <a name="FirstStep"></a> Первый шаг. Запуск обнаружения знаний  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Запуск клиентского приложения Data Quality Client](../../2014/data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Если необходимо выполнить обнаружение набора знаний в новой базе знаний, нажмите кнопку **Создать базу знаний**, введите имя и описание и укажите, на основе чего создается база знаний (если это применимо). Если обнаружение набора знаний необходимо выполнить в существующей базе знаний, нажмите кнопку **Открыть базу знаний**и выберите базу знаний.  
  
3.  Выберите действие **Обнаружение знаний** и нажмите кнопку **Создать** , чтобы создать новую базу знаний, или нажмите кнопку **Открыть** , чтобы открыть существующую базу знаний.  
  
##  <a name="Mapping"></a> Стадия сопоставления  
  
1.  В поле **Источник данных** выберите **SQL Server** (по умолчанию) или **Файл Excel**.  
  
    > [!NOTE]  
    >  На этой странице устанавливается соединение с сервером SQL Server или источником данных Excel, а затем сопоставляются столбцы источника данных с доменом в базе знаний. В таблице «Сопоставления» отображаются все столбцы в базе данных-источнике, которые будут проанализированы для добавления набора знаний в соответствующие домены. Сопоставление производится между столбцами источника данных и доменом в базе знаний.  
  
2.  Если используется источник данных **SQL Server**, выполните следующие действия.  
  
    1.  В поле **База данных** выберите базу данных-источник, которую необходимо проанализировать для создания базы знаний. В текстовом поле с раскрывающимся списком содержится список доступных баз данных. База данных-источник должна находиться на том же экземпляре SQL Server, что и [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]. В противном случае она не появится в раскрывающемся списке.  
  
    2.  В поле **Таблица или представление** выберите таблицу или представление, которые необходимо проанализировать для создания базы знаний. Таблица или представление должны быть образцом данных, а не всей базой данных-источником, в которой выполняется очистка или сопоставление. В текстовом поле с раскрывающимся списком отображается список таблиц и представлений, доступных в выбранной базе данных.  
  
3.  Если используется источник данных **Excel**, выполните следующие действия.  
  
    1.  Нажмите кнопку **Обзор** и выберите файл Excel, который необходимо проанализировать для создания базы знаний. На компьютере [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] должна быть установлена программа Excel, если исходные данные, подлежащие очистке, находятся в файле Excel. Если программа Excel не установлена на компьютере [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , кнопка «Обзор» будет недоступна, а под этим текстовым полем появится уведомление об отсутствии Excel.  
  
    2.  Установите флажок **Использовать первую строку в качестве заголовка** , если первая строка файла Excel содержит данные заголовков.  
  
4.  В таблице **Сопоставления** сопоставьте каждый из исходных столбцов, в которых необходимо провести обнаружение наборов знаний, с доменами в базе знаний, как описано ниже.  
  
    1.  Создайте сопоставление, выбрав исходный столбец из раскрывающегося списка для столбца **Исходный столбец** пустой строки, а затем выбрав домен из раскрывающегося списка в столбце **Домен** той же строки, если домен существует. Если домен не существует, нажмите кнопку **Создать домен** или **Создать составной домен** , чтобы создать домен. Дополнительные сведения см. в разделе [Создание правила домена](../../2014/data-quality-services/create-a-domain-rule.md) или [Создание составного домена](../../2014/data-quality-services/create-a-composite-domain.md).  
  
    2.  Повторите предыдущий шаг для каждого сопоставления. Чтобы изменить число строк в таблице, нажмите кнопку **Добавить сопоставление столбцов**или выберите строку и нажмите кнопку **Удалить выбранное сопоставление столбцов**. Если нажать кнопку **Удалить выбранное сопоставление столбцов** при выбранной заполненной строке, эта заполненная строка будет удалена даже при наличии другой незаполненной строки.  
  
        > [!NOTE]  
        >  Вы можете сопоставить исходные данные с доменом служб DQS для проведения обнаружения набора знаний, только если исходный тип данных поддерживается службами DQS и совпадает с типом данных домена служб DQS. Дополнительные сведения о поддерживаемых типах данных см. в разделе [Типы данных SQL Server и службы SSIS, поддерживаемые для доменов DQS](../../2014/data-quality-services/supported-sql-server-and-ssis-data-types-for-dqs-domains.md).  
  
    3.  Нажмите кнопку **Просмотр/выбор составных доменов** для отображения определенных составных доменов. Если составные домены не определены, элемент управления будет недоступен.  
  
    4.  Нажмите кнопку **Предварительный просмотр источника данных** , чтобы просмотреть во всплывающем окне все данные из источника данных, выбранного в текстовом поле **Таблица или представление** или **Файл Excel** .  
  
5.  Нажмите кнопку **Далее** , чтобы перейти на страницу **Обнаружение** мастера обнаружения набора знаний. Также вы можете выбрать следующие действия.  
  
    -   Нажмите кнопку **Отмена** , чтобы прекратить действие обнаружения набора знаний с потерей полученных результатов и вернуться на домашнюю страницу DQS.  
  
    -   Нажмите кнопку **Закрыть** , чтобы вернуться на домашнюю страницу DQS с сохранением результатов работы. База знаний будет заблокирована вами, а в таблице баз знаний на экране **Открытие базы знаний** для этой базы знаний будет отображаться состояние **Обнаружение — сопоставление**. После нажатия кнопки **Закрыть**для выполнения действий управления доменами потребуется нажать кнопку **Обнаружение знаний** на экране **Открыть базу знаний** , перейти на экран **Управление базами знаний: управление терминами доменов** , нажать кнопку **Готово**, а затем кнопку **Да** , чтобы опубликовать базу знаний, или **Нет** , чтобы сохранить работу в базе знаний и выйти.  
  
##  <a name="Discover"></a> Этап обнаружения  
  
1.  Нажмите кнопку **Запустить** для анализа источника данных.  
  
    > [!NOTE]  
    >  Обнаружение выполняется для столбцов, заданных в таблице **Сопоставления** на странице **Карта** . Домены, сопоставленные с каждым из столбцов, будут заполняться полученными при обнаружении набора знаний. Если домен является составным, то набор знаний будут добавлены в отдельные домены, входящие в составной домен.  
  
2.  По мере выполнения процесса обнаружения проверяйте состояние завершения каждого из шагов обнаружения: **Предварительная обработка записей**, **Выполнение правил домена**и **Выполнение обнаружения**. Для каждого из этих этапов отображаются процент завершения и состояние завершения.  
  
3.  После завершения анализа убедитесь, что строка состояния под статистическими показателями выполнения содержит сообщение об успешном завершении.  
  
    > [!NOTE]  
    >  Если покинуть экран до загрузки файла, процесс загрузки файла будет прерван.  
  
4.  После завершения анализа проверьте статистические показатели на вкладке **«Профилировщик»** , чтобы определить состояние данных. Дополнительные сведения см. в разделе **Профилирование данных и уведомления в DQS**.  
  
5.  После завершения анализа данных кнопка **Пуск** преобразуется в кнопку **Перезапустить** . Нажмите кнопку **Перезапуск** для повторного запуска процесса анализа. Однако если результаты предыдущего анализа еще не были сохранены, то после нажатия кнопки **Перезапустить** ранее полученные данные теряются. Чтобы продолжить нажмите кнопку **Да** во всплывающем меню. Во время выполнения анализа не уходите с этой страницы, поскольку процесс анализа будет прекращен.  
  
6.  Нажмите кнопку **Далее** , чтобы перейти на страницу **Управление значениями домена** мастера обнаружения набора знаний. На этой странице вы можете изменить знания, добавленные в домены базы знаний. Также вы можете выбрать следующие действия.  
  
    -   Нажмите кнопку **Отмена** , чтобы прекратить действие обнаружения набора знаний с потерей полученных результатов и вернуться на домашнюю страницу DQS.  
  
    -   Нажмите кнопку **Закрыть** , чтобы вернуться на домашнюю страницу DQS с сохранением результатов работы. База знаний будет заблокирована вами, а в таблице баз знаний на экране **Открытие базы знаний** эта база знаний перейдет в состояние **Обнаружение — обнаружение**. После нажатия кнопки **Закрыть**для выполнения действий управления доменами потребуется нажать кнопку **Обнаружение знаний** на экране **Открыть базу знаний** , перейти на экран **Управление базами знаний: управление терминами доменов** , нажать кнопку **Готово**, а затем кнопку **Да** , чтобы опубликовать базу знаний, или **Нет** , чтобы сохранить работу в базе знаний и выйти.  
  
    -   Щелкните, чтобы вернуться на страницу **Обнаружение** .  
  
##  <a name="Manage"></a> Этап управления результатами обнаружения данных  
 После выполнения действия обнаружения знаний можно изменять значения следующими способами.  
  
-   Добавить значение домена в список значений или выбрать значение и удалить его из списка.  
  
-   Изменить состояние значения домена, назначенное на этапе анализа службами DQS, на одно из следующих: «верно», «ошибочно» или «недопустимо».  
  
-   Ввод значения для замены ошибочного или недопустимого значения  
  
-   Задать два значения или несколько в качестве синонимов и изменить ведущее значение, назначенное в процессе обнаружения, в результате чего ведущее значение заменяет значение синонима, если при создании домена было установлено свойство **Использование ведущего значения**  
  
-   Импорт значений домена из файла Excel.  
  
 В таблице **Значение** отображаются знания, добавленные в базу знаний для отдельного домена. Домен выбирается в списке доменов на панели слева. Поле содержит следующие столбцы.  
  
-   Столбец **Значение** отображает все значения, добавленные процессом обнаружения к выбранному домену из поля в образце данных. Любое значение, рассматриваемое как ошибочное, будет показано в качестве синонима для значения, рассматриваемого как верное.  
  
-   Столбец **Частота** отображает число вхождений значения в поле примеров базы данных, с которым сопоставлен домен. Для составного домена отображаются только значения с частотой, большей или равной 20. Сведения о частоте доступны благодаря тому, что процесс обнаружения набора знаний все еще сохраняет соединение с образцом базы данных. Сведения о частоте недоступны в таблице доменов на вкладке «Значения домена» экрана «Управление доменами», поскольку у процесса управления доменами нет соединения с образцом базы данных.  
  
-   Столбец **Тип** отображает состояние значения, определенное процессом обнаружения. Зеленый флажок указывает, что значение верно или исправлено; красный крест — что значение ошибочно, а оранжевый треугольник с восклицательным знаком — что значение недопустимо. Недопустимое значение не соответствует требованиям к данным для домена. Ошибочное значение может быть допустимым, но неправильным по причинам, связанным с данными.  
  
-   В столбце **Исправить на** показано правильное значение, на которое изменяется исходное значение, отмеченное как ошибочное или недопустимое. По результатам процесса обнаружения службы DQS могут предложить правильное значение.  
  
 Управление результатами обнаружения производится следующим образом.  
  
1.  На панели **Список доменов** в левой части экрана выберите домен, для которого следует задать значения домена. Для изменения отображаемых значений вы можете выполнить следующие действия.  
  
    -   Отображение требуемых результатов в таблице на основе их состояния, выбранного в списке **Фильтр** .  
  
    -   Найти данные, которые нужно проверить или изменить, добавляя по одной букве для поиска в текстовое поле Найти. В результате эти буквы будут выделяться всегда, когда они встречаются в любом отображаемом значении.  
  
    -   Выберите **Показывать только новые** , чтобы отображать в таблице только значения, обнаруженные только в текущем сеансе.  
  
    -   Нажмите кнопку **Развернуть все** , чтобы отображать все значения во всех группах синонимов, когда отображение свернуто, или кнопку **Свернуть все** , чтобы скрыть все значения, кроме ведущего, во всех группах синонимов, когда отображение развернуто.  
  
    -   Нажмите кнопку **Показать или скрыть панель журнала изменений значений домена** , чтобы отобразить всплывающее окно предварительного вида в нижней части таблицы значений, которое показывает недавние изменения в наборе значений домена.  
  
2.  Поиск предлагаемых службами Data Quality Services исправлений — для этого установите в поле **Фильтр** значение **Ошибка**. Убедитесь, что значение действительно является ошибочным, а значение в столбце **Исправить на** допустимо.  
  
3.  Выберите в поле **Фильтр** значение **Все значения** и убедитесь, что состояния значений допустимы. Чтобы изменить состояние значения, выберите значение и нажмите кнопку **Задать выбранные значения домена как исправленные** (с изображением галочки), **Задать выбранные значения домена как ошибки** (с крестиком) или **Задать выбранные значения домена как недопустимые** (с треугольником).  
  
4.  Чтобы изменить состояние значения, выполните следующие действия.  
  
    1.  **Обозначить выбранные значения домена как исправленные**. Чтобы изменить состояние значения с ошибочного или недопустимого на исправленное, выберите значение и щелкните пункт **Обозначить выбранные значения домена как исправленные** (галочка) в меню направленной вниз стрелки на панели значков или в раскрывающемся списке «Тип». Если ошибочное или недопустимое значение сгруппировано с правильным значением, удалите это значение после операции.  
  
    2.  **Обозначить выбранные значения домена как ошибки**. Чтобы изменить состояние значения с верного или недопустимого на ошибочное, выберите значение и щелкните пункт **Обозначить выбранные значения домена как ошибки** (крестик) в меню направленной вниз стрелки на панели значков или в раскрывающемся списке «Тип». Вы можете ввести исправление в столбце **Исправить на** или оставить его пустым.  
  
    3.  **Обозначить выбранные значения домена как недопустимые**. Чтобы изменить состояние значения с верного или ошибочного на недопустимое, выберите значение и щелкните пункт **Обозначить выбранные значения домена как недопустимые** (треугольник) в меню направленной вниз стрелки на панели значков или в раскрывающемся списке «Тип». Вы можете ввести исправление в столбце **Исправить на** или оставить его пустым.  
  
    4.  **Исправить на**. После задания значения как ошибочного или недопустимого введите новое значение в столбец **Исправить на** . При этом службы DQS добавляют новую строку для замещающего значения и назначают его верным, а затем группируют оба эти значения. Новое значение будет показано как ведущее значение, ведущее значение выделено полужирным шрифтом, а ошибочное или недопустимое значение показано с отступами.  
  
5.  Чтобы определить значения как группы синонимов, выберите несколько значений, которые являются правильными, а затем выполните следующие действия.  
  
    -   **Установить выбранные значения домена в качестве синонимов**. Щелкните для установки выбранных значений в качестве синонимов. DQS выберет одно из значений в качестве ведущего, которым будут заменяться другие значения.  
  
        > [!NOTE]  
        >  Если выбрано два или несколько значений или несколько в группе и другое значение вне этой группы, а затем они назначены синонимами, будет получено неверное сообщение об ошибке. После закрытия всплывающего сообщения об ошибке значения будут правильно назначены синонимами.  
  
    -   **Разорвать отношение между выбранными синонимами**: щелкните для отмены назначения синонима.  
  
    -   **Установить выбранное значение домена в качестве ведущего значения своей группы**. Чтобы изменить ведущее значение группы, выберите в группе значение, не назначенное ведущим, и нажмите кнопку **Установить выбранное значение домена в качестве ведущего значения своей группы** .  
  
6.  **Программа проверки орфографии**. Если средство проверки орфографии включено на странице «Свойства домена», то обратите внимание на все значения с волнистым подчеркиванием красным цветом: это означает, что средство проверки орфографии предлагает исправить значение. Щелкните правой кнопкой мыши подчеркнутое значение и выберите одно из исправлений, если оно применимо. Тип значения становится ошибочным (или остается таковым), а исправление добавляется в столбец **Исправить на** . Щелкните стрелку «вниз» для просмотра дополнительных предложенных исправлений. Введите исправление вручную, чтобы добавить его к словарю средства проверки орфографии, с учетом того, что это значение должно быть выбрано как исправление. Дополнительные сведения см. в разделах [Использование средства проверки орфографии DQS](../../2014/data-quality-services/use-the-dqs-speller.md) и [Настройка свойств домена](../../2014/data-quality-services/set-domain-properties.md).  
  
    > [!NOTE]  
    >  Для использования средства проверки орфографии вы можете либо включить его на странице **Свойства домена** , либо, если оно отключено на странице **Свойства домена** , щелкнуть значок **Включить/отключить средство проверки орфографии** на странице **Управление результатами обнаружения набора знаний** , чтобы включить его на этой странице.  
  
7.  **Добавить новое значение домена**. Добавьте новое значение в домен, нажав кнопку **Добавить новое значение домена** для добавления строки в конец таблицы. После ввода значения строка будет перемещена с учетом алфавитного порядка.  
  
8.  **Импорт значений домена из Excel**. Чтобы добавить новые значения из электронной таблицы Excel, щелкните стрелку «вниз» для значка **Импортировать значения** и выберите **Импорт значений домена из Excel**. Введите имя файла, выберите **Использовать первую строку в качестве заголовка** , если это возможно, и нажмите кнопку **ОК**. Дополнительные сведения см. в статье [Импорт значений из файла Excel в домен](../../2014/data-quality-services/import-values-from-an-excel-file-into-a-domain.md).  
  
9. **Импорт значений проекта**. Для добавления новых значений из проекта служб DQS щелкните стрелку «вниз» для значка **Импортировать значения** и выберите **Импорт значений проекта**. Введите имя файла, выберите **Использовать первую строку в качестве заголовка** , если это возможно, и нажмите кнопку **ОК**. Выберите проект, из которого нужно импортировать значения, и нажмите кнопку **ОК**. Будут отображены импортированные значения. Нажмите кнопку **Готово**. Дополнительные сведения см. в разделе «Импорт значений проекта в домен».  
  
10. **Удалить выбранные значения домена**. Удалите одно или несколько существующих значений из домена, выбрав значения и нажав кнопку **Удалить выбранные значения домена** . Удалить элемент DQS_NULL нельзя, поэтому, если удаляется несколько значений, одно из которых — элемент DQS_NULL, операция завершится ошибкой.  
  
11. Нажмите кнопку **Готово** , чтобы завершить работу действия обнаружения набора знаний. Если просмотрены не все домены, отобразится всплывающее сообщение. Нажмите кнопку **Да** для дальнейшего просмотра или **Нет** , чтобы продолжить работу. При нажатии кнопки «Нет» отобразится другое всплывающее сообщение, позволяющее выбрать один из следующих вариантов.  
  
    1.  **Опубликовать**. База знаний будет опубликована и доступна для использования текущим пользователем или другими пользователями. База знаний не будет заблокирована, ее состояние (в таблице баз знаний) будет пустым. Будут доступны как операция управления доменами, так и операция обнаружения набора знаний. Выполняется возврат на домашнюю страницу. Для завершения процесса нажмите во всплывающем сообщении кнопку **Да** .  
  
    2.  **Нет**. Работа сохраняется, база знаний остается заблокированной, а ее состояние отображается как «В работе». Будут доступны как операция управления доменами, так и операция обнаружения знаний. Выполняется возврат на домашнюю страницу.  
  
    3.  **Отмена**. Всплывающее окно закрывается, и экран возвращается на страницу **Управление значениями домена** .  
  
12. Также вы можете нажать одну из следующих кнопок:  
  
    -   **Отмена** — чтобы прекратить действие обнаружения набора знаний и вернуться на домашнюю страницу DQS с потерей результатов выполненной работы.  
  
    -   **Закрыть** — чтобы вернуться на домашнюю страницу DQS с сохранением результатов работы. База знаний будет заблокирована вами, а в таблице баз знаний на экране **Открытие базы знаний** для этой базы данных будет отображаться состояние **Обнаружение — управление значениями**.  
  
    -   Нажмите кнопку **Назад** , чтобы вернуться на страницу **Обнаружение** . После нажатия кнопки **Закрыть**для выполнения действий управления доменами потребуется нажать кнопку **Обнаружение знаний** на экране **Открыть базу знаний** , перейти на экран **Управление базами знаний: управление терминами доменов** , нажать кнопку **Готово**, а затем кнопку **Да** , чтобы опубликовать базу знаний, или **Нет** , чтобы сохранить работу в базе знаний и выйти.  
  
##  <a name="FollowUp"></a> Дальнейшие действия. После выполнения обнаружения знаний  
 После добавления набора знаний в базу знаний в процессе автоматизированного обнаружения набора знаний можно либо использовать базу знаний для немедленной очистки проекта, либо произвести перед очисткой управление доменами. Дополнительные сведения об очистке данных и управлении доменами см. в разделах [Очистка данных](../../2014/data-quality-services/data-cleansing.md) и [Управление доменом](../../2014/data-quality-services/managing-a-domain.md).  
  
##  <a name="Meaning"></a> Смысл правильного, ошибочного и недопустимого значений  
 Каждому значению в таблице **Значение** на странице **Значения домена** назначается параметр **Тип** — **Правильно**, **Ошибка**или **Недопустимо**. Тип значения первоначально назначается операцией обнаружения знаний, и его вы можете изменить по своему усмотрению. Последний тип, основанный на обнаружении и интерактивных изменениях, формируется операцией очистки. Эти значения имеют следующий смысл.  
  
-   **Правильно.** Это значение принадлежит к домену и не имеет каких-либо синтаксических ошибок. Например, значение «Чикаго» в домене «Город» — правильное.  
  
-   **Ошибка.** Это значение принадлежит домену, но является неверным. Например, «Шикаго» вместо «Чикаго» в домене «Город» — ошибка. Службы DQS определяют значение как ошибочное, если выявлена синтаксическая ошибка, и назначают связанное исправление в процессе обнаружения. Орфографические ошибки относятся к числу синтаксических ошибок.  
  
-   **Недопустимый.** Это значение не принадлежит к домену и не имеет исправления. Например, значение «12345» в домене «Город» является недопустимым. Службы DQS определяют значение как недопустимое, если оно не соответствует правилу домена.  
  
 Тип значения вы можете изменить вручную на любое из двух других значений. Службы DQS не обеспечивают правильность и семантику ошибок при ручных операциях. Исправление для недопустимого значения вы можете ввести без изменения его статуса. Вы можете объявить значение недопустимым, даже если оно не нарушает правила домена. Службы DQS могут определить значение как ошибочное, даже если в процессе обнаружения не выявлены синтаксические ошибки. Вы можете также удалить исправление ошибочного значения, которое отмечено как правильное, без изменения его статуса.  
  
 При интерактивной очистке данных на странице **Управление результатами и их просмотр** операции **Очистка** как недопустимые, так и ошибочные значения представлены на вкладке **Недопустимые** на странице **Управление результатами и их просмотр** .  
  
##  <a name="Display"></a> How to Display the Appropriate Values  
 Вы можете изменять отображаемые сведения следующим образом.  
  
-   **Фильтровать** результаты, которые нужно внести в таблицу, по их состоянию, выбирая состояние в раскрывающемся списке **Фильтр** .  
  
-   **Найти** данные, которые нужно проверить или изменить, добавляя по одной букве для поиска в текстовое поле **Найти** . В результате эти буквы будут выделяться всегда, когда они встречаются в любом отображаемом значении.  
  
-   Выберите **Показывать только новые** , чтобы отображать в таблице только значения, обнаруженные только в текущем сеансе.  
  
-   Нажмите кнопку **Развернуть все** , чтобы показать все значения в любой группе синонимов, если текущее состояние свернутое.  
  
-   Нажмите кнопку **Свернуть все** , чтобы скрыть все значения, кроме ведущего, в любой группе синонимов, если текущее состояние развернутое.  
  
-   Нажмите кнопку **Показать или скрыть панель журнала изменений значений домена** , чтобы отобразить всплывающее окно предварительного вида в нижней части таблицы значений, которое показывает недавние изменения в наборе значений домена.  
  
##  <a name="Profiler"></a> Статистические данные профилировщика  
 На вкладке «Профилировщик» представлены статистические данные, отражающие качество исходных данных. Эти статистические данные не измеряют качество базы знаний. Профилирование при обнаружении знаний дает сведения об их полноте и уникальности. Профилирование при обнаружении знаний не измеряет точность. Профилирование при обнаружении знаний помогает оценить полезность источника данных для построения и улучшения набора знаний в базе набора знаний.  
  
 На вкладке **«Профилировщик»** предоставлены следующие статистические данные для процесса обнаружения, упорядоченные по полям и доменам:  
  
-   **Записи**. Число обнаруженных в образце данных записей.  
  
-   **Всего значений**. Сколько всего значений найдено для каждого из полей и в целом.  
  
-   **Новые значения**. Общее количество новых значений для каждого из полей и всех сопоставленных полей с момента последнего процесса обнаружения, а также их процентная доля в общем количестве значений.  
  
-   **Уникальные значения**. Общее количество уникальных значений для каждого из полей и всех сопоставленных полей, а также их процентная доля в общем количестве значений.  
  
-   **Новые уникальные значения**. Общее количество уникальных значений для каждого из полей и всех сопоставленных полей с момента последнего процесса обнаружения, а также их процентная доля в общем количестве значений.  
  
-   **Действительные значения в домене**. Общее количество допустимых значений для каждого из полей и всех сопоставленных полей, а также их процентная доля в общем количестве значений.  
  
 Статистические данные поля включают следующее:  
  
-   **Поле**. Имя поля в базе данных-источнике.  
  
-   **Домен**. Имя домена, который сопоставляется с полем.  
  
-   **Создать**. Количество новых значений и процент новых значений по сравнению с существующими значениями в домене.  
  
-   **Уникальный**. Количество уникальных записей в поле и их процент от общего количества.  
  
-   **Действительные в домене**. Количество допустимых значений домена и их процент от общего количества.  
  
-   **Полнота**. Полнота каждого поля-источника, которое сопоставляется при применении сопоставления.  
  
 Профилирование при обнаружении знаний дает сведения о полноте данных. Если профилирование указывает, что поле является относительно неполным, то может потребоваться удалить его из базы знаний проекта служб DQS. Профилирование может не предоставлять надежных статистических данных по полноте для составных доменов. Если требуются статистические данные по полноте, используйте одиночные домены вместо составных. Если необходимо использовать составные домены, то, возможно, потребуется создать одну базу знаний с одиночными доменами для профилирования в целях определения полноты и другой домен с составным доменом для процесса очистки. Например, профилирование может показать полноту 95% для записей адреса в составном домене, но для одного из столбцов (например, столбца почтового индекса) уровень неполноты может оказаться гораздо больше. В этом примере может потребоваться измерить полноту столбца почтового индекса с помощью одиночного домена. Профилирование с большей вероятностью вы можете предоставить надежные статистические данные по точности для составных доменов, поскольку позволяет измерить точность для нескольких столбцов вместе. Значение этих данных находится в составном агрегате, поэтому может потребоваться измерить точность с помощью составного домена.  
  
 Статистика отображается на вкладке «Профилировщик» на следующих этапах:  
  
-   На этапе **Предварительная обработка записей** службы DQS загружают данные и индексируют их. Обработка производится по одной записи или по одному пакету, поэтому ход выполнения может отображаться по количеству записей. Во время выполнения этого шага может формироваться большинство данных профилирования, за исключением значений **Допустимых в домене** .  
  
-   На этапе **Выполнение правил домена** столбец **Допустимых в домене** заполняется, так как все правила домена выполняются как атомарные единицы для каждого из значений домена.  
  
-   На этапе **Запуск обнаружения** данные на вкладке «Профилировщик» не обновляются. Все обнаруженные синтаксические ошибки можно увидеть на следующем шаге мастера, на этапе **Управление значениями домена**.  
  
 При действии обнаружения знаний уведомления возникают в следующих условиях:  
  
-   В поле отсутствуют новые значения; рекомендуется исключить его из сопоставления.  
  
-   В поле мало новых значений; возможно, его следует исключить из сопоставления.  
  
-   Поле пусто; рекомендуется исключить его из сопоставления.  
  
-   Показатель полноты поля очень низкий. Может потребоваться исключение этого поля из сопоставления.  
  
-   Все значения в поле являются недопустимыми. Следует проверить сопоставление и релевантность правил домена относительно содержания поля.  
  
-   В этом поле низкий уровень допустимых значений. Следует проверить сопоставление и релевантность правил домена относительно содержания поля.  
  
 Дополнительные сведения о профилировании см. в разделе [Профилирование данных и уведомления в DQS](../../2014/data-quality-services/data-profiling-and-notifications-in-dqs.md).  
  
  