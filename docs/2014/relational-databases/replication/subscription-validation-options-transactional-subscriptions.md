---
title: Параметры проверки подписки (транзакционные подписки) | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.rep.validate.options.f1
helpviewer_keywords:
- Subscription Validation Options dialog box
ms.assetid: fd66ad1f-df01-4240-9e89-8f41bff12c1e
caps.latest.revision: 17
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 37fdbafa1f6dbdbc593277e4e5d4df37ad054d82
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/02/2018
ms.locfileid: "37230664"
---
# <a name="subscription-validation-options-transactional-subscriptions"></a>Параметры проверки подписки (подписки на публикацию транзакций)
  Используйте диалоговое окно **Параметры проверки подписки** для определения, должна ли проверка правильности использовать только количество строк или количество строк и двоичную контрольную сумму.  
  
## <a name="options"></a>Параметры  
 **Проверить, совпадают ли числа реплицированных строк данных у подписчика и у издателя**  
 Выберите для выполнения тип проверки количества строк. Для публикаций Oracle единственный доступный параметр — это параметр **Выполнить подсчет действительного числа строк путем непосредственных запросов к таблицам**.  
  
 **Сравнить контрольные суммы для проверки правильности данных в строке**  
 Кроме подсчета количества строк на подписчике и на издателе, вычисляется контрольная сумма всех данных с помощью двоичного алгоритма подсчета контрольной суммы. Если количество строк не совпадает, то контрольная сумма не проверяется.  
  
 **Остановить агент распространителя после завершения проверки**  
 По умолчанию агент распространителя работает постоянно. Выберите этот параметр для остановки агента после выполнения проверки. Это позволяет удостовериться в успешном завершении проверки перед продолжением копирования данных к подписчику.  
  
## <a name="see-also"></a>См. также  
 [Проверка данных на подписчике](validate-data-at-the-subscriber.md)   
 [Проверка реплицированных данных](validate-replicated-data.md)  
  
  