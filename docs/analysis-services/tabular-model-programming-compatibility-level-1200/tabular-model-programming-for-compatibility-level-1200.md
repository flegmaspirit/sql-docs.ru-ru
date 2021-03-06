---
title: Программирование табличных моделей уровня совместимости 1200 | Документы Microsoft
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 8e0bfc84806e44ef05312da9d15d1afaa7dd9754
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/10/2018
---
# <a name="tabular-model-programming-for-compatibility-level-1200-and-higher"></a>Табличные модели программирования для совместимости уровня 1200 и выше
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
Начиная с уровнем совместимости 1200, табличных метаданных используется для описания модели конструкций, заменив исторических многомерные метаданные как дескрипторы для табличной модели объектов. Метаданные для таблицы, столбцы и связи являются таблицы, столбца и связи, а не многомерные эквиваленты (измерений и атрибутов).  
  
Можно создавать новые модели на уровне совместимости 1200 или выше с помощью API Microsoft.AnalysisServices.Tabular, последнюю версию из SQL Server Data Tools (SSDT), или путем изменения **CompatibilityLevel** существующих табличных модель для обновления (также выполняется в SSDT). Таким образом привязывает модель к более новым версиям сервера, средств и программных интерфейсов.   
  
Обновление существующего табличного решения рекомендуется, но не является обязательным. Существующий скрипт и пользовательских решений, которые используют или управление табличными моделями или баз данных можно использовать в качестве-является. Более ранними уровнями совместимости полностью поддерживаются в SQL Server 2016 с помощью функции, доступные на этом уровне. Azure Analysis Services поддерживает только уровень совместимости 1200 и выше.
  
 Новых табличных моделей потребуется другой код и сценарии, в приведенных ниже разделах.  
  
## <a name="object-model-definitions-as-tabular-metadata-constructs"></a>Определения модели объектов как конструкции табличных метаданных  
 Объектную модель табличных моделей 1200 или выше представлены в JSON через [языке скриптов табличных моделей](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md) и с помощью языка описания данных объектов AMO через новое пространство имен [ Microsoft.AnalysisServices.Tabular](http://msdn.microsoft.com/library/microsoft.analysisservices.tabular.aspx)

## <a name="script-for-tabular-models-and-databases"></a>Скрипт для табличных моделей и баз данных  
 TMSL — это JSON язык сценариев для табличных моделей с поддержкой создание, чтение, обновление, операции удаления. Можно обновить данные через TMSL и вызова операций базы данных для присоединения, отъединение, резервного копирования и восстановления и синхронизации.  
  
 Объекты AMO PowerShell сценарий TMSL принимает в качестве входных данных.  
  
 В разделе [языке скриптов табличных моделей &#40;TMSL&#41; ссылки](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md) и [Analysis Services PowerShell Reference](../../analysis-services/powershell/analysis-services-powershell-reference.md) для получения дополнительной информации.  
  
## <a name="query-languages"></a>Языки запросов  
 DAX и многомерных Выражений поддерживаются для всех табличных моделей.  
  
## <a name="expression-language"></a>Язык выражений  
 Фильтры и выражения, используемые для создания вычисляемых объектов, включая меры и ключевые показатели эффективности, организуются в DAX. В разделе [основные сведения о DAX в табличных моделях](../../analysis-services/tabular-models/understanding-dax-in-tabular-models-ssas-tabular.md) и [выражения анализа данных &#40;DAX&#41; в службах Analysis Services](http://msdn.microsoft.com/library/abb336c9-3346-4cab-b91b-90f93f4575e5).  
  
## <a name="managed-code-for-tabular-models-and-databases"></a>Управляемый код для табличных моделей и баз данных  
 Объекты AMO включает новое пространство имен Microsoft.AnalysisServices.Tabular, для работы с моделями, программными средствами. В разделе [Microsoft.AnalysisServices имен](https://msdn.microsoft.com/library/ms146720\(SQL.130\).aspx) для получения дополнительной информации.  
  
> [!NOTE]  
>  Клиентские библиотеки табличной модели объектов (TOM), ADOMD.NET и объекты управления Analysis Services (AMO) теперь модуля выполнения .NET 4.0.   
  
## <a name="see-also"></a>См. также  
 [Документация для разработчика служб Analysis Services](../../analysis-services/analysis-services-developer-documentation.md)   
 [Программирование табличных моделей для обеспечения совместимости уровни 1050 до 1103](../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/tabular-model-programming-for-compatibility-levels-1050-through-1103.md)   
 [Технический справочник по ](../../analysis-services/powershell/technical-reference-ssas.md) [обновление служб Analysis Services](../../database-engine/install-windows/upgrade-analysis-services.md)  
 [Уровни совместимости табличных моделей и баз данных](../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/tabular-model-programming-for-compatibility-levels-1050-through-1103.md)  
  
  
