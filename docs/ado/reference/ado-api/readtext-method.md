---
title: "Метод ReadText | Документы Microsoft"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- _Stream::raw_ReadText
- _Stream::ReadText
helpviewer_keywords:
- ReadText method [ADO]
ms.assetid: be5a409e-cf87-4859-9ea5-713401755a77
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b134e064cc3d1dfa06c5d948d74e49f643756bd1
ms.contentlocale: ru-ru
ms.lasthandoff: 09/09/2017

---
# <a name="readtext-method"></a>Метод ReadText
Считывает указанное число символов из текстового [поток](../../../ado/reference/ado-api/stream-object-ado.md) объекта.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
String = Stream.ReadText ( NumChars)  
```  
  
#### <a name="parameters"></a>Параметры  
 *NumChars*  
 Необязательно. Объект **длинные** значение, указывающее число символов для чтения из файла или [StreamReadEnum](../../../ado/reference/ado-api/streamreadenum.md) значение. Значение по умолчанию — **adReadAll**.  
  
## <a name="return-value"></a>Возвращаемое значение  
 **ReadText** метод считывает указанное число символов, всю строку или весь поток из **поток** объекта и возвращает результирующую строку.  
  
## <a name="remarks"></a>Замечания  
 Если *NumChar* остается больше числа символов в потоке, возвращаются только символов, оставшихся. Чтение строки заполнено в соответствии с длиной, определяемой *NumChar*. Если нет доступных для чтения символов, возвращается значение типа variant, значение которого равно null. **ReadText** не может использоваться для чтения в обратном направлении.  
  
> [!NOTE]
>  **ReadText** метод используется с текстовыми потоками ([тип](../../../ado/reference/ado-api/type-property-ado-stream.md) — **adTypeText**). Для двоичных потоков (**тип** — **adTypeBinary**), используйте [чтения](../../../ado/reference/ado-api/read-method.md).  
  
 Запросы, которые приводят к большой объем XML-данные возвращенные с помощью **ReadText** Если это делается в компонент COM +, из которой вызывается метод объекта потока объектов данных ActiveX (ADO) может занять немало времени для выполнения; ASP-страницы, сеанс пользователя может истечь время ожидания. ADO преобразует поток объекта данные из кодировки UTF-8 в Юникоде. перераспределение часто памяти, участвующие в преобразовании такой большой объем данных за один раз — довольно много времени. Чтобы решить, выполнять повторяющиеся вызовы к **ReadText** метод ADO объект команды и укажите меньшее число символов. Тесты показали, значение которого эквивалентно значению 128 КБ (131,072) является оптимальной. Время отклика уменьшается, как уменьшить это значение. Дополнительные сведения см. в статье базы знаний 280067, «PRB: получения очень больших XML-документов из SQL Server 2000 с помощью метода ReadText объекта ADO потока может быть медленным», в базе знаний Майкрософт на http://support.microsoft.com.  
  
## <a name="applies-to"></a>Объект применения  
 [Объект потока (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>См. также:  
 [Read, метод](../../../ado/reference/ado-api/read-method.md)