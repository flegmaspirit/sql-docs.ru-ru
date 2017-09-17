---
title: "Сохранение записей в формате XML | Документы Microsoft"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- persisting data [ADO]
- data updates [ADO], persisting data
- data persistence [ADO]
- XML persistence [ADO]
- updating data [ADO], persisting data
ms.assetid: f3113ec4-ae31-428f-89c6-bc1024f128ea
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a45c434bdcf551e97eb97f85997ab73c883b599c
ms.contentlocale: ru-ru
ms.lasthandoff: 09/09/2017

---
# <a name="persisting-records-in-xml-format"></a>Сохранение записей в формате XML
Формату ADTG **записей** сохраняемости в формате XML реализуется с помощью поставщика сохраняемости Microsoft OLE DB. Этот поставщик создает однопроходный, только для чтения строк из сохраненных XML-файл или поток, содержащий данные схемы ADO. Аналогичным образом, может потребоваться ADO **записей**, создают XML-документ и сохранить его в файл или любой объект, реализующий COM **IStream** интерфейса. (На самом деле он просто еще один пример объекта, который поддерживает **IStream**.) 2.5 и более поздних версиях ADO использует для синтаксического анализа Microsoft XML (MSXML) для загрузки XML в **записей**; поэтому msxml.dll не требуется.  
  
> [!NOTE]
>  Существуют некоторые ограничения при сохранении иерархические **наборы записей** (данные фигуры) в формат XML. Не удается сохранить в XML, если иерархическое **записей** содержит отложенные обновления, и не удается сохранить параметризованную иерархические **набора записей**. Дополнительные сведения см. в разделе [сохранение отфильтрована и иерархические наборы записей](../../../ado/guide/data/persisting-filtered-and-hierarchical-recordsets.md).  
  
 Самый простой способ хранения данных в формат XML и загрузить его обратно снова через ADO — с **Сохранить** и **откройте** методы, соответственно. В следующем примере кода ADO показано, как сохранить данные в **заголовки** таблицы в файл с именем titles.sav.  
  
```  
Dim rs as new Recordset  
Dim rs2 as new Recordset  
Dim c as new Connection  
Dim s as new Stream  
  
' Query the Titles table.  
c.Open "provider=sqloledb;data source=MySQLServer;initial catalog=pubs;Integrated Security='SSPI'"  
rs.cursorlocation = adUseClient  
rs.Open "select * from titles", c, adOpenStatic  
  
' Save to the file in the XML format. Note that if you don't specify   
' adPersistXML, a binary format (ADTG) will be used by default.  
rs.Save "titles.sav", adPersistXML  
  
' Save the recordset into the ADO Stream object.  
rs.save s, adPersistXML  
rs.Close  
c.Close  
  
set rs = nothing  
  
' Reopen the file.  
rs.Open "titles.sav",,,,adCmdFile  
' Open the Stream back into a Recordset.  
rs2.open s  
```  
  
 ADO всегда сохраняется вся **записей** объекта. Если вы хотите сохранить подмножество строк из **записей** , используйте **фильтра** метод, чтобы сузить строки или изменить предложение вашего выбора. Тем не менее, необходимо открыть **записей** объект с клиентский курсор (**CursorLocation** = **adUseClient**) для использования **фильтрации** метод для сохранения подмножества строк. Например, чтобы получить заголовки, которые начинаются с буквы «b», можно применить фильтр для открытого **записей** объекта:  
  
```  
rs.Filter "title_id like 'B*'"  
rs.Save "btitles.sav", adPersistXML  
```  
  
 ADO всегда использует обработчик курсоров клиентов набора строк для получения прокрутки, bookmarkable **записей** объекта на основе данных последовательного доступа, созданные поставщиком сохраняемости.  
  
 Этот раздел содержит следующие подразделы.  
  
-   [Формат хранения XML](../../../ado/guide/data/xml-persistence-format.md)  
  
-   [Пространства имен](../../../ado/guide/data/namespaces.md)  
  
-   [Раздел схемы](../../../ado/guide/data/schema-section.md)  
  
-   [Раздел данных](../../../ado/guide/data/data-section.md)  
  
-   [Иерархические наборы записей в формате XML](../../../ado/guide/data/hierarchical-recordsets-in-xml.md)  
  
-   [Динамический набор записей свойств в XML](../../../ado/guide/data/recordset-dynamic-properties-in-xml.md)  
  
-   [Преобразования XSLT](../../../ado/guide/data/xslt-transformations.md)  
  
-   [Сохранение объекта XML DOM](../../../ado/guide/data/saving-to-the-xml-dom-object.md)  
  
-   [Вопросы безопасности XML](../../../ado/guide/data/xml-security-considerations.md)  
  
-   [Сценарий сохраняемости XML набора записей](../../../ado/guide/data/xml-recordset-persistence-scenario.md)