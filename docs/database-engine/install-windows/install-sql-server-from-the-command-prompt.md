---
title: "Установка SQL Server из командной строки | Документы Майкрософт"
ms.custom: 
ms.date: 09/07/2017
ms.prod:
- sql-server-2016
- sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- server-general
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- installing SQL Server, command prompt
- installation scripts [SQL Server]
- maintenance scripts [SQL Server]
- REMOVENODE property
- components [SQL Server], removing
- command prompt [SQL Server], SQL Server installations
- ASACCOUNT parameter
- failover clustering [SQL Server], installing
- master database [SQL Server], rebuilding
- SQLCOLLATION parameter
- clusters [SQL Server], installing
- unattended installations [SQL Server]
- modifying collations
- AGTPASSWORD parameter
- USESYSDB parameter
- RSPASSWORD parameter
- AUTOSTART parameter
- ASPASSWORD parameter
- stand-alone installations [SQL Server]
- SAMPLEDATABASESERVER parameter
- adding components
- SAPWD parameter
- scripts [SQL Server], uninstallations
- remote installations [SQL Server]
- components [SQL Server], installing
- TARGETCOMPUTER parameter
- REMOVENODE parameter
- REINSTALLMODE parameter
- scripts [SQL Server], maintenance
- rebuilding registry
- SQLPASSWORD parameter
- rebuilding databases
- IP property
- PIDKEY parameter
- RSCONFIGURATION parameter
- ADDLOCAL parameter
- Setup [SQL Server], command prompt
- REBUILDDATABASE parameter
- SECURITYMODE parameter
- REMOVE property
- DISABLENETWORKPROTOCOLS parameter
- INSTALLDATADIR parameter
- REMOVE parameter
- removing components
- SQLACCOUNT parameter
- parameters [SQL Server], SQL Server installations
- UPGRADE parameter
- shortcuts [SQL Server]
- updating components
- removing SQL Server
- clustered instance of SQL Server
- INSTALLSQLDATADIR parameter
- RSACCOUNT parameter
- ADMINPASSWORD parameter
- GROUP property
- ERRORREPORTING property
- uninstallation scripts [SQL Server]
- AGTACCOUNT parameter
- SAVESYSDB parameter
- INSTALLVS parameter
- INSTANCENAME parameter
- scripts [SQL Server], installations
- rebuilding database, master
- uninstalling SQL Server
- ASCOLLATION parameter
- .ini files
- ADDNODE parameter
- command line installations [SQL Server]
- VS parameter
- INSTALLASDATADIR parameter
- INSTALLSQLDIR parameter
- nodes [Faillover Clustering], command prompt
- INSTALLSQLSHAREDDIR parameter
ms.assetid: df40c888-691c-4962-a420-78a57852364d
caps.latest.revision: 255
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 1df54edd5857ac2816fa4b164d268835d9713638
ms.openlocfilehash: 0015d57b64757afb886fb6ded1d5803d93ed13e3
ms.contentlocale: ru-ru
ms.lasthandoff: 09/12/2017

---
# <a name="install-sql-server-from-the-command-prompt"></a>Установка SQL Server из командной строки
  Прежде чем запускать программу установки SQL Server, изучите статью [Планирование установки SQL Server](../../sql-server/install/planning-a-sql-server-installation.md).  
  
 При установке нового экземпляра SQL Server из командной строки можно указать устанавливаемые компоненты и способ их настройки. Также можно выбрать автоматическое, базовое или полное взаимодействие с пользовательским интерфейсом программы установки.  
  
