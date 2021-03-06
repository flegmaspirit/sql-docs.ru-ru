---
title: Установить новые пакеты R на машины обучения SQL Server Services | Документы Microsoft
description: Добавить новый R-пакеты служб SQL Server 2016 R или обучения машины службы (в базе данных) для SQL Server 2017 г.
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/29/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: e05842a8e8a5a1d2454dbbe500b4d5aa95fca660
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/04/2018
ms.locfileid: "34707082"
---
# <a name="install-new-r-packages-on-sql-server"></a>Установить новые пакеты R на сервере SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

В этой статье описывается установка нового R-пакетов в экземпляр SQL Server, где включена машинного обучения. Существует несколько методов для установки новых пакетов R, в зависимости от версии SQL Server имеется, и является ли сервер подключен к Интернету. Возможны следующие подходы для новой установки пакета.

| Подход                           | Разрешения               | Удаленной или локальной |
|------------------------------------|---------------------------|--------------|
| [Используйте обычную диспетчеров пакетов R](use-r-package-managers-on-sql-server.md)  | Административный | Local |
| [Использование RevoScaleR](use-revoscaler-to-manage-r-packages.md) |  Включен администратора, ролей базы данных после | both|
| [Использование T-SQL (Создание ВНЕШНЕЙ БИБЛИОТЕКИ)](install-r-packages-tsql.md) | Включен администратора, ролей базы данных после | both 

## <a name="who-installs-permissions"></a>Кто устанавливает (разрешения)

Библиотеки пакета R физически расположены в папке Program Files своего экземпляра SQL Server, в защищенную папку с ограниченным доступом. Запись в этом расположении необходимы права администратора.

Администраторы не могут установить пакеты, но в этом случае требуется addititional конфигурации и возможностей, которые недоступны при начальной установке. Существует два подхода для установки пакетов без прав администратора: RevoScaleR, с помощью версии 9.0.1 и более поздней версии, либо с помощью СОЗДАНИЯ ВНЕШНЕЙ БИБЛИОТЕКИ (2017 только SQL Server). В SQL Server 2017 г **dbo_owner** или другой пользователь с разрешением на создание ВНЕШНЕЙ БИБЛИОТЕКИ можно установить пакеты R на текущую базу данных.

R разработчики привыкли к созданию библиотек пользователей для пакетов, которые им необходимы, если центральный библиотеки являются off-limits. Это представляет проблему для код R, выполняемый в экземпляр ядра СУБД SQL Server. SQL Server не может загружать пакеты из внешние библиотеки, даже если этой библиотеки на том же компьютере. Только пакеты из экземпляра библиотеки можно использовать в коде R, выполняющемся на SQL Server.

Обычно доступ к файловой системе ограничен на сервере и даже при наличии прав администратора и доступ в папку документов пользователя на сервере среды выполнения внешнего сценария, выполняющегося в SQL Server не может получить доступ к все пакеты, установленные за пределами экземпляра по умолчанию Библиотека. 

## <a name="considerations-for-package-installation"></a>Рекомендации для установки пакета

Прежде чем устанавливать новые пакеты, рассмотрите возможность подходят ли возможностей данного пакета в среде SQL Server. В среде SQL Server с жесткой требуется избежать следующее:

+ Пакеты, которые требуют доступа к сети
+ Пакеты, которые требуют Java и других платформ, обычно не используется в среде SQL Server
+ Пакеты, которые требуют доступа с повышенными привилегиями файловой системы
+ Пакет используется для веб-разработки или другие задачи, которые не выигрывают, выполнив в SQL Server

## <a name="offline-installation-no-internet-access"></a>Установки в автономном режиме (без доступа к Интернету)

Как правило серверы, на которых размещены рабочие базы данных блокировать подключения к Интернету. Для установки новых пакетов R или Python в таких средах требуется подготовить пакеты и зависимости заранее и скопируйте файлы в папку на сервере для установки в автономном режиме.

Определение всех зависимостей затруднения. Для R, мы рекомендуем использовать [miniCRAN для создания локального репозитория](create-a-local-package-repository-using-minicran.md) и последующей передачи полностью определенную репозитория для изолированного экземпляра SQL Server.

Alternativley, можно выполнить этот шаг вручную.

1. Определите все зависимости пакета. 
2. Проверьте, установлены ли необходимые пакеты на сервере. Если пакет установлен, проверьте правильность версии.
3. Загрузите пакет и все зависимости на отдельный компьютер.
4. Переместите файлы в папку, доступную на сервере.
5. Выполните команду поддерживаемой установки или DDL-инструкции для установки пакета в библиотеку экземпляра.

### <a name="download-the-package-as-a-zipped-file"></a>Загрузить пакет как ZIP-файл

Для установки на сервере без доступа к Интернету необходимо загрузить копию пакета в формате ZIP-файл для установки в автономном режиме. **Не распаковать пакет.**

Например, следующая процедура описывает, чтобы получить правильную версию [FISHalyseR](http://bioconductor.org/packages/release/bioc/html/FISHalyseR.html) пакет с сайта Bioconductor, при условии, что у компьютера есть доступ к Интернету.

1.  В списке **Package Archives** (Архивы пакетов) найдите версию **Windows binary** (Двоичный файл Windows).

2.  Щелкните правой кнопкой мыши ссылку. ZIP-файл и выберите **сохранить объект как**.

3.  Перейдите к локальной папке, где хранятся ZIP-пакеты и нажмите кнопку **Сохранить**.

    Будет создана локальная копия пакета. 

4. Если появляется ошибка загрузки, попробуйте другой зеркальный сайт.

5. После загрузки пакета архива можно установить пакет, или скопируйте ZIP-пакет на сервере, у которого нет доступа к Интернету.

> [!TIP]
> Если по ошибке устанавливается пакет вместо загрузки двоичных файлов, копия загруженный ZIP-файл сохраняется на компьютере. Следите за сообщения о состоянии пакета установки, чтобы определить расположение файла. Этот ZIP-файл можно скопировать на сервер, который не имеет доступа к Интернету.
> 
> Тем не менее при получении пакетов с помощью этого метода зависимости, не включаются. 


## <a name="side-by-side-installation-with-standalone-r-or-python-servers"></a>Параллельную установку с R автономный или серверами Python

В некоторых продуктах Майкрософт, все из которых может сосуществовать на одном компьютере включены возможности R и Python.

Если вы установили обучения компьютера сервера (автономный) для SQL Server 2017 г. Корпорация Майкрософт или SQL Server 2016 R Server (изолированный) помимо аналитика в базе данных (службы SQL Server 2017 г машины обучения и служб R SQL Server 2016), на компьютере уже отдельные установки R для каждого дубликатов средств R и библиотек.

Пакеты, установленные в библиотеку R_SERVER используются только на отдельном сервере и не доступны для экземпляра SQL Server (в базе данных). Всегда используйте `R_SERVICES` библиотеки при установке пакетов, которые вы хотите использовать в базе данных на сервере SQL Server. Дополнительные сведения о путях см. в разделе [библиотеки размещение пакета](installing-and-managing-r-packages.md#package-library-location).


## <a name="see-also"></a>См. также

+ [Установка новых пакетов Python](../python/install-additional-python-packages-on-sql-server.md)
+ [Руководства, примеры, решения](../tutorials/machine-learning-services-tutorials.md)