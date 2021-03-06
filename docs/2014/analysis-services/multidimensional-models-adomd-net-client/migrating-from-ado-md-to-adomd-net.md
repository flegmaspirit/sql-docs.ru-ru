---
title: Миграция от ADO MD к ADOMD.NET | Документация Майкрософт
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- ADOMD.NET, migrating to
- migrating ADO MD to ADOMD.NET
- ADO MD migration [ADOMD.NET]
ms.assetid: 8c760db3-c475-468e-948d-e5f599d985ad
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 77065088ed85e5467e28d501921a162eb39e1ccf
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/02/2018
ms.locfileid: "48153044"
---
# <a name="migrating-from-ado-md-to-adomdnet"></a>Миграция от ADO MD к ADOMD.NET
  Библиотека ADOMD.NET похожа на библиотеку ADO MD, представляющую собой расширение библиотеки ActiveX Data Objects (ADO), которая в клиентских приложениях на основе COM используется для доступа к многомерным данным. ADO MD обеспечивает простой доступ к многомерным данным из таких неуправляемых языков, как C++ и [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic. ADOMD.NET обеспечивает простой доступ к аналитическим данным (и многомерным, и используемым в интеллектуальном анализе) из таких управляемых языков, как [!INCLUDE[msCoName](../../includes/msconame-md.md)] C# и [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic .NET. Кроме того, ADOMD.NET предоставляет улучшенную модель объектов метаданных.  
  
 Миграция существующих клиентских приложений от ADO MD к ADOMD.NET является несложной, однако в отношении миграции этого типа имеется несколько важных отличий.  
  
 **Для обеспечения подключения и доступа к данным для клиентских приложений**  
 |ADO MD|ADOMD.NET|  
|------------|---------------|  
|Требует ссылок на файлы Adodb.dll и Adomd.dll.|Требует одной ссылки на файл Microsoft.AnalysisServices.AdomdClient.dll.|  
  
 Класс <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> в дополнение к доступу к метаданным обеспечивает поддержку обмена данными.  
  
 **Для получения метаданных для многомерных объектов**  
 |ADO MD|ADOMD.NET|  
|------------|---------------|  
|Класс каталога.|Используйте свойство <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.Cubes%2A> объекта <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection>.|  
  
 **Для выполнения запросов и возвращение объектов набора ячеек**  
 |ADO MD|ADOMD.NET|  
|------------|---------------|  
|Класс набора ячеек.|Используйте класс <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand>.|  
  
 **Для доступа к метаданным, который используется для отображения набора ячеек**  
 |ADO MD|ADOMD.NET|  
|------------|---------------|  
|Класс позиции.|Используйте объекты <xref:Microsoft.AnalysisServices.AdomdClient.Set> и <xref:Microsoft.AnalysisServices.AdomdClient.Tuple>.|  
  
> [!NOTE]  
>  Класс <xref:Microsoft.AnalysisServices.AdomdClient.Position> поддерживается для обратной совместимости.  
  
 **Для получения метаданных модели интеллектуального анализа данных**  
 |ADO MD|ADOMD.NET|  
|------------|---------------|  
|Не доступен ни один класс.|Используйте одну из коллекций интеллектуального анализа данных.<br /><br /> - <xref:Microsoft.AnalysisServices.AdomdClient.MiningModelCollection> Содержит список всех моделей интеллектуального анализа данных в источнике данных.<br />- <xref:Microsoft.AnalysisServices.AdomdClient.MiningServiceCollection> Предоставляет сведения об алгоритмах интеллектуального анализа данных.<br />- <xref:Microsoft.AnalysisServices.AdomdClient.MiningStructureCollection> Предоставляет сведения о структурах интеллектуального анализа данных на сервере.|  
  
 Чтобы можно было подчеркнуть эти различия, в следующем примере миграции существующее приложение ADO MD сравнивается с эквивалентным ему приложением ADOMD.NET.  
  
## <a name="looking-at-a-migration-example"></a>Анализ примера миграции  
 И пример кода существующего приложения ADO MD, и его эквивалент ADOMD.NET, приведенные в этом разделе, выполняют одинаковый набор действий: создание соединения, выполнение инструкции многомерного выражения, а также извлечение метаданных и данных. Однако для выполнения указанных задач в этих двух наборах кода используются разные объекты.  
  
### <a name="existing-ado-md-code"></a>Существующий код ADO MD  
 В следующем примере кода из документации по ADO MD 2.8, написан [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic® 6.0 и используется ADO MD для демонстрации подключения и выполнения запросов [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] источника данных. В этом примере ADO MD используются следующие объекты:  
  
-   Создает соединение с использованием объекта `Catalog`.  
  
-   Выполняет инструкцию многомерного выражения при помощи объекта `Cellset`.  
  
-   Получает метаданные и данные из объекта `Position`, возвращаемого объектом `Cellset`.  
  
```  
Private Sub cmdCellSettoDebugWindow_Click()  
Dim cat As New ADOMD.Catalog  
Dim cst As New ADOMD.Cellset  
Dim i As Integer  
Dim j As Integer  
Dim k As Integer  
Dim strServer As String  
Dim strSource As String  
Dim strColumnHeader As String  
Dim strRowText As String  
  
On Error GoTo Error_cmdCellSettoDebugWindow_Click  
Screen.MousePointer = vbHourglass  
'*-----------------------------------------------------------------------  
'* Set server to local host.  
'*-----------------------------------------------------------------------  
    strServer = "LOCALHOST"  
  
'*-----------------------------------------------------------------------  
'* Set MDX query string source.  
'*-----------------------------------------------------------------------  
    strSource = strSource & "SELECT "  
    strSource = strSource & "{[Measures].members} ON COLUMNS,"  
    strSource = strSource & _  
        "NON EMPTY [Store].[Store City].members ON ROWS"  
    strSource = strSource & " FROM Sales"  
  
'*-----------------------------------------------------------------------  
'* Set active connection.  
'*-----------------------------------------------------------------------  
        cat.ActiveConnection = "Data Source=" & strServer & _  
            ";Provider=msolap;"  
  
'*-----------------------------------------------------------------------  
'* Set cellset source to MDX query string.  
'*-----------------------------------------------------------------------  
        cst.Source = strSource  
  
'*-----------------------------------------------------------------------  
'* Set cellset active connection to current connection  
'*-----------------------------------------------------------------------  
    Set cst.ActiveConnection = cat.ActiveConnection  
  
'*-----------------------------------------------------------------------  
'* Open cellset.  
'*-----------------------------------------------------------------------  
    cst.Open  
  
'*-----------------------------------------------------------------------  
'* Allow space for row header text.  
'*-----------------------------------------------------------------------  
strColumnHeader = vbTab & vbTab & vbTab & vbTab & vbTab & vbTab  
  
'*-----------------------------------------------------------------------  
'* Loop through column headers.  
'*-----------------------------------------------------------------------  
       For i = 0 To cst.Axes(0).Positions.Count - 1  
            strColumnHeader = strColumnHeader & _  
                cst.Axes(0).Positions(i).Members(0).Caption & vbTab & _  
                    vbTab & vbTab & vbTab  
       Next  
       Debug.Print vbTab & strColumnHeader & vbCrLf  
  
'*-----------------------------------------------------------------------  
'* Loop through row headers and provide data for each row.  
'*-----------------------------------------------------------------------  
        strRowText = ""  
        For j = 0 To cst.Axes(1).Positions.Count - 1  
            strRowText = strRowText & _  
                cst.Axes(1).Positions(j).Members(0).Caption & vbTab & _  
                    vbTab & vbTab & vbTab  
            For k = 0 To cst.Axes(0).Positions.Count - 1  
                strRowText = strRowText & cst(k, j).FormattedValue & _  
                    vbTab & vbTab & vbTab & vbTab  
            Next  
            Debug.Print strRowText & vbCrLf  
            strRowText = ""  
        Next  
  
    Screen.MousePointer = vbDefault  
Exit Sub  
  
Error_cmdCellSettoDebugWindow_Click:  
   Beep  
   Screen.MousePointer = vbDefault  
   MsgBox "The following error has occurred:" & vbCrLf & _  
      Err.Description, vbCritical, " Error!"  
   Exit Sub  
End Sub  
```  
  
### <a name="equivalent-adomdnet-code"></a>Эквивалентный код ADOMD.NET  
 Следующий пример кода, написанный на языке Visual Basic .NET с использованием ADOMD.NET, демонстрирует выполнение таких же действий, которые выполняются в предыдущем примере на Visual Basic 6.0. Основная разница между приведенным далее примером и примером ADO MD, показанным ранее, заключается в том, какие объекты используются для выполнения действий. В примере ADOMD.NET используются следующие объекты.  
  
-   Создает соединение с помощью объекта `AdomdConnection`.  
  
-   Выполнение инструкции многомерных выражений при помощи объекта `AdomdCommand`.  
  
-   Получает метаданные и данные из объекта `Set`, возвращаемого объектом `Cellset`.  
  
```  
Private Sub DisplayCellSetInOutputWindow()  
    Dim conn As AdomdConnection  
    Dim cmd As AdomdCommand  
    Dim cst As CellSet  
    Dim i As Integer  
    Dim j As Integer  
    Dim k As Integer  
    Dim strServer As String = "LOCALHOST"  
    Dim strSource As String = "SELECT [Measures].members ON COLUMNS, " & _  
        "NON EMPTY [Store].[Store City].members ON ROWS FROM SALES"  
    Dim strOutput As New System.IO.StringWriter  
  
    '*-----------------------------------------------------------------------  
    '* Open connection.  
    '*-----------------------------------------------------------------------  
    Try  
        ' Create a new AdomdConnection object, providing the connection  
        ' string.  
        conn = New AdomdConnection("Data Source=" & strServer & _  
        ";Provider=msolap;")  
        ' Open the connection.  
        conn.Open()  
    Catch ex As Exception  
        Throw New ApplicationException( _  
            "An error occurred while connecting.")  
    End Try  
  
    Try  
    '*-----------------------------------------------------------------------  
    '* Open cellset.  
    '*-----------------------------------------------------------------------  
        ' Create a new AdomdCommand object, providing the MDX query string.  
        cmd = New AdomdCommand(strSource, conn)  
        ' Run the command and return a CellSet object.  
        cst = cmd.ExecuteCellSet()  
  
    '*-----------------------------------------------------------------------  
    '* Concatenate output.  
    '*-----------------------------------------------------------------------  
  
    ' Include spacing to account for row headers.  
    strOutput.Write(vbTab, 6)  
  
    ' Iterate through the first axis of the CellSet object and  
    ' retrieve column headers.  
    For i = 0 To cst.Axes(0).Set.Tuples.Count - 1  
        strOutput.Write(cst.Axes(0).Set.Tuples(i).Members(0).Caption)  
        strOutput.Write(vbTab, 4)  
    Next  
    strOutput.WriteLine()  
  
    ' Iterate through the second axis of the CellSet object and  
    ' retrieve row headers and cell data.  
    For j = 0 To cst.Axes(1).Set.Tuples.Count - 1  
        ' Append the row header.  
        strOutput.Write(cst.Axes(1).Set.Tuples(j).Members(0).Caption)  
        strOutput.Write(vbTab, 4)  
  
        ' Append the cell data for that row.  
        For k = 0 To cst.Axes(0).Set.Tuples.Count - 1  
            strOutput.Write(cst.Cells(k, j).FormattedValue)  
            strOutput.Write(vbTab, 4)  
        Next  
        strOutput.WriteLine()  
    Next  
  
    ' Display the output.  
    Debug.WriteLine(strOutput.ToString)  
  
    '*-----------------------------------------------------------------------  
    '* Release resources.  
    '*-----------------------------------------------------------------------  
        conn.Close()  
    Catch ex As Exception  
        ' Ignore or handle errors.  
    Finally  
        cst = Nothing  
        cmd = Nothing  
        conn = Nothing  
    End Try  
End Sub  
```  
  
  
