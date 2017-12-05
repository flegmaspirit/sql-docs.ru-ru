---
title: "srv_paramdata (интерфейс API расширенных хранимых процедур) | Документы Майкрософт"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: extended-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: reference
apiname: srv_paramdata
apilocation: opends60.dll
apitype: DLLExport
dev_langs: C++
helpviewer_keywords: srv_paramdata
ms.assetid: 3104514d-b404-47c9-b6d7-928106384874
caps.latest.revision: "30"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d68a33d8d09114d6142ef10d45e1f92e349d92ea
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/17/2017
---
# <a name="srvparamdata-extended-stored-procedure-api"></a>srv_paramdata (API-интерфейс расширенных хранимых процедур)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Используйте вместо этого интеграцию со средой CLR.  
  
 Возвращает значение параметра вызова удаленной хранимой процедуры. Эта функция заменена функцией **srv_paraminfo**.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
void * srv_paramdata (  
SRV_PROC *  
srvproc  
,  
int  
n   
);  
```  
  
## <a name="arguments"></a>Аргументы  
 *srvproc*  
 Указатель на структуру SRV_PROC, представляющую собой дескриптор соединения с клиентом (в данном случае — дескриптор, который получил вызов удаленной хранимой процедуры). Эта структура содержит сведения, которые используются библиотекой расширенных хранимых процедур для управления связью и передачи данных между приложением и клиентом.  
  
 *n*  
 Номер параметра. Первый параметр имеет номер 1.  
  
## <a name="returns"></a>Возвращает  
 Указатель на значение параметра. Если значение *n*-го параметра равно NULL, не существует никакого *n*-го параметра или удаленной хранимой процедуры, то возвращается значение NULL. Если значением параметра является строка, она не может завершаться нулевым байтом. Используйте функцию **srv_paramlen**, чтобы определить длину строки.  
  
 Если параметр принадлежит к одному из типов данных [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], то эта функция возвращает указанные ниже значения. В данных указателя показано, является ли этот указатель допустимым для типа данных (VP), NULL или не применимым (N/A), а также содержимое тех данных, на которые он указывает.  
  
|Новые типы данных|Длина входных данных|  
|--------------------|-----------------------|  
|BITN|**NULL:** VP, NULL<br /><br /> **ZERO:** VP, NULL<br /><br /> **>=255:** недоступно<br /><br /> **<255:** недоступно|  
|BIGVARCHAR|**NULL:** NULL, недоступно<br /><br /> **ZERO:** VP, NULL<br /><br /> **>=255:** VP, 255 символов<br /><br /> **<255:** VP, фактические данные|  
|BIGCHAR|**NULL:** NULL, недоступно<br /><br /> **ZERO:** VP, 255 пробелов<br /><br /> **>=255:** VP, 255 символов<br /><br /> **<255:** VP, фактические данные + заполнение (до 255)|  
|BIGBINARY|**NULL:** NULL, недоступно<br /><br /> **ZERO:** VP, 255 0x00<br /><br /> **>=255:** VP, 255 байт<br /><br /> **<255:** VP, фактические данные + заполнение (до 255)|  
|BIGVARBINARY|**NULL:** NULL, недоступно<br /><br /> **ZERO:** VP, 0x00<br /><br /> **>=255:** VP, 255 байт<br /><br /> **<255:** VP, фактические данные|  
|NCHAR|**NULL:** NULL, недоступно<br /><br /> **ZERO:** VP, 255 пробелов<br /><br /> **>=255:** VP, 255 символов<br /><br /> **<255:** VP, фактические данные + заполнение (до 255)|  
|NVARCHAR|**NULL:** NULL, недоступно<br /><br /> **ZERO:** VP, NULL<br /><br /> **>=255:** VP, 255 символов<br /><br /> **<255:** VP, фактические данные|  
|NTEXT|**NULL:** недоступно<br /><br /> **ZERO:** недоступно<br /><br /> **>=255:** недоступно<br /><br /> **\<255:** недоступно|  
  
 \* Данные не завершаются нулевым байтом; при отсечении данных >255 символов предупреждение не выдается.  
  
## <a name="remarks"></a>Замечания  
 Если известно имя параметра, то с помощью функции **srv_paramnumber** можно возвратить его номер. Используйте функцию **srv_paramlen**, чтобы определить, имеет ли параметр значение NULL.  
  
 Когда удаленная хранимая процедура вызывается с параметрами, то эти параметры могут быть переданы либо по имени, либо по позиции (без указания имени). Если при вызове удаленной хранимой процедуры часть параметров передается по имени, а часть — по позиции, возникает ошибка. Обработчик SRV_RPC вызывается и при возникновении ошибки, однако он действует так, как будто параметры не были переданы, и функция **srv_rpcparams** возвращает значение 0.  
  
> [!IMPORTANT]  
>  Необходимо тщательно просмотреть исходный код расширенных хранимых процедур и проверить скомпилированные библиотеки DLL перед их установкой на рабочий сервер. Сведения о проверке безопасности см. на следующем [веб-сайте Майкрософт](http://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409http://msdn.microsoft.com/security/).  
  
## <a name="see-also"></a>См. также:  
 [srv_rpcparams (интерфейс API расширенных хранимых процедур)](../../relational-databases/extended-stored-procedures-reference/srv-rpcparams-extended-stored-procedure-api.md)  
  
  