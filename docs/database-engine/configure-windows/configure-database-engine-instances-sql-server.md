---
title: Настройка экземпляров компонента Database Engine (SQL Server) | Документы Майкрософт
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: 84e36fcb-2c78-48e8-8e4b-bf784a3ee557
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 8a233814c86779b3c8fca67e6fb79c9f183a91d7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/01/2018
ms.locfileid: "47670882"
---
# <a name="configure-database-engine-instances-sql-server"></a>Настройка экземпляров компонента Database Engine (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Каждый экземпляр компонента [!INCLUDE[ssDE](../../includes/ssde-md.md)] должен быть настроен в соответствии с требованиями производительности и доступности, определенными для базы данных, которая размещена экземпляром. В компоненте [!INCLUDE[ssDE](../../includes/ssde-md.md)] предусмотрены параметры конфигурации, которые управляют такими режимами работы, как использование ресурсов и доступность функций, например срабатывание аудита или триггера.  
  
## <a name="instance-configuration"></a>Конфигурация экземпляра  
 Когда база данных развернута в эксплуатацию, обычно имеется соглашение уровня службы (SLA), определяющее области, например уровни производительности, необходимые для базы данных, и необходимый уровень доступности базы данных. Как правило, условия соглашения по уровню обслуживания (SLA) устанавливают требования к конфигурации экземпляра.  
  
 Экземпляр настраивается обычно сразу же после установки. Начальная конфигурация обычно определяется требованиями соглашения по уровню обслуживания (SLA) типов баз данных, которые запланированы для развертывания к экземпляру. После развертывания базы данных администратор наблюдает за производительностью экземпляра и регулирует настройки конфигурации, если показатели производительности, которые демонстрирует экземпляр, не отвечают требованиям SLA.  
  
## <a name="configuration-tasks"></a>Задачи конфигурации  
  
|Описание задачи|Раздел|  
|----------------------|-----------|  
|Описываются различные параметры конфигурации экземпляра, а также способы просмотра или изменения этих параметров.|[Параметры конфигурации сервера (SQL Server)](../../database-engine/configure-windows/server-configuration-options-sql-server.md)|  
|Описывается просмотр и конфигурация местоположений по умолчанию для новых данных и файлов журнала в экземпляре.|[Просмотр или изменение расположения по умолчанию для файлов данных и журнала (среда SQL Server Management Studio)](../../database-engine/configure-windows/view-or-change-the-default-locations-for-data-and-log-files.md)|  
|Описывается настройка SQL Server для использования программного NUMA.|[Архитектура Soft-NUMA (SQL Server)](../../database-engine/configure-windows/soft-numa-sql-server.md)|  
|Описывается сопоставление порта TCP/IP с узлом архитектуры NUMA.|[Сопоставление портов TCP/IP с узлами NUMA (SQL Server)](../../database-engine/configure-windows/map-tcp-ip-ports-to-numa-nodes-sql-server.md)|  
|Описывается включение функции «Блокировка страниц в памяти Windows». Эта политика определяет, какие учетные записи вправе использовать процесс для хранения данных в физической памяти, что предотвращает страничную запись данных операционной системой в область виртуальной памяти на диск.|[Включение параметра "Блокировка страниц в памяти" (Windows)](../../database-engine/configure-windows/enable-the-lock-pages-in-memory-option-windows.md)|  
  
## <a name="see-also"></a>См. также:  
 [Экземпляры компонента Database Engine (SQL Server)](../../database-engine/configure-windows/database-engine-instances-sql-server.md)  
  
  
