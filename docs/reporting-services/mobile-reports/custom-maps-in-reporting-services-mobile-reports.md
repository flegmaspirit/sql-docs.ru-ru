---
title: Пользовательские карты в мобильных отчетах Reporting Services | Документы Майкрософт
ms.date: 03/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: mobile-reports
ms.topic: conceptual
ms.assetid: 59a4ebad-587a-4770-afcd-c69216b8afd9
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 5a25999826655f4ad48992ffa4705f86c9422650
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/01/2018
ms.locfileid: "47776892"
---
# <a name="custom-maps-in-reporting-services-mobile-reports"></a>Custom maps in Reporting Services mobile reports
Географические карты в издателе мобильных отчетов для SQL Server определяются в формате, известном как *файлы фигур ESRI*.  
  
Этот формат, первоначально разработанный частной компанией, теперь является широко распространенным частично открытым форматом, используемым во многих приложениях GIS. В соответствии с этим форматом для издателя мобильных отчетов требуется два файла, чтобы определить карту:  
  
- SHP-файл для контуров фигур  
- DBF-файл для метаданных  
  
Базовые имена файлов должны совпадать (например, *canada.shp* и *canada.dbf*). Метаданные должны включать поле *NAME* со значением соответствующего имени фигуры (ключа), которое будет использоваться при заполнении карты данными.  
  
> **Примечание**. Два файла карты вместе, SHP и DBF, по размеру не должны превышать 512 КБ. Если файлы карты слишком велики, для уменьшения их размера можно воспользоваться таким средством, как [http://mapshaper.org/](http://mapshaper.org/).  
  
Узнайте, как [добавлять пользовательские карты в мобильные отчеты](../../reporting-services/mobile-reports/add-a-custom-map-to-a-reporting-services-mobile-report.md).  
  
## <a name="technical-information"></a>Технические сведения  
  
- Официальная спецификация: [http://www.esri.com/library/whitepapers/pdfs/shapefile.pdf](http://www.esri.com/library/whitepapers/pdfs/shapefile.pdf)  
- Статье о файлах фигур в Википедии: [http://en.wikipedia.org/wiki/Shapefile](http://en.wikipedia.org/wiki/Shapefile)  
  
## <a name="creating--editing-map-geometry"></a>Создание и редактирование геометрии карты  
  
Создание и редактирование файлов фигур является сложным процессом, описание которого выходит за рамки данного документа. Ниже приведены некоторые ресурсы и приложения, которые помогут вам приступить к работе.  
  
- ArcGIS: [http://www.arcgis.com/](http://www.arcgis.com/)  
- Подключаемый модуль MAPublisher для Adobe Illustrator: [http://www.avenza.com/mapublisher](http://www.avenza.com/mapublisher)  
- QuantumGIS (бесплатно): [http://www.qgis.org/](http://www.qgis.org/)  
- Редактор Manco файлов фигур: [http://www.mancosoftware.com/ShapeFileEditor](http://www.mancosoftware.com/ShapeFileEditor)  
  
## <a name="existing-shapefiles"></a>Существующие файлы фигур  
  
Многие существующие файлы фигур можно скачать с веб-сайтов, таких как:  
  
- Diva-GIS: [http://www.diva-gis.org/Data](http://www.diva-gis.org/Data)  
- OpenStreetMap: [http://openstreetmapdata.com/data](http://openstreetmapdata.com/data)  
  
### <a name="see-also"></a>См. также раздел  
- [Maps in Reporting Services mobile reports](../../reporting-services/mobile-reports/maps-in-reporting-services-mobile-reports.md)  
- [Создание и публикация мобильных отчетов с помощью издателя мобильных отчетов SQL Server](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)   
  
  
  
