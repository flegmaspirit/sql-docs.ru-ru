---
title: () (скобки) (выражение служб SSIS) | Документы Майкрософт
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- () (parentheses operator)
- evaluation order [Integration Services]
- parentheses operator ()
ms.assetid: 931e10eb-1707-4121-b2f1-43565561119f
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 705dbabc07308d4e6112489d3d22a0354075fcad
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/01/2018
ms.locfileid: "47595442"
---
# <a name="-parentheses-ssis-expression"></a>() (скобки) (выражение служб SSIS)
  Определяет порядок вычисления выражений. Выражения, взятые в скобки, имеют самый высокий приоритет вычисления. Вложенные выражения в скобках вычисляются от внутреннего к внешнему.  
  
 Кроме того, скобки применяются для того, чтобы облегчить чтение сложных выражений.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
(expression)  
  
```  
  
## <a name="arguments"></a>Аргументы  
 *expression*  
 Любое допустимое выражение.  
  
## <a name="result-types"></a>Типы результата  
 Тип данных *expression*. Дополнительные сведения см. в статье [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
## <a name="expression-examples"></a>Примеры выражений  
 В этом примере показано изменение приоритета операторов с помощью скобок. Значение для первого выражения — 100, для второго — 31.  
  
```  
(5 + 5) * (4 + 6)  
5 + 5 * 4 + 6  
  
```  
  
## <a name="see-also"></a>См. также:  
 [Очередность и ассоциативность операторов](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [Операторы (выражение служб SSIS)](../../integration-services/expressions/operators-ssis-expression.md)  
  
  
