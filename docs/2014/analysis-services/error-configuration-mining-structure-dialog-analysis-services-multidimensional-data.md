---
title: Конфигурация ошибок (диалоговое окно «Структура интеллектуального анализа данных») (службы Analysis Services — многомерные данные) | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.miningstructuredialog.general.f1
ms.assetid: d9aa028b-bad9-49c7-a81c-c2150e4dd481
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c1cf11c572860815f46e6d20a0cf1a4b82399a93
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/02/2018
ms.locfileid: "48210914"
---
# <a name="error-configuration-mining-structure-dialog-box-analysis-services---multidimensional-data"></a>Конфигурация ошибок (диалоговое окно «Структура интеллектуального анализа данных») (службы Analysis Services — многомерные данные)
  Страница **Конфигурация ошибок** диалогового окна **Свойства структуры интеллектуального анализа данных** среды **SQL Server Management Studio** используется для задания свойств конфигурации ошибок структуры интеллектуального анализа данных в базе данных служб [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .  
  
## <a name="options"></a>Параметры  
 **Использовать конфигурацию ошибок по умолчанию**  
 Выберите этот параметр, чтобы использовать конфигурацию ошибок по умолчанию для объектов в операциях обработки.  
  
 **Действие при возникновении ошибки ключа**  
 Выберите одно из следующих действий, происходящее при обнаружении нового ключа, который невозможно найти, во время обработки.  
  
-   **Преобразовать в неизвестный тип** — проводит статистическую обработку данных для записи в неизвестный тип.  
  
-   **Отменить запись** — исключает данные для записи из процесса обработки вместе с объектом.  
  
 **Не учитывать счетчик ошибок**  
 Нажмите для игнорирования всех ошибок во время обработки.  
  
 **Остановить при возникновении ошибки**  
 Нажмите для остановки обработки при возникновении ошибок. Этот режим включает режимы **Количество ошибок** и **Действие при возникновении ошибки** .  
  
 **Количество ошибок**  
 Введите количество ошибок, которые будут проигнорированы до остановки процесса.  
  
 **Действие при возникновении ошибки**  
 Выберите одно из следующих действий для выполнения, когда количество ошибок превышает значение, указанное в параметре **Количество ошибок**.  
  
-   **Остановить обработку** — завершает операцию обработки.  
  
-   **Остановить ведение журнала** — останавливает запись журнала ошибок, но не прекращает обработку.  
  
 **Ключ не найден**  
 Укажите одно из следующих действий, которое должно быть предпринято, если во время обработки объекта ключ не найден.  
  
-   **Пропускать ошибки** — ошибки пропускаются  
  
-   **Создать отчет и продолжить** — сообщить об ошибке и продолжить обработку  
  
-   **Создать отчет и остановить выполнение** — вывести сообщение об ошибке и остановить операцию обработки.  
  
 **Повторяющийся ключ**  
 Укажите одно из следующих действий, которое должно предприниматься, если во время обработки объекта обнаружен повторяющийся ключ.  
  
-   **Пропускать ошибки** — ошибки пропускаются  
  
-   **Создать отчет и продолжить** — сообщить об ошибке и продолжить обработку  
  
-   **Создать отчет и остановить выполнение** — вывести сообщение об ошибке и остановить операцию обработки.  
  
 **Ключ NULL преобразован в неизвестный**  
 Укажите одно из следующих действий, которое должно предприниматься, если во время обработки объекта ключ NULL элемента добавляется к неизвестному элементу.  
  
-   **Пропускать ошибки** — ошибки пропускаются  
  
-   **Создать отчет и продолжить** — сообщить об ошибке и продолжить обработку  
  
-   **Создать отчет и остановить выполнение** — вывести сообщение об ошибке и остановить операцию обработки.  
  
 **Ключ NULL не допускается**  
 Укажите одно из следующих действий, которое должно быть предпринято, если во время обработки объекта найден недопустимый ключ NULL.  
  
-   **Пропускать ошибки** — ошибки пропускаются  
  
-   **Создать отчет и продолжить** — сообщить об ошибке и продолжить обработку  
  
-   **Создать отчет и остановить выполнение** — вывести сообщение об ошибке и остановить операцию обработки.  
  
 **Путь к журналу ошибок**  
 Введите полный путь и имя файла журнала ошибок.  
  
## <a name="see-also"></a>См. также  
 [Диалоговое окно свойств структуры интеллектуального &#40;службы Analysis Services — Интеллектуальный анализ данных&#41;](mining-structure-properties-dialog-analysis-services-data-mining.md)   
 [Общие &#40;интеллектуального анализа данных диалоговое окно «Структура»&#41; &#40;службы Analysis Services — Интеллектуальный анализ данных&#41;](general-mining-structure-dialog-box-analysis-services-data-mining.md)  
  
  
