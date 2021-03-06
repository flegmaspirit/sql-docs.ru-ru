---
title: Получение нескольких наборов записей | Документация Майкрософт
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- receiving multiple Recordsets [ADO]
- Recordset object [ADO], receiving multiple Recordsets
ms.assetid: 2a7ad7a6-f00d-4355-b0b5-d0ab957b0566
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e70dc047456549b625a1e66250d413009293f4a0
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/01/2018
ms.locfileid: "47684239"
---
# <a name="receiving-multiple-recordsets"></a>Получение нескольких наборов записей
[Поставщик Microsoft OLE DB для SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md) поддерживает возврат нескольких **записей** объекты для одной команды, содержащего несколько инструкций SQL, один **записей**одной инструкции SQL. Порядок, в котором **записей**возвращаются будет учитываться порядок, в котором указаны инструкции SQL в тексте команды.  
  
 Поставщик Microsoft OLE DB для SQL Server также возвращает несколько результирующих наборов в ADO, если команда содержит предложение COMPUTE. Например, команду, содержащую следующую инструкцию SQL будет возвращать результаты в двух **записей** объектов: один для набора строк (*ProductID*, *ProductName*, *UnitPrice*), а другой — для среднюю цену всех продуктов в таблице.  
  
```  
SELECT ProductID, ProductName, UnitPrice   
  FROM PRODUCTS   
  COMPUTE AVG(UnitPrice)  
```  
  
 Можно использовать **Recordset.NextRecordset** метода для перечисления двух объектов.  
  
 Дополнительные сведения см. в разделе [NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md).
