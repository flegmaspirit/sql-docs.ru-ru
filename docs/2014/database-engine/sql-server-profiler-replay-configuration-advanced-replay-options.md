---
title: SQL Server Profiler — конфигурация воспроизведения (Дополнительные параметры воспроизведения) | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.pro.replay.generaloptions.advanced.f1
helpviewer_keywords:
- Replay Configuration dialog box
ms.assetid: b4eb34f7-3af6-4a44-ba7e-2b8430ec3cd7
caps.latest.revision: 22
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7d010365e010fc7748e6cb04d6d71479f0f2f9d4
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/02/2018
ms.locfileid: "37280320"
---
# <a name="sql-server-profiler---replay-configuration-advanced-replay-options"></a>Приложение SQL Server Profiler — Конфигурация воспроизведения (дополнительные параметры воспроизведения)
  В диалоговом окне **Конфигурация воспроизведения** используйте вкладку **Дополнительные параметры воспроизведения** для задания способа воспроизведения файла трассировки.  
  
 Для просмотра этого окна используйте приложение [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] для открытия файла трассировки или таблицы, содержащей события, предназначенные для воспроизведения. Дополнительные сведения см. в разделе [Replay Requirements](../tools/sql-server-profiler/replay-requirements.md). После открытия файла трассировки или таблицы в меню **Воспроизвести** выберите команду **Запустить**, соединитесь с экземпляром SQL Server, содержащим необходимую трассировку, и перейдите на вкладку **Дополнительные параметры воспроизведения** .  
  
## <a name="options"></a>Параметры  
 **Воспроизвести системные SPID**  
 Указывает, воспроизводит ли приложение [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] идентификаторы системных процессов (SPID).  
  
 **Воспроизвести только один SPID**  
 Воспроизводится только деятельность в файле трассировки источника, относящемся к выбранному SPID.  
  
 **SPID для воспроизведения**  
 Задает SPID для воспроизведения.  
  
 **Ограничить воспроизведение по дате и времени**  
 Установите для воспроизведения только части файла трассировки источника.  
  
 **Время начала**  
 Дата и время из файла трассировки источника, когда должно начаться воспроизведение.  
  
 **Время завершения**  
 Дата и время из файла трассировки источника, когда должно завершиться воспроизведение.  
  
 **Интервал ожидания монитора исправности (сек)**  
 Задает интервал ожидания воспроизведения в секундах. По умолчанию — 3 600 секунд (1 час). Эта установка влияет на количество времени, предоставляемое для выполнения процесса, по истечении которого монитор исправности прерывает процесс.  
  
 **Интервал опроса монитора исправности (сек)**  
 Задайте интервал опроса монитора исправности во время воспроизведения в секундах. По умолчанию — 60 секунд. Это значение дает возможность пользователю определить, как часто монитор исправности выполняет опрос кандидатов на завершение.  
  
 **Включить монитор заблокированных процессов SQL Server**  
 Включает процесс, который ищет блокированные или блокирующие процессы.  
  
 **Интервал ожидания монитора заблокированных процессов (сек)**  
 Устанавливает, как часто монитор заблокированных процессов ищет заблокированные или блокирующие процессы.  
  
## <a name="see-also"></a>См. также  
 [Воспроизведение таблицы трассировки &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/replay-a-trace-table-sql-server-profiler.md)   
 [Воспроизведение файла трассировки (приложение SQL Server Profiler)](../tools/sql-server-profiler/replay-a-trace-file-sql-server-profiler.md)   
 [Воспроизведение трассировок](../tools/sql-server-profiler/replay-traces.md)  
  
  