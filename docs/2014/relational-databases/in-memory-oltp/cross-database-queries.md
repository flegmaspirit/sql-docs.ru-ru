---
title: Межбазовые запросы | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: a0305f5b-91bd-4d18-a2fc-ec235b062fd3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0ccf8ea4fc15be567d0e95a66b2e5320fae7dbbc
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/02/2018
ms.locfileid: "48205164"
---
# <a name="cross-database-queries"></a>Межбазовые запросы
  В [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]транзакции между базами данных не поддерживаются с таблицами, оптимизированными для памяти. Нельзя получить доступ к другой базе данных из той же транзакции или того же запроса, которые также получают доступ к оптимизированной для памяти таблицы. Нельзя скопировать данные из одной таблицы в базе данных в оптимизированную для памяти таблицу в другой базе данных.  
  
 Табличные переменные не является транзакционными. Поэтому табличные переменные, оптимизированные для памяти, можно использовать в запросах между базами данных. Такие переменные упрощают перемещение данных из таблицы в одной базе данных в оптимизированные для памяти таблицы в другой базе данных. Можно использовать две транзакции. В первой транзакции вставьте данные из удаленной таблицы в переменную. Во второй транзакции вставьте данные в локальную оптимизированную для памяти таблицу из переменной.  
  
 Например, чтобы скопировать строку из таблицы t1 в базе данных db1 в таблицу t2 в db2, с помощью переменной @v1 типа dbo.tt1, можно использовать примерно следующим образом:  
  
```tsql  
USE db2   
GO   
DECLARE @v1 dbo.tt1   
INSERT @v1 SELECT * FROM db1.dbo.t1   
INSERT dbo.t2 SELECT * FROM @v1   
GO  
```  
  
## <a name="see-also"></a>См. также  
 [Миграция в In-Memory OLTP](migrating-to-in-memory-oltp.md)  
  
  
