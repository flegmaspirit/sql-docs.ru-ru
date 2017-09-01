---
title: "Программная работа с переменными | Документы Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- System namespace
- scope [Integration Services]
- variables [Integration Services], programmatically
- configuration files [Integration Services]
- Variables collection
- User namespace
- custom variables [Integration Services]
- variables [Integration Services], customizing
ms.assetid: c4b76a3d-94ca-4a8e-bb45-cb8bd0ea3ec1
caps.latest.revision: 53
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 4a8ade977c971766c8f716ae5f33cac606c8e22d
ms.openlocfilehash: 5c8968302f42e1b8fde55894810ecb77cf715ab6
ms.contentlocale: ru-ru
ms.lasthandoff: 08/03/2017

---
# <a name="working-with-variables-programmatically"></a>Программная работа с переменными
  С помощью переменных можно динамически задавать значения и управлять процессами в пакетах, контейнерах, задачах и обработчиках событий. Переменные могут также использоваться элементами управления очередностью для управления направлением потока данных к различным задачам. С помощью переменных можно:  
  
-   Обновлять свойства пакета во время выполнения.  
  
-   Заполнять значения параметров инструкций Transact-SQL во время выполнения.  
  
-   Управлять потоком цикла по каждому элементу. Дополнительные сведения см. в разделе [Добавление перечисления к поток управления](http://msdn.microsoft.com/library/f212b5fb-3cc4-422e-9b7c-89eb769a812a).  
  
-   Управлять управлением очередностью, используя его в выражении. Управление очередностью может содержать переменные в определении ограничения. Дополнительные сведения см. в статье [Добавление выражений к элементам управления очередностью](http://msdn.microsoft.com/library/5574d89a-a68e-4b84-80ea-da93305e5ca1).  
  
-   Управлять условным повторением контейнера «цикл по элементам». Дополнительные сведения см. в разделе [Добавление итерации к поток управления](http://msdn.microsoft.com/library/eb3a7494-88ae-4165-9d0f-58715eb1734a).  
  
-   Строить выражения, содержащие значения переменных.  
  
-   Можно создать пользовательские переменные для всех типов контейнеров: пакетов, **цикл** контейнеры, **цикл For** контейнеры, **последовательности** контейнеров, серверов задач и обработчиков событий. Дополнительные сведения см. в разделах [Переменные в службах Integration Services (SSIS)](../../integration-services/integration-services-ssis-variables.md) и [Использование переменных в пакетах](http://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787).  
  
## <a name="scope"></a>Область действия  
 Каждый контейнер имеет собственную коллекцию <xref:Microsoft.SqlServer.Dts.Runtime.Variables>. При создании новой переменной она располагается в области своего родительского контейнера. Поскольку контейнер пакета находится на верхнем уровне иерархии контейнеров, переменные в области пакета ведут себя как глобальные переменные и могут использоваться во всех контейнерах пакета. Доступ к коллекции переменных для контейнера могут также получать дочерние элементы контейнера через коллекцию <xref:Microsoft.SqlServer.Dts.Runtime.Variables>, используя имя переменной или ее индекс в коллекции.  
  
 Поскольку доступность переменной определяется сверху вниз, переменные, объявленные на уровне пакета, являются доступными для всех контейнеров в пакете. Таким образом, коллекция <xref:Microsoft.SqlServer.Dts.Runtime.Variables> в контейнере включает все переменные, принадлежащие родительской коллекции, в дополнение к своим собственным.  
  
 С другой стороны, переменные, содержащиеся в задаче, ограничены по области применения и доступности и доступны только задаче.  
  
 Если пакет выполняет другие пакеты, переменные, определенные в области вызывающего пакета, доступны для вызываемого пакета. Единственным исключением является случай, когда в вызываемом пакете существует переменная с тем же именем. При возникновении такой коллизии значение переменной из вызываемого пакета переопределяет значение переменной из вызывающего пакета. Переменные, определенные в области вызываемого пакета, недоступны для вызывающего пакета.  
  
 В следующем примере кода программным способом создается переменная `myCustomVar` в области пакета, а затем просматриваются все переменные, доступные для пакета, выводятся на печать их имена, тип данных и значения.  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
  
namespace Microsoft.SqlServer.Dts.Samples  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      Application app = new Application();  
      // Load a sample package that contains a variable that sets the file name.  
      Package pkg = app.LoadPackage(  
        @"C:\Program Files\Microsoft SQL Server\100\Samples\Integration Services" +  
        @"\Package Samples\CaptureDataLineage Sample\CaptureDataLineage\CaptureDataLineage.dtsx",  
        null);  
      Variables pkgVars = pkg.Variables;  
      Variable myVar = pkg.Variables.Add("myCustomVar", false, "User", "3");  
      foreach (Variable pkgVar in pkgVars)  
      {  
        Console.WriteLine("Variable: {0}, {1}, {2}", pkgVar.Name,  
          pkgVar.DataType, pkgVar.Value.ToString());  
      }  
      Console.Read();  
    }  
  }  
}  
```  
  
```vb  
Imports Microsoft.SqlServer.Dts.Runtime  
  
Module Module1  
  
  Sub Main()  
  
    Dim app As Application = New Application()  
    ' Load a sample package that contains a variable that sets the file name.  
    Dim pkg As Package = app.LoadPackage( _  
      "C:\Program Files\Microsoft SQL Server\100\Samples\Integration Services" & _  
      "\Package Samples\CaptureDataLineage Sample\CaptureDataLineage\CaptureDataLineage.dtsx", _  
      Nothing)  
    Dim pkgVars As Variables = pkg.Variables  
    Dim myVar As Variable = pkg.Variables.Add("myCustomVar", False, "User", "3")  
    Dim pkgVar As Variable  
    For Each pkgVar In pkgVars  
      Console.WriteLine("Variable: {0}, {1}, {2}", pkgVar.Name, _  
        pkgVar.DataType, pkgVar.Value.ToString())  
    Next  
    Console.Read()  
  
  End Sub  
  
End Module  
```  
  
 **Вывод образца:**  
  
 `Variable: CancelEvent, Int32, 0`  
  
 `Variable: CreationDate, DateTime, 4/18/2003 11:57:00 AM`  
  
 `Variable: CreatorComputerName, String,`  
  
 `Variable: CreatorName, String,`  
  
 `Variable: ExecutionInstanceGUID, String, {237AB5A4-7E59-4FC9-8D61-E8F20363DF25}`  
  
 `Variable: FileName, String, Junk`  
  
 `Variable: InteractiveMode, Boolean, False`  
  
 `Variable: LocaleID, Int32, 1033`  
  
 `Variable: MachineName, String, MYCOMPUTERNAME`  
  
 `Variable: myCustomVar, String, 3`  
  
 `Variable: OfflineMode, Boolean, False`  
  
 `Variable: PackageID, String, {F0D2E396-A6A5-42AE-9467-04CE946A810C}`  
  
 `Variable: PackageName, String, DTSPackage1`  
  
 `Variable: StartTime, DateTime, 1/28/2005 7:55:39 AM`  
  
 `Variable: UserName, String, <domain>\<userid>`  
  
 `Variable: VersionBuild, Int32, 198`  
  
 `Variable: VersionComments, String,`  
  
 `Variable: VersionGUID, String, {90E105B4-B4AF-4263-9CBD-C2050C2D6148}`  
  
 `Variable: VersionMajor, Int32, 1`  
  
 `Variable: VersionMinor, Int32, 0`  
  
 Обратите внимание, что все переменные, определенные в **системы** пространства имен доступны в пакет. Дополнительные сведения см. в статье [System Variables](../../integration-services/system-variables.md).  
  
## <a name="namespaces"></a>Пространства имен  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ([!INCLUDE[ssIS](../../includes/ssis-md.md)]) предоставляют два пространства имен по умолчанию, где располагаются переменные; **Пользователя** и **системы** пространства имен. По умолчанию любая пользовательская переменная, созданная разработчиком добавляется **пользователя** пространства имен. Системные переменные располагаются в **системы** пространства имен. Можно создать дополнительные пространства имен, отличное от **пользователя** пространство имен для размещения пользовательских переменных и можно изменить имя **пользователя** пространства имен, но нельзя добавлять и изменять переменные в **системы** пространства имен, или назначить системные переменные другому пространству имен.  
  
 Доступность системных переменных определяется типом контейнера. Список системных переменных, доступных для пакетов, контейнеров, задач и обработчиков событий см. в разделе [системные переменные](../../integration-services/system-variables.md).  
  
## <a name="value"></a>Значение  
 Значением пользовательской переменной может быть строка или выражение.  
  
-   Если необходимо задать для переменной литеральное значение, укажите значение ее свойства <xref:Microsoft.SqlServer.Dts.Runtime.Variable.Value%2A>.  
  
-   Если требуется переменная содержала выражение, результат выражения можно использовать как его значение, задайте <xref:Microsoft.SqlServer.Dts.Runtime.Variable.EvaluateAsExpression%2A> свойства переменной для **true**и указать выражение в <xref:Microsoft.SqlServer.Dts.Runtime.Variable.Expression%2A> свойство. Во время выполнения выражение вычисляется, и его результат используется в качестве значения переменной. Например, если свойство выражения переменной имеет вид `"100 * 2""100 * 2"`, в результате вычисления переменная получает значение 200.  
  
 Для переменной нельзя явно задать значение <xref:Microsoft.SqlServer.Dts.Runtime.Variable.DataType%2A>. Значение <xref:Microsoft.SqlServer.Dts.Runtime.Variable.DataType%2A> выводится из исходного значения, присвоенного переменной, и в дальнейшем не может быть изменено. Дополнительные сведения о типах данных переменных см. в разделе [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
 В следующем примере кода создается новая переменная, свойству <xref:Microsoft.SqlServer.Dts.Runtime.Variable.EvaluateAsExpression%2A> для **true**, присваивает выражение `"100 * 2"` свойства expression переменной, а затем выводит значение переменной.  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
  
namespace Microsoft.SqlServer.Dts.Samples  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      Package pkg = new Package();  
      Variable v100 = pkg.Variables.Add("myVar", false, "", 1);  
      v100.EvaluateAsExpression = true;  
      v100.Expression = "100 * 2";  
      Console.WriteLine("Expression for myVar: {0}",   
        v100.Properties["Expression"].GetValue(v100));  
      Console.WriteLine("Value of myVar: {0}", v100.Value.ToString());  
      Console.Read();  
    }  
  }  
}  
```  
  
```vb  
Imports Microsoft.SqlServer.Dts.Runtime  
  
Module Module1  
  
  Sub Main()  
  
    Dim pkg As Package = New Package  
    Dim v100 As Variable = pkg.Variables.Add("myVar", False, "", 1)  
    v100.EvaluateAsExpression = True  
    v100.Expression = "100 * 2"  
    Console.WriteLine("Expression for myVar: {0}", _  
      v100.Properties("Expression").GetValue(v100))  
    Console.WriteLine("Value of myVar: {0}", v100.Value.ToString)  
    Console.Read()  
  
  End Sub  
  
End Module  
```  
  
 **Вывод образца:**  
  
 `Expression for myVar: 100 * 2`  
  
 `Value of myVar: 200`  
  
 Выражение должно быть действительным выражением, использующим синтаксис выражений служб [!INCLUDE[ssIS](../../includes/ssis-md.md)]. Литералы допускаются в выражениях переменных, в дополнение к операторам и функциям, которые предоставляются синтаксисом выражений, однако выражения не могут ссылаться на другие переменные или столбцы. Дополнительные сведения см. в разделе [Выражения служб Integration Services (SSIS)](../../integration-services/expressions/integration-services-ssis-expressions.md).  
  
## <a name="configuration-files"></a>Файлы конфигурации  
 Если в файле конфигурации содержится пользовательская переменная, эта переменная может быть обновлена во время выполнения. Это означает, что при выполнении пакета значение переменной, содержавшееся в пакете изначально, заменяется новым значением из файла конфигурации. Такой способ замены оказывается полезным, когда пакет развертывается на нескольких серверах, где требуются разные значения переменной. Например, переменной можно задать количество повторов **цикл** контейнера повторяет его рабочего процесса, или список получателей, которые обработчик событий направляет сообщения электронной почты при возникновении ошибки или измените число ошибок, может произойти перед сбоем пакета. Эти переменные динамически передаются в файлах конфигурации для каждой среды. По этой причине в файлах конфигурации допускается использование только переменных, доступных для чтения и записи. Дополнительные сведения см. в разделе [Создание конфигурации пакетов](../../integration-services/packages/create-package-configurations.md).  
  
## <a name="see-also"></a>См. также:  
 [Службы Integration Services &#40; Службы SSIS &#41; Переменные](../../integration-services/integration-services-ssis-variables.md)   
 [Использование переменных в пакетах](http://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)  
  
  