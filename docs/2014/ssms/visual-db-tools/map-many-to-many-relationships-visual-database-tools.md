---
title: Построение связи "многие ко многим" (визуальные инструменты для баз данных) | Документация Майкрософт
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- relationships [SQL Server], many-to-many
- junction tables [SQL Server]
- many-to-many relationships [SQL Server]
- mapping many-to-many relationships [SQL Server]
- database diagrams [SQL Server], relationships
ms.assetid: 2977cf92-98b5-48b2-b0fd-8fbc7040f2b4
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: eec838c9d7ada526bfa72265a28fb5b28e8299d8
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/02/2018
ms.locfileid: "48170916"
---
# <a name="map-many-to-many-relationships-visual-database-tools"></a>Построение связи «многие ко многим» (визуальные инструменты для баз данных)
  Отношения «многие ко многим» позволяют связать каждую строку одной таблицы с несколькими строками другой таблицы и наоборот. Например, отношение «многие ко многим» можно создать для таблиц `authors` и `titles` , чтобы связать каждого автора с его книгами и сопоставить каждой книге ее автора. Если создать связь «один ко многим» в любой таблице, получится, что каждая книга сможет иметь только одного автора или каждый автор — только одну книгу.  
  
 Для осуществления связей «многие ко многим» между таблицами базы данных применяются связующие таблицы. Они содержат первичные ключевые столбцы двух таблиц, которые необходимо связать. После этого можно создать связи между первичными ключевыми столбцами каждой таблицы и соответствующими столбцами в связующей таблице. В базе данных pubs связующей является таблица `titleauthor` .  
  
### <a name="to-create-a-many-to-many-relationship-between-tables"></a>Для создания связи «многие ко многим» между таблицами  
  
1.  Добавьте таблицы, которые должны обладать связью «многие ко многим» в диаграмму базы данных.  
  
2.  Создайте третью таблицу, щелкнув диаграмму правой кнопкой мыши и выбрав **Создать таблицу** . Эта таблица станет связующей.  
  
3.  В диалоговом окне **Выбор имени** измените имя, назначенное системой. Например, связующую таблицу для таблиц `titles` и `authors` можно назвать `titleauthors`.  
  
4.  Скопируйте первичные ключевые столбцы обеих таблиц в связующую таблицу. В эту таблицу можно добавить другие столбцы, как в любую другую таблицу.  
  
5.  Создайте первичный ключ в связующей таблице так, чтобы он содержал все первичные ключевые столбцы исходных таблиц. Дополнительные сведения см. в разделе [создание первичных ключей](../../relational-databases/tables/create-primary-keys.md).  
  
6.  Определите отношение «один ко многим» между каждой из первоначальных таблиц и связующей таблицей. Связующая таблица должна находиться на стороне «многих» обоих отношений. Дополнительные сведения см. в разделе [Create Foreign Key Relationships](../../relational-databases/tables/create-foreign-key-relationships.md).  
  
    > [!NOTE]  
    >  Создание связующей таблицы в диаграмме базы данных не подразумевает ее заполнение данными из связанных таблиц. Дополнительные сведения о вставке данных в эту таблицу см. в разделе [Создание запросов вставки результатов (визуальные инструменты для баз данных)](visual-database-tools.md).  
  
## <a name="see-also"></a>См. также  
 [Работа с диаграммами баз данных (визуальные инструменты для баз данных)](work-with-database-diagrams-visual-database-tools.md)  
  
  