> **ПРИМЕЧАНИЕ.** При установке из командной строки SQL Server поддерживает режим полностью автоматической установки (включается параметром /Q) и режим простой автоматической установки (включается параметром /QS). При указании параметра /QS показывается только ход выполнения, не запрашивается ввод данных и не выводятся сообщения об обнаруженных ошибках. Параметр /QS поддерживается только в случае, когда указан режим /Action=install.  
  
 Независимо от метода установки необходимо подтвердить принятие условий лицензии на ПО от имени физического лица или организации, за исключением случаев, когда использование ПО соответствует отдельному соглашению, такому как соглашение Майкрософт о корпоративном лицензировании или соглашение сторонних производителей с ISV или OEM.  
  
 Условия лицензионного соглашения отображаются для ознакомления и принятия в пользовательском интерфейсе программы установки. Автоматические установки (с использованием параметров /Q или /QS) должны включать параметр /IACCEPTSQLSERVERLICENSETERMS. Ознакомиться с условиями лицензии можно на странице [Условия лицензионного соглашения о программном обеспечении Майкрософт](http://go.microsoft.com/fwlink/?LinkId=148209).  
  
> **ПРИМЕЧАНИЕ.** В зависимости от способа получения программного обеспечения (например, по программе корпоративного лицензирования Майкрософт) на использование ПО могут накладываться дополнительные условия.  
  
 Поддерживаются следующие варианты установки из командной строки.  
  
-   Установка, обновление и удаление экземпляра SQL Server одновременно с общими компонентами на локальном компьютере с использованием синтаксиса и параметров, заданных в командной строке.  
  
-   Установка, обновление или удаление экземпляра отказоустойчивого кластера.  
  
-   Обновление одного выпуска SQL Server до другого выпуска SQL Server.  
  
-   Установка экземпляра SQL Server на локальный компьютер с использованием синтаксиса и параметров, указанных в файле конфигурации. Этот способ можно использовать для копирования конфигурации установки на несколько компьютеров или установки нескольких узлов отказоустойчивого кластера.  
  
 При установке SQL Server из командной строки параметры установки задаются в командной строке в соответствии с синтаксисом команды установки.  
  
> **ПРИМЕЧАНИЕ.** Для локальных установок необходимо запускать программу установки с правами администратора. Если SQL Server устанавливается с удаленного общего ресурса, необходимо использовать учетную запись домена, у которой есть разрешения чтения и записи на этом удаленном ресурсе. Для установок отказоустойчивого кластера необходимо быть локальным администратором с разрешениями, позволяющими входить в систему от имени службы и действовать как часть операционной системы на всех узлах отказоустойчивого кластера.  
  
##  <a name="ProperUse"></a> Правильное использование параметров программы установки  
 Следующие рекомендации помогут вам в создании синтаксически правильных команд установки:  
  
-   /ПАРАМЕТР  
  
-   /ПАРАМЕТР=true/false  
  
-   /ПАРАМЕТР=1/0 для логических типов данных  
  
-   /ПАРАМЕТР="значение" для всех параметров-одиночных значений. Рекомендуется использовать двойные кавычки, а если значение содержит пробел, то их использование обязательно.  
  
-   /ПАРАМЕТР="значение1" "значение2" "значение3" для всех многозначных параметров. Рекомендуется использовать двойные кавычки, а если значение содержит пробел, то их использование обязательно.  
  
 **Исключения:**  
  
-   Параметр /FEATURES является многозначным, но для него используется формат /FEATURES=AS,RS,IS, где не используются пробелы, а значения разделяются запятыми.  
  
 **Примеры:**  
  
-   /INSTANCEDIR=c:\Path поддерживается.  
  
-   /INSTANCEDIR=”c:\Path” поддерживается  
  
> [!NOTE]  
>  -   Если при установке SQL Server указать для INSTANCEDIR и SQLUSERDBDIR один и тот же путь к каталогу, агент SQL Server и полнотекстовый поиск не будут запускаться из-за отсутствия разрешений.  
>   
>      Значения реляционных серверов поддерживают пути в форматах, заканчивающихся обратной косой чертой (один или два символа обратной косой черты).  
> -   /PID — значение для этого параметра следует заключать в двойные кавычки.  
  
## <a name="sql-server-parameters"></a>Параметры SQL Server  
 В следующих разделах представлены параметры, предназначенные для разработки скриптов установки из командной строки в случаях установки, обновления и исправления.  
  
 Параметры, указанные для определенного компонента SQL Server, поддерживаются только этим компонентом. Параметры агента SQL Server и обозревателя SQL Server применяются только во время установки компонента [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
-   [Параметры установки](#Install)  
  
-   [Параметры SysPrep](#SysPrep)  
  
-   [Параметры обновления](#Upgrade)  
  
-   [Параметры исправления](#Repair)  
  
-   [Параметры перестроения системной базы данных](#Rebuild)  
  
-   [Параметры удаления](#Uninstall)  
  
-   [Параметры отказоустойчивого кластера](#ClusterInstall)  
  
-   [Параметры учетных записей служб](#Accounts)  
  
-   [Параметры компонентов](#Feature)  
  
-   [Параметры роли](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md#RoleParameters)  
  
-   [Управление способом отработки отказа с помощью параметра /FAILOVERCLUSTERROLLOWNERSHIP](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md#RollOwnership)  
  
-   [Настройка идентификатора экземпляра или InstanceID](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md#InstanceID) 
  
##  <a name="Install"></a> Параметры установки  
 При разработке скриптов установки из командной строки можно использовать параметры, приведенные в следующей таблице.  
  
|Компонент SQL Server|Параметр|Description|  
|-----------------------------------------|---------------|-----------------|  
|Управление программой установки SQL Server|/ACTION<br /><br /> **Обязательно**|Необходим для указания на рабочий процесс операций установки.<br /><br /> Поддерживаемые значения: **Установка**.|  
|Управление программой установки SQL Server|/IACCEPTSQLSERVERLICENSETERMS<br /><br /> **Требуется только в том случае, если для автоматической установки указан параметр /Q или /QS.**|Требуется для подтверждения принятия условий лицензии.|  
|Управление программой установки SQL Server|/IACCEPTROPENLICENSETERMS <br /><br /> **Требуется только в том случае, если для автоматической установки, включающей службы R (в базе данных) или Microsoft R Server, указан параметр /Q или /QS.**|Требуется для подтверждения принятия условий лицензии.| 
|Управление программой установки SQL Server|/ENU<br /><br /> **Необязательно**|Этот параметр используется для установки англоязычной версии SQL Server в локализованной операционной системе, если на установочном носителе доступны языковые пакеты для английского языка и языка операционной системы.|  
|Управление программой установки SQL Server|/UpdateEnabled<br /><br /> **Необязательно**|Задает, должна ли программа установки SQL Server обнаруживать и включать обновления продукта. Допустимые значения — True и False либо 1 и 0. По умолчанию программа установки SQL Server будет включать найденные обновления.|  
|Управление программой установки SQL Server|/UpdateSource<br /><br /> **Необязательно**|Задает расположение, откуда программа установки SQL Server будет получать обновления продукта. Допустимые значения: "MU" (поиск в Центре обновления [!INCLUDE[msCoName](../../includes/msconame-md.md)] ); допустимый путь к папке, относительный путь (например, .\MyUpdates) или общая папка в формате UNC. По умолчанию программа установки SQL Server выполняет поиск в центре обновления [!INCLUDE[msCoName](../../includes/msconame-md.md)] или в службе обновления Windows через службы Windows Server Update Services.|  
|Управление программой установки SQL Server|/CONFIGURATIONFILE<br /><br /> **Необязательно**|Указывает используемый файл [ConfigurationFile](../../database-engine/install-windows/install-sql-server-2016-using-a-configuration-file.md) .|  
|Управление программой установки SQL Server|/ERRORREPORTING<br /><br /> **Необязательно**|Не оказывает влияния в решении SQL Server 2016. <br/><br/> Сведения о том, как управлять отправкой отзывов об ошибках в корпорацию Майкрософт, см. в статье [How to configure SQL Server 2016 to send feedback to Microsoft](http://support.microsoft.com/kb/3153756)(Как настроить отправку отзывов в корпорацию Майкрософт в SQL Server 2016). <br/><br/>В предыдущих версиях этот компонент задает отправку отчетов об ошибках для SQL Server.<br /><br /> Дополнительные сведения см. в документе [Privacy Statement for the Microsoft Error Reporting Service](http://go.microsoft.com/fwlink/?LinkID=72173)(на английском языке).<br /><br /> Поддерживаемые значения:<br /><br /> 0=отключено<br /><br /> 1 = включено|  
|Управление программой установки SQL Server|/FEATURES<br /><br /> -или-<br /><br /> /ROLE<br /><br /> **Обязательно**|Указывает компоненты для установки.<br /><br /> Выберите **/FEATURES** , чтобы указать отдельные компоненты SQL Server для установки. Дополнительные сведения см. в документе [Параметры компонентов](#Feature) ниже.<br /><br /> Выберите **/ROLE** , чтобы указать роль установки. Роли установки позволяют установить SQL Server в предопределенной конфигурации.|  
|Управление программой установки SQL Server|/HELP, H, ?<br /><br /> **Необязательно**|Отображает варианты использования для параметров установки.|  
|Управление программой установки SQL Server|/INDICATEPROGRESS<br /><br /> **Необязательно**|Указывает, что подробный файл журнала установки выводится на консоль.|  
|Управление программой установки SQL Server|/INSTALLSHAREDDIR<br /><br /> **Необязательно**|Указывает каталог установки, отличный от заданного по умолчанию для 64-разрядных общих компонентов.<br /><br /> Значение по умолчанию — %Program Files%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server<br /><br /> Не может принимать значение %Program Files(x86)%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server|  
|Управление программой установки SQL Server|/INSTALLSHAREDWOWDIR<br /><br /> **Необязательно**|Указывает каталог установки, отличный от заданного по умолчанию для 32-разрядных общих компонентов. Поддерживается только в 64-разрядной системе.<br /><br /> Значение по умолчанию — %Program Files(x86)%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server<br /><br /> Не может принимать значение %Program Files%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server|  
|Управление программой установки SQL Server|/INSTANCEDIR<br /><br /> **Необязательно**|Задает для компонентов, зависящих от экземпляра, каталог установки, отличный от каталога по умолчанию.|  
|Управление программой установки SQL Server|/INSTANCEID<br /><br /> **Необязательно**|Указывает значение идентификатора [InstanceID](#InstanceID), отличное от заданного по умолчанию.|  
|Управление программой установки SQL Server|/INSTANCENAME<br /><br /> **Обязательно**|Указывает имя экземпляра SQL Server.<br /><br /> Дополнительные сведения см. в разделе [Instance Configuration](http://msdn.microsoft.com/library/5bf822fc-6dec-4806-a153-e200af28e9a5).|  
|PolyBase|/PBENGSVCACCOUNT<br /><br /> **Необязательно**|Задает учетную запись для службы ядра. Значение по умолчанию — **NT Authority\NETWORK SERVICE**.|  
|PolyBase|/PBDMSSVCPASSWORD<br /><br /> **Необязательно**|Задает пароль для учетной записи службы ядра.|  
|PolyBase|/PBENGSVCSTARTUPTYPE<br /><br /> **Необязательно**|Задает режим запуска для службы PolyBase Engine: Automatic (автоматически, используется по умолчанию), Disabled (отключена) или Manual (вручную).|  
|PolyBase|/PBPORTRANGE<br /><br /> **Необязательно**|Указывает диапазон портов для служб PolyBase, включающий не менее 6 портов. Пример<br /><br /> `/PBPORTRANGE=16450-16460`|  
|PolyBase|/PBSCALEOUT<br /><br /> **Необязательно**|Указывает, будет ли этот экземпляр SQL Server использоваться в составе вычислительной масштабируемой группы PolyBase. Поддерживаемые значения: **True**, **False**|  
|Управление программой установки SQL Server|/PID<br /><br /> **Необязательно**|Указывает ключ продукта для выпуска SQL Server. Если этот параметр не указан, то используется выпуск Evaluation.|  
|Управление программой установки SQL Server|/Q<br /><br /> **Необязательно**|Указывает, что программа установки работает в тихом режиме (без пользовательского интерфейса). Этот параметр предназначен для автоматической установки.|  
|Управление программой установки SQL Server|/QS<br /><br /> **Необязательно**|Указывает, что программа установки запускается и отображает в пользовательском интерфейсе ход выполнения, но не принимает вводимые значения и не выводит сообщения об ошибке.|  
|Управление программой установки SQL Server|/UIMODE<br /><br /> **Необязательно**|Показывает, нужно ли выводить в ходе установки лишь минимально необходимое количество диалоговых окон.<br /><br /> Параметр**/UIMode** может использоваться только вместе с параметрами **/ACTION=INSTALL** и **UPGRADE** . Поддерживаемые значения:<br /><br /> Значение**/UIMODE=Normal** используется по умолчанию для всех выпусков, кроме Express. В этом случае выводятся все диалоговые окна программы установки для выбранных компонентов.<br /><br /> Значение**/UIMODE=AutoAdvance** используется по умолчанию для выпусков Express. В этом случае необязательные диалоговые окна пропускаются.<br /><br /> <br /><br /> Обратите внимание на то, что в сочетании с другими параметрами **UIMODE** переопределяется. Например, если указаны оба параметра, **/UIMODE=AutoAdvance** и **/ADDCURRENTUSERASSQLADMIN=FALSE** , то диалоговое окно провизионирования не заполняется автоматически в соответствии с текущим пользователем.<br /><br /> Параметр **UIMode** нельзя использовать вместе с параметрами **/Q** и **/QS** .|  
|Управление программой установки SQL Server|/SQMREPORTING<br /><br /> **Необязательно**|Не оказывает влияния в решении SQL Server 2016. <br/><br/>Сведения о том, как управлять отправкой отзывов об ошибках в корпорацию Майкрософт, см. в статье [How to configure SQL Server 2016 to send feedback to Microsoft](http://support.microsoft.com/kb/3153756)(Как настроить отправку отзывов в корпорацию Майкрософт в SQL Server 2016). <br/><br/>В предыдущих версиях этот компонент задает отправку отчетов об использовании компонентов для SQL Server.<br /><br />Поддерживаемые значения:<br /><br /> 0=отключено<br /><br /> 1 = включено|  
|Управление программой установки SQL Server|/HIDECONSOLE<br /><br /> **Необязательно**|Указывает, что окно консоли скрыто или закрыто.|  
|SQL Server, агент|/AGTSVCACCOUNT<br /><br /> **Обязательно**|Задает учетную запись для службы агента SQL Server.|  
|SQL Server, агент|/AGTSVCPASSWORD<br /><br /> [Обязательно](#Accounts)|Задает пароль для учетной записи службы агента SQL Server.|  
|SQL Server, агент|/AGTSVCSTARTUPTYPE<br /><br /> **Необязательно**|Задает режим [запуска](#Accounts) для службы агента SQL Server.<br /><br /> Поддерживаемые значения:<br /><br /> **Автоматически**<br /><br /> **Отключено**<br /><br /> **Вручную**|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASBACKUPDIR<br /><br /> **Необязательно**|Указывает каталог для файлов резервных копий служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Значения по умолчанию:<br /><br /> Для режима WOW в 64-разрядной системе: %Program Files(x86)%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\\<INSTANCEDIR\>\\<ASInstanceID\>\OLAP\Backup.<br /><br /> Для всех других вариантов установки: %Program Files%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\\<INSTANCEDIR\>\\<ASInstanceID\>\OLAP\Backup.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASCOLLATION<br /><br /> **Необязательно**|Задает параметры сортировки для служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].<br /><br /> Значение по умолчанию: **Latin1_General_CI_AS**|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASCONFIGDIR<br /><br /> **Необязательно**|Указывает каталог для файлов конфигурации служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Значения по умолчанию:<br /><br /> Для режима WOW в 64-разрядной системе: %Program Files(x86)%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\\<INSTANCEDIR\>\\<ASInstanceID\>\OLAP\Config.<br /><br /> Для всех других вариантов установки: %Program Files%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\\<INSTANCEDIR\>\\<ASInstanceID\>\OLAP\Config.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASDATADIR<br /><br /> **Необязательно**|Указывает каталог для файлов данных служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Значения по умолчанию:<br /><br /> Для режима WOW в 64-разрядной системе: %Program Files(x86)%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\\<INSTANCEDIR\>\\<ASInstanceID\>\OLAP\Data.<br /><br /> Для всех других вариантов установки: %Program Files%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\\<INSTANCEDIR\>\\<ASInstanceID\>\OLAP\Data.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASLOGDIR<br /><br /> **Необязательно**|Указывает каталог для файлов журналов служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Значения по умолчанию:<br /><br /> Для режима WOW в 64-разрядной системе: %Program Files(x86)%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\\<INSTANCEDIR\>\\<ASInstanceID\>\OLAP\Log.<br /><br /> Для всех других вариантов установки: %Program Files%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\\<INSTANCEDIR\>\\<ASInstanceID\>\OLAP\Log.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASSERVERMODE<br /><br /> **Необязательно**|Указывает режим сервера экземпляра служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Допустимые значения: MULTIDIMENSIONAL, POWERPIVOT или TABULAR. Параметр**ASSERVERMODE** учитывает регистр. Все значения должны задаваться в верхнем регистре. Дополнительные сведения о допустимых значениях см. в разделе [Установка служб Analysis Services](../../analysis-services/instances/install-windows/install-analysis-services.md).|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASSVCACCOUNT<br /><br /> **Обязательно**|Задает учетную запись для службы [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASSVCPASSWORD<br /><br /> [Обязательно](#Accounts)|Указывает пароль для службы [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASSVCSTARTUPTYPE<br /><br /> **Необязательно**|Указывает режим [запуска](#Accounts) для службы [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Поддерживаемые значения:<br /><br /> **Автоматически**<br /><br /> **Отключено**<br /><br /> **Вручную**|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASSYSADMINACCOUNTS<br /><br /> **Обязательно**|Задает учетные данные администратора для служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASTEMPDIR<br /><br /> **Необязательно**|Указывает каталог для временных файлов служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Значения по умолчанию:<br /><br /> Для режима WOW в 64-разрядной системе: %Program Files(x86)%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server \\<INSTANCEDIR\>\\<ASInstanceID\>\OLAP\Temp.<br /><br /> Для всех других вариантов установки: %Program Files%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\\<INSTANCEDIR\>\\<ASInstanceID\>\OLAP\Temp.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASPROVIDERMSOLAP<br /><br /> **Необязательно**|Указывает, может ли поставщик MSOLAP выполняться внутрипроцессно.<br /><br /> Значение по умолчанию: 1 = включено|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/FARMACCOUNT<br /><br /> **Требуется для SPI_AS_NewFarm**|Определяет учетную запись пользователя домена для запуска служб центра администрирования SharePoint и других важных служб на ферме.<br /><br /> Этот параметр используется только для экземпляров служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , которые установлены путем выбора /ROLE = SPI_AS_NEWFARM.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/FARMPASSWORD<br /><br /> **Требуется для SPI_AS_NewFarm**|Позволяет задать пароль для учетной записи фермы.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/PASSPHRASE<br /><br /> **Требуется для SPI_AS_NewFarm**|Определяет парольную фразу, используемую для добавления дополнительных серверов приложений или серверов клиентских веб-интерфейсов к ферме SharePoint.<br /><br /> Этот параметр используется только для экземпляров служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , которые установлены путем выбора /ROLE = SPI_AS_NEWFARM.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/FARMADMINIPORT<br /><br /> **Требуется для SPI_AS_NewFarm**|Определяет порт, используемый для соединения с веб-приложением центра администрирования SharePoint.<br /><br /> Этот параметр используется только для экземпляров служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , которые установлены путем выбора /ROLE = SPI_AS_NEWFARM.|  
|Обозреватель SQL Server|/BROWSERSVCSTARTUPTYPE<br /><br /> **Необязательно**|Указывает режим [запуска](#Accounts) для службы обозревателя SQL Server. Поддерживаемые значения:<br /><br /> **Автоматически**<br /><br /> **Отключено**<br /><br /> **Вручную**|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/ENABLERANU<br /><br /> **Необязательно**|Включает ввод учетных данных в режиме «Запуск от имени» для установки [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] .|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/INSTALLSQLDATADIR<br /><br /> **Необязательно**|Указывает каталог для файлов данных SQL Server. Значения по умолчанию:<br /><br /> Для режима WOW в 64-разрядной системе: %Program Files(x86)%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\\<br /><br /> Для всех других вариантов установки: %Program Files%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SAPWD<br /><br /> **Требуется, если /SECURITYMODE=SQL**|Задает пароль для учетной записи sa SQL Server.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SECURITYMODE<br /><br /> **Необязательно**|Указывает режим безопасности для SQL Server.<br /><br /> Если этот параметр не задан, то поддерживается только режим проверки подлинности Windows.<br /><br /> Поддерживаемое значение: **SQL**|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLBACKUPDIR<br /><br /> **Необязательно**|Указывает каталог для файлов резервных копий.<br /><br /> Значение по умолчанию: \<InstallSQLDataDir>\ \<SQLInstanceID>\MSSQL\Backup|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLCOLLATION<br /><br /> **Необязательно**|Указывает параметры сортировки для SQL Server.<br /><br /> Значение по умолчанию основано на локали операционной системы Windows. Дополнительные сведения см. в разделе [Настройка параметров сортировки в программе установки](http://msdn.microsoft.com/library/ms143508%28v=sql.105%29.aspx).|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/ADDCURRENTUSERASSQLADMIN<br /><br /> **Необязательно**|Добавляет текущего пользователя в предопределенную роль сервера**sysadmin** SQL Server. Параметр /ADDCURRENTUSERASSQLADMIN может использоваться при установке выпусков Express или при использовании /Role=ALLFeatures_WithDefaults. Дополнительные сведения см. в подразделе /ROLE ниже.<br /><br /> Использование /ADDCURRENTUSERASSQLADMIN является необязательным, но обязательным является /ADDCURRENTUSERASSQLADMIN или /SQLSYSADMINACCOUNTS. Значения по умолчанию:<br /><br /> **Верно** для выпусков [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]<br /><br /> **False** для всех остальных выпусков|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLSVCACCOUNT<br /><br /> **Обязательно**|Указывает учетную запись запуска для службы SQL Server.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLSVCPASSWORD<br /><br /> [Обязательно](#Accounts)|Указывает пароль для SQLSVCACCOUNT.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLSVCSTARTUPTYPE<br /><br /> **Необязательно**|Указывает режим [запуска](#Accounts) для службы SQL Server. Поддерживаемые значения:<br /><br /> **Автоматически**<br /><br /> **Отключено**<br /><br /> **Вручную**|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLSYSADMINACCOUNTS<br /><br /> **Обязательно**|С помощью этого параметра имена входа подготавливаются в качестве членов роли sysadmin.<br /><br /> Для выпусков SQL Server, отличных от [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)], параметр /SQLSYSADMINACCOUNTS является обязательным. Для выпусков [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]использование параметра /SQLSYSADMINACCOUNTS является необязательным, но нужно указать один из двух параметров — /SQLSYSADMINACCOUNTS или /ADDCURRENTUSERASSQLADMIN.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBDIR<br /><br /> **Необязательно**|Указывает каталог для файлов данных tempdb. При указании нескольких каталогов их нужно разделять пробелами. Если указано несколько каталогов, файлы данных tempdb будут распределяться по каталогам по методу циклического перебора.<br /><br /> Значение по умолчанию: \<InstallSQLDataDir>\ \<SQLInstanceID>\MSSQL\Data(каталог системных данных)<br /><br /> Примечание. Этот параметр также добавляется к сценарию RebuildDatabase.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBLOGDIR<br /><br /> **Необязательно**|Указывает каталог для файла журнала tempdb.<br /><br /> Значение по умолчанию: \<InstallSQLDataDir>\ \<SQLInstanceID>\MSSQL\Data(каталог системных данных)<br /><br /> Примечание. Этот параметр также добавляется к сценарию RebuildDatabase.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBFILECOUNT<br /><br /> **Необязательно**|Указывает, сколько файлов данных базы данных tempdb должна добавить программа установки. Это значение можно увеличивать до количества ядер. Значение по умолчанию:<br /><br /> 1 для [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]<br /><br /> 8 или количество ядер (меньшее из этих значений) для всех остальных выпусков.<br /><br /> **\*\* Важно! \*\*** Первичным файлом для базы данных tempdb по-прежнему будет tempdb.mdf. Дополнительные файлы tempdb получают имя tempdb_mssql_#.ndf, где вместо # указывается уникальный номер каждого дополнительного файла базы данных tempdb, созданного в процессе установки. Это соглашение об именовании предназначено для того, чтобы обеспечить их уникальность. При удалении экземпляра SQL Server удаляются файлы с именами вида tempdb_mssql_#.ndf. Не используйте соглашение об именах tempdb_mssql_*.ndf для файлов пользовательской базы данных.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBFILESIZE<br /><br /> **Необязательно**|Представлено в [!INCLUDE[SQL VERSION](../../includes/sssql15-md.md)]. Задает первоначальный размер каждого файла данных tempdb.<br/><br/>Значение по умолчанию: 4 МБ для [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)], 8 МБ для всех остальных выпусков.<br/><br/>Минимум: (4 или 8 МБ).<br/><br/>Максимум: 1024 МБ (262 144 МБ для [!INCLUDE[SQL VERSION](../../includes/sssqlv14-md.md)])|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBFILEGROWTH<br /><br /> **Необязательно**|Определяет шаг увеличения размера для файла данных tempdb (в МБ). Значение 0 указывает, что автоматическое приращение отключено и добавление пространства запрещено. Программа установки поддерживает размер до 1024 МБ.<br /><br /> Значение по умолчанию: 64. Допустимый диапазон: минимум = 0, максимум = 1024|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBLOGFILESIZE<br /><br /> **Необязательно**|Представлено в [!INCLUDE[SQL VERSION](../../includes/sssql15-md.md)]. Задает первоначальный размер каждого файла журнала tempdb.<br/><br/>Значение по умолчанию: 4 МБ для [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)], 8 МБ для всех остальных выпусков.<br/><br/>Минимум: (4 или 8 МБ).<br/><br/>Максимум: 1024 МБ (262 144 МБ для [!INCLUDE[SQL VERSION](../../includes/sssqlv14-md.md)])|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBLOGFILEGROWTH<br /><br /> **Необязательно**|Определяет шаг увеличения размера для файла данных tempdb (в МБ). Значение 0 указывает, что автоматическое приращение отключено и добавление пространства запрещено. Программа установки поддерживает размер до 1024 МБ.<br /><br /> Значение по умолчанию: 64. Допустимый диапазон: минимум = 0, максимум = 1024|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLUSERDBDIR<br /><br /> **Необязательно**|Указывает каталог для файлов данных пользовательских баз данных.<br /><br /> Значение по умолчанию: \<InstallSQLDataDir>\ \<SQLInstanceID>\MSSQL\Data|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLSVCINSTANTFILEINIT<br /><br /> **Необязательно**|Включает мгновенную инициализацию файлов для учетной записи службы SQL Server. Вопросы безопасности и производительности рассматриваются в статье [Database Instant File Initialization](../../relational-databases/databases/database-instant-file-initialization.md).<br /><br /> Значение по умолчанию: False<br /><br /> Необязательное значение: True|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLUSERDBLOGDIR<br /><br /> **Необязательно**|Указывает каталог для файлов журнала пользовательских баз данных.<br /><br /> Значение по умолчанию: \<InstallSQLDataDir>\ \<SQLInstanceID>\MSSQL\Data|  
|FILESTREAM|/FILESTREAMLEVEL<br /><br /> **Необязательно**|Указывает уровень доступа для функции FILESTREAM. Поддерживаемые значения:<br /><br /> 0 = отключить поддержку FILESTREAM для данного экземпляра. (Значение по умолчанию)<br /><br /> 1= включить FILESTREAM для доступа с помощью [!INCLUDE[tsql](../../includes/tsql-md.md)] .<br /><br /> 2 = включить FILESTREAM при доступе через [!INCLUDE[tsql](../../includes/tsql-md.md)] и при потоковом доступе файлового ввода-вывода. (Недопустимо для кластерных сценариев.)<br /><br /> 3 = разрешить удаленным клиентам потоковый доступ к данным FILESTREAM.|  
|FILESTREAM|/FILESTREAMSHARENAME<br /><br /> **Необязательно**<br /><br /> **Требуется, если значение FILESTREAMLEVEL больше 1.**|Указывает имя общей папки Windows, в которой будут храниться данные FILESTREAM.|  
|Компонент SQL Server Full-Text Search|/FTSVCACCOUNT<br /><br /> **Необязательно**|Указывает учетную запись для службы запуска полнотекстовой фильтрации.<br /><br /> В [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)]этот параметр не учитывается. Для повышения защищенности передачи данных между SQL Server и управляющей программой полнотекстовой фильтрации используется идентификатор ServiceSID. Если эти значения не указаны, служба запуска полнотекстовой фильтрации будет отключена. Чтобы изменить учетную запись службы и включить полнотекстовые функции, необходимо использовать диспетчер управления SQL Server.<br /><br /> Значение по умолчанию: локальная учетная запись службы|  
|Компонент SQL Server Full-Text Search|/FTSVCPASSWORD<br /><br /> **Необязательно**|Указывает пароль для службы запуска полнотекстовой фильтрации.<br /><br /> В [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)]этот параметр не учитывается.|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|/ISSVCACCOUNT<br /><br /> **Обязательно**|Указывает учетную запись для служб [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].<br /><br /> Значение по умолчанию: NT AUTHORITY\NETWORK SERVICE|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|/ISSVCPASSWORD<br /><br /> [Обязательно](#Accounts)|Указывает пароль для служб [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|/ISSVCStartupType<br /><br /> **Необязательно**|Указывает режим [запуска](#Accounts) для службы [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .|  
|Сетевая конфигурация SQL Server|/NPENABLED<br /><br /> **Необязательно**|Указывает состояние протокола именованных каналов для службы SQL Server. Поддерживаемые значения:<br /><br /> 0 — отключить протокол именованных каналов.<br /><br /> 1 — включить протокол именованных каналов.|  
|Сетевая конфигурация SQL Server|/TCPENABLED<br /><br /> **Необязательно**|Указывает состояние протокола TCP для службы SQL Server. Поддерживаемые значения:<br /><br /> 0 — отключить протокол TCP.<br /><br /> 1 — включить протокол TCP.|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSINSTALLMODE<br /><br /> **Необязательно**|Указывает режим установки для служб [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Поддерживаемые значения:<br /><br /> **SharePointFilesOnlyMode**<br /><br /> **DefaultNativeMode**<br /><br /> **FilesOnlyMode**<br /><br /> <br /><br /> Примечание. Если установка включает компонент SQL Server[!INCLUDE[ssDE](../../includes/ssde-md.md)], то предусмотренным по умолчанию значением для RSINSTALLMODE является DefaultNativeMode.<br /><br /> Если установка не включает компонент SQL Server[!INCLUDE[ssDE](../../includes/ssde-md.md)], то предусмотренным по умолчанию значением для RSINSTALLMODE является FilesOnlyMode.<br /><br /> Если выбрано значение DefaultNativeMode, но установка не включает компонент SQL Server[!INCLUDE[ssDE](../../includes/ssde-md.md)], то в процессе установки автоматически произойдет замена значения RSINSTALLMODE на FilesOnlyMode.|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSSVCACCOUNT<br /><br /> **Обязательно**|Указывает стартовую учетную запись для служб [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSSVCPASSWORD<br /><br /> [Обязательно](#Accounts)|Указывает пароль стартовой учетной записи для службы [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSSVCStartupType<br /><br /> **Необязательно**|Указывает режим [запуска](#Accounts) для службы [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].|  
|Службы R Services (в базе данных)|MRCACHEDIRECTORY|Используйте этот параметр для указания каталога кэша для компонентов Microsoft R Open и Microsoft R Server, как описано в [этом разделе](https://msdn.microsoft.com/library/mt695942.aspx). Этот параметр обычно используется при установке служб SQL Server R Services из командной строки на компьютере без доступа к Интернету.|  
  
###### <a name="sample-syntax"></a>Образец синтаксиса  
 Установка нового изолированного экземпляра с компонентами [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], Full-Text Search и поддержкой репликации и включение мгновенной инициализации файлов для [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. 
  
```  
  
Setup.exe /q /ACTION=Install /FEATURES=SQL /INSTANCENAME=MSSQLSERVER /SQLSVCACCOUNT="<DomainName\UserName>" /SQLSVCPASSWORD="<StrongPassword>" /SQLSYSADMINACCOUNTS="<DomainName\UserName>" /AGTSVCACCOUNT="NT AUTHORITY\Network Service" /SQLSVCINSTANTFILEINIT="True" /IACCEPTSQLSERVERLICENSETERMS  
  
```  
  
##  <a name="SysPrep"></a> Параметры SysPrep  
 Дополнительные сведения о SysPrep в SQL Server см. в разделе  
  
 [Установка SQL Server 2016 с помощью SysPrep](../../database-engine/install-windows/install-sql-server-using-sysprep.md). 
  
#### <a name="prepare-image-parameters"></a>Подготовка параметров образа  
 При разработке сценариев командной строки для подготовки экземпляра SQL Server без настройки можно использовать параметры, приведенные в следующей таблице. 
  
|Компонент SQL Server|Параметр|Description|  
|-----------------------------------------|---------------|-----------------|  
|Управление программой установки SQL Server|/ACTION<br /><br /> **Обязательно**|Необходим для указания на рабочий процесс операций установки.<br /><br /> Поддерживаемые значения: **PrepareImage**|  
|Управление программой установки SQL Server|/IACCEPTSQLSERVERLICENSETERMS<br /><br /> **Требуется только в том случае, если для автоматической установки указан параметр /Q или /QS.**|Требуется для подтверждения принятия условий лицензии.|  
|Управление программой установки SQL Server|/ENU<br /><br /> **Необязательно**|Этот параметр используется для установки англоязычной версии SQL Server в локализованной операционной системе, если на установочном носителе доступны языковые пакеты для английского языка и языка операционной системы.|  
|Управление программой установки SQL Server|/UpdateEnabled<br /><br /> **Необязательно**|Задает, должна ли программа установки SQL Server обнаруживать и включать обновления продукта. Допустимые значения — True и False либо 1 и 0. По умолчанию программа установки SQL Server будет включать найденные обновления.|  
|Управление программой установки SQL Server|/UpdateSource<br /><br /> **Необязательно**|Задает расположение, откуда программа установки SQL Server будет получать обновления продукта. Допустимые значения: "MU" (поиск в Центре обновления [!INCLUDE[msCoName](../../includes/msconame-md.md)] ); допустимый путь к папке, относительный путь (например, .\MyUpdates) или общая папка в формате UNC. По умолчанию программа установки SQL Server выполняет поиск в центре обновления [!INCLUDE[msCoName](../../includes/msconame-md.md)] или в службе обновления Windows через службы Windows Server Update Services.|  
|Управление программой установки SQL Server|/CONFIGURATIONFILE<br /><br /> **Необязательно**|Указывает используемый файл [ConfigurationFile](../../database-engine/install-windows/install-sql-server-2016-using-a-configuration-file.md) .|  
|Управление программой установки SQL Server|/FEATURES<br /><br /> **Обязательно**|Указывает [компоненты](#Feature) для установки.<br /><br /> Поддерживаемые значения: SQLEngine, Replication, FullText, DQ, AS, AS_SPI, RS, RS_SHP, RS_SHPWFE, DQC, Conn, IS, BC, SDK, DREPLAY_CTLR, DREPLAY_CLT, SNAC_SDK, SQLODBC, SQLODBC_SDK, LocalDB, MDS, POLYBASE|  
|Управление программой установки SQL Server|/HELP, H, ?<br /><br /> **Необязательно**|Отображает варианты использования для параметров установки.|  
|Управление программой установки SQL Server|/HIDECONSOLE<br /><br /> **Необязательно**|Указывает, что окно консоли скрыто или закрыто.|  
|Управление программой установки SQL Server|/INDICATEPROGRESS<br /><br /> **Необязательно**|Указывает, что подробный файл журнала установки выводится на консоль.|  
|Управление программой установки SQL Server|/INSTALLSHAREDDIR<br /><br /> **Необязательно**|Указывает каталог установки, отличный от заданного по умолчанию для 64-разрядных общих компонентов.<br /><br /> Значение по умолчанию — %Program Files%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server<br /><br /> Не может принимать значение %Program Files(x86)%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server|  
|Управление программой установки SQL Server|/INSTANCEDIR<br /><br /> **Необязательно**|Задает для компонентов, зависящих от экземпляра, каталог установки, отличный от каталога по умолчанию.|  
|Управление программой установки SQL Server|/INSTANCEID<br /><br /> До [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] с пакетом обновления 1 (SP1) и накопительным обновлением 2 (январь 2013) **Обязательно**<br /><br /> Начиная с [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] с пакетом обновления 1 (SP 1) и накопительным обновлением 2 (CU 2), является **обязательным** для компонентов экземпляра.|Определяет InstanceID для подготавливаемого экземпляра.|  
|PolyBase|/PBENGSVCACCOUNT<br /><br /> **Необязательно**|Задает учетную запись для службы ядра. Значение по умолчанию — **NT Authority\NETWORK SERVICE**.|  
|PolyBase|/PBDMSSVCPASSWORD<br /><br /> **Необязательно**|Задает пароль для учетной записи службы ядра.|  
|PolyBase|/PBENGSVCSTARTUPTYPE<br /><br /> **Необязательно**|Задает режим запуска для службы PolyBase Engine: Automatic (автоматически, используется по умолчанию), Disabled (отключена) или Manual (вручную).|  
|PolyBase|/PBPORTRANGE<br /><br /> **Необязательно**|Указывает диапазон портов для служб PolyBase, включающий не менее 6 портов. Пример<br /><br /> `/PBPORTRANGE=16450-16460`|  
|PolyBase|/PBSCALEOUT<br /><br /> **Необязательно**|Указывает, будет ли этот экземпляр SQL Server использоваться в составе вычислительной масштабируемой группы PolyBase. Поддерживаемые значения: **True**, **False**|  
|Управление программой установки SQL Server|/Q<br /><br /> **Необязательно**|Указывает, что программа установки работает в тихом режиме (без пользовательского интерфейса). Этот параметр предназначен для автоматической установки.|  
|Управление программой установки SQL Server|/QS<br /><br /> **Необязательно**|Указывает, что программа установки запускается и отображает в пользовательском интерфейсе ход выполнения, но не принимает вводимые значения и не выводит сообщения об ошибке.|  
  
###### <a name="sample-syntax"></a>Образец синтаксиса  
 Подготовка нового изолированного экземпляра с компонентами [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], Full-Text Search, поддержкой репликации и службами [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. 
  
```  
Setup.exe /q /ACTION=PrepareImage /FEATURES=SQL,RS /InstanceID =<MYINST> /IACCEPTSQLSERVERLICENSETERMS  
```  
  
#### <a name="complete-image-parameters"></a>Параметры завершения образа  
 При разработке сценариев командной строки для завершения и настройки подготовленного экземпляра SQL Server можно использовать параметры, приведенные в следующей таблице. 
  
|Компонент SQL Server|Параметр|Description|  
|-----------------------------------------|---------------|-----------------|  
|Управление программой установки SQL Server|/ACTION<br /><br /> **Обязательно**|Необходим для указания на рабочий процесс операций установки.<br /><br /> Поддерживаемые значения: **CompleteImage**|  
|Управление программой установки SQL Server|/IACCEPTSQLSERVERLICENSETERMS<br /><br /> **Требуется только в том случае, если для автоматической установки указан параметр /Q или /QS.**|Требуется для подтверждения принятия условий лицензии.|  
|Управление программой установки SQL Server|/ENU<br /><br /> **Необязательно**|Этот параметр используется для установки англоязычной версии SQL Server в локализованной операционной системе, если на установочном носителе доступны языковые пакеты для английского языка и языка операционной системы.|  
|Управление программой установки SQL Server|/CONFIGURATIONFILE<br /><br /> **Необязательно**|Указывает используемый файл [ConfigurationFile](../../database-engine/install-windows/install-sql-server-2016-using-a-configuration-file.md) .|  
|Управление программой установки SQL Server|/ERRORREPORTING<br /><br /> **Необязательно**|Не оказывает влияния в решении SQL Server 2016. <br/><br/>Сведения о том, как управлять отправкой отзывов об ошибках в корпорацию Майкрософт, см. в статье [How to configure SQL Server 2016 to send feedback to Microsoft](http://support.microsoft.com/kb/3153756)(Как настроить отправку отзывов в корпорацию Майкрософт в SQL Server 2016). <br/><br/>В предыдущих версиях этот компонент задает отправку отчетов об ошибках для SQL Server.<br /><br /> Дополнительные сведения см. в документе [Privacy Statement for the Microsoft Error Reporting Service](http://go.microsoft.com/fwlink/?LinkID=72173)(на английском языке). Поддерживаемые значения:<br /><br /> 1 = включено<br /><br /> 0=отключено|  
|Управление программой установки SQL Server|/HELP, H, ?<br /><br /> **Необязательно**|Отображает варианты использования для параметров установки.|  
|Управление программой установки SQL Server|/INDICATEPROGRESS<br /><br /> **Необязательно**|Указывает, что подробный файл журнала установки выводится на консоль.|  
|Управление программой установки SQL Server|/INSTANCEID<br /><br /> До [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] с пакетом обновления 1 (SP1) и накопительным обновлением 2 (январь 2013) **Обязательно**<br /><br /> Начиная с [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] с пакетом обновления 1 (SP1) и накопительным обновлением 2, является **необязательным**|Пользуйтесь Instance ID, указанным на этапе подготовки образа.<br /><br /> Поддерживаемые значения: InstanceID подготовленного экземпляра.|  
|Управление программой установки SQL Server|/INSTANCENAME<br /><br /> До [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] с пакетом обновления 1 (SP1) и накопительным обновлением 2 (январь 2013) **Обязательно**<br /><br /> Начиная с [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] с пакетом обновления 1 (SP1) и накопительным обновлением 2, является **необязательным**|Определяет имя экземпляра SQL Server для завершаемого экземпляра.<br /><br /> Дополнительные сведения см. в разделе [Instance Configuration](http://msdn.microsoft.com/library/5bf822fc-6dec-4806-a153-e200af28e9a5).|  
|PolyBase|/PBENGSVCACCOUNT<br /><br /> **Необязательно**|Задает учетную запись для службы ядра. Значение по умолчанию — **NT Authority\NETWORK SERVICE**.|  
|PolyBase|/PBDMSSVCPASSWORD<br /><br /> **Необязательно**|Задает пароль для учетной записи службы ядра.|  
|PolyBase|/PBENGSVCSTARTUPTYPE<br /><br /> **Необязательно**|Задает режим запуска для службы PolyBase Engine: Automatic (автоматически, используется по умолчанию), Disabled (отключена) или Manual (вручную).|  
|PolyBase|/PBPORTRANGE<br /><br /> **Необязательно**|Указывает диапазон портов для служб PolyBase, включающий не менее 6 портов. Пример<br /><br /> `/PBPORTRANGE=16450-16460`|  
|PolyBase|/PBSCALEOUT<br /><br /> **Необязательно**|Указывает, будет ли этот экземпляр SQL Server использоваться в составе вычислительной масштабируемой группы PolyBase. Поддерживаемые значения: **True**, **False**|  
|Управление программой установки SQL Server|/PID<br /><br /> **Необязательно**|Указывает ключ продукта для выпуска SQL Server. Если этот параметр не указан, то используется выпуск Evaluation.<br /><br /> Примечание. При установке выпуска SQL Server Express, SQL Server Express с набором средств управления или SQL Server Express с дополнительными службами применяется стандартный идентификатор PID.|  
|Управление программой установки SQL Server|/Q<br /><br /> **Необязательно**|Указывает, что программа установки работает в тихом режиме (без пользовательского интерфейса). Этот параметр предназначен для автоматической установки.|  
|Управление программой установки SQL Server|/QS<br /><br /> **Необязательно**|Указывает, что программа установки запускается и отображает в пользовательском интерфейсе ход выполнения, но не принимает вводимые значения и не выводит сообщения об ошибке.|  
|Управление программой установки SQL Server|/SQMREPORTING<br /><br /> **Необязательно**|Не оказывает влияния в решении SQL Server 2016. <br/><br/>Сведения о том, как управлять отправкой отзывов об ошибках в корпорацию Майкрософт, см. в статье [How to configure SQL Server 2016 to send feedback to Microsoft](http://support.microsoft.com/kb/3153756)(Как настроить отправку отзывов в корпорацию Майкрософт в SQL Server 2016). <br/><br/>В предыдущих версиях этот компонент задает отправку отчетов об использовании компонентов для SQL Server.<br /><br />Поддерживаемые значения:<br /><br /> 0=отключено<br /><br /> 1 = включено|  
|Управление программой установки SQL Server|/HIDECONSOLE<br /><br /> **Необязательно**|Указывает, что окно консоли скрыто или закрыто.|  
|SQL Server, агент|/AGTSVCACCOUNT<br /><br /> **Обязательно**|Задает учетную запись для службы агента SQL Server.|  
|SQL Server, агент|/AGTSVCPASSWORD<br /><br /> [Обязательно](#Accounts)|Задает пароль для учетной записи службы агента SQL Server.|  
|SQL Server, агент|/AGTSVCSTARTUPTYPE<br /><br /> **Необязательно**|Задает режим [запуска](#Accounts) для службы агента SQL Server. Поддерживаемые значения:<br /><br /> **Автоматически**<br /><br /> **Отключено**<br /><br /> **Вручную**|  
|Обозреватель SQL Server|/BROWSERSVCSTARTUPTYPE<br /><br /> **Необязательно**|Указывает режим [запуска](#Accounts) для службы обозревателя SQL Server. Поддерживаемые значения:<br /><br /> **Автоматически**<br /><br /> **Отключено**<br /><br /> **Вручную**|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/ENABLERANU<br /><br /> **Необязательно**|Включает ввод учетных данных в режиме "запуск от имени" для установки SQL Server Express.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/INSTALLSQLDATADIR<br /><br /> **Необязательно**|Указывает каталог для файлов данных SQL Server. Значения по умолчанию:<br /><br /> Для режима WOW в 64-разрядной системе: %Program Files(x86)%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\\<br /><br /> Для всех других вариантов установки: %Program Files%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SAPWD<br /><br /> **Требуется, если /SECURITYMODE=SQL**|Задает пароль для учетной записи sa SQL Server.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SECURITYMODE<br /><br /> **Необязательно**|Указывает режим безопасности для SQL Server.<br /><br /> Если этот параметр не задан, то поддерживается только режим проверки подлинности Windows.<br /><br /> Поддерживаемое значение: **SQL**|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLBACKUPDIR<br /><br /> **Необязательно**|Указывает каталог для файлов резервных копий.<br /><br /> Значение по умолчанию:<br /><br /> \<InstallSQLDataDir>\ \<SQLInstanceID>\MSSQL\Backup|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLCOLLATION<br /><br /> **Необязательно**|Указывает параметры сортировки для SQL Server.<br /><br /> Значение по умолчанию основано на локали операционной системы Windows. Дополнительные сведения см. в разделе [Настройка параметров сортировки в программе установки](http://msdn.microsoft.com/library/ms143508%28v=sql.105%29.aspx).|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLSVCACCOUNT<br /><br /> **Обязательно**|Указывает учетную запись запуска для службы SQL Server.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLSVCPASSWORD<br /><br /> [Обязательно](#Accounts)|Указывает пароль для SQLSVCACCOUNT.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLSVCSTARTUPTYPE<br /><br /> **Необязательно**|Указывает режим [запуска](#Accounts) для службы SQL Server. Поддерживаемые значения:<br /><br /> **Автоматически**<br /><br /> **Отключено**<br /><br /> **Вручную**|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLSYSADMINACCOUNTS<br /><br /> **Обязательно**|С помощью этого параметра имена входа подготавливаются в качестве членов роли sysadmin.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBDIR<br /><br /> **Необязательно**|Указывает каталог для файлов данных tempdb. При указании нескольких каталогов их нужно разделять пробелами. Если указано несколько каталогов, файлы данных tempdb будут распределяться по каталогам по методу циклического перебора.<br /><br /> Значение по умолчанию: \<InstallSQLDataDir>\ \<SQLInstanceID>\MSSQL\Data(каталог системных данных)<br /><br /> Примечание. Этот параметр также добавляется к сценарию RebuildDatabase.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBLOGDIR<br /><br /> **Необязательно**|Указывает каталог для файла журнала tempdb.<br /><br /> Значение по умолчанию: \<InstallSQLDataDir>\ \<SQLInstanceID>\MSSQL\Data(каталог системных данных)<br /><br /> Примечание. Этот параметр также добавляется к сценарию RebuildDatabase.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBFILESIZE<br /><br /> **Необязательно**|Представлено в [!INCLUDE[SQL VERSION](../../includes/sssql15-md.md)]. Задает первоначальный размер каждого файла данных tempdb.<br/><br/>Значение по умолчанию: 4 МБ для [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)], 8 МБ для всех остальных выпусков.<br/><br/>Минимум: (4 или 8 МБ).<br/><br/>Максимум: 1024 МБ (262 144 МБ для [!INCLUDE[SQL VERSION](../../includes/sssqlv14-md.md)]).|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBFILEGROWTH<br /><br /> **Необязательно**|Определяет шаг увеличения размера для файла данных tempdb (в МБ). Значение 0 указывает, что автоматическое приращение отключено и добавление пространства запрещено. Программа установки поддерживает размер до 1024 МБ.<br /><br /> Значение по умолчанию: 64.<br /><br /> Допустимый диапазон: минимум = 0, максимум = 1024|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBLOGFILESIZE<br /><br /> **Необязательно**|Задает первоначальный размер файла журнала tempdb (в МБ). Программа установки поддерживает размер до 1024 МБ.<br /><br /> Значение по умолчанию:<br /><br /> 4 для [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]<br /><br /> 8 для всех остальных выпусков.<br /><br /> Допустимый диапазон: минимум = значение по умолчанию (4 или 8), максимум = 1024|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBLOGFILEGROWTH<br /><br /> **Необязательно**|Представлено в [!INCLUDE[SQL VERSION](../../includes/sssql15-md.md)]. Задает первоначальный размер каждого файла журнала tempdb.<br/><br/>Значение по умолчанию: 4 МБ для [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)], 8 МБ для всех остальных выпусков.<br/><br/>Минимум: (4 или 8 МБ).<br/><br/>Максимум: 1024 МБ (262 144 МБ для [!INCLUDE[SQL VERSION](../../includes/sssqlv14-md.md)])|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBFILECOUNT<br /><br /> **Необязательно**|Указывает, сколько файлов данных базы данных tempdb должна добавить программа установки. Это значение можно увеличивать до количества ядер. Значение по умолчанию:<br /><br /> 1 для [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]<br /><br /> 8 или количество ядер (меньшее из этих значений) для всех остальных выпусков.<br /><br /> **\*\* Важно! \*\*** Первичным файлом для базы данных tempdb по-прежнему будет tempdb.mdf. Дополнительные файлы tempdb получают имя tempdb_mssql_#.ndf, где вместо # указывается уникальный номер каждого дополнительного файла базы данных tempdb, созданного в процессе установки. Это соглашение об именовании предназначено для того, чтобы обеспечить их уникальность. При удалении экземпляра SQL Server удаляются файлы с именами вида tempdb_mssql_#.ndf. Не используйте соглашение об именах tempdb_mssql_\*.ndf для файлов пользовательской базы данных.<br /><br /> **\*\* Предупреждение. \*\*** [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]не поддерживается для настройки этого параметра. Программа установки устанавливает только один файл данных tempdb.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLUSERDBDIR<br /><br /> **Необязательно**|Указывает каталог для файлов данных пользовательских баз данных.<br /><br /> Значение по умолчанию: \<InstallSQLDataDir>\ \<SQLInstanceID>\MSSQL\Data|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLUSERDBLOGDIR<br /><br /> **Необязательно**|Указывает каталог для файлов журнала пользовательских баз данных.<br /><br /> Значение по умолчанию: \<InstallSQLDataDir>\ \<SQLInstanceID>\MSSQL\Data|  
|FILESTREAM|/FILESTREAMLEVEL<br /><br /> **Необязательно**|Указывает уровень доступа для функции FILESTREAM. Поддерживаемые значения:<br /><br /> 0 = отключить поддержку FILESTREAM для данного экземпляра. (Значение по умолчанию)<br /><br /> 1= включить FILESTREAM для доступа с помощью [!INCLUDE[tsql](../../includes/tsql-md.md)] .<br /><br /> 2 = включить FILESTREAM при доступе через [!INCLUDE[tsql](../../includes/tsql-md.md)] и при потоковом доступе файлового ввода-вывода. (Недопустимо для кластерных сценариев.)<br /><br /> 3 = разрешить удаленным клиентам потоковый доступ к данным FILESTREAM.|  
|FILESTREAM|/FILESTREAMSHARENAME<br /><br /> **Необязательно**<br /><br /> **Требуется, если значение FILESTREAMLEVEL больше 1.**|Указывает имя общей папки Windows, в которой будут храниться данные FILESTREAM.|  
|Компонент SQL Server Full-Text Search|/FTSVCACCOUNT<br /><br /> **Необязательно**|Указывает учетную запись для службы запуска полнотекстовой фильтрации.<br /><br /> В [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)]этот параметр не учитывается. Для повышения защищенности передачи данных между SQL Server и управляющей программой полнотекстовой фильтрации используется идентификатор ServiceSID. Если эти значения не указаны, служба запуска полнотекстовой фильтрации будет отключена. Чтобы изменить учетную запись службы и включить полнотекстовые функции, необходимо использовать диспетчер управления SQL Server.<br /><br /> Значение по умолчанию: локальная учетная запись службы|  
|Компонент SQL Server Full-Text Search|/FTSVCPASSWORD<br /><br /> **Необязательно**|Указывает пароль для службы запуска полнотекстовой фильтрации.<br /><br /> В [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)]этот параметр не учитывается.|  
|Сетевая конфигурация SQL Server|/NPENABLED<br /><br /> **Необязательно**|Указывает состояние протокола именованных каналов для службы SQL Server. Поддерживаемые значения:<br /><br /> 0 — отключить протокол именованных каналов.<br /><br /> 1 — включить протокол именованных каналов.|  
|Сетевая конфигурация SQL Server|/TCPENABLED<br /><br /> **Необязательно**|Указывает состояние протокола TCP для службы SQL Server. Поддерживаемые значения:<br /><br /> 0 — отключить протокол TCP.<br /><br /> 1 — включить протокол TCP.|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSINSTALLMODE<br /><br /> **Необязательно**|Указывает режим установки для служб [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSSVCACCOUNT<br /><br /> **Обязательно**|Указывает стартовую учетную запись для служб [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSSVCPASSWORD<br /><br /> [Обязательно](#Accounts)|Указывает пароль стартовой учетной записи для службы [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSSVCStartupType<br /><br /> **Необязательно**|Указывает режим [запуска](#Accounts) для службы [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].|  
  
###### <a name="sample-syntax"></a>Образец синтаксиса  
 Завершение подготовленного изолированного экземпляра, включающего компоненты [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], Full-Text Search и поддержку репликации. 
  
```  
  
setup.exe /q /ACTION=CompleteImage /INSTANCENAME=MYNEWINST /INSTANCEID=<MYINST> /SQLSVCACCOUNT="<DomainName\UserName>" /SQLSVCPASSWORD="<StrongPassword>" /SQLSYSADMINACCOUNTS="<DomainName\UserName>" /AGTSVCACCOUNT="NT AUTHORITY\Network Service" /IACCEPTSQLSERVERLICENSETERMS  
  
```  
  
##  <a name="Upgrade"></a> Параметры обновления  
 При разработке скриптов командной строки для обновления можно использовать параметры, приведенные в следующей таблице. 
  
|Компонент SQL Server|Параметр|Description|  
|-----------------------------------------|---------------|-----------------|  
|Управление программой установки SQL Server|/ACTION<br /><br /> **Обязательно**|Необходим для указания на рабочий процесс операций установки. Поддерживаемые значения:<br /><br /> **Обновление**<br /><br /> **EditionUpgrade**<br /><br /> <br /><br /> Значение **EditionUpgrade** используется для обновления существующего выпуска [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] на другой выпуск. Дополнительные сведения о поддерживаемой версии и обновлении выпуском см. в разделе [Supported Version and Edition Upgrades](../../database-engine/install-windows/supported-version-and-edition-upgrades.md).|  
|Управление программой установки SQL Server|/IACCEPTSQLSERVERLICENSETERMS<br /><br /> **Требуется только в том случае, если для автоматической установки указан параметр /Q или /QS.**|Требуется для подтверждения принятия условий лицензии.|  
|Управление программой установки SQL Server|/ENU<br /><br /> **Необязательно**|Этот параметр используется для установки англоязычной версии SQL Server в локализованной операционной системе, если на установочном носителе доступны языковые пакеты для английского языка и языка операционной системы.|  
|Управление программой установки SQL Server|/*UpdateEnabled*<br /><br /> **Необязательно**|Задает, должна ли программа установки SQL Server обнаруживать и включать обновления продукта. Допустимые значения — True и False либо 1 и 0. По умолчанию программа установки SQL Server будет включать найденные обновления.|  
|Управление программой установки SQL Server|/*UpdateSource*<br /><br /> **Необязательно**|Задает расположение, откуда программа установки SQL Server будет получать обновления продукта. Допустимые значения: "MU" (поиск в Центре обновления [!INCLUDE[msCoName](../../includes/msconame-md.md)] ); допустимый путь к папке, относительный путь (например, .\MyUpdates) или общая папка в формате UNC. По умолчанию программа установки SQL Server выполняет поиск в центре обновления [!INCLUDE[msCoName](../../includes/msconame-md.md)] или в службе обновления Windows через службы Windows Server Update Services.|  
|Управление программой установки SQL Server|/CONFIGURATIONFILE<br /><br /> **Необязательно**|Указывает используемый файл [ConfigurationFile](../../database-engine/install-windows/install-sql-server-2016-using-a-configuration-file.md) .|  
|Управление программой установки SQL Server|/ERRORREPORTING<br /><br /> **Необязательно**|Не оказывает влияния в решении SQL Server 2016. <br/><br/>Сведения о том, как управлять отправкой отзывов об ошибках в корпорацию Майкрософт, см. в статье [How to configure SQL Server 2016 to send feedback to Microsoft](http://support.microsoft.com/kb/3153756)(Как настроить отправку отзывов в корпорацию Майкрософт в SQL Server 2016). <br/><br/>В предыдущих версиях этот компонент задает отправку отчетов об ошибках для SQL Server.<br /><br /> Дополнительные сведения см. в документе [Privacy Statement for the Microsoft Error Reporting Service](http://go.microsoft.com/fwlink/?LinkID=72173)(на английском языке). Поддерживаемые значения:<br /><br /> 1 = включено<br /><br /> 0=отключено|  
|Управление программой установки SQL Server|/HELP, H, ?<br /><br /> **Необязательно**|Отображает варианты использования для параметров.|  
|Управление программой установки SQL Server|/INDICATEPROGRESS<br /><br /> **Необязательно**|Указывает, что подробный журнал установки должен быть выведен на консоль.|  
|Управление программой установки SQL Server|/INSTANCEDIR<br /><br /> **Необязательно**|Указывает каталог для общих компонентов, отличный от заданного по умолчанию.|  
|Управление программой установки SQL Server|/INSTANCEID<br /><br /> **Обязательный при обновлении с [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]** или более поздней версии.<br /><br /> **Необязательный при обновлении с [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]**|Указывает значение идентификатора [InstanceID](#InstanceID), отличное от заданного по умолчанию.|  
|Управление программой установки SQL Server|/INSTANCENAME<br /><br /> **Обязательно**|Указывает имя экземпляра SQL Server.<br /><br /> Дополнительные сведения см. в разделе [Instance Configuration](http://msdn.microsoft.com/library/5bf822fc-6dec-4806-a153-e200af28e9a5).|  
|Управление программой установки SQL Server|/PID<br /><br /> **Необязательно**|Указывает ключ продукта для выпуска SQL Server. Если этот параметр не указан, то используется выпуск Evaluation.|  
|Управление программой установки SQL Server|/Q<br /><br /> **Необязательно**|Указывает, что программа установки работает в тихом режиме (без пользовательского интерфейса). Этот параметр предназначен для автоматической установки.|  
|Управление программой установки SQL Server|/UIMODE<br /><br /> **Необязательно**|Показывает, нужно ли выводить в ходе установки лишь минимально необходимое количество диалоговых окон. <br />                Параметр**/UIMode** может использоваться только вместе с параметрами **/ACTION=INSTALL** и **UPGRADE** . Поддерживаемые значения:<br /><br /> Значение**/UIMODE=Normal** используется по умолчанию для всех выпусков, кроме Express. В этом случае выводятся все диалоговые окна программы установки для выбранных компонентов.<br /><br /> Значение**/UIMODE=AutoAdvance** используется по умолчанию для выпусков Express. В этом случае необязательные диалоговые окна пропускаются.<br /><br /> Обратите внимание на то, что параметр **UIMode** нельзя использовать вместе с параметрами **/Q** и **/QS** .|  
|Управление программой установки SQL Server|/SQMREPORTING<br /><br /> **Необязательно**|Не оказывает влияния в решении SQL Server 2016. <br/><br/>Сведения о том, как управлять отправкой отзывов об ошибках в корпорацию Майкрософт, см. в статье [How to configure SQL Server 2016 to send feedback to Microsoft](http://support.microsoft.com/kb/3153756)(Как настроить отправку отзывов в корпорацию Майкрософт в SQL Server 2016). <br/><br/>В предыдущих версиях этот компонент задает отправку отчетов об использовании компонентов для SQL Server.<br /><br />Поддерживаемые значения:<br /><br /> 1 = включено<br /><br /> 0=отключено|  
|Управление программой установки SQL Server|/HIDECONSOLE<br /><br /> **Необязательно**|Указывает, что окно консоли должно быть скрыто или закрыто.|  
|Служба браузера SQL Server|/BROWSERSVCSTARTUPTYPE<br /><br /> **Необязательно**|Указывает режим [запуска](#Accounts) для службы обозревателя SQL Server. Поддерживаемые значения:<br /><br /> **Автоматически**<br /><br /> **Отключено**<br /><br /> **Вручную**|  
|Компонент SQL Server Full-Text Search|/FTUPGRADEOPTION<br /><br /> **Необязательно**|Указывает параметр обновления полнотекстового каталога. Поддерживаемые значения:<br /><br /> **REBUILD**<br /><br /> **RESET**<br /><br /> **IMPORT**|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|/ISSVCACCOUNT<br /><br /> **Обязательно**|Указывает учетную запись для служб [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].<br /><br /> Значение по умолчанию: NT AUTHORITY\NETWORK SERVICE|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|/ISSVCPASSWORD<br /><br /> [Обязательно](#Accounts)|Указывает пароль для служб [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|/ISSVCStartupType<br /><br /> **Необязательно**|Указывает режим [запуска](#Accounts) для службы [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSUPGRADEDATABASEACCOUNT<br /><br /> **Необязательно**|Это свойство используется только при обновлении сервера отчетов с режимом SharePoint версии 2008 R2 или более ранней. Выполняются дополнительные операции обновления для серверов отчетов, использующих более старую архитектуру режима интеграции с SharePoint, которая была изменена в SQL Server 2012 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Если этот параметр не включен при установке из командной строки, для старого экземпляра сервера отчетов используется учетная запись службы по умолчанию. Если это свойство используется, укажите пароль для учетной записи с помощью свойства **/RSUPGRADEPASSWORD** .|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSUPGRADEPASSWORD<br /><br /> **Необязательно**|Пароль существующей учетной записи службы сервера отчетов.|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/ALLOWUPGRADEFORSSRSSHAREPOINTMODE|Параметр требуется при обновлении установки в режиме интеграции с SharePoint, в основе которой лежит архитектура общих служб SharePoint. Этот параметр не требуется для обновления версий служб [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], которые не являются общими.|  
  
###### <a name="sample-syntax"></a>Образец синтаксиса  
 Обновление существующего экземпляра или узла отказоустойчивого кластера с предыдущей версии SQL Server,  
  
```  
Setup.exe /q /ACTION=upgrade /INSTANCEID = <INSTANCEID>/INSTANCENAME=MSSQLSERVER /RSUPGRADEDATABASEACCOUNT="<Provide a SQL Server logon account that can connect to the report server during upgrade>" /RSUPGRADEPASSWORD="<Provide a password for the report server upgrade account>" /ISSVCAccount="NT Authority\Network Service" /IACCEPTSQLSERVERLICENSETERMS  
```  
  
##  <a name="Repair"></a> Параметры исправления  
 При разработке скриптов командной строки для исправления можно использовать параметры, приведенные в следующей таблице. 
  
|Компонент SQL Server|Параметр|Description|  
|-----------------------------------------|---------------|-----------------|  
|Управление программой установки SQL Server|/ACTION<br /><br /> **Обязательно**|Необходим для указания на рабочий процесс операций исправления.<br /><br /> Поддерживаемые значения: **Repair**|  
|Управление программой установки SQL Server|/ENU<br /><br /> **Необязательно**|Этот параметр используется для установки англоязычной версии SQL Server в локализованной операционной системе, если на установочном носителе доступны языковые пакеты для английского языка и языка операционной системы.|  
|Управление программой установки SQL Server|/FEATURES<br /><br /> **Обязательно**|Указывает [компоненты](#Feature) для исправления.|  
|Управление программой установки SQL Server|/INSTANCENAME<br /><br /> **Обязательно**|Указывает имя экземпляра SQL Server.<br /><br /> Дополнительные сведения см. в разделе [Instance Configuration](http://msdn.microsoft.com/library/5bf822fc-6dec-4806-a153-e200af28e9a5).|  
|PolyBase|/PBENGSVCACCOUNT<br /><br /> **Необязательно**|Задает учетную запись для службы ядра. Значение по умолчанию — **NT Authority\NETWORK SERVICE**.|  
|PolyBase|/PBDMSSVCPASSWORD<br /><br /> **Необязательно**|Задает пароль для учетной записи службы ядра.|  
|PolyBase|/PBENGSVCSTARTUPTYPE<br /><br /> **Необязательно**|Задает режим запуска для службы PolyBase Engine: Automatic (автоматически, используется по умолчанию), Disabled (отключена) или Manual (вручную).|  
|PolyBase|/PBPORTRANGE<br /><br /> **Необязательно**|Указывает диапазон портов для служб PolyBase, включающий не менее 6 портов. Пример<br /><br /> `/PBPORTRANGE=16450-16460`|  
|PolyBase|/PBSCALEOUT<br /><br /> **Необязательно**|Указывает, будет ли этот экземпляр SQL Server использоваться в составе вычислительной масштабируемой группы PolyBase. Поддерживаемые значения: **True**, **False**|  
|Управление программой установки SQL Server|/Q<br /><br /> **Необязательно**|Указывает, что программа установки работает в тихом режиме (без пользовательского интерфейса). Этот параметр предназначен для автоматической установки.|  
|Управление программой установки SQL Server|/HIDECONSOLE<br /><br /> **Необязательно**|Указывает, что окно консоли скрыто или закрыто.|  
  
###### <a name="sample-syntax"></a>Образец синтаксиса  
 Исправить экземпляр и общие компоненты. 
  
```  
Setup.exe /q /ACTION=Repair /INSTANCENAME=<instancename>  
```  
  
##  <a name="Rebuild"></a> Параметры перестроения системной базы данных  
 При разработке скриптов, запускаемых из командной строки для перестройки системных баз данных master, model, msdb и tempdb, используются параметры, приведенные в следующей таблице. Дополнительные сведения см. в разделе [Перестроение системных баз данных](../../relational-databases/databases/rebuild-system-databases.md). 
  
|Компонент SQL Server|Параметр|Description|  
|-----------------------------------------|---------------|-----------------|  
|Управление программой установки SQL Server|/ACTION<br /><br /> **Обязательно**|Необходим для указания на рабочий процесс операций перестроения баз данных.<br /><br /> Поддерживаемые значения: **Rebuilddatabase**|  
|Управление программой установки SQL Server|/INSTANCENAME<br /><br /> **Обязательно**|Указывает имя экземпляра SQL Server.<br /><br /> Дополнительные сведения см. в разделе [Instance Configuration](http://msdn.microsoft.com/library/5bf822fc-6dec-4806-a153-e200af28e9a5).|  
|Управление программой установки SQL Server|/Q<br /><br /> **Необязательно**|Указывает, что программа установки работает в тихом режиме (без пользовательского интерфейса). Этот параметр предназначен для автоматической установки.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLCOLLATION<br /><br /> **Необязательно**|Указывает новые параметры сортировки на уровне сервера.<br /><br /> Значение по умолчанию основано на локали операционной системы Windows. Дополнительные сведения см. в разделе [Настройка параметров сортировки в программе установки](http://msdn.microsoft.com/library/ms143508%28v=sql.105%29.aspx).|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SAPWD<br /><br /> **Обязательно, если во время установки экземпляра был указан режим /SECURITYMODE=SQL.**|Указывает пароль для учетной записи SQL SA.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLSYSADMINACCOUNTS<br /><br /> **Обязательно**|С помощью этого параметра имена входа подготавливаются в качестве членов роли sysadmin.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBDIR<br /><br /> **Необязательно**|Указывает каталог для файлов данных tempdb. При указании нескольких каталогов их нужно разделять пробелами. Если указано несколько каталогов, файлы данных tempdb будут распределяться по каталогам по методу циклического перебора.<br /><br /> Значение по умолчанию: \<InstallSQLDataDir>\ \<SQLInstanceID>\MSSQL\Data(каталог системных данных)<br /><br /> Примечание. Этот параметр также добавляется к сценарию RebuildDatabase.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBLOGDIR<br /><br /> **Необязательно**|Указывает каталог для файла журнала tempdb.<br /><br /> Значение по умолчанию: \<InstallSQLDataDir>\ \<SQLInstanceID>\MSSQL\Data(каталог системных данных)<br /><br /> Примечание. Этот параметр также добавляется к сценарию RebuildDatabase.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBFILECOUNT<br /><br /> **Необязательно**|Указывает, сколько файлов данных базы данных tempdb должна добавить программа установки. Это значение можно увеличивать до количества ядер. Значение по умолчанию:<br /><br /> 1 для [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]<br /><br /> 8 или количество ядер (меньшее из этих значений) для всех остальных выпусков.<br /><br /> **\*\* Важно! \*\*** Первичным файлом для базы данных tempdb по-прежнему будет tempdb.mdf. Дополнительные файлы tempdb получают имя tempdb_mssql_#.ndf, где вместо # указывается уникальный номер каждого дополнительного файла базы данных tempdb, созданного в процессе установки. Это соглашение об именовании предназначено для того, чтобы обеспечить их уникальность. При удалении экземпляра SQL Server удаляются файлы с именами вида tempdb_mssql_#.ndf. Не используйте соглашение об именах tempdb_mssql_\*.ndf для файлов пользовательской базы данных.<br /><br /> **\*\* Предупреждение. \*\*** [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]не поддерживается для настройки этого параметра. Программа установки устанавливает только один файл данных tempdb.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBFILESIZE<br /><br /> **Необязательно**|Представлено в [!INCLUDE[SQL VERSION](../../includes/sssql15-md.md)]. Задает первоначальный размер каждого файла данных tempdb.<br/><br/>Значение по умолчанию: 4 МБ для [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)], 8 МБ для всех остальных выпусков.<br/><br/>Минимум: (4 или 8 МБ).<br/><br/>Максимум: 1024 МБ (262 144 МБ для [!INCLUDE[SQL VERSION](../../includes/sssqlv14-md.md)]).|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBFILEGROWTH<br /><br /> **Необязательно**|Определяет шаг увеличения размера для файла данных tempdb (в МБ). Значение 0 указывает, что автоматическое приращение отключено и добавление пространства запрещено. Программа установки поддерживает размер до 1024 МБ.<br /><br /> Значение по умолчанию: 64.<br /><br /> Допустимый диапазон: минимум = 0, максимум = 1024|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBLOGFILESIZE<br /><br /> **Необязательно**|Задает первоначальный размер файла журнала tempdb (в МБ). Программа установки поддерживает размер до 1024 МБ. Значение по умолчанию:<br /><br /> 4 для [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]<br /><br /> 8 для всех остальных выпусков.<br /><br /> Допустимый диапазон: минимум = значение по умолчанию (4 или 8), максимум = 1024|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBLOGFILEGROWTH<br /><br /> **Необязательно**|Представлено в [!INCLUDE[SQL VERSION](../../includes/sssql15-md.md)]. Задает первоначальный размер каждого файла журнала tempdb.<br/><br/>Значение по умолчанию: 4 МБ для [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)], 8 МБ для всех остальных выпусков.<br/><br/>Минимум: (4 или 8 МБ).<br/><br/>Максимум: 1024 МБ (262 144 МБ для [!INCLUDE[SQL VERSION](../../includes/sssqlv14-md.md)])|  
  
##  <a name="Uninstall"></a> Параметры удаления  
 При разработке скриптов командной строки для удаления можно использовать параметры, приведенные в следующей таблице. 
  
|Компонент SQL Server|Параметр|Description|  
|-----------------------------------------|---------------|-----------------|  
|Управление программой установки SQL Server|/ACTION<br /><br /> **Обязательно**|Необходим для указания на поток операций удаления.<br /><br /> Поддерживаемые значения: **Uninstall**|  
|Управление программой установки SQL Server|/CONFIGURATIONFILE<br /><br /> **Необязательно**|Указывает используемый файл [ConfigurationFile](../../database-engine/install-windows/install-sql-server-2016-using-a-configuration-file.md) .|  
|Управление программой установки SQL Server|/FEATURES<br /><br /> **Обязательно**|Указывает удаляемые [компоненты](#Feature) .|  
|Управление программой установки SQL Server|/HELP, H, ?<br /><br /> **Необязательно**|Отображает варианты использования для параметров.|  
|Управление программой установки SQL Server|/INDICATEPROGRESS<br /><br /> **Необязательно**|Указывает, что подробный журнал установки должен быть выведен на консоль.|  
|Управление программой установки SQL Server|/INSTANCENAME<br /><br /> **Обязательно**|Указывает имя экземпляра SQL Server.<br /><br /> Дополнительные сведения см. в разделе [Instance Configuration](http://msdn.microsoft.com/library/5bf822fc-6dec-4806-a153-e200af28e9a5).|  
|Управление программой установки SQL Server|/Q<br /><br /> **Необязательно**|Указывает, что программа установки работает в тихом режиме (без пользовательского интерфейса). Этот параметр предназначен для автоматической установки.|  
|Управление программой установки SQL Server|/HIDECONSOLE<br /><br /> **Необязательно**|Указывает, что окно консоли скрыто или закрыто.|  
  
###### <a name="sample-syntax"></a>Образец синтаксиса  
 Удаление существующего экземпляра SQL Server. 
  
```  
Setup.exe /Action=Uninstall /FEATURES=SQL,AS,RS,IS,Tools /INSTANCENAME=MSSQLSERVER  
```  
  
 Чтобы удалить именованный экземпляр, укажите имя экземпляра вместо имени MSSQLSERVER, указанного в примере, который ранее был приведен в этом разделе. 
  
##  <a name="ClusterInstall"></a> Параметры отказоустойчивого кластера  
 Перед установкой экземпляра отказоустойчивого кластера SQL Server ознакомьтесь со следующими разделами:  
  
-   [Требования к оборудованию и программному обеспечению для установки SQL Server 2016](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)  
  
-   [[Вопросы безопасности при установке SQL Server](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)]
  
-   [Подготовка к установке отказоустойчивого кластера](../../sql-server/failover-clusters/install/before-installing-failover-clustering.md)  
  
-   [Экземпляры отказоустойчивого кластера AlwaysOn &#40;SQL Server&#41;](../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md)  
  
    > [!IMPORTANT]  
    >  Для всех команд установки отказоустойчивого кластера требуется базовый кластер Windows. Все узлы, которые составят отказоустойчивый кластер SQL Server, должны быть частью одного кластера Windows. 
  
 Проверьте следующие скрипты установки отказоустойчивого кластера и внесите необходимые изменения. 
  
#### <a name="integrated-install-failover-cluster-parameters"></a>Параметры интегрированной установки отказоустойчивого кластера  
 При разработке скриптов установки отказоустойчивого кластера из командной строки можно использовать параметры, приведенные в следующей таблице. 
  
 Дополнительные сведения об интегрированной установке см. в статье [Экземпляры отказоустойчивого кластера (режим AlwaysOn) (SQL Server)](../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md). 
  
> **ПРИМЕЧАНИЕ.** Чтобы добавить дополнительные узлы после установки, используйте действие [Добавление узла](#AddNode). 
  
|Компонент SQL Server|Параметр|Сведения|  
|-----------------------------------------|---------------|-------------|  
|Управление программой установки SQL Server|/ACTION<br /><br /> **Обязательно**|Необходим для указания на поток операций установки отказоустойчивого кластера.<br /><br /> Поддерживаемые значения: **InstallFailoverCluster**|  
|Управление программой установки SQL Server|/IACCEPTSQLSERVERLICENSETERMS<br /><br /> **Требуется только в том случае, если для автоматической установки указан параметр /Q или /QS.**|Требуется для подтверждения принятия условий лицензии.|  
|Управление программой установки SQL Server|/ENU<br /><br /> **Необязательно**|Этот параметр используется для установки англоязычной версии SQL Server в локализованной операционной системе, если на установочном носителе доступны языковые пакеты для английского языка и языка операционной системы.|  
|Управление программой установки SQL Server|/FAILOVERCLUSTERGROUP<br /><br /> **Необязательно**|Указывает имя группы ресурсов, используемой для отказоустойчивого кластера SQL Server. Это может быть имя существующей группы кластера или имя новой группы ресурсов.<br /><br /> Значение по умолчанию:<br /><br /> SQL Server (\<имя_экземпляра >)|  
|PolyBase|/PBENGSVCACCOUNT<br /><br /> **Необязательно**|Задает учетную запись для службы ядра. Значение по умолчанию — **NT Authority\NETWORK SERVICE**.|  
|PolyBase|/PBDMSSVCPASSWORD<br /><br /> **Необязательно**|Задает пароль для учетной записи службы ядра.|  
|PolyBase|/PBENGSVCSTARTUPTYPE<br /><br /> **Необязательно**|Задает режим запуска для службы PolyBase Engine: Automatic (автоматически, используется по умолчанию), Disabled (отключена) или Manual (вручную).|  
|PolyBase|/PBPORTRANGE<br /><br /> **Необязательно**|Указывает диапазон портов для служб PolyBase, включающий не менее 6 портов. Пример<br /><br /> `/PBPORTRANGE=16450-16460`|  
|PolyBase|/PBSCALEOUT<br /><br /> **Необязательно**|Указывает, будет ли этот экземпляр SQL Server использоваться в составе вычислительной масштабируемой группы PolyBase. Поддерживаемые значения: **True**, **False**|  
|Управление программой установки SQL Server|/*UpdateEnabled*<br /><br /> **Необязательно**|Задает, должна ли программа установки SQL Server обнаруживать и включать обновления продукта. Допустимые значения — True и False либо 1 и 0. По умолчанию программа установки SQL Server будет включать найденные обновления.|  
|Управление программой установки SQL Server|/*UpdateSource*<br /><br /> **Необязательно**|Задает расположение, откуда программа установки SQL Server будет получать обновления продукта. Допустимые значения: "MU" (поиск в Центре обновления [!INCLUDE[msCoName](../../includes/msconame-md.md)] ); допустимый путь к папке, относительный путь (например, .\MyUpdates) или общая папка в формате UNC. По умолчанию программа установки SQL Server выполняет поиск в центре обновления [!INCLUDE[msCoName](../../includes/msconame-md.md)] или в службе обновления Windows через службы Windows Server Update Services.|  
|Управление программой установки SQL Server|/CONFIGURATIONFILE<br /><br /> **Необязательно**|Указывает используемый файл [ConfigurationFile](../../database-engine/install-windows/install-sql-server-2016-using-a-configuration-file.md) .|  
|Управление программой установки SQL Server|/ERRORREPORTING<br /><br /> **Необязательно**|Не оказывает влияния в решении SQL Server 2016. <br/><br/>Сведения о том, как управлять отправкой отзывов об ошибках в корпорацию Майкрософт, см. в статье [How to configure SQL Server 2016 to send feedback to Microsoft](http://support.microsoft.com/kb/3153756)(Как настроить отправку отзывов в корпорацию Майкрософт в SQL Server 2016). <br/><br/>В предыдущих версиях этот компонент задает отправку отчетов об ошибках для SQL Server.<br /><br /> Дополнительные сведения см. в документе [Privacy Statement for the Microsoft Error Reporting Service](http://go.microsoft.com/fwlink/?LinkID=72173)(на английском языке). Поддерживаемые значения:<br /><br /> 1 = включено<br /><br /> 0=отключено|  
|Управление программой установки SQL Server|/FEATURES<br /><br /> **Обязательно**|Указывает [компоненты](#Feature) для установки.|  
|Управление программой установки SQL Server|/HELP, H, ?<br /><br /> **Необязательно**|Отображает варианты использования для параметров.|  
|Управление программой установки SQL Server|/INDICATEPROGRESS<br /><br /> **Необязательно**|Указывает, что подробный журнал установки должен быть выведен на консоль.|  
|Управление программой установки SQL Server|/INSTALLSHAREDDIR<br /><br /> **Необязательно**|Указывает каталог установки, отличный от заданного по умолчанию для 64-разрядных общих компонентов.<br /><br /> Значение по умолчанию — %Program Files%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server<br /><br /> Не может принимать значение %Program Files(x86)%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server|  
|Управление программой установки SQL Server|/INSTALLSHAREDWOWDIR<br /><br /> **Необязательно**|Указывает каталог установки, отличный от заданного по умолчанию для 32-разрядных общих компонентов. Поддерживается только в 64-разрядной системе.<br /><br /> Значение по умолчанию — %Program Files(x86)%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server<br /><br /> Не может принимать значение %Program Files%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server|  
|Управление программой установки SQL Server|/INSTANCEDIR<br /><br /> **Необязательно**|Задает для компонентов, зависящих от экземпляра, каталог установки, отличный от каталога по умолчанию.|  
|Управление программой установки SQL Server|/INSTANCEID<br /><br /> **Необязательно**|Указывает значение идентификатора [InstanceID](#InstanceID), отличное от заданного по умолчанию.|  
|Управление программой установки SQL Server|/INSTANCENAME<br /><br /> **Обязательно**|Указывает имя экземпляра SQL Server.<br /><br /> Дополнительные сведения см. в разделе [Instance Configuration](http://msdn.microsoft.com/library/5bf822fc-6dec-4806-a153-e200af28e9a5).|  
|Управление программой установки SQL Server|/PID<br /><br /> **Необязательно**|Указывает ключ продукта для выпуска SQL Server. Если этот параметр не указан, то используется выпуск Evaluation.|  
|Управление программой установки SQL Server|/Q<br /><br /> **Необязательно**|Указывает, что программа установки работает в тихом режиме (без пользовательского интерфейса). Этот параметр предназначен для автоматической установки.|  
|Управление программой установки SQL Server|/QS<br /><br /> **Необязательно**|Указывает, что программа установки запускается и отображает в пользовательском интерфейсе ход выполнения, но не принимает вводимые значения и не выводит сообщения об ошибке.|  
|Управление программой установки SQL Server|/SQMREPORTING<br /><br /> **Необязательно**|Не оказывает влияния в решении SQL Server 2016. <br/><br/>Сведения о том, как управлять отправкой отзывов об ошибках в корпорацию Майкрософт, см. в статье [How to configure SQL Server 2016 to send feedback to Microsoft](http://support.microsoft.com/kb/3153756)(Как настроить отправку отзывов в корпорацию Майкрософт в SQL Server 2016). <br/><br/>В предыдущих версиях этот компонент задает отправку отчетов об использовании компонентов для SQL Server.<br /><br />Поддерживаемые значения:<br /><br /> 1 = включено<br /><br /> 0=отключено|  
|Управление программой установки SQL Server|/HIDECONSOLE<br /><br /> **Необязательно**|Указывает, что окно консоли должно быть скрыто или закрыто.|  
|Управление программой установки SQL Server|/FAILOVERCLUSTERDISKS<br /><br /> **Необязательно**|Указывает список общих дисков, которые должны быть включены в группу ресурсов отказоустойчивого кластера SQL Server.<br /><br /> Значение по умолчанию: первый диск используется в качестве диска по умолчанию для всех баз данных.|  
|Управление программой установки SQL Server|/FAILOVERCLUSTERIPADDRESSES<br /><br /> **Обязательно**|Указывает зашифрованный IP-адрес. Шифры разделяются точкой с запятой (;) и имеют формат: \<тип IP>;\<адрес>;\<сетевое имя>;\<маска подсети>. Поддерживаемые типы IP: DHCP, IPv4 и IPv6.<br />Можно указать IP-адреса нескольких отказоустойчивых кластеров, разделив их пробелами. См. следующие примеры.<br /><br /> FAILOVERCLUSTERIPADDRESSES=DEFAULT<br /><br /> FAILOVERCLUSTERIPADDRESSES=IPv4;DHCP;ClusterNetwork1<br /><br /> FAILOVERCLUSTERIPADDRESSES=IPv4;172.16.0.0;ClusterNetwork1;172.31.255.255<br /><br /> FAILOVERCLUSTERIPADDRESSES=IPv6;DHCP;ClusterNetwork1<br /><br /> FAILOVERCLUSTERIPADDRESSES=IPv6;2001:db8:23:1002:20f:1fff:feff:b3a3;ClusterNetwork1|  
|Управление программой установки SQL Server|/FAILOVERCLUSTERNETWORKNAME<br /><br /> **Обязательно**|Указывает сетевое имя для нового отказоустойчивого кластера SQL Server. Это имя используется для идентификации нового экземпляра отказоустойчивого кластера SQL Server в сети.|  
|SQL Server, агент|/AGTSVCACCOUNT<br /><br /> **Обязательно**|Задает учетную запись для службы агента SQL Server.|  
|SQL Server, агент|/AGTSVCPASSWORD<br /><br /> [Обязательно](#Accounts)|Задает пароль для учетной записи службы агента SQL Server.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASBACKUPDIR<br /><br /> **Необязательно**|Указывает каталог для файлов резервных копий служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Значения по умолчанию:<br /><br /> Для режима WOW в 64-разрядной системе: %Program Files(x86)%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\\<INSTANCEDIR\>\\<ASInstanceID\>\OLAP\Backup.<br /><br /> Для всех других вариантов установки: %Program Files%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\\<INSTANCEDIR\>\\<ASInstanceID\>\OLAP\Backup.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASCOLLATION<br /><br /> **Необязательно**|Задает параметры сортировки для служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].<br /><br /> Значение по умолчанию: **Latin1_General_CI_AS**|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASCONFIGDIR<br /><br /> **Необязательно**|Указывает каталог для файлов конфигурации служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Значения по умолчанию:<br /><br /> Для режима WOW в 64-разрядной системе: %Program Files(x86)%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\\<INSTANCEDIR\>\\<ASInstanceID\>\OLAP\Config.<br /><br /> Для всех других вариантов установки: %Program Files%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\\<INSTANCEDIR\>\\<ASInstanceID\>\OLAP\Config.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASDATADIR<br /><br /> **Необязательно**|Указывает каталог для файлов данных служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Значения по умолчанию:<br /><br /> Для режима WOW в 64-разрядной системе: %Program Files(x86)%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\\<INSTANCEDIR\>\\<ASInstanceID\>\OLAP\Data.<br /><br /> Для всех других вариантов установки: %Program Files%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\\<INSTANCEDIR\>\\<ASInstanceID\>\OLAP\Data.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASLOGDIR<br /><br /> **Необязательно**|Указывает каталог для файлов журналов служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Значения по умолчанию:<br /><br /> Для режима WOW в 64-разрядной системе: %Program Files(x86)%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\\<INSTANCEDIR\>\\<ASInstanceID\>\OLAP\Log.<br /><br /> Для всех других вариантов установки: %Program Files%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\\<INSTANCEDIR\>\\<ASInstanceID\>\OLAP\Log.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASSYSADMINACCOUNTS<br /><br /> **Обязательно**|Задает учетные данные администратора для служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASTEMPDIR<br /><br /> **Необязательно**|Указывает каталог для временных файлов служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Значения по умолчанию:<br /><br /> Для режима WOW в 64-разрядной системе: %Program Files(x86)%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\\<INSTANCEDIR\>\\<ASInstanceID\>\OLAP\Temp.<br /><br /> Для всех других вариантов установки: %Program Files%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\\<INSTANCEDIR\>\\<ASInstanceID\>\OLAP\Temp.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASPROVIDERMSOLAP<br /><br /> **Необязательно**|Указывает, может ли поставщик MSOLAP выполняться внутрипроцессно.<br /><br /> Значение по умолчанию: 1 = включено|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASSERVERMODE<br /><br /> **Необязательно**|Указывает режим сервера экземпляра служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Допустимые значения в сценарии кластера — MULTIDIMENSIONAL или TABULAR. Параметр**ASSERVERMODE** учитывает регистр. Все значения должны задаваться в верхнем регистре. Дополнительные сведения о допустимых значениях см. в разделе «Службы Analysis Services в табличном режиме».|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/INSTALLSQLDATADIR<br /><br /> **Обязательно**|Указывает каталог для файлов данных SQL Server.<br /><br /> Необходимо указать каталог данных, который должен располагаться на общем диске кластера.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SAPWD<br /><br /> **Требуется, если /SECURITYMODE=SQL**|Задает пароль для учетной записи sa SQL Server.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SECURITYMODE<br /><br /> **Необязательно**|Указывает режим безопасности для SQL Server.<br /><br /> Если этот параметр не задан, то поддерживается только режим проверки подлинности Windows.<br /><br /> Поддерживаемое значение: **SQL**|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLBACKUPDIR<br /><br /> **Необязательно**|Указывает каталог для файлов резервных копий.<br /><br /> Значение по умолчанию: \<InstallSQLDataDir>\ \<SQLInstanceID>\MSSQL\Backup.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLCOLLATION<br /><br /> **Необязательно**|Указывает параметры сортировки для SQL Server.<br /><br /> Значение по умолчанию основано на локали операционной системы Windows. Дополнительные сведения см. в разделе [Настройка параметров сортировки в программе установки](http://msdn.microsoft.com/library/ms143508%28v=sql.105%29.aspx).|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLSVCACCOUNT<br /><br /> **Обязательно**|Указывает учетную запись запуска для службы SQL Server.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLSVCPASSWORD<br /><br /> [Обязательно](#Accounts)|Указывает пароль для SQLSVCACCOUNT.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLSYSADMINACCOUNTS<br /><br /> **Обязательно**|С помощью этого параметра имена входа подготавливаются в качестве членов роли sysadmin.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLUSERDBDIR<br /><br /> **Необязательно**|Указывает каталог для файлов данных пользовательских баз данных.<br /><br /> Значение по умолчанию: \<InstallSQLDataDir>\ \<SQLInstanceID>\MSSQL\Data|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBDIR<br /><br /> **Необязательно**|Указывает каталог для файлов данных tempdb. При указании нескольких каталогов их нужно разделять пробелами. Если указано несколько каталогов, файлы данных tempdb будут распределяться по каталогам по методу циклического перебора.<br /><br /> Значение по умолчанию: \<InstallSQLDataDir>\ \<SQLInstanceID>\MSSQL\Data(каталог системных данных)<br /><br /> Примечание. Этот параметр также добавляется к сценарию RebuildDatabase.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBLOGDIR<br /><br /> **Необязательно**|Указывает каталог для файла журнала tempdb.<br /><br /> Значение по умолчанию: \<InstallSQLDataDir>\ \<SQLInstanceID>\MSSQL\Data(каталог системных данных)<br /><br /> Примечание. Этот параметр также добавляется к сценарию RebuildDatabase.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBFILECOUNT<br /><br /> **Необязательно**|Указывает, сколько файлов данных базы данных tempdb должна добавить программа установки. Это значение можно увеличивать до количества ядер. Значение по умолчанию:<br /><br /> 1 для [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]<br /><br /> 8 или количество ядер (меньшее из этих значений) для всех остальных выпусков.<br /><br /> **\*\* Важно! \*\*** Первичным файлом для базы данных tempdb по-прежнему будет tempdb.mdf. Дополнительные файлы tempdb получают имя tempdb_mssql_#.ndf, где вместо # указывается уникальный номер каждого дополнительного файла базы данных tempdb, созданного в процессе установки. Это соглашение об именовании предназначено для того, чтобы обеспечить их уникальность. При удалении экземпляра SQL Server удаляются файлы с именами вида tempdb_mssql_#.ndf. Не используйте соглашение об именах tempdb_mssql_\*.ndf для файлов пользовательской базы данных.<br /><br /> **\*\* Предупреждение. \*\*** [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]не поддерживается для настройки этого параметра. Программа установки устанавливает только один файл данных tempdb.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBFILESIZE<br /><br /> **Необязательно**|Представлено в [!INCLUDE[SQL VERSION](../../includes/sssql15-md.md)]. Задает первоначальный размер каждого файла данных tempdb.<br/><br/>Значение по умолчанию: 8 МБ.<br/><br/>Минимум: 8 МБ.<br/><br/>Максимум: 1024 МБ (262 144 МБ для [!INCLUDE[SQL VERSION](../../includes/sssqlv14-md.md)]).|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBFILEGROWTH<br /><br /> **Необязательно**|Определяет шаг увеличения размера для файла данных tempdb (в МБ). Значение 0 указывает, что автоматическое приращение отключено и добавление пространства запрещено. Программа установки поддерживает размер до 1024 МБ.<br /><br /> Значение по умолчанию: 64.<br /><br /> Допустимый диапазон: минимум = 0, максимум = 1024|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBLOGFILESIZE<br /><br /> **Необязательно**|Задает первоначальный размер файла журнала tempdb (в МБ). Программа установки поддерживает размер до 1024 МБ. <br /> Значение по умолчанию:<br /><br /> 4 для [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]<br /><br /> 8 для всех остальных выпусков.<br /><br /> Допустимый диапазон: минимум = значение по умолчанию (4 или 8), максимум = 1024|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBLOGFILEGROWTH<br /><br /> **Необязательно**|Представлено в [!INCLUDE[SQL VERSION](../../includes/sssql15-md.md)]. Задает первоначальный размер каждого файла журнала tempdb.<br/><br/>Значение по умолчанию: 4 МБ для [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)], 8 МБ для всех остальных выпусков.<br/><br/>Минимум: (4 или 8 МБ).<br/><br/>Максимум: 1024 МБ (262 144 МБ для [!INCLUDE[SQL VERSION](../../includes/sssqlv14-md.md)])|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLUSERDBLOGDIR<br /><br /> **Необязательно**|Указывает каталог для файлов журнала пользовательских баз данных.<br /><br /> Значение по умолчанию: \<InstallSQLDataDir>\ \<SQLInstanceID>\MSSQL\Data|  
|FILESTREAM|/FILESTREAMLEVEL<br /><br /> **Необязательно**|Указывает уровень доступа для функции FILESTREAM. Поддерживаемые значения:<br /><br /> 0 = отключить поддержку FILESTREAM для данного экземпляра. (Значение по умолчанию)<br /><br /> 1= включить FILESTREAM для доступа с помощью [!INCLUDE[tsql](../../includes/tsql-md.md)] .<br /><br /> 2 = включить FILESTREAM при доступе через [!INCLUDE[tsql](../../includes/tsql-md.md)] и при потоковом доступе файлового ввода-вывода. (Недопустимо для кластерных сценариев.)<br /><br /> 3 = разрешить удаленным клиентам потоковый доступ к данным FILESTREAM.|  
|FILESTREAM|/FILESTREAMSHARENAME<br /><br /> **Необязательно**<br /><br /> **Требуется, если значение FILESTREAMLEVEL больше 1.**|Указывает имя общей папки Windows, в которой будут храниться данные FILESTREAM.|  
|Компонент SQL Server Full-Text Search|/FTSVCACCOUNT<br /><br /> **Необязательно**|Указывает учетную запись для службы запуска полнотекстовой фильтрации.<br /><br /> В [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)]этот параметр не учитывается. Для повышения защищенности передачи данных между SQL Server и управляющей программой полнотекстовой фильтрации будет использоваться идентификатор ServiceSID.<br /><br /> Если эти значения не указаны, служба запуска полнотекстовой фильтрации будет отключена. Чтобы изменить учетную запись службы и включить полнотекстовые функции, необходимо использовать диспетчер управления SQL Server.<br /><br /> Значение по умолчанию: локальная учетная запись службы|  
|Компонент SQL Server Full-Text Search|/FTSVCPASSWORD<br /><br /> **Необязательно**|Указывает пароль для службы запуска полнотекстовой фильтрации.<br /><br /> В [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)]этот параметр не учитывается.|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|/ISSVCACCOUNT<br /><br /> **Обязательно**|Указывает учетную запись для служб [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].<br /><br /> Значение по умолчанию: NT AUTHORITY\NETWORK SERVICE|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|/ISSVCPASSWORD<br /><br /> [Обязательно](#Accounts)|Указывает пароль для служб [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|/ISSVCStartupType<br /><br /> **Необязательно**|Указывает режим [запуска](#Accounts) для службы [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSINSTALLMODE<br /><br /> **Необязательно**|Указывает режим установки для служб [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSSVCACCOUNT<br /><br /> **Обязательно**|Указывает стартовую учетную запись для служб [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSSVCPASSWORD<br /><br /> [Обязательно](#Accounts)|Указывает пароль стартовой учетной записи для службы [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSSVCStartupType<br /><br /> **Необязательно**|Указывает режим [запуска](#Accounts) для службы [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].|  
  
 Рекомендуется вместо групп домена использовать идентификатор безопасности службы. 
  
##### <a name="additional-notes"></a>Дополнительные замечания  
 Компонент [!INCLUDE[ssDE](../../includes/ssde-md.md)] и службы [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] являются единственными компонентами, поддерживающими работу в кластере. Остальные компоненты не поддерживают работу в кластере и не обеспечивают высокий уровень доступности за счет отработки отказа. 
  
###### <a name="sample-syntax"></a>Образец синтаксиса  
 Установка экземпляра отказоустойчивого кластера SQL Server с одним узлом с компонентами [!INCLUDE[ssDE](../../includes/ssde-md.md)] и службами [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], экземпляр по умолчанию. 
  
```  
setup.exe /q /ACTION=InstallFailoverCluster /InstanceName=MSSQLSERVER /INDICATEPROGRESS /ASSYSADMINACCOUNTS="<DomainName\UserName>" /ASDATADIR=<Drive>:\OLAP\Data /ASLOGDIR=<Drive>:\OLAP\Log /ASBACKUPDIR=<Drive>:\OLAP\Backup /ASCONFIGDIR=<Drive>:\OLAP\Config /ASTEMPDIR=<Drive>:\OLAP\Temp /FAILOVERCLUSTERDISKS="<Cluster Disk Resource Name - for example, 'Disk S:'" /FAILOVERCLUSTERNETWORKNAME="<Insert Network Name>" /FAILOVERCLUSTERIPADDRESSES="IPv4;xx.xxx.xx.xx;Cluster Network;xxx.xxx.xxx.x" /FAILOVERCLUSTERGROUP="MSSQLSERVER" /Features=AS,SQL /ASSVCACCOUNT="<DomainName\UserName>" /ASSVCPASSWORD="xxxxxxxxxxx" /AGTSVCACCOUNT="<DomainName\UserName>" /AGTSVCPASSWORD="xxxxxxxxxxx" /INSTALLSQLDATADIR="<Drive>:\<Path>\MSSQLSERVER" /SQLCOLLATION="SQL_Latin1_General_CP1_CS_AS" /SQLSVCACCOUNT="<DomainName\UserName>" /SQLSVCPASSWORD="xxxxxxxxxxx" /SQLSYSADMINACCOUNTS="<DomainName\UserName> /IACCEPTSQLSERVERLICENSETERMS  
```  
  
#### <a name="prepare-failover-cluster-parameters"></a>Параметры подготовки отказоустойчивого кластера  
 При разработке скриптов подготовки отказоустойчивого кластера из командной строки можно использовать параметры, приведенные в следующей таблице. В качестве первого шага в расширенной установке отказоустойчивого кластера необходимо подготовить экземпляры отказоустойчивого кластера на всех узлах отказоустойчивого кластера. Дополнительные сведения см. в разделе [Экземпляры отказоустойчивого кластера (режим AlwaysOn) (SQL Server)](../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md). 
  
|Компонент SQL Server|Параметр|Description|  
|-----------------------------------------|---------------|-----------------|  
|Управление программой установки SQL Server|/ACTION<br /><br /> **Обязательно**|Необходим для указания на поток операций подготовки отказоустойчивого кластера.<br /><br /> Поддерживаемые значения: **PrepareFailoverCluster**|  
|Управление программой установки SQL Server|/IACCEPTSQLSERVERLICENSETERMS<br /><br /> **Требуется только в том случае, если для автоматической установки указан параметр /Q или /QS.**|Требуется для подтверждения принятия условий лицензии.|  
|Управление программой установки SQL Server|/ENU<br /><br /> **Необязательно**|Этот параметр используется для установки англоязычной версии SQL Server в локализованной операционной системе, если на установочном носителе доступны языковые пакеты для английского языка и языка операционной системы.|  
|Управление программой установки SQL Server|/*UpdateEnabled*<br /><br /> **Необязательно**|Задает, должна ли программа установки SQL Server обнаруживать и включать обновления продукта. Допустимые значения — True и False либо 1 и 0. По умолчанию программа установки SQL Server будет включать найденные обновления.|  
|Управление программой установки SQL Server|/*UpdateSource*<br /><br /> **Необязательно**|Задает расположение, откуда программа установки SQL Server будет получать обновления продукта. Допустимые значения: "MU" (поиск в Центре обновления [!INCLUDE[msCoName](../../includes/msconame-md.md)] ); допустимый путь к папке, относительный путь (например, .\MyUpdates) или общая папка в формате UNC. По умолчанию программа установки SQL Server выполняет поиск в центре обновления [!INCLUDE[msCoName](../../includes/msconame-md.md)] или в службе обновления Windows через службы Windows Server Update Services.|  
|Управление программой установки SQL Server|/CONFIGURATIONFILE<br /><br /> **Необязательно**|Указывает используемый файл [ConfigurationFile](../../database-engine/install-windows/install-sql-server-2016-using-a-configuration-file.md) .|  
|Управление программой установки SQL Server|/ERRORREPORTING<br /><br /> **Необязательно**|Не оказывает влияния в решении SQL Server 2016. <br/><br/>Сведения о том, как управлять отправкой отзывов об ошибках в корпорацию Майкрософт, см. в статье [How to configure SQL Server 2016 to send feedback to Microsoft](http://support.microsoft.com/kb/3153756)(Как настроить отправку отзывов в корпорацию Майкрософт в SQL Server 2016). <br/><br/>В предыдущих версиях этот компонент задает отправку отчетов об ошибках для SQL Server.<br /><br /> Дополнительные сведения см. в документе [Privacy Statement for the Microsoft Error Reporting Service](http://go.microsoft.com/fwlink/?LinkID=72173)(на английском языке). Поддерживаемые значения:<br /><br /> 0=отключено<br /><br /> 1 = включено|  
|Управление программой установки SQL Server|/FEATURES<br /><br /> **Обязательно**|Указывает [компоненты](#Feature) для установки.|  
|Управление программой установки SQL Server|/HELP, H, ?<br /><br /> **Необязательно**|Отображает варианты использования для параметров.|  
|Управление программой установки SQL Server|/INDICATEPROGRESS<br /><br /> **Необязательно**|Указывает, что подробный журнал установки должен быть выведен на консоль.|  
|Управление программой установки SQL Server|/INSTALLSHAREDDIR<br /><br /> **Необязательно**|Указывает каталог установки, отличный от заданного по умолчанию для 64-разрядных общих компонентов.<br /><br /> Значение по умолчанию — %Program Files%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server<br /><br /> Не может принимать значение %Program Files(x86)%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server|  
|Управление программой установки SQL Server|/INSTALLSHAREDWOWDIR<br /><br /> **Необязательно**|Указывает каталог установки, отличный от заданного по умолчанию для 32-разрядных общих компонентов. Поддерживается только в 64-разрядной системе.<br /><br /> Значение по умолчанию — %Program Files(x86)%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server<br /><br /> Не может принимать значение %Program Files%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server|  
|Управление программой установки SQL Server|/INSTANCEDIR<br /><br /> **Необязательно**|Задает для компонентов, зависящих от экземпляра, каталог установки, отличный от каталога по умолчанию.|  
|Управление программой установки SQL Server|/INSTANCEID<br /><br /> **Необязательно**|Указывает значение идентификатора [InstanceID](#InstanceID), отличное от заданного по умолчанию.|  
|Управление программой установки SQL Server|/INSTANCENAME<br /><br /> **Обязательно**|Указывает имя экземпляра SQL Server.<br /><br /> Дополнительные сведения см. в разделе [Instance Configuration](http://msdn.microsoft.com/library/5bf822fc-6dec-4806-a153-e200af28e9a5).|  
|PolyBase|/PBENGSVCACCOUNT<br /><br /> **Необязательно**|Задает учетную запись для службы ядра. Значение по умолчанию — **NT Authority\NETWORK SERVICE**.|  
|PolyBase|/PBDMSSVCPASSWORD<br /><br /> **Необязательно**|Задает пароль для учетной записи службы ядра.|  
|PolyBase|/PBENGSVCSTARTUPTYPE<br /><br /> **Необязательно**|Задает режим запуска для службы PolyBase Engine: Automatic (автоматически, используется по умолчанию), Disabled (отключена) или Manual (вручную).|  
|PolyBase|/PBPORTRANGE<br /><br /> **Необязательно**|Указывает диапазон портов для служб PolyBase, включающий не менее 6 портов. Пример<br /><br /> `/PBPORTRANGE=16450-16460`|  
|PolyBase|/PBSCALEOUT<br /><br /> **Необязательно**|Указывает, будет ли этот экземпляр SQL Server использоваться в составе вычислительной масштабируемой группы PolyBase. Поддерживаемые значения: **True**, **False**|  
|Управление программой установки SQL Server|/PID<br /><br /> **Необязательно**|Указывает ключ продукта для выпуска SQL Server. Если этот параметр не указан,<br /><br /> используется выпуск Evaluation.|  
|Управление программой установки SQL Server|/Q<br /><br /> **Необязательно**|Указывает, что программа установки работает в тихом режиме (без пользовательского интерфейса). Этот параметр предназначен для автоматической установки.|  
|Управление программой установки SQL Server|/QS<br /><br /> **Необязательно**|Указывает, что программа установки запускается и отображает в пользовательском интерфейсе ход выполнения, но не принимает вводимые значения и не выводит сообщения об ошибке.|  
|Управление программой установки SQL Server|/SQMREPORTING<br /><br /> **Необязательно**|Не оказывает влияния в решении SQL Server 2016. <br/><br/>Сведения о том, как управлять отправкой отзывов об ошибках в корпорацию Майкрософт, см. в статье [How to configure SQL Server 2016 to send feedback to Microsoft](http://support.microsoft.com/kb/3153756)(Как настроить отправку отзывов в корпорацию Майкрософт в SQL Server 2016). <br/><br/>В предыдущих версиях этот компонент задает отправку отчетов об использовании компонентов для SQL Server.<br /><br />Поддерживаемые значения:<br /><br /> 0=отключено<br /><br /> 1 = включено|  
|Управление программой установки SQL Server|/HIDECONSOLE<br /><br /> **Необязательно**|Указывает, что окно консоли скрыто или закрыто.|  
|SQL Server, агент|/AGTSVCACCOUNT<br /><br /> **Обязательно**|Задает учетную запись для службы агента SQL Server.|  
|SQL Server, агент|/AGTSVCPASSWORD<br /><br /> [Обязательно](#Accounts)|Задает пароль для учетной записи службы агента SQL Server.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASSVCACCOUNT<br /><br /> **Обязательно**|Задает учетную запись для службы [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASSVCPASSWORD<br /><br /> [Обязательно](#Accounts)|Указывает пароль для службы [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLSVCACCOUNT<br /><br /> **Обязательно**|Указывает учетную запись запуска для службы SQL Server.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLSVCPASSWORD<br /><br /> [Обязательно](#Accounts)|Указывает пароль для SQLSVCACCOUNT.|  
|FILESTREAM|/FILESTREAMLEVEL<br /><br /> **Необязательно**|Указывает уровень доступа для функции FILESTREAM. Поддерживаемые значения:<br /><br /> 0 = отключить поддержку FILESTREAM для данного экземпляра. (Значение по умолчанию)<br /><br /> 1= включить FILESTREAM для доступа с помощью [!INCLUDE[tsql](../../includes/tsql-md.md)] .<br /><br /> 2 = включить FILESTREAM при доступе через [!INCLUDE[tsql](../../includes/tsql-md.md)] и при потоковом доступе файлового ввода-вывода. (Недопустимо для кластерных сценариев.)<br /><br /> 3 = разрешить удаленным клиентам потоковый доступ к данным FILESTREAM.|  
|FILESTREAM|/FILESTREAMSHARENAME<br /><br /> **Необязательно**<br /><br /> **Обязательный** , если значение FILESTREAMLEVEL больше 1.|Указывает имя общей папки Windows, в которой будут храниться данные FILESTREAM.|  
|Компонент SQL Server Full-Text Search|/FTSVCACCOUNT<br /><br /> **Необязательно**|Указывает учетную запись для службы запуска полнотекстовой фильтрации.<br /><br /> В [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)]этот параметр не учитывается. Для повышения защищенности передачи данных между SQL Server и управляющей программой полнотекстовой фильтрации будет использоваться идентификатор ServiceSID.<br /><br /> Если эти значения не указаны, служба запуска полнотекстовой фильтрации будет отключена. Чтобы изменить учетную запись службы и включить полнотекстовые функции, необходимо использовать диспетчер управления SQL Server.<br /><br /> Значение по умолчанию: локальная учетная запись службы|  
|Компонент SQL Server Full-Text Search|/FTSVCPASSWORD<br /><br /> **Необязательно**|Указывает пароль для службы запуска полнотекстовой фильтрации.<br /><br /> В [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)]этот параметр не учитывается.|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|/ISSVCACCOUNT<br /><br /> **Обязательно**|Указывает учетную запись для служб [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].<br /><br /> Значение по умолчанию: NT AUTHORITY\NETWORK SERVICE|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|/ISSVCPASSWORD<br /><br /> [Обязательно](#Accounts)|Указывает пароль для служб [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|/ISSVCStartupType<br /><br /> **Необязательно**|Указывает режим [запуска](#Accounts) для службы [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSINSTALLMODE<br /><br /> **Доступен только в режиме "Только файлы".**|Указывает режим установки для служб [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSSVCACCOUNT<br /><br /> **Обязательно**|Указывает стартовую учетную запись для служб [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSSVCPASSWORD<br /><br /> [Обязательно](#Accounts)|Указывает пароль стартовой учетной записи для службы [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSSVCStartupType<br /><br /> **Необязательно**|Указывает режим [запуска](#Accounts) для службы [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].|  
  
 Рекомендуется вместо групп домена использовать идентификатор безопасности службы. 
  
###### <a name="sample-syntax"></a>Образец синтаксиса  
 Выполнение подготовительного шага при расширенной установке отказоустойчивого кластера для компонента [!INCLUDE[ssDE](../../includes/ssde-md.md)] и служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. 
  
 Чтобы подготовить экземпляр по умолчанию, выполните следующую команду в командной строке:  
  
```  
setup.exe /q /ACTION=PrepareFailoverCluster /InstanceName=MSSQLSERVER /Features=AS,SQL /INDICATEPROGRESS /ASSVCACCOUNT="<DomainName\UserName>" /ASSVCPASSWORD="xxxxxxxxxxx" /SQLSVCACCOUNT="<DomainName\UserName>" /SQLSVCPASSWORD="xxxxxxxxxxx" /AGTSVCACCOUNT="<DomainName\UserName>" /AGTSVCPASSWORD="xxxxxxxxxxx" /IACCEPTSQLSERVERLICENSETERMS  
```  
  
 Чтобы подготовить именованный экземпляр, выполните следующую команду в командной строке:  
  
```  
setup.exe /q /ACTION=PrepareFailoverCluster /InstanceName="<Insert Instance name>" /Features=AS,SQL /INDICATEPROGRESS /ASSVCACCOUNT="<DomainName\UserName>" /ASSVCPASSWORD="xxxxxxxxxxx" /SQLSVCACCOUNT="<DomainName\UserName>" /SQLSVCPASSWORD="xxxxxxxxxxx" /AGTSVCACCOUNT="<DomainName\UserName>" /AGTSVCPASSWORD="xxxxxxxxxxx" /IACCEPTSQLSERVERLICENSETERMS  
```  
  
#### <a name="complete-failover-cluster-parameters"></a>Параметры завершения отказоустойчивого кластера  
 При разработке скриптов завершения отказоустойчивого кластера из командной строки можно использовать параметры, приведенные в следующей таблице. Это действие является вторым шагом в расширенной установке отказоустойчивого кластера. После выполнения подготовки на всех узлах отказоустойчивого кластера необходимо выполнить эту команду на узле, которому принадлежат общие диски. Дополнительные сведения см. в разделе [Экземпляры отказоустойчивого кластера (режим AlwaysOn) (SQL Server)](../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md). 
  
|Компонент SQL Server|Параметр|Description|  
|-----------------------------------------|---------------|-----------------|  
|Управление программой установки SQL Server|/ACTION<br /><br /> **Обязательно**|Необходим для указания на поток операций завершения отказоустойчивого кластера.<br /><br /> Поддерживаемые значения: **CompleteFailoverCluster**|  
|Управление программой установки SQL Server|/ENU<br /><br /> **Необязательно**|Этот параметр используется для установки англоязычной версии SQL Server в локализованной операционной системе, если на установочном носителе доступны языковые пакеты для английского языка и языка операционной системы.|  
|Управление программой установки SQL Server|/FAILOVERCLUSTERGROUP<br /><br /> **Необязательно**|Указывает имя группы ресурсов, используемой для отказоустойчивого кластера SQL Server. Это может быть имя существующей группы кластера или имя новой группы ресурсов.<br /><br /> Значение по умолчанию:<br /><br /> SQL Server (\<имя_экземпляра >)|  
|Управление программой установки SQL Server|/CONFIGURATIONFILE<br /><br /> **Необязательно**|Указывает используемый файл [ConfigurationFile](../../database-engine/install-windows/install-sql-server-2016-using-a-configuration-file.md) .|  
|Управление программой установки SQL Server|/ERRORREPORTING<br /><br /> **Необязательно**|Не оказывает влияния в решении SQL Server 2016. <br/><br/>Сведения о том, как управлять отправкой отзывов об ошибках в корпорацию Майкрософт, см. в статье [How to configure SQL Server 2016 to send feedback to Microsoft](http://support.microsoft.com/kb/3153756)(Как настроить отправку отзывов в корпорацию Майкрософт в SQL Server 2016). <br/><br/>В предыдущих версиях этот компонент задает отправку отчетов об ошибках для SQL Server.<br /><br /> Дополнительные сведения см. в документе [Privacy Statement for the Microsoft Error Reporting Service](http://go.microsoft.com/fwlink/?LinkID=72173)(на английском языке). Поддерживаемые значения:<br /><br /> 1 = включено<br /><br /> 0=отключено|  
|Управление программой установки SQL Server|/HELP, H, ?<br /><br /> **Необязательно**|Отображает варианты использования для параметров.|  
|Управление программой установки SQL Server|/INDICATEPROGRESS<br /><br /> **Необязательно**|Указывает, что подробный журнал установки должен быть выведен на консоль.|  
|Управление программой установки SQL Server|/INSTANCENAME<br /><br /> **Обязательно**|Указывает имя экземпляра SQL Server.<br /><br /> Дополнительные сведения см. в разделе [Instance Configuration](http://msdn.microsoft.com/library/5bf822fc-6dec-4806-a153-e200af28e9a5).|  
|Управление программой установки SQL Server|/PID<br /><br /> **Необязательно**|Указывает ключ продукта для выпуска SQL Server. Если этот параметр не указан, то используется выпуск Evaluation.|  
|Управление программой установки SQL Server|/Q<br /><br /> **Необязательно**|Указывает, что программа установки работает в тихом режиме (без пользовательского интерфейса). Этот параметр предназначен для автоматической установки.|  
|Управление программой установки SQL Server|/QS<br /><br /> **Необязательно**|Указывает, что программа установки запускается и отображает в пользовательском интерфейсе ход выполнения, но не принимает вводимые значения и не выводит сообщения об ошибке.|  
|Управление программой установки SQL Server|/SQMREPORTING<br /><br /> **Необязательно**|Не оказывает влияния в решении SQL Server 2016. <br/><br/>Сведения о том, как управлять отправкой отзывов об ошибках в корпорацию Майкрософт, см. в статье [How to configure SQL Server 2016 to send feedback to Microsoft](http://support.microsoft.com/kb/3153756)(Как настроить отправку отзывов в корпорацию Майкрософт в SQL Server 2016). <br/><br/>В предыдущих версиях этот компонент задает отправку отчетов об использовании компонентов для SQL Server.<br /><br />Поддерживаемые значения:<br /><br /> 1 = включено<br /><br /> 0=отключено|  
|Управление программой установки SQL Server|/HIDECONSOLE<br /><br /> **Необязательно**|Указывает, что окно консоли скрыто или закрыто.|  
|Управление программой установки SQL Server|/FAILOVERCLUSTERDISKS<br /><br /> **Необязательно**|Указывает список общих дисков, которые должны быть включены в группу ресурсов отказоустойчивого кластера SQL Server.<br /><br /> Значение по умолчанию:<br /><br /> Первый диск используется в качестве диска по умолчанию для всех баз данных.|  
|Управление программой установки SQL Server|/FAILOVERCLUSTERIPADDRESSES<br /><br /> **Обязательно**|Указывает зашифрованный IP-адрес. Шифры разделяются точкой с запятой (;) и имеют формат: \<тип IP>;\<адрес>;\<сетевое имя>;\<маска подсети>. Поддерживаемые типы IP: DHCP, IPv4 и IPv6.<br />Можно указать IP-адреса нескольких отказоустойчивых кластеров, разделив их пробелами. См. следующие примеры.<br /><br /> FAILOVERCLUSTERIPADDRESSES=DEFAULT<br /><br /> FAILOVERCLUSTERIPADDRESSES=IPv4;DHCP;ClusterNetwork1<br /><br /> FAILOVERCLUSTERIPADDRESSES=IPv4;172.16.0.0;ClusterNetwork1;172.31.255.255<br /><br /> FAILOVERCLUSTERIPADDRESSES=IPv6;DHCP;ClusterNetwork1<br /><br /> FAILOVERCLUSTERIPADDRESSES=IPv6;2001:db8:23:1002:20f:1fff:feff:b3a3;ClusterNetwork1|  
|Управление программой установки SQL Server|/FAILOVERCLUSTERNETWORKNAME<br /><br /> **Обязательно**|Указывает сетевое имя для нового отказоустойчивого кластера SQL Server. Это имя используется для идентификации нового экземпляра отказоустойчивого кластера SQL Server в сети.|  
|Управление программой установки SQL Server|/CONFIRMIPDEPENDENCYCHANGE|Указывает согласие присвоить зависимости ресурса IP-адреса значение OR для отказоустойчивых кластеров с несколькими подсетями. Дополнительные сведения см. на странице [Создание нового отказоустойчивого кластера SQL Server (программа установки)](../../sql-server/failover-clusters/install/create-a-new-sql-server-failover-cluster-setup.md). Поддерживаемые значения:<br /><br /> 0 = False (значение по умолчанию)<br /><br /> 1 = True|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASBACKUPDIR<br /><br /> **Необязательно**|Указывает каталог для файлов резервных копий служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Значения по умолчанию:<br /><br /> Для режима WOW в 64-разрядной системе: %Program Files(x86)%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\\<INSTANCEDIR\>\\<ASInstanceID\>\OLAP\Backup.<br /><br /> Для всех других вариантов установки: %Program Files%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\\<INSTANCEDIR\>\\<ASInstanceID\>\OLAP\Backup.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASCOLLATION<br /><br /> **Необязательно**|Задает параметры сортировки для служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].<br /><br /> Значение по умолчанию: **Latin1_General_CI_AS**|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASCONFIGDIR<br /><br /> **Необязательно**|Указывает каталог для файлов конфигурации служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Значения по умолчанию:<br /><br /> Для режима WOW в 64-разрядной системе: %Program Files(x86)%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\\<INSTANCEDIR\>\\<ASInstanceID\>\OLAP\Config.<br /><br /> Для всех других вариантов установки: %Program Files%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\\<INSTANCEDIR\>\\<ASInstanceID\>\OLAP\Config.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASDATADIR<br /><br /> **Необязательно**|Указывает каталог для файлов данных служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Значения по умолчанию:<br /><br /> Для режима WOW в 64-разрядной системе: %Program Files(x86)%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\\<INSTANCEDIR\>\\<ASInstanceID\>\OLAP\Data.<br /><br /> Для всех других вариантов установки: %Program Files%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\\<INSTANCEDIR\>\\<ASInstanceID\>\OLAP\Data.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASLOGDIR<br /><br /> **Необязательно**|Указывает каталог для файлов журналов служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Значения по умолчанию:<br /><br /> Для режима WOW в 64-разрядной системе: %Program Files(x86)%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\ \<INSTANCEDIR>\\<ASInstanceID\>\OLAP\Log.<br /><br /> Для всех других вариантов установки: %Program Files%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\ \<INSTANCEDIR>\\<ASInstanceID\>\OLAP\Log.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASSERVERMODE<br /><br /> **Необязательно**|Указывает режим сервера экземпляра служб Analysis Services. Допустимые значения в сценарии кластера — MULTIDIMENSIONAL или TABULAR. Параметр**ASSERVERMODE** учитывает регистр. Все значения должны задаваться в верхнем регистре. Дополнительные сведения о допустимых значениях см. в разделе «Службы Analysis Services в табличном режиме».|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASSYSADMINACCOUNTS<br /><br /> **Обязательно**|Задает учетные данные администратора для служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASTEMPDIR<br /><br /> **Необязательно**|Указывает каталог для временных файлов служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Значение по умолчанию:<br /><br /> Для режима WOW в 64-разрядной системе: %Program Files(x86)%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\ \<INSTANCEDIR>\\<ASInstanceID\>\OLAP\Temp.<br /><br /> Для всех других вариантов установки: %Program Files%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\ \<INSTANCEDIR>\\<ASInstanceID\>\OLAP\Temp.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASPROVIDERMSOLAP<br /><br /> **Необязательно**|Указывает, может ли поставщик MSOLAP выполняться внутрипроцессно.<br /><br /> Значение по умолчанию: 1 = включено|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/INSTALLSQLDATADIR<br /><br /> **Обязательно**|Указывает каталог для файлов данных SQL Server.<br /><br /> Необходимо указать каталог данных, который должен располагаться на общем диске кластера.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SAPWD<br /><br /> **Требуется, если /SECURITYMODE=SQL**|Задает пароль для учетной записи sa SQL Server.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SECURITYMODE<br /><br /> **Необязательно**|Указывает режим безопасности для SQL Server.<br /><br /> Если этот параметр не задан, то поддерживается только режим проверки подлинности Windows<br /><br /> Поддерживаемое значение: **SQL**|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLBACKUPDIR<br /><br /> **Необязательно**|Указывает каталог для файлов резервных копий.<br /><br /> Значение по умолчанию: \<InstallSQLDataDir>\ \<SQLInstanceID>\MSSQL\Backup.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLCOLLATION<br /><br /> **Необязательно**|Указывает параметры сортировки для SQL Server.<br /><br /> Значение по умолчанию основано на локали операционной системы Windows. Дополнительные сведения см. в разделе [Настройка параметров сортировки в программе установки](http://msdn.microsoft.com/library/ms143508%28v=sql.105%29.aspx).|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLSYSADMINACCOUNTS<br /><br /> **Обязательно**|С помощью этого параметра имена входа подготавливаются в качестве членов роли sysadmin.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLUSERDBDIR<br /><br /> **Необязательно**|Указывает каталог для файлов данных пользовательских баз данных.<br /><br /> Значение по умолчанию: \<InstallSQLDataDir>\ \<SQLInstanceID>\MSSQL\Data|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLUSERDBLOGDIR<br /><br /> **Необязательно**|Указывает каталог для файлов журнала пользовательских баз данных.<br /><br /> Значение по умолчанию: \<InstallSQLDataDir>\ \<SQLInstanceID>\MSSQL\Data|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSINSTALLMODE<br /><br /> **Доступен в режиме "Только файлы".**|Указывает режим установки для служб [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBDIR<br /><br /> **Необязательно**|Указывает каталог для файлов данных tempdb. При указании нескольких каталогов их нужно разделять пробелами. Если указано несколько каталогов, файлы данных tempdb будут распределяться по каталогам по методу циклического перебора.<br /><br /> Значение по умолчанию: \<InstallSQLDataDir>\ \<SQLInstanceID>\MSSQL\Data(каталог системных данных)<br /><br /> Примечание. Этот параметр также добавляется к сценарию RebuildDatabase.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBLOGDIR<br /><br /> **Необязательно**|Указывает каталог для файла журнала tempdb.<br /><br /> Значение по умолчанию: \<InstallSQLDataDir>\ \<SQLInstanceID>\MSSQL\Data(каталог системных данных)<br /><br /> Примечание. Этот параметр также добавляется к сценарию RebuildDatabase.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBFILECOUNT<br /><br /> **Необязательно**|Указывает, сколько файлов данных базы данных tempdb должна добавить программа установки. Это значение можно увеличивать до количества ядер. Значение по умолчанию:<br /><br /> 1 для [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]<br /><br /> 8 или количество ядер (меньшее из этих значений) для всех остальных выпусков.<br /><br /> **\*\* Важно! \*\*** Первичным файлом для базы данных tempdb по-прежнему будет tempdb.mdf. Дополнительные файлы tempdb получают имя tempdb_mssql_#.ndf, где вместо # указывается уникальный номер каждого дополнительного файла базы данных tempdb, созданного в процессе установки. Это соглашение об именовании предназначено для того, чтобы обеспечить их уникальность. При удалении экземпляра SQL Server удаляются файлы с именами вида tempdb_mssql_#.ndf. Не используйте соглашение об именах tempdb_mssql_\*.ndf для файлов пользовательской базы данных.<br /><br /> **\*\* Предупреждение. \*\*** [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]не поддерживается для настройки этого параметра. Программа установки устанавливает только один файл данных tempdb.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBFILESIZE<br /><br /> **Необязательно**|Представлено в [!INCLUDE[SQL VERSION](../../includes/sssql15-md.md)]. Задает первоначальный размер каждого файла данных tempdb.<br/><br/>Значение по умолчанию: 8 МБ.<br/><br/>Минимум: 8 МБ.<br/><br/>Максимум: 1024 МБ (262 144 МБ для [!INCLUDE[SQL VERSION](../../includes/sssqlv14-md.md)]).|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBFILEGROWTH<br /><br /> **Необязательно**|Определяет шаг увеличения размера для файла данных tempdb (в МБ). Значение 0 указывает, что автоматическое приращение отключено и добавление пространства запрещено. Программа установки поддерживает размер до 1024 МБ.<br /><br /> Значение по умолчанию: 64.<br /><br /> Допустимый диапазон: минимум = 0, максимум = 1024|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBLOGFILESIZE<br /><br /> **Необязательно**|Задает первоначальный размер файла журнала tempdb (в МБ). Программа установки поддерживает размер до 1024 МБ. <br /> Значение по умолчанию:<br /><br /> 4 для [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]<br /><br /> 8 для всех остальных выпусков.<br /><br /> Допустимый диапазон: минимум = значение по умолчанию (4 или 8), максимум = 1024|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBLOGFILEGROWTH<br /><br /> **Необязательно**|Представлено в [!INCLUDE[SQL VERSION](../../includes/sssql15-md.md)]. Задает первоначальный размер каждого файла журнала tempdb.<br/><br/>Значение по умолчанию: 4 МБ для [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)], 8 МБ для всех остальных выпусков.<br/><br/>Минимум: (4 или 8 МБ).<br/><br/>Максимум: 1024 МБ (262 144 МБ для [!INCLUDE[SQL VERSION](../../includes/sssqlv14-md.md)])|  
  
###### <a name="sample-syntax"></a>Образец синтаксиса  
 Выполнение завершающего шага расширенной установки отказоустойчивого кластера для компонентов [!INCLUDE[ssDE](../../includes/ssde-md.md)] и служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. На компьютере, который станет активным узлом в отказоустойчивом кластере, выполните следующую команду, чтобы его можно было использовать. Действие «CompleteFailoverCluster» необходимо выполнить на узле, на котором находится общий диск в отказоустойчивом кластере служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . 
  
 Чтобы завершить установку отказоустойчивого кластера для экземпляра по умолчанию, выполните следующую команду в командной строке:  
  
```  
setup.exe /q /ACTION=CompleteFailoverCluster /InstanceName=MSSQLSERVER /INDICATEPROGRESS /ASSYSADMINACCOUNTS="<DomainName\Username>" /ASDATADIR=<Drive>:\OLAP\Data /ASLOGDIR=<Drive>:\OLAP\Log /ASBACKUPDIR=<Drive>:\OLAP\Backup /ASCONFIGDIR=<Drive>:\OLAP\Config /ASTEMPDIR=<Drive>:\OLAP\Temp /FAILOVERCLUSTERDISKS="<Cluster Disk Resource Name - for example, 'Disk S:'>:" /FAILOVERCLUSTERNETWORKNAME="<Insert FOI Network Name>" /FAILOVERCLUSTERIPADDRESSES="IPv4;xx.xxx.xx.xx;Cluster Network;xxx.xxx.xxx.x" /FAILOVERCLUSTERGROUP="MSSQLSERVER" /INSTALLSQLDATADIR="<Drive>:\<Path>\MSSQLSERVER" /SQLCOLLATION="SQL_Latin1_General_CP1_CS_AS" /SQLSYSADMINACCOUNTS="<DomainName\UserName>"  
```  
  
 Чтобы завершить установку отказоустойчивого кластера для именованного экземпляра, выполните следующую команду в командной строке:  
  
```  
setup.exe /q /ACTION=CompleteFailoverCluster /InstanceName="<Insert Instance Name>" /INDICATEPROGRESS /ASSYSADMINACCOUNTS="<DomainName\UserName>" /ASDATADIR=<Drive>:\KATMAI\Data /ASLOGDIR=<drive>:\KATMAI\Log /ASBACKUPDIR=<Drive>:\KATMAI\Backup /ASCONFIGDIR=<Drive>:\KATMAI\Config /ASTEMPDIR=<Drive>:\KATMAI\Temp /FAILOVERCLUSTERDISKS="<Cluster Disk Resource Name - for example, 'Disk S:'>" /FAILOVERCLUSTERNETWORKNAME="CompNamedFOI" /FAILOVERCLUSTERIPADDRESSES="IPv4;xx.xxx.xx.xx;ClusterNetwork1;xxx.xxx.xxx.x" /FAILOVERCLUSTERGROUP="<Insert New Group Name>" /INSTALLSQLDATADIR="<Drive>:\<Path>\MSSQLSERVER_KATMAI" /SQLCOLLATION="SQL_Latin1_General_CP1_CS_AS" /SQLSYSADMINACCOUNTS="<DomainName\Username>"  
```  
  
#### <a name="upgrade-failover-cluster-parameters"></a>Параметры обновления отказоустойчивого кластера  
 При разработке скриптов обновления отказоустойчивого кластера из командной строки можно использовать параметры, приведенные в следующей таблице. Дополнительные сведения см. в статьях [Обновление экземпляра отказоустойчивого кластера SQL Server (программа установки)](../../sql-server/failover-clusters/windows/upgrade-a-sql-server-failover-cluster-instance-setup.md) и [Экземпляры отказоустойчивого кластера (режим AlwaysOn) (SQL Server)](../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md). 
  
|Компонент SQL Server|Параметр|Description|  
|-----------------------------------------|---------------|-----------------|  
|Управление программой установки SQL Server|/ACTION<br /><br /> **Обязательно**|Необходим для указания на рабочий процесс операций установки.<br /><br /> Поддерживаемое значение: **Upgrade**|  
|Управление программой установки SQL Server|/IACCEPTSQLSERVERLICENSETERMS<br /><br /> **Требуется только в том случае, если для автоматической установки указан параметр /Q или /QS.**|Требуется для подтверждения принятия условий лицензии.|  
|Управление программой установки SQL Server|/ENU<br /><br /> **Необязательно**|Этот параметр используется для установки англоязычной версии SQL Server в локализованной операционной системе, если на установочном носителе доступны языковые пакеты для английского языка и языка операционной системы.|  
|Управление программой установки SQL Server|/*UpdateEnabled*<br /><br /> **Необязательно**|Задает, должна ли программа установки SQL Server обнаруживать и включать обновления продукта. Допустимые значения — True и False либо 1 и 0. По умолчанию программа установки SQL Server будет включать найденные обновления.|  
|Управление программой установки SQL Server|/*UpdateSource*<br /><br /> **Необязательно**|Задает расположение, откуда программа установки SQL Server будет получать обновления продукта. Допустимые значения: "MU" (поиск в Центре обновления [!INCLUDE[msCoName](../../includes/msconame-md.md)] ); допустимый путь к папке, относительный путь (например, .\MyUpdates) или общая папка в формате UNC. По умолчанию программа установки SQL Server выполняет поиск в центре обновления [!INCLUDE[msCoName](../../includes/msconame-md.md)] или в службе обновления Windows через службы Windows Server Update Services.|  
|Управление программой установки SQL Server|/CONFIGURATIONFILE<br /><br /> **Необязательно**|Указывает используемый файл [ConfigurationFile](../../database-engine/install-windows/install-sql-server-2016-using-a-configuration-file.md) .|  
|Управление программой установки SQL Server|/ERRORREPORTING<br /><br /> **Необязательно**|Не оказывает влияния в решении SQL Server 2016. <br/><br/>Сведения о том, как управлять отправкой отзывов об ошибках в корпорацию Майкрософт, см. в статье [How to configure SQL Server 2016 to send feedback to Microsoft](http://support.microsoft.com/kb/3153756)(Как настроить отправку отзывов в корпорацию Майкрософт в SQL Server 2016). <br/><br/>В предыдущих версиях этот компонент задает отправку отчетов об ошибках для SQL Server.<br /><br /> Дополнительные сведения см. в документе [Privacy Statement for the Microsoft Error Reporting Service](http://go.microsoft.com/fwlink/?LinkID=72173)(на английском языке). Поддерживаемые значения:<br /><br /> 0=отключено<br /><br /> 1 = включено|  
|Управление программой установки SQL Server|/HELP, H, ?<br /><br /> **Необязательно**|Отображает варианты использования для параметров.|  
|Управление программой установки SQL Server|/INDICATEPROGRESS<br /><br /> **Необязательно**|Указывает, что подробный журнал установки должен быть выведен на консоль.|  
|Управление программой установки SQL Server|/INSTANCEDIR<br /><br /> **Необязательно**|Указывает каталог для общих компонентов, отличный от заданного по умолчанию.|  
|Управление программой установки SQL Server|/INSTANCEID<br /><br /> **Обязательный при обновлении с [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] или более поздней версии.**<br /><br /> **Необязательный при обновлении с [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]**|Указывает значение идентификатора [InstanceID](#InstanceID), отличное от заданного по умолчанию.|  
|Управление программой установки SQL Server|/INSTANCENAME<br /><br /> **Обязательно**|Указывает имя экземпляра SQL Server.<br /><br /> Дополнительные сведения см. в разделе [Instance Configuration](http://msdn.microsoft.com/library/5bf822fc-6dec-4806-a153-e200af28e9a5).|  
|Управление программой установки SQL Server|/PID<br /><br /> **Необязательно**|Указывает ключ продукта для выпуска SQL Server. Если этот параметр не указан, то используется выпуск Evaluation.|  
|Управление программой установки SQL Server|/Q<br /><br /> **Необязательно**|Указывает, что программа установки работает в тихом режиме (без пользовательского интерфейса). Этот параметр предназначен для автоматической установки.|  
|Управление программой установки SQL Server|/SQMREPORTING<br /><br /> **Необязательно**|Не оказывает влияния в решении SQL Server 2016. В предыдущих версиях этот компонент задает отправку отчетов об использовании компонентов для SQL Server.<br /><br />Поддерживаемые значения:<br /><br /> 0=отключено<br /><br /> 1 = включено|  
|Управление программой установки SQL Server|/HIDECONSOLE<br /><br /> **Необязательно**|Указывает, что окно консоли скрыто или закрыто.|  
|Управление программой установки SQL Server|/FAILOVERCLUSTERROLLOWNERSHIP|Задает [способ отработки отказа](#RollOwnership) в ходе обновления.|  
|Служба браузера SQL Server|/BROWSERSVCSTARTUPTYPE<br /><br /> **Необязательно**|Указывает режим [запуска](#Accounts) для службы обозревателя SQL Server. Поддерживаемые значения:<br /><br /> **Автоматически**<br /><br /> **Отключено**<br /><br /> **Вручную**|  
|Компонент SQL Server Full-Text Search|/FTUPGRADEOPTION<br /><br /> **Необязательно**|Указывает параметр обновления полнотекстового каталога. Поддерживаемые значения:<br /><br /> **REBUILD**<br /><br /> **RESET**<br /><br /> **IMPORT**|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|/ISSVCACCOUNT<br /><br /> **Обязательно**|Указывает учетную запись для служб [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].<br /><br /> Значение по умолчанию: NT AUTHORITY\NETWORK SERVICE|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|/ISSVCPASSWORD<br /><br /> [Обязательно](#Accounts)|Указывает пароль для служб [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|/ISSVCStartupType<br /><br /> **Необязательно**|Указывает режим [запуска](#Accounts) для службы [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSUPGRADEDATABASEACCOUNT<br /><br /> **Необязательно**|Это свойство используется только при обновлении сервера отчетов с режимом SharePoint версии 2008 R2 или более ранней. Выполняются дополнительные операции обновления для серверов отчетов, использующих более старую архитектуру режима интеграции с SharePoint, которая была изменена в SQL Server 2012 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Если этот параметр не включен при установке из командной строки, для старого экземпляра сервера отчетов используется учетная запись службы по умолчанию. Если это свойство используется, укажите пароль для учетной записи с помощью свойства **/RSUPGRADEPASSWORD** .|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSUPGRADEPASSWORD<br /><br /> **Необязательно**|Пароль существующей учетной записи службы сервера отчетов.|  
  
####  <a name="AddNode"></a> Параметры добавления узла  
 При разработке скриптов командной строки для добавления узла можно использовать параметры, приведенные в следующей таблице. 
  
|Компонент SQL Server|Параметр|Description|  
|-----------------------------------------|---------------|-----------------|  
|Управление программой установки SQL Server|/ACTION<br /><br /> **Обязательно**|Необходим для указания на поток операций добавления узла.<br /><br /> Поддерживаемое значение: **AddNode**|  
|Управление программой установки SQL Server|/IACCEPTSQLSERVERLICENSETERMS<br /><br /> **Требуется только в том случае, если для автоматической установки указан параметр /Q или /QS.**|Требуется для подтверждения принятия условий лицензии.|  
|Управление программой установки SQL Server|/ENU<br /><br /> **Необязательно**|Этот параметр используется для установки англоязычной версии SQL Server в локализованной операционной системе, если на установочном носителе доступны языковые пакеты для английского языка и языка операционной системы.|  
|Управление программой установки SQL Server|/*UpdateEnabled*<br /><br /> **Необязательно**|Задает, должна ли программа установки SQL Server обнаруживать и включать обновления продукта. Допустимые значения — True и False либо 1 и 0. По умолчанию программа установки SQL Server будет включать найденные обновления.|  
|Управление программой установки SQL Server|/*UpdateSource*<br /><br /> **Необязательно**|Задает расположение, откуда программа установки SQL Server будет получать обновления продукта. Допустимые значения: "MU" (поиск в Центре обновления [!INCLUDE[msCoName](../../includes/msconame-md.md)] ); допустимый путь к папке, относительный путь (например, .\MyUpdates) или общая папка в формате UNC. По умолчанию программа установки SQL Server выполняет поиск в центре обновления [!INCLUDE[msCoName](../../includes/msconame-md.md)] или в службе обновления Windows через службы Windows Server Update Services.|  
|Управление программой установки SQL Server|/CONFIGURATIONFILE<br /><br /> **Необязательно**|Указывает используемый файл [ConfigurationFile](../../database-engine/install-windows/install-sql-server-2016-using-a-configuration-file.md) .|  
|Управление программой установки SQL Server|/HELP, H, ?<br /><br /> **Необязательно**|Отображает варианты использования для параметров.|  
|Управление программой установки SQL Server|/INDICATEPROGRESS<br /><br /> **Необязательно**|Указывает, что подробный журнал установки должен быть выведен на консоль.|  
|Управление программой установки SQL Server|/INSTANCENAME<br /><br /> **Обязательно**|Указывает имя экземпляра SQL Server.<br /><br /> Дополнительные сведения см. в разделе [Instance Configuration](http://msdn.microsoft.com/library/5bf822fc-6dec-4806-a153-e200af28e9a5).|  
|PolyBase|/PBENGSVCACCOUNT<br /><br /> **Необязательно**|Задает учетную запись для службы ядра. Значение по умолчанию — **NT Authority\NETWORK SERVICE**.|  
|PolyBase|/PBDMSSVCPASSWORD<br /><br /> **Необязательно**|Задает пароль для учетной записи службы ядра.|  
|PolyBase|/PBENGSVCSTARTUPTYPE<br /><br /> **Необязательно**|Задает режим запуска для службы PolyBase Engine: Automatic (автоматически, используется по умолчанию), Disabled (отключена) или Manual (вручную).|  
|PolyBase|/PBPORTRANGE<br /><br /> **Необязательно**|Указывает диапазон портов для служб PolyBase, включающий не менее 6 портов. Пример<br /><br /> `/PBPORTRANGE=16450-16460`|  
|PolyBase|/PBSCALEOUT<br /><br /> **Необязательно**|Указывает, будет ли этот экземпляр SQL Server использоваться в составе вычислительной масштабируемой группы PolyBase. Поддерживаемые значения: **True**, **False**|  
|Управление программой установки SQL Server|/PID<br /><br /> **Необязательно**|Указывает ключ продукта для выпуска SQL Server. Если этот параметр не указан, то используется выпуск Evaluation.|  
|Управление программой установки SQL Server|/Q<br /><br /> **Необязательно**|Указывает, что программа установки работает в тихом режиме (без пользовательского интерфейса). Этот параметр предназначен для автоматической установки.|  
|Управление программой установки SQL Server|/QS<br /><br /> **Необязательно**|Указывает, что программа установки запускается и отображает в пользовательском интерфейсе ход выполнения, но не принимает вводимые значения и не выводит сообщения об ошибке.|  
|Управление программой установки SQL Server|/HIDECONSOLE<br /><br /> **Необязательно**|Указывает, что окно консоли скрыто или закрыто.|  
|Управление программой установки SQL Server|/FAILOVERCLUSTERIPADDRESSES<br /><br /> **Обязательно**|Указывает зашифрованный IP-адрес. Шифры разделяются точкой с запятой (;) и имеют формат: \<тип IP>;\<адрес>;\<сетевое имя>;\<маска подсети>. Поддерживаемые типы IP: DHCP, IPv4 и IPv6.<br />Можно указать IP-адреса нескольких отказоустойчивых кластеров, разделив их пробелами. См. следующие примеры.<br /><br /> FAILOVERCLUSTERIPADDRESSES=DEFAULT<br /><br /> FAILOVERCLUSTERIPADDRESSES=IPv4;DHCP;ClusterNetwork1<br /><br /> FAILOVERCLUSTERIPADDRESSES=IPv4;172.16.0.0;ClusterNetwork1;172.31.255.255<br /><br /> FAILOVERCLUSTERIPADDRESSES=IPv6;DHCP;ClusterNetwork1<br /><br /> FAILOVERCLUSTERIPADDRESSES=IPv6;2001:db8:23:1002:20f:1fff:feff:b3a3;ClusterNetwork1<br /><br /> <br /><br /> Дополнительные сведения см. на странице [Добавление и удаление узлов в отказоустойчивом кластере SQL Server (настройка)](../../sql-server/failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md).|  
|Управление программой установки SQL Server|/CONFIRMIPDEPENDENCYCHANGE<br /><br /> **Обязательно**|Указывает согласие присвоить зависимости ресурса IP-адреса значение OR для отказоустойчивых кластеров с несколькими подсетями. Дополнительные сведения см. на странице [Добавление и удаление узлов в отказоустойчивом кластере SQL Server (настройка)](../../sql-server/failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md). Поддерживаемые значения.<br /><br /> 0 = False (значение по умолчанию)<br /><br /> 1 = True|  
|SQL Server, агент|/AGTSVCACCOUNT<br /><br /> **Обязательно**|Задает учетную запись для службы агента SQL Server.|  
|SQL Server, агент|/AGTSVCPASSWORD<br /><br /> [Обязательно](#Accounts)|Задает пароль для учетной записи службы агента SQL Server.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASSVCACCOUNT<br /><br /> **Обязательно**|Задает учетную запись для службы [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASSVCPASSWORD<br /><br /> [Обязательно](#Accounts)|Указывает пароль для службы [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLSVCACCOUNT<br /><br /> **Обязательно**|Указывает учетную запись запуска для службы SQL Server.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLSVCPASSWORD<br /><br /> [Обязательно](#Accounts)|Указывает пароль для SQLSVCACCOUNT.|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|/ISSVCPASSWORD<br /><br /> [Обязательно](#Accounts)|Указывает пароль для служб [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSINSTALLMODE<br /><br /> **Доступен в режиме "Только файлы".**|Указывает режим установки для служб [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSSVCPASSWORD<br /><br /> [Обязательно](#Accounts)|Указывает пароль стартовой учетной записи для службы [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .|  
  
##### <a name="additional-notes"></a>Дополнительные замечания  
 Компонент [!INCLUDE[ssDE](../../includes/ssde-md.md)] и службы [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] являются единственными компонентами, поддерживающими работу в кластере. Остальные компоненты не поддерживают работу в кластере и не обеспечивают высокий уровень доступности за счет отработки отказа. 
  
###### <a name="sample-syntax"></a>Образец синтаксиса  
 Добавление узла к существующему экземпляру отказоустойчивого кластера с компонентом [!INCLUDE[ssDE](../../includes/ssde-md.md)] и службами [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. 
  
```  
setup.exe /q /ACTION=AddNode /INSTANCENAME="<Insert Instance Name>" /SQLSVCACCOUNT="<SQL account that is used on other nodes>" /SQLSVCPASSWORD="<password for SQL account>" /AGTSVCACCOUNT="<SQL Server Agent account that is used on other nodes>", /AGTSVCPASSWORD="<SQL Server Agent account password>" /ASSVCACCOUNT="<AS account that is used on other nodes>" /ASSVCPASSWORD=”<password for AS account>” /INDICATEPROGRESS /IACCEPTSQLSERVERLICENSETERMS /FAILOVERCLUSTERIPADDRESSES="IPv4;xx.xxx.xx.xx;ClusterNetwork1;xxx.xxx.xxx.x" /CONFIRMIPDEPENDENCYCHANGE=0  
```  
  
#### <a name="remove-node-parameters"></a>Параметры удаления узла  
 При разработке скриптов удаления узла из командной строки можно использовать параметры, приведенные в следующей таблице. Для удаления отказоустойчивого кластера необходимо выполнить операцию удаления узла на каждом узле отказоустойчивого кластера. Дополнительные сведения см. в разделе [Экземпляры отказоустойчивого кластера (режим AlwaysOn) (SQL Server)](../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md). 
  
|Компонент SQL Server|Параметр|Description|  
|-----------------------------------------|---------------|-----------------|  
|Управление программой установки SQL Server|/ACTION<br /><br /> **Обязательно**|Необходим для указания на поток операций удаления узла.<br /><br /> Поддерживаемое значение: **RemoveNode**|  
|Управление программой установки SQL Server|/CONFIGURATIONFILE<br /><br /> **Необязательно**|Указывает используемый файл [ConfigurationFile](../../database-engine/install-windows/install-sql-server-2016-using-a-configuration-file.md) .|  
|Управление программой установки SQL Server|/HELP, H, ?<br /><br /> **Необязательно**|Отображает варианты использования для параметров.|  
|Управление программой установки SQL Server|/INDICATEPROGRESS<br /><br /> **Необязательно**|Указывает, что подробный журнал установки должен быть выведен на консоль.|  
|Управление программой установки SQL Server|/INSTANCENAME<br /><br /> **Обязательно**|Указывает имя экземпляра SQL Server.<br /><br /> Дополнительные сведения см. в разделе [Instance Configuration](http://msdn.microsoft.com/library/5bf822fc-6dec-4806-a153-e200af28e9a5).|  
|Управление программой установки SQL Server|/Q<br /><br /> **Необязательно**|Указывает, что программа установки работает в тихом режиме (без пользовательского интерфейса). Этот параметр предназначен для автоматической установки.|  
|Управление программой установки SQL Server|/QS<br /><br /> **Необязательно**|Указывает, что программа установки запускается и отображает в пользовательском интерфейсе ход выполнения, но не принимает вводимые значения и не выводит сообщения об ошибке.|  
|Управление программой установки SQL Server|/HIDECONSOLE<br /><br /> **Необязательно**|Указывает, что окно консоли скрыто или закрыто.|  
|Управление программой установки SQL Server|/CONFIRMIPDEPENDENCYCHANGE<br /><br /> **Обязательно**|Указывает согласие присвоить зависимости ресурса IP-адреса значение от OR до AND для отказоустойчивых кластеров с несколькими подсетями. Дополнительные сведения см. на странице [Добавление и удаление узлов в отказоустойчивом кластере SQL Server (настройка)](../../sql-server/failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md). Поддерживаемые значения.<br /><br /> 0 = False (значение по умолчанию)<br /><br /> 1 = True|  
  
###### <a name="sample-syntax"></a>Образец синтаксиса  
 Удаление узла из существующего экземпляра отказоустойчивого кластера с компонентом [!INCLUDE[ssDE](../../includes/ssde-md.md)] и службами [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. 
  
```  
setup.exe /q /ACTION=RemoveNode /INSTANCENAME="<Insert Instance Name>" [/INDICATEPROGRESS] /CONFIRMIPDEPENDENCYCHANGE=0  
```  
  
##  <a name="Accounts"></a> Параметры учетных записей служб  
 Можно настроить службы SQL Server с помощью встроенной учетной записи, локальной учетной записи или учетной записи домена. 
  
> **ПРИМЕЧАНИЕ.** При использовании управляемой учетной записи службы, виртуальной учетной записи или встроенной учетной записи не следует указывать соответствующие параметры пароля. Дополнительные сведения об этих учетных записях службы см. в разделе **Новые типы учетных записей, доступные в [!INCLUDE[win7](../../includes/win7-md.md)] и [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]** статьи [Настройка учетных записей службы Windows и разрешений](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md). 
  
 Дополнительные сведения о настройке учетных записей служб см. в разделе [Configure Windows Service Accounts and Permissions](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md). 
  
|Компонент SQL Server|Параметр учетной записи|Параметр пароля|Тип запуска|  
|-----------------------------------------|-----------------------|------------------------|------------------|  
|SQL Server, агент|/AGTSVCACCOUNT|/AGTSVCPASSWORD|/AGTSVCSTARTUPTYPE|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASSVCACCOUNT|/ASSVCPASSWORD|/ASSVCSTARTUPTYPE|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLSVCACCOUNT|/SQLSVCPASSWORD|/SQLSVCSTARTUPTYPE|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|/ISSVCACCOUNT|/ISSVCPASSWORD|/ISSVCStartupType|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSSVCACCOUNT|/RSSVCPASSWORD|/RSSVCStartupType|  
  
##  <a name="Feature"></a> Параметры компонентов  
 Чтобы установить конкретные компоненты, необходимо использовать параметр /FEATURES и указать родительский компонент или один из компонентов, приведенных в следующей таблице. Сведения о функциях, поддерживаемых различными выпусками SQL Server, см. в статье [Возможности, поддерживаемые различными выпусками SQL Server 2016](../../sql-server/editions-and-supported-features-for-sql-server-2016.md). 
  
|Параметр родительского компонента|Параметр компонента|Description|  
|:---|:---|:---|  
|SQL||Устанавливает компонент [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], компонент репликации, компонент Fulltext и [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)].|  
||SQLEngine|Устанавливает только компонент [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].|  
||Репликация|Устанавливает компонент репликации вместе с компонентом [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].|  
||FullText|Устанавливает компонент FullText вместе с компонентом [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].|  
||DQ|Копирует файлы, необходимые для завершения установки [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] . После завершения установки SQL Server необходимо запустить файл DQSInstaller.exe, чтобы завершить установку [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] . Дополнительные сведения см. в статье [Запуск файла DQSInstaller.exe для завершения установки сервера служб DQS](../../data-quality-services/install-windows/run-dqsinstaller-exe-to-complete-data-quality-server-installation.md). Также устанавливает компонент [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].|  
||PolyBase|Устанавливает компоненты PolyBase.|  
||AdvancedAnalytics|Устанавливает службы R Services (в базе данных).|  
|AS||Устанавливает все компоненты служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
|Сервер отчетов||Устанавливает все компоненты служб [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .|  
|RS_SHP||Устанавливает компоненты [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] для SharePoint.|  
|RS_SHPWFE||Устанавливает надстройку [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] для продуктов SharePoint. |  
|DQC||Установка среды [!INCLUDE[ssDQSClient](../../includes/ssdqsclient-md.md)].|  
|IS||Устанавливает все компоненты служб [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .|  
|MDS||Установка среды [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)].|  
|SQL_SHARED_MR||Устанавливает Microsoft R Server.|  
|Инструменты*||Устанавливает клиентские средства и компоненты электронной документации по SQL Server.|  
||BC|Устанавливает компоненты обратной совместимости.|  
||Conn|Устанавливает компоненты связи.|
||DREPLAY_CTLR|Устанавливает контроллер распределенного воспроизведения|  
||DREPLAY_CLT|Устанавливает клиент распределенного воспроизведения|  
||SNAC_SDK|Устанавливает пакет SDK для [!INCLUDE[msCoName](../../includes/msconame-md.md)] SQL Server Native Client|  
||SDK|Устанавливает пакет средств разработки программного обеспечения.|  
||LocalDB**|Устанавливает LocalDB, режим выполнения [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] , предназначенный для разработчиков программ.|  

* Для средств управления SQL Server (SSMS) теперь доступен изолированный установщик, отдельный от установщика SQL Server. Дополнительные сведения см. в статье [Установка среды SQL Server Management Studio из командной строки](https://msdn.microsoft.com/library/bb500441.aspx#Anchor_1).

 ** LocalDB подходит только при установке номера SKU [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Express. Дополнительные сведения см. на странице [SQL Server 2016 Express LocalDB](../../database-engine/configure-windows/sql-server-2016-express-localdb.md). 
  
### <a name="feature-parameter-examples"></a>Примеры параметров компонентов  
  
|Параметр и значения|Описание|  
|--------------------------|-----------------|  
|/FEATURES=SQLEngine|Устанавливает компонент [!INCLUDE[ssDE](../../includes/ssde-md.md)] без репликации и без компонента Full-Text Search.|  
|/FEATURES=SQLEngine, FullText|Устанавливает компонент [!INCLUDE[ssDE](../../includes/ssde-md.md)] с компонентом Full-Text Search.|  
|/FEATURES=SQL, Tools|Устанавливает полный набор функций компонента [!INCLUDE[ssDE](../../includes/ssde-md.md)] и все средства.|  
|/FEATURES=BOL|Устанавливает компоненты электронной документации по SQL Server для просмотра содержимого справки и управления им.|  
|/FEATURES=SQLEngine, PolyBase|Устанавливает обработчик PolyBase.|  
  
##  <a name="RoleParameters"></a> Параметры роли  
 Роль установки или параметр /Role позволяет устанавливать стандартный набор компонентов. Роли [!INCLUDE[ssAS_md](../../includes/ssas-md.md)] устанавливают экземпляр служб [!INCLUDE[ssAS_md](../../includes/ssas-md.md)] в существующей ферме SharePoint либо в новой, ненастроенной ферме. Каждый сценарий поддерживается двумя ролями установки. Одновременно может быть выбрана только одна роль установки. При выборе роли программа установки устанавливает функции и компоненты, которые принадлежат роли. Указанные для роли компоненты могут быть изменены. Дополнительные сведения об использовании параметра роли функций см. в разделе [Установка Power Pivot из командной строки](http://msdn.microsoft.com/7f1f2b28-c9f5-49ad-934b-02f2fa6b9328). 
  
 Роль AllFeatures_WithDefaults действует по умолчанию для выпусков [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] и позволяет сократить количество диалоговых окон, показываемых пользователю. Она может быть указана из командной строки при установке выпуска SQL Server, не являющегося [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]. 
  
|Роль|Description|Установка...|  
|----------|-----------------|---------------|  
|SPI_AS_ExistingFarm|Устанавливает службы [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] в качестве именованного экземпляра [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] в существующей ферме [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] или на отдельном сервере.|Модуль вычислений[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , предварительно настроенный для хранения и обработки данных в оперативной памяти.<br /><br /> Пакеты решения[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] <br /><br /> Установщик для [!INCLUDE[ssGeminiClient](../../includes/ssgeminiclient-md.md)]<br /><br /> электронная документация по SQL Server|  
|SPI_AS_NewFarm|Устанавливает службы [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] и компонент [!INCLUDE[ssDE](../../includes/ssde-md.md)] как именованный экземпляр [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] в новой ненастроенной ферме Office [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] или на отдельном сервере. Программа установки SQL Server настроит ферму при установке роли.|Модуль вычислений[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , предварительно настроенный для хранения и обработки данных в оперативной памяти.<br /><br /> Пакеты решения[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] <br /><br /> электронная документация по SQL Server<br /><br /> [!INCLUDE[ssDE](../../includes/ssde-md.md)]<br /><br /> Средства настройки<br /><br /> [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]|  
|AllFeatures_WithDefaults|Устанавливает все компоненты, доступные в текущем выпуске.<br /><br /> Добавляет текущего пользователя в предопределенную роль сервера **sysadmin** SQL Server.<br /><br /> Если в [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)] и следующих версиях операционная система не является контроллером домена, то по умолчанию в компоненте [!INCLUDE[ssDE](../../includes/ssde-md.md)]и службах [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] используется учетная запись NTAUTHORITY\NETWORK SERVICE, а в службах [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] — учетная запись NTAUTHORITY\NETWORK SERVICE.<br /><br /> В выпусках [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]эта роль по умолчанию включена. Для всех остальных выпусков данная роль не включена, но может быть определена через пользовательский интерфейс или с помощью параметров командной строки.|Для выпусков [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]устанавливает только те функции, которые доступны в выпуске. Для прочих выпусков устанавливает все компоненты SQL Server.<br /><br /> Параметр **AllFeatures_WithDefaults** может сочетаться с другими параметрами, которые переопределяют настройки параметра **AllFeatures_WithDefaults** . Например, сочетание параметра **AllFeatures_WithDefaults** с параметром **/Features=RS** переопределит команду для установки всех компонентов и установит лишь службы [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], но будет соблюдать параметр **AllFeatures_WithDefaults** , определяющий использование учетной записи службы по умолчанию для служб [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].<br /><br /> При использовании параметра **AllFeatures_WithDefaults** с параметром **/ADDCURRENTUSERASSQLADMIN=FALSE** диалоговое окно провизионирования настройки не заполняется автоматически в соответствии с текущим пользователем. Добавьте параметры **/AGTSVCACCOUNT** и **/AGTSVCPASSWORD** , чтобы определить учетную запись службы и пароль для агента SQL Server.|  
  
##  <a name="RollOwnership"></a> Управление способом отработки отказа с помощью параметра /FAILOVERCLUSTERROLLOWNERSHIP  
 Чтобы обновить отказоустойчивый кластер SQL Server до версии [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], необходимо поочередно запустить программу установки на каждом узле отказоустойчивого кластера, начиная с пассивных узлов. Программа установки определяет момент перехода на другой ресурс в зависимости от общего числа узлов в экземпляре отказоустойчивого кластера и от количества уже обновленных узлов. Если была обновлена половина узлов или более, программа установки по умолчанию вызовет отработку отказа на обновленный узел. 
  
 Чтобы управлять отработкой отказа узлов кластера во время обновления, запустите операцию обновления из командной строки и воспользуйтесь параметром /FAILOVERCLUSTERROLLOWNERSHIP для управления способом отработки отказа до того, как операция обновления переключит узел в режим «вне сети». Используйте этот параметр следующим образом:  
  
-   Значение /FAILOVERCLUSTERROLLOWNERSHIP=0 не передает владение кластером обновленным узлам (не перемещает группу), а по окончании обновления не добавляет этот узел в список возможных владельцев кластера SQL Server. 
  
-   Значение /FAILOVERCLUSTERROLLOWNERSHIP=1 передает владение кластером обновленным узлам (перемещает группу), а по окончании обновления добавляет этот узел в список возможных владельцев кластера SQL Server. 
  
-   /FAILOVERCLUSTERROLLOWNERSHIP=2 — значение по умолчанию. Оно используется, если этот параметр не задан. Этот параметр указывает, что программа установки SQL Server будет управлять владением кластера (перемещением группы) по мере необходимости. 
  
##  <a name="InstanceID"></a> Настройка идентификатора экземпляра или InstanceID  
 Параметр Instance ID или /InstanceID используется для указания пути установки компонентов экземпляра и пути к экземпляру в реестре. Значение INSTANCEID — строка, которая должна быть уникальной. 
  
-   Идентификатор экземпляра SQL: MSSQL13.\<INSTANCEID>  
  
-   Идентификатор экземпляра AS: MSAS13.\<INSTANCEID>  
  
-   Идентификатор экземпляра служб RS: MSRS13.\<INSTANCEID>  
  
 Компоненты, привязанные к экземпляру, устанавливаются в следующие папки:  
  
 %Program Files%\\Microsoft SQL Server\\<SQLInstanceID\>  
  
 %Program Files%\\Microsoft SQL Server\\<ASInstanceID\>  
  
 %Program Files Microsoft SQL Server\\<RSInstanceID\>  
  
> **ПРИМЕЧАНИЕ.** Если в командной строке не указано INSTANCEID, программа установки по умолчанию заменяет \<INSTANCEID> на \<INSTANCENAME>. 
  
## <a name="see-also"></a>См. также:  
 [Установка SQL Server 2016 с помощью мастера установки](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)   
 [Установка отказоустойчивого кластера SQL Server](../../sql-server/failover-clusters/install/sql-server-failover-cluster-installation.md)   
 [[Установка компонентов бизнес-аналитики SQL Server 2016](../../sql-server/install/install-sql-server-business-intelligence-features.md)]  
  
