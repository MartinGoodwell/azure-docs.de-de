---
title: "Referenz für Analytics in Azure Application Insights | Microsoft Docs"
description: "Referenz für Anweisungen in Analytics, dem leistungsfähigen Suchtool von Application Insights. "
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: eea324de-d5e5-4064-9933-beb3a97b350b
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: cfreeman
ms.translationtype: Human Translation
ms.sourcegitcommit: b1d56fcfb472e5eae9d2f01a820f72f8eab9ef08
ms.openlocfilehash: dd3478966e4e5ccc9f108940401c7ee9454087dd
ms.contentlocale: de-de
ms.lasthandoff: 07/06/2017


---
# <a name="reference-for-analytics"></a>Referenz für Analytics
[Analytics](app-insights-analytics.md) ist die leistungsfähige Suchfunktion von [Application Insights](app-insights-overview.md). Auf diesen Seiten wird die Analytics-Abfragesprache beschrieben.

Zusätzliche Informationsquellen:

* Während der Eingabe in Analytics ist viel Referenzmaterial verfügbar. Beginnen Sie einfach mit der Eingabe einer Abfrage, und Sie erhalten Vervollständigungsvorschläge.
* [Die Seite „Tutorial“](app-insights-analytics-tour.md) bietet eine schrittweise Einführung in die Sprachfunktionen.
* In der [Kurzübersicht für SQL-Benutzer](https://aka.ms/sql-analytics) finden Sie eine Übersetzung der gängigsten Sprachen.
* [Testen Sie Analytics mit unseren simulierten Daten](https://analytics.applicationinsights.io/demo), wenn Ihre eigene App noch keine Daten an Application Insights sendet.
 

## <a name="index"></a>Index
**Let** [let](#let-clause) | [materialize](#materialize) 

**Abfragen und Operatoren** [as](#as-operator) | [autocluster](#evaluate-autocluster_v2) | [basket](#evaluate-basketv2) | [count](#count-operator) | [datatable](#datatable-operator) | [diffpatterns](#evaluate-diffpatterns_v2) | [distinct](#distinct-operator) | [evaluate](#evaluate-operator) | [extend](#extend-operator) | [extractcolumns](#evaluate-extractcolumns) | [find](#find-operator) | [getschema](#getschema-operator) | [join](#join-operator) | [limit](#limit-operator) | [make-series](#make-series-operator) | [mvexpand](#mvexpand-operator) | [parse](#parse-operator) | [project](#project-operator) | [project-away](#project-away-operator) | [range](#range-operator) | [reduce](#reduce-operator) | [render directive](#render-directive) | [restrict clause](#restrict-clause) | [sample](#sample-operator) | [sample-distinct](#sample-distinct-operator) | [sort](#sort-operator) | [summarize](#summarize-operator) | [table](#table-operator) | [take](#take-operator) | [top](#top-operator) | [topnested](#top-nested-operator) | [union](#union-operator) | [where](#where-operator) 

**Aggregationen** [any](#any) | [argmax](#argmax) | [argmin](#argmin) | [avg](#avg) | [buildschema](#buildschema) | [count](#count) | [countif](#countif) | [dcount](#dcount) | [dcountif](#dcountif) | [makelist](#makelist) | [makeset](#makeset) | [max](#max) | [min](#min) | [percentile](#percentile) | [percentiles](#percentiles) | [percentilesw](#percentilesw) | [percentilew](#percentilew) | [stdev](#stdev) | [sum](#sum) | [variance](#variance)

**Skalare** [Boolesche Literale](#boolean-literals) | [Boolesche Operatoren](#boolean-operators) | [Typumwandlungen](#casts) | [Skalare Vergleiche](#scalar-comparisons) | [gettype](#gettype) | [hash](#hash) | [iff](#iff) | [isnotnull](#isnotnull) | [isnull](#isnull) | [notnull](#notnull) | [toscalar](#toscalar)

**Zahlen** [Arithmetische Operatoren](#arithmetic-operators) | [Numerische Literale](#numeric-literals) | [abs](#abs) | [bin](#bin) | [exp](#exp) | [floor](#floor) | [gamma](#gamma) | [log](#log) | [rand](#rand) | [sqrt](#sqrt) | [todouble](#todouble) | [toint](#toint) | [tolong](#tolong)

**Zahlenfolge** 
[series_fir](#seriesfir) | [series\_fit\_line](#seriesfitline) | [series\_fit\_2lines](#seriesfit2lines) | [series_iir](#seriesiir) |[series_outliers](#seriesoutliers)| [series_periods](#seriesperiods) | [series_stats](#seriesstats) | 

**Datum und Uhrzeit** [Datums- und Uhrzeitausdrücke](#date-and-time-expressions) | [Datums- und Uhrzeitliterale](#date-and-time-literals) | [ago](#ago) | [datepart](#datepart) | [dayofmonth](#dayofmonth) | [dayofweek](#dayofweek) | [dayofyear](#dayofyear) | [endofday](#endofday) | [endofmonth](#endofmonth) | [endofweek](#endofweek) | [endofyear](#endofyear) | [getmonth](#getmonth) | [getyear](#getyear) | [now](#now) | [startofday](#startofday) | [startofmonth](#startofmonth) | [startofweek](#startofweek) | [startofyear](#startofyear) | [todatetime](#todatetime) | [totimespan](#totimespan) | [weekofyear](#weekofyear)

**Zeichenfolge** [GUIDs](#guids) | [Verborgene Zeichenfolgenliterale](#obfuscated-string-literals) | [Zeichenfolgenliterale](#string-literals) | [Zeichenfolgenvergleiche](#string-comparisons) | [countof](#countof) | [extract](#extract) | [in, !in](#in) | [isempty](#isempty) | [isnotempty](#isnotempty) | [notempty](#notempty)| [parseurl](#parseurl) | [replace](#replace) | [split](#split) | [strcat](#strcat) | [strlen](#strlen) | [substring](#substring) | [tolower](#tolower) | [toupper](#toupper)

**Arrays, Objekte und Dynamik** [Array- und Objektliterale](#array-and-object-literals) | [Dynamische Objektfunktionen](#dynamic-object-functions) | [Dynamische Objekte in let-Klauseln](#dynamic-objects-in-let-clauses) | [JSON Path-Ausdrücke](#json-path-expressions) | [Namen](#names) | [arraylength](#arraylength) | [extractjson](#extractjson) | [in, !in](#in) | [parsejson](#parsejson) | [range](#range) | [todynamic](#todynamic) | [treepath](#treepath)

## <a name="let"></a>Let
### <a name="let-clause"></a>let-Klausel
**Tabellarisches let – Benennen einer Tabelle**

    let recentReqs = requests | where timestamp > ago(3d); 
    recentReqs | count

**Skalares let – Benennen eines Werts**

    let interval = 3d; 
    requests | where timestamp > ago(interval)

**Lambda-let – Benennen einer Funktion**

    let Recent = 
       (interval:timespan) { requests | where timestamp > ago(interval) };
    Recent(3h) | count

    let us_date = (t:datetime)
    {
      strcat(getmonth(t), "/", dayofmonth(t),"/", getyear(t), " ", 
      bin((t-1h)%12h+1h,1s), iff(t%24h<12h, "AM", "PM"))
    };
    requests 
    | summarize count() by bin(timestamp, 1h) 
    | project count_, pacificTime=us_date(timestamp-8h)

Eine let-Klausel bindet einen [Namen](#names) an ein tabellarisches Ergebnis, einen Skalarwert oder eine Funktion. Die Klausel ist das Präfix einer Abfrage, und diese Abfrage ist der Bereich der Bindung. (Die let-Klausel bietet keine Möglichkeit, Dinge zu benennen, die Sie später in der Sitzung verwenden.)

**Syntax**

    let name = scalar_constant_expression ; query

    let name = query ; query

    let name = (parameterName : type [, ...]) { plain_query }; query

    let name = (parameterName : type [, ...]) { scalar_expression }; query

* *type:* `bool`, `int`, `long`, `double`, `string`, `timespan`, `datetime`, `guid`, [`dynamic`](#dynamic-type)
* *plain_query:* Eine Abfrage ohne vorangestellte let-Klausel.

**Beispiele**

    let rows = (n:long) { range steps from 1 to n step 1 };
    rows(10) | ...

Konvertieren eines Tabellenergebnisses zu einem Skalar und Verwendung in einer Abfrage:

```
let topCities =  toscalar ( // convert single column to value
   requests
   | summarize count() by client_City 
   | top 4 by count_ 
   | summarize makeset(client_City)) ;
requests
| where client_City in (topCities) 
| summarize count() by client_City;
```

### <a name="materialize"></a>materialize

Verwenden Sie „materialize()“, um die Leistung zu verbessern, wenn das Ergebnis einer let-Klausel im weiteren Verlauf mehrmals verwendet wird. „materialize()“ wertet eine tabellarische let-Klausel zum Zeitpunkt der Abfrageausführung aus und speichert das Ergebnis zwischen. Dadurch wird sichergestellt, dass die Abfrage nicht mehrmals ausgeführt wird.

**Syntax**

    materialize(expression)

**Argumente**

* `expresion`: Tabellarischer Ausdruck, der im Rahmen der Abfrageausführung ausgewertet und zwischengespeichert werden soll.

**Tipps**

* Verwenden Sie „materialize“, wenn Sie über „join/union“ mit Operanden mit gegenseitigen Unterabfragen verfügen, die einmal ausgeführt werden können (wie in den folgenden Beispielen zu sehen).
* Auch hilfreich in Szenarien, in denen Verzweigungsabschnitte für „join/union“ benötigt werden.
* Wenn „materialize“ in let-Anweisungen verwendet wird, muss das zwischengespeicherte Ergebnis benannt werden.
* Die Cachegröße von „materialize“ ist auf 5 GB begrenzt. Dieser Grenzwert gilt pro Clusterknoten und für alle Abfragen.

**Beispiel: self-join**


```AIQL
let totalPagesPerDay = pageViews
| summarize by name, Day = startofday(timestamp)
| summarize count() by Day;
let materializedScope = pageViews
| summarize by name, Day = startofday(timestamp);
let cachedResult = materialize(materializedScope);
cachedResult
| project name, Day1 = Day
| join kind = inner
(
    cachedResult
    | project name, Day2 = Day
)
on name
| where Day2 > Day1
| summarize count() by Day1, Day2
| join kind = inner
    totalPagesPerDay
on $left.Day1 == $right.Day
| project Day1, Day2, Percentage = count_*100.0/count_1
```

Bei der nicht zwischengespeicherten Version wird das Ergebnis `scope` zweimal verwendet:

```AIQL
let totalPagesPerDay = pageViews
| summarize by name, Day = startofday(timestamp)
| summarize count() by Day;
let scope = pageViews
| summarize by name, Day = startofday(timestamp);
scope      // First use of this table.
| project name, Day1 = Day
| join kind = inner
(
    scope  // Second use can cause evaluation twice.
    | project name, Day2 = Day
)
on name
| where Day2 > Day1
| summarize count() by Day1, Day2
| join kind = inner
    totalPagesPerDay
on $left.Day1 == $right.Day
| project Day1, Day2, Percentage = count_*100.0/count_1
```

## <a name="queries-and-operators"></a>Abfragen und Operatoren
Eine Abfrage in Ihrer Telemetrie besteht aus einen Verweis auf einen Quelldatenstrom, gefolgt von einer Pipeline von Filtern. Zum Beispiel:

```AIQL
requests // The request table starts this pipeline.
| where client_City == "London" // filter the records
   and timestamp > ago(3d)
| count 
```

Jeder Filter mit einem senkrechten Strich ( `|` ) als Präfix ist eine Instanz eines *Operators*mit einigen Parametern. Die Eingabe des Operators ist die Tabelle, die das Ergebnis der vorhergehenden Pipeline ist. In den meisten Fällen sind alle Parameter [skalare Ausdrücke](#scalars) über die Spalten der Eingabe hinweg. In einigen Fällen sind die Parameter die Namen von Eingabespalten, und in einigen Fällen ist der Parameter eine zweite Tabelle. Das Ergebnis einer Abfrage ist immer eine Tabelle, auch wenn sie nur eine Spalte und eine Zeile enthält.

Abfragen können einzelne Zeilenumbrüche enthalten, aber sie werden mit einer Leerzeile beendet. Unter Umständen enthalten sie Kommentare zwischen `//` und dem Ende der Zeile.

Eine Abfrage kann eine oder mehrere [let-Klauseln](#let-clause)als Präfix aufweisen, mit denen Skalare, Tabellen oder Funktionen definiert werden, die in der Abfrage verwendet werden können.

```AIQL

    let interval = 3d ;
    let city = "London" ;
    let req = (city:string) {
      requests
      | where client_City == city and timestamp > ago(interval) };
    req(city) | count
```

> `T` wird in den folgenden Abfragebeispielen verwendet, um die vorhergehende Pipeline oder Quelltabelle anzugeben.
> 
> 

### <a name="as-operator"></a>as-Operator

Bindet einen Namen vorübergehend an den tabellarischen Eingabeausdruck.

**Syntax**

    T | as name

**Argumente**

* *name:* Ein temporärer Namen für die Tabelle.

**Hinweise**

* Verwenden Sie [let](#let-clause) anstelle von *as*, wenn Sie den Namen in einem späteren Teilausdruck verwenden möchten.
* Verwenden Sie *as*, um den Namen der Tabelle so anzugeben, wie er im Ergebnis eines Vorgangs vom Typ [union](#union-operator), [find](#find-operator) oder [search](#search-operator) erscheint.

**Beispiel**

```AIQL
range x from 1 to 10 step 1 | as T1
| union withsource=TableName (requests | take 10 | as T2)
```

### <a name="count-operator"></a>count-Operator
Der `count` -Operator gibt die Anzahl von Datensätzen (Zeilen) in der Eingabe-Datensatzgruppe an.

**Syntax**

    T | count

**Argumente**

* *T:*Die tabellarischen Daten, deren Datensätze gezählt werden.

**Rückgabe**

Diese Funktion gibt eine Tabelle mit einem einzelnen Datensatz und einer Spalte vom Typ `long`zurück. Der Wert der einzigen Zelle ist die Anzahl von Datensätzen in *T*. 

**Beispiel**

```AIQL
requests | count
```

### <a name="datatable-operator"></a>datatable-Operator

Legen Sie inline eine Tabelle fest. Das Schema und die Werte werden in der Abfrage selbst definiert.

Beachten Sie, dass dieser Operator über keine Pipelineeingabe verfügt.

**Syntax**

    datatable ( ColumnName1 : ColumnType1 , ...) [ScalarValue1, ...]

* *ColumnName* Ein Name für eine Spalte
* *ColumnType* Ein [Datentyp](#scalars) 
* *ScalarValue* Ein Wert des entsprechenden Typs. Die Anzahl der Werte muss ein Vielfaches der Spaltenanzahl sein. 

**Rückgabe**

Eine Tabelle mit den angegebenen Werten

**Beispiel**

```AIQL
datatable (Date:datetime, Event:string)
    [datetime(1910-06-11), "Born",
     datetime(1930-01-01), "Enters Ecole Navale",
     datetime(1953-01-01), "Published first book",
     datetime(1997-06-25), "Died"]
| where strlen(Event) > 4
```

### <a name="distinct-operator"></a>distinct-Operator

Gibt eine Tabelle zurück, die eine Gruppe von Zeilen mit unterschiedlichen Wertekombinationen enthält. Verweist optional auf einen Teil der Spalten vor der Operation.

**Syntax**

    T | distinct *              // All columns
    T | distinct Column1, ...   // Columns to project

**Beispiel**

```AIQL
datatable (Supplier: string, Fruit: string, Price:int) 
["Contoso", "Grapes", 22,
"Fabrikam", "Apples", 14,
"Contoso", "Apples", 15,
"Fabrikam", "Grapes", 22]
| distinct Fruit, Price 
```


|Frucht|Preis|
|---|---|
|Trauben|22|
|Äpfel|14|
|Äpfel|15|


### <a name="evaluate-operator"></a>evaluate-Operator
`evaluate` ist ein Erweiterungsmechanismus, mit dem spezielle Algorithmen an Abfragen angefügt werden können.

`evaluate` muss der letzte Operator in der Abfragepipeline sein (mit Ausnahme eines möglichen `render`-Elements). Er darf nicht in einem Funktionsrumpf erscheinen.

[evaluate autocluster](#evaluate-autocluster_v2) | [evaluate basket](#evaluate-basketv2) | [evaluate diffpatterns](#evaluate-diffpatterns_v2) | [evaluate extractcolumns](#evaluate-extractcolumns)

#### <a name="evaluate-autocluster-deprecated"></a>evaluate autocluster (veraltet)
     T | evaluate autocluster()

Autocluster ist eine schnelle Möglichkeit, um die natürlichen Gruppierungen in einem Dataset zu suchen. So könnten Sie z.B. aus einer Masse an Anforderungsdaten schnell erkennen, dass 80% der 404-Fehler Anforderungen für eine bestimmte URL waren, die von einem Client in einer bestimmten Stadt erfolgten.

Mit AutoCluster werden häufige Muster von diskreten Attributen (Dimensionen) in den Daten ermittelt, und die Ergebnisse der ursprünglichen Abfrage (ob mit 100 oder 100.000 Zeilen) werden auf eine kleine Anzahl von Mustern reduziert. AutoCluster wurde als Hilfe beim Analysieren von Fehlern (z.B. Ausnahmen, Abstürze) entwickelt, kann aber für jedes gefilterte Dataset verwendet werden. 

**Diese Version von `autocluster` ist veraltet. Verwenden Sie stattdessen [autocluster_v2](#evaluate-autocluster_v2).**

**Syntax**

    T | evaluate autocluster( arguments )

**Rückgabe**

AutoCluster gibt eine (in der Regel kleine) Gruppe von Mustern zurück, in der Teile der Daten mit gemeinsamen Werten über mehrere diskrete Attribute hinweg erfasst werden. Jede Zeile in den Ergebnissen steht für ein Muster. 

Die ersten beiden Spalten enthalten die Anzahl und den Prozentsatz der Zeilen aus der ursprünglichen Abfrage, die mit dem Muster erfasst wurden. Die restlichen Spalten stammen aus der ursprünglichen Abfrage. Sie enthalten als Wert entweder einen bestimmten Wert aus der Spalte oder „*“ (variable Werte). 

Beachten Sie, dass die Muster nicht unzusammenhängend sind: sie können sich überlappen und decken normalerweise nicht alle ursprünglichen Zeilen ab. Einige Zeilen fallen ggf. nicht in eines der Muster.

**Tipps**

* Verwenden Sie `where` und `project` im Pipe-Eingangselement, um die Daten auf den Teil zu reduzieren, der für Sie interessant ist.
* Wenn Sie eine interessante Zeile finden, können Sie dafür einen Drilldown durchführen, indem Sie die jeweiligen Werte dem `where` -Filter hinzufügen.

**Argumente (alle optional)**

* `output=all | values | minimal` 
  
    Das Format der Ergebnisse. Die Spalten „Count“ und „Percent“ werden immer in den Ergebnissen angezeigt. 
  
  * `all` – Alle Spalten der Eingabe werden ausgegeben.
  * `values` – Filtert alle Spalten heraus, die in den Ergebnissen nur „*“ enthalten.
  * `minimal` – Filtert auch Spalten heraus, die für alle Zeilen in der ursprünglichen Abfrage identisch sind. 
* `min_percent=`*double* (Standardwert: 1)
  
    Die prozentuale Mindestabdeckung der generierten Zeilen.
  
    Beispiel: `T | evaluate autocluster("min_percent=5.5")`
* `num_seeds=` *int* (Standardwert: 25) 
  
    Die Anzahl von Startwerten bestimmt die Anzahl von anfänglichen lokalen Suchpunkten des Algorithmus. Je nach der Struktur der Daten erhöht sich beim Erhöhen der Anzahl von Startwerten in einigen Fällen die Anzahl (bzw. Qualität) von Ergebnissen, da ein größerer Suchbereich vorhanden ist. Gleichzeitig verlangsamen sich die Abfragen. Das Argument „num_seeds“ verfügt in beiden Richtungen über abnehmende Ergebnisse. Eine Verringerung unter den Wert 5 führt daher nur zu vernachlässigbaren Leistungssteigerungen, und bei einer Erhöhung auf über 50 werden nur selten weitere Muster generiert.
  
    Beispiel: `T | evaluate autocluster("num_seeds=50")`
* `size_weight=` *0<double<1*+ (Standardwert: 0,5)
  
    Hiermit erhalten Sie Kontrolle über die Balance zwischen der „generischen“ (hohe Abdeckung) und „informativen“ (viele gemeinsame Werte) Vorgehensweise. Wenn Sie „size_weight“ erhöhen, wird die Anzahl von Mustern normalerweise reduziert, und jedes Muster deckt einen größeren Prozentsatz ab. Wenn Sie „size_weight“ verringern, werden normalerweise mehr spezifische Muster mit mehr gemeinsamen Werten und einer geringeren prozentualen Abdeckung produziert. Die Formel im Hintergrund ist ein gewichteter geometrischer Mittelwert zwischen der normalisierten generischen Punktzahl und der informativen Punktzahl mit „size_weight“ und „1-size_weight“ als Gewichtungen. 
  
    Beispiel: `T | evaluate autocluster("size_weight=0.8")`
* `weight_column=` *column_name*
  
    Berücksichtigt jede Zeile der Eingabe gemäß der angegebenen Gewichtung (jede Zeile hat standardmäßig eine Gewichtung von „1“). Die übliche Nutzung einer Gewichtungsspalte besteht darin, die Stichprobenerstellung oder die Bucket-Zuordnung/Aggregation der Daten zu berücksichtigen, die bereits in die einzelnen Zeilen eingebettet sind.
  
    Beispiel: `T | evaluate autocluster("weight_column=sample_Count")` 

<a name="evaluate-autocluster_v2"></a>

#### <a name="evaluate-autoclusterv2"></a>evaluate autocluster_v2

    T | evaluate autocluster_v2()

Mit AutoCluster werden häufige Muster von diskreten Attributen (Dimensionen) in den Daten ermittelt, und die Ergebnisse der ursprünglichen Abfrage (ob mit 100 oder 100.000 Zeilen) werden auf eine kleine Anzahl von Mustern reduziert. AutoCluster wurde als Hilfe beim Analysieren von Fehlern (z.B. Ausnahmen, Abstürze) entwickelt, kann aber für jedes gefilterte Dataset verwendet werden. Der AutoCluster-Algorithmus wurde vom Developer Analytics-Forschungsteam (KustoML@microsoft.com) entwickelt.

Dieses Plug-In ersetzt die veraltete Syntax des autocluster-Plug-Ins.     

**Syntax**
`T | evaluate autocluster_v2( arguments )`

**Rückgabe** AutoCluster gibt eine (in der Regel kleine) Gruppe von Mustern zurück, in der Teile der Daten mit gemeinsamen Werten über mehrere diskrete Attribute hinweg erfasst werden. Jede Zeile in den Ergebnissen steht für ein Muster. Die erste Spalte enthält die Segment-ID. Die nächsten beiden Spalten enthalten die Anzahl und den Prozentsatz der Zeilen aus der ursprünglichen Abfrage, die mit dem Muster erfasst wurden. Die restlichen Spalten stammen aus der ursprünglichen Abfrage. Sie enthalten als Wert entweder einen bestimmten Wert aus der Spalte oder einen Platzhalterwert (standardmäßig NULL) – also variable Werte. Beachten Sie, dass die Muster nicht unzusammenhängend sind: sie können sich überlappen und decken normalerweise nicht alle ursprünglichen Zeilen ab. Einige Zeilen fallen ggf. nicht in eines der Muster.

**Tipps** Verwenden Sie `where` und `project` im Pipe-Eingangselement, um die Daten auf den Teil zu reduzieren, der für Sie interessant ist.
Wenn Sie eine interessante Zeile finden, können Sie dafür einen Drilldown durchführen, indem Sie die jeweiligen Werte dem `where` -Filter hinzufügen.

**Argumente (alle optional)** `T | evaluate autocluster_V2([*SizeWight*,*WeightColumn*,*NumSeeds*,*CustomWildcard*,...])

Alle Argumente sind optional, aber sie müssen wie oben angegeben sortiert werden. Um anzugeben, dass der Standardwert verwendet werden sollte, können Sie eine Tilde („~“) angeben (siehe Beispiele unten).

**Verfügbare Argumente**

- SizeWeight - 0<*double* <1 [Standardwert: 0,5] Hiermit erhalten Sie die Kontrolle über die Balance zwischen der „generischen“ (hohe Abdeckung) und „informativen“ (viele gemeinsame Werte) Vorgehensweise. Wenn Sie den Wert erhöhen, wird die Anzahl von Mustern normalerweise reduziert, und jedes Muster deckt einen größeren Prozentsatz ab. Wenn Sie den Wert verringern, werden normalerweise mehr spezifische Muster mit mehr gemeinsamen Werten und einer geringeren prozentualen Abdeckung produziert. Die Formel im Hintergrund ist ein gewichteter geometrischer Mittelwert zwischen der normalisierten generischen Punktzahl und der informativen Punktzahl mit *SizeWeight* und *1-SizeWeight* als Gewichtungen. 

**Beispiel**
`T | evaluate autocluster_v2(0.8)`

- WeightColumn - *column_name*

Berücksichtigt jede Zeile in der Eingabe gemäß dem angegebenen Gewicht (standardmäßig verfügt jede Spalte über eine Gewichtung von „1“). Das Argument muss ein Name einer numerischen Spalte sein (z.B. int, long, real). Eine übliche Nutzung einer Gewichtungsspalte besteht darin, die Stichprobenerstellung oder die Bucket-Zuordnung/Aggregation der Daten zu berücksichtigen, die bereits in die einzelnen Zeilen eingebettet sind.

**Beispiel**
`T | evaluate autocluster_v2('~', sample_Count)`

`- NumSeeds - *int* [Standardwert: 25]

Die Anzahl von Startwerten bestimmt die Anzahl von anfänglichen lokalen Suchpunkten des Algorithmus. Je nach der Struktur der Daten erhöht sich beim Erhöhen der Anzahl von Startwerten in einigen Fällen die Anzahl (bzw. Qualität) von Ergebnissen, da ein größerer Suchbereich vorhanden ist. Gleichzeitig verlangsamen sich die Abfragen. Der Wert verfügt in beiden Richtungen über abnehmende Ergebnisse. Eine Verringerung unter den Wert 5 führt daher nur zu vernachlässigbaren Leistungssteigerungen, und bei einer Erhöhung auf über 50 werden nur selten weitere Muster generiert.

**Beispiel**
`T | evaluate autocluster_v2('~','~',15)`

- CustomWildcard - *any_value_per_type*

Legt den Platzhalterwert für einen bestimmten Typ in der Ergebnistabelle fest, der angibt, dass das aktuelle Muster keine Einschränkung für diese Spalte besitzt. Der Standard ist „null“, da der Standard eine leere Zeichenfolge ist. Ist der Standard ein gültiger Wert in den Daten, muss ein anderer Platzhalterwert verwendet werden (z.B. *).

**Beispiel**

`T | evaluate autocluster_v2('~','~','~',int (-1), double(-1), long(0), datetime(1900-1-1))`

**Beispiel**
```
StormEvents 
| where monthofyear(StartTime) == 5
| extend Damage = iff(DamageCrops + DamageProperty > 0 , "YES" , "NO")
| project State , EventType , Damage
| evaluate autocluster_v2(0.6)
```
**Ergebnisse**
|SegmentId|Count|Prozent|Zustand|EventType|Damage|
----------|-----|-------|-----|---------|------|
0|2.278|38,7||Hagel|NO
1|512|8,7||Sturm|JA
2|898|15,3|TEXAS|||

**Beispiel mit benutzerdefinierten Platzhaltern**
```
StormEvents 
| where monthofyear(StartTime) == 5
| extend Damage = iff(DamageCrops + DamageProperty > 0 , "YES" , "NO")
| project State , EventType , Damage 
| evaluate autocluster_v2(0.2, '~', '~', '*')
```
**Ergebnisse**
|SegmentId|Count|Prozent|Zustand|EventType|Damage|
----------|-----|-------|-----|---------|------|
0|2.278|38,7|\*|Hagel|NO
1|512|8,7|\*|Sturm|JA
2|898|15,3|TEXAS|\*|\*|

**Zusätzliche Informationen**

-  AutoCluster basiert zum größten Teil auf dem Seed-Expand-Algorithmus des folgenden Dokuments: [Algorithms for Telemetry Data Mining using Discrete Attributes](http://www.scitepress.org/DigitalLibrary/PublicationsDetail.aspx?ID=d5kcrO+cpEU=&t=1) (Algorithmen für Data Mining von Telemetriedaten mit diskreten Attributen). Link zum gesamten Text: [PDF](https://kusto.azurewebsites.net/docs/queryLanguage/images/queries/ICPRAM17telemetry.pdf). 


#### <a name="evaluate-basket-deprecated"></a>evaluate basket (veraltet)

     T | evaluate basket()

**Diese Version von `basket` ist veraltet. Verwenden Sie [basket_v2](#evaluate-basketv2).**

**Rückgabe**

Alle Muster, die in mehr als einem angegebenen Bruchteil (Standardwert: 0,05) der Ereignisse enthalten sind.

**Argumente (alle optional)**

* `threshold=` *0,015<double<1* (Standardwert: 0,05) 
  
    Legt das minimale Verhältnis der Zeilen fest, das als häufig angesehen werden soll (Muster mit einem geringeren Verhältnis werden nicht zurückgegeben).
  
    Beispiel: `T | evaluate basket("threshold=0.02")`
* `weight_column=` *column_name*
  
    Berücksichtigt jede Zeile der Eingabe gemäß der angegebenen Gewichtung (jede Zeile hat standardmäßig eine Gewichtung von „1“). Die übliche Nutzung einer Gewichtungsspalte besteht darin, die Stichprobenerstellung oder die Bucket-Zuordnung/Aggregation der Daten zu berücksichtigen, die bereits in die einzelnen Zeilen eingebettet sind.
  
    Beispiel: T | evaluate basket("weight_column=sample_Count")
* `max_dims=` *1<int* (Standardwert: 5)
  
    Legt die maximale Anzahl von nicht korrelierten Dimensionen pro Basket fest – standardmäßig begrenzt, um die Abfragelaufzeit zu verringern.
* `output=minimize` | `all` 
  
    Das Format der Ergebnisse. Die Spalten „Count“ und „Percent“ werden immer in den Ergebnissen angezeigt.
  
  * `minimize` – Filtert alle Spalten heraus, die in den Ergebnissen nur „*“ enthalten.
  * `all` – Alle Spalten der Eingabe werden ausgegeben.

<a name="evaluate-basket"></a>
#### <a name="evaluate-basketv2"></a>evaluate basket_v2

     T | evaluate basket_v2()

Mit „Basket“ werden alle häufigen Muster diskreter Attribute (Dimensionen) in den Daten ermittelt und alle häufigen Muster zurückgegeben, die den Häufigkeitsschwellenwert in der ursprünglichen Abfrage überschritten haben. Mit Basket ist sichergestellt, dass alle häufigen Muster in den Daten gefunden werden, aber es ist nicht sichergestellt, dass eine polynomische Laufzeit vorhanden ist. Die Laufzeit der Abfrage liegt linear in der Anzahl von Zeilen vor, aber in einigen Fällen auch exponentiell in der Anzahl von Spalten (Dimensionen). Basket basiert auf dem Apriori-Algorithmus, der ursprünglich für das Data Mining per Basket-Analyse entwickelt wurde. 

Ersetzt die veraltete Syntax `evaluate basket`.

**Rückgabe**

Der Basket gibt alle häufigen Muster zurück, die über dem Verhältnisschwellenwert (Standard: 0,05) der Zeilen liegen. Jede Zeile in den Ergebnissen steht für ein Muster.

Die erste Spalte enthält die Segment-ID. Die nächsten beiden Spalten enthalten die Anzahl und den Prozentsatz der Zeilen aus der ursprünglichen Abfrage, die mit dem Muster erfasst wurden. Die restlichen Spalten stammen aus der ursprünglichen Abfrage. Sie enthalten als Wert entweder einen bestimmten Wert aus der Spalte oder einen Platzhalterwert (standardmäßig NULL) – also variable Werte.

**Argumente (alle optional)**

Beispiel: `T | evaluate basket_v2([Threshold, WeightColumn, MaxDimensions, CustomWildcard, CustomWildcard, ...])`

Alle Argumente sind optional, müssen jedoch in der folgenden Reihenfolge festgelegt werden. Verwenden Sie das Tildesymbol „~“ (siehe folgendes Beispiel), um anzugeben, dass ein Standardwert verwendet werden soll.

* Schwellenwert: 0,015 < *double* < 1 (Standard: 0,05) 
  
    Legt das minimale Verhältnis der Zeilen fest, das als häufig angesehen werden soll (Muster mit einem geringeren Verhältnis werden nicht zurückgegeben).
  
    Beispiel: `T | evaluate basket_v2(0.02)`
* Weight column *-column_name*
  
    Berücksichtigt jede Zeile in der Eingabe gemäß dem angegebenen Gewicht (standardmäßig verfügt jede Spalte über eine Gewichtung von „1“). Das Argument muss ein Name einer numerischen Spalte sein (z.B. int, long, real). Eine übliche Nutzung einer Gewichtungsspalte besteht darin, die Stichprobenerstellung oder die Bucket-Zuordnung/Aggregation der Daten zu berücksichtigen, die bereits in die einzelnen Zeilen eingebettet sind.
  
    Beispiel: `T | evaluate basket_v2('~', sample_Count)`
* Max. Dimensionen: 1 < *int* (Standard: 5)
  
    Legt die maximale Anzahl von nicht korrelierten Dimensionen pro Basket fest – standardmäßig begrenzt, um die Abfragelaufzeit zu verringern.

    Beispiel: `T | evaluate basket_v2('~', '~', 3)`
* Benutzerdefinierte Platzhalter-Typen: *any value per type*
  
    Legt den Platzhalterwert für einen bestimmten Typ in der Ergebnistabelle fest, der angibt, dass das aktuelle Muster keine Einschränkung für diese Spalte besitzt. Der Standard ist „null“, da der Standard eine leere Zeichenfolge ist. Ist der Standard ein gültiger Wert in den Daten, muss ein anderer Platzhalterwert verwendet werden (z.B. *).

    Beispiel: `T | evaluate basket_v2('~', '~', '~', '*', int(-1), double(-1), long(0), datetime(1900-1-1))`

**Beispiele**

``` 
StormEvents 
| where monthofyear(StartTime) == 5
| extend Damage = iff(DamageCrops + DamageProperty > 0 , "YES" , "NO")
| project State, EventType, Damage, DamageCrops
| evaluate basket_v2(0.2)
```
Ergebnisse

|SegmentId|Count|Prozent|Zustand|EventType|Damage|DamageCrops
----------|-----|-------|-----|---------|------|-----------
0|4.574|77,7|||NO|0
1|2.278|38,7||Hagel|NO|0
2|5.675|96,4||||0
3|2.371|40,3||Hagel||0
4|1.279|21,7||Sturm||0
5|2.468|41,9||Hagel|||
6|1.310|22,3|||JA||
7|1.291|21,9||Sturm||

Beispiel mit benutzerdefinierten Platzhaltern
```
StormEvents 
| where monthofyear(StartTime) == 5
| extend Damage = iff(DamageCrops + DamageProperty > 0 , "YES" , "NO")
| project State, EventType, Damage, DamageCrops
| evaluate basket_v2(0.2, '~', '~', '*', int(-1))
```
Ergebnisse

|SegmentId|Count|Prozent|Zustand|EventType|Damage|DamageCrops
----------|-----|-------|-----|---------|------|-----------
0|4.574|77,7|\*|\*|NO|0
1|2.278|38,7|\*|Hagel|NO|0
2|5.675|96,4|\*|\*|\*|0
3|2.371|40,3|\*|Hagel|\*|0
4|1.279|21,7|\*|Sturm|\*|0
5|2.468|41,9|\*|Hagel|\*|-1|
6|1.310|22,3|\*|\*|JA|-1|
7|1.291|21,9|\*|Sturm|\*|-1|

#### <a name="evaluate-diffpatterns-deprecated"></a>evaluate diffpatterns (veraltet)
**Diese Version des diffpatterns-Plug-Ins ist veraltet. Verwenden Sie die neue Syntax für das [diffpatterns](#evaluate-diffpatterns_v2)-Plug-In**.
requests | evaluate diffpatterns("split=success")

Diffpatterns identifiziert die Unterschiede zwischen zwei Datasets mit der gleichen Struktur – z.B. das Anforderungsprotokoll zum Zeitpunkt eines Vorfalls sowie normale Anforderungsprotokolle. Diffpatterns wurde als Hilfe bei der Analyse von Fehlern entwickelt (z.B. per Vergleich von Fehlern mit Nicht-Fehlern in einem bestimmten Zeitraum). Es ist damit ggf. aber auch möglich, Unterschiede zwischen zwei beliebigen Datasets mit derselben Struktur zu ermitteln. 

**Syntax**

`T | evaluate diffpatterns("split=` *BinaryColumn* `" [, arguments] )`

**Rückgabe**

Diffpatterns gibt eine (normalerweise kleine) Gruppe von Mustern zurück, in denen unterschiedliche Teile der Daten in den beiden Datasets erfasst werden (also ein Muster, bei dem ein größerer Prozentsatz der Zeilen im ersten Dataset und ein geringerer Prozentsatz der Zeilen im zweiten Dataset erfasst wird). Jede Zeile in den Ergebnissen steht für ein Muster.

Die ersten vier Spalten enthalten die Anzahl und den Prozentsatz von Spalten der ursprünglichen Abfrage, die vom Muster in jedem Dataset erfasst werden. Die fünfte Spalte enthält die Differenz (in absoluten Prozentpunkten) zwischen den beiden Datasets. Die restlichen Spalten stammen aus der ursprünglichen Abfrage. Sie enthalten als Wert entweder einen bestimmten Wert aus der Spalte oder „*“ (variable Werte). 

Beachten Sie, dass die Muster nicht unzusammenhängend sind: sie können sich überlappen und decken normalerweise nicht alle ursprünglichen Zeilen ab. Einige Zeilen fallen ggf. nicht in eines der Muster.

**Tipps**

* Verwenden Sie „where“ und „project“ im Pipe-Eingangselement, um die Daten auf den Teil zu reduzieren, der für Sie interessant ist.
* Wenn Sie eine interessante Zeile finden, können Sie dafür einen Drilldown durchführen, indem Sie die jeweiligen Werte dem where-Filter hinzufügen.

**Argumente**

* `split=` *column name* (erforderlich)
  
    Die Spalte muss genau zwei Werte haben. Erstellen Sie diese Spalte bei Bedarf:
  
    `requests | extend fault = toint(resultCode) >= 500` <br/>
    `| evaluate diffpatterns("split=fault")`
* `target=` *string*
  
    Weist den Algorithmus an, nur nach Mustern zu suchen, die im Zieldataset über einen höheren Prozentsatz verfügen. Das Ziel muss einer der beiden Werte der split-Spalte sein.
  
    `requests | evaluate diffpatterns("split=success", "target=false")`
* `threshold=` *0,015<double<1* (Standardwert: 0,05) 
  
    Legt die minimale Musterdifferenz (Verhältnis) zwischen den beiden Datasets fest.
  
    `requests | evaluate diffpatterns("split=success", "threshold=0.04")`
* `output=minimize | all`
  
    Das Format der Ergebnisse. Die Spalten „Count“ und „Percent“ werden immer in den Ergebnissen angezeigt. 
  
  * `minimize` – Filtert alle Spalten heraus, die in den Ergebnissen nur „*“ enthalten.
  * `all` – Alle Spalten der Eingabe werden ausgegeben.
* `weight_column=` *column_name*
  
    Berücksichtigt jede Zeile in der Eingabe gemäß dem angegebenen Gewicht (standardmäßig verfügt jede Spalte über eine Gewichtung von „1“). Eine übliche Nutzung einer Gewichtungsspalte besteht darin, die Stichprobenerstellung oder die Bucket-Zuordnung/Aggregation der Daten zu berücksichtigen, die bereits in die einzelnen Zeilen eingebettet sind.
  
    `requests | evaluate autocluster("weight_column=itemCount")`

<a name="evaluate-diffpatterns_v2"></a>
#### <a name="evaluate-diffpatternsv2"></a>evaluate diffpatterns_v2
'T | evaluate diffpatterns_v2(splitColumn)'

Mit Diffpatterns werden zwei Datasets mit der gleichen Struktur verglichen und Muster mit diskreten Attributen (Dimensionen) ermittelt, die die Unterschiede zwischen den beiden Datasets ausmachen. Diffpatterns wurde als Hilfe bei der Analyse von Fehlern entwickelt (z.B. per Vergleich von Fehlern mit Nicht-Fehlern in einem bestimmten Zeitraum). Es ist damit ggf. aber auch möglich, Unterschiede zwischen zwei beliebigen Datasets mit derselben Struktur zu ermitteln. Der Diffpatterns-Algorithmus wurde vom Developer Analytics-Forschungsteam (KustoML@microsoft.com) entwickelt.

Dieses Plug-In ersetzt die Syntax des veralteten diffpatterns-Plug-Ins.

**Syntax**

`T | evaluate diffpatterns_v2(SplitColumn, SplitValueA, SplitValueB [, arguments] )`

**Rückgabe**

Diffpatterns gibt eine (normalerweise kleine) Gruppe von Mustern zurück, in denen unterschiedliche Teile der Daten in den beiden Datasets erfasst werden (also ein Muster, bei dem ein größerer Prozentsatz der Zeilen im ersten Dataset und ein geringerer Prozentsatz der Zeilen im zweiten Dataset erfasst wird). Jede Zeile in den Ergebnissen steht für ein Muster.
Die erste Spalte enthält die Segment-ID. Die folgenden vier Spalten enthalten die Anzahl und den Prozentsatz von Spalten der ursprünglichen Abfrage, die vom Muster in jedem Dataset erfasst werden. Die sechste Spalte enthält die Differenz (in absoluten Prozentpunkten) zwischen den beiden Datasets. Die übrigen Spalten stammen aus der ursprünglichen Abfrage.
In jedem Muster enthalten Spalten, die nicht im Muster (d.h. ohne Einschränkung auf einen bestimmten Wert) festgelegt sind, einen Platzhalterwert, der standardmäßig NULL ist (im Abschnitt „Argumente“ erfahren Sie, wie Platzhalter manuell geändert werden können).
Beachten Sie, dass die Muster nicht unzusammenhängend sind: sie können sich überlappen und decken normalerweise nicht alle ursprünglichen Zeilen ab. Einige Zeilen fallen ggf. nicht in eines der Muster.

**Tipps**

Verwenden Sie „where“ und „project“ im Pipe-Eingangselement, um die Daten auf den Teil zu reduzieren, der für Sie interessant ist.
Wenn Sie eine interessante Zeile finden, können Sie dafür einen Drilldown durchführen, indem Sie die jeweiligen Werte dem `where` -Filter hinzufügen.

**Erforderliche Argumente**

`T | evaluate diffpatterns_v2(SplitColumn, SplitValueA, SplitValueB [, WeightColumn, Threshold, MaxDimensions, CustomWildcard, ...])` 

- SplitColumn - *column_name* 

Weist den Algorithmus an, wie die Abfrage in Datasets geteilt wird. Gemäß den angegebenen Werten für die Argumente SplitValueA und SplitValueB (siehe unten) teilt der Algorithmus die Abfrage in zwei Datasets („A“ und „B“) und analysiert ihre Unterschiede. Die split-Spalte muss mindestens zwei eindeutige Werte enthalten.

- SplitValueA - *string*

Eine Zeichenfolgendarstellung für einen der Werte in SplitColumn, der angegeben wurde. Alle Zeilen, die diesen Wert in SplitColumn enthalten, werden als Dataset „A“ angesehen.

- SplitValueB - *string*

Eine Zeichenfolgendarstellung für einen der Werte in SplitColumn, der angegeben wurde. Alle Zeilen, die diesen Wert in SplitColumn enthalten, werden als Dataset „B“ angesehen.

**Beispiel**

```
T | extend splitColumn=iff(request_responseCode == 200, "Success" , "Failure") | evaluate diffpatterns_v2(splitColumn, "Success","Failure")
```
**Optionale Argumente**

Alle anderen Argumente sind optional, aber sie müssen wie unten angegeben sortiert werden. Um anzugeben, dass der Standardwert verwendet werden sollte, können Sie eine Tilde („~“) angeben (siehe Beispiele unten).

- WeightColumn - *column_name*

Berücksichtigt jede Zeile in der Eingabe gemäß dem angegebenen Gewicht (standardmäßig verfügt jede Spalte über eine Gewichtung von „1“). Das Argument muss ein Name einer numerischen Spalte sein (z.B. int, long, real). Eine übliche Nutzung einer Gewichtungsspalte besteht darin, die Stichprobenerstellung oder die Bucket-Zuordnung/Aggregation der Daten zu berücksichtigen, die bereits in die einzelnen Zeilen eingebettet sind.

**Beispiel**
```
T | extend splitColumn=iff(request_responseCode == 200, "Success" , "Failure") | evaluate diffpatterns_v2(splitColumn, "Success","Failure", sample_Count)
```
- Threshold - 0.015 < double < 1 [Standardwert: 0,05]

Legt die minimale Musterdifferenz (Verhältnis) zwischen den beiden Datasets fest.

**Beispiel**
```
T | extend splitColumn = iff(request_responseCode == 200, "Success" , "Failure") | evaluate diffpatterns_v2(splitColumn, "Success","Failure", "~", 0.04)
```
- MaxDimensions - 0 < int [Standardwert: unbegrenzt]

Legt die maximale Anzahl von nicht korrelierten Dimensionen pro Ergebnismuster fest, und es wird ein Grenzwert angegeben, um die Laufzeit von Abfragen zu verringern.

**Beispiel**
```
T | extend splitColumn = iff(request_responseCode == 200, "Success" , "Failure") | evaluate diffpatterns_v2(splitColumn, "Success","Failure", "~", "~", 3)
```
- CustomWildcard - *any_value_per_type*

Legt den Platzhalterwert für einen bestimmten Typ in der Ergebnistabelle fest, der angibt, dass das aktuelle Muster keine Einschränkung für diese Spalte besitzt. Der Standard ist „null“, da der Standard eine leere Zeichenfolge ist. Ist der Standard ein gültiger Wert in den Daten, muss ein anderer Platzhalterwert verwendet werden (z.B. *). Unten finden Sie ein Beispiel hierzu.

**Beispiel**
```
T | extend splitColumn = iff(request_responseCode == 200, "Success" , "Failure") | evaluate diffpatterns_v2(splitColumn, "Success","Failure", "~", "~", "~", int(-1), double(-1), long(0), datetime(1900-1-1))
```

**Beispiel**
```
StormEvents 
| where monthofyear(StartTime) == 5
| extend Damage = iff(DamageCrops + DamageProperty > 0 , 1 , 0)
| project State , EventType , Source , Damage, DamageCrops
| evaluate diffpatterns_v2(Damage, "0", "1" )
```
**Ergebnisse**

|SegmentId|CountA|CountB|PercentA|PercentB|DiffAB|Zustand|EventType|Quelle|DamageCrops
----------|------|------|--------|--------|------|-----|---------|------|-----------
0|2.278|93|49,8|7,1|42,7||Hagel||0
1|779|512|17,03|39,08|22,05||Sturm|||
2|1.098|118|24,01|9,01|15|||Ausgebildeter „Spotter“|0|
3|136|158|2,97|12,06|9,09|||Zeitung||
4|359|214|7,85|16,34|8,49||Überschwemmung|||
5|50|122|1,09|9,31|8,22|IOWA||||
6|655|279|14,32|21,3|6,98|||Strafverfolgungsbehörden||
7|150|117|3,28|8,93|5,65||Hochwasser|||
8|362|176|7,91|13,44|5,52|||Katastrophenschutz||

#### <a name="evaluate-extractcolumns"></a>evaluate extractcolumns
     exceptions | take 1000 | evaluate extractcolumns("details=json") 

Extractcolumns wird verwendet, um eine Tabelle mit mehreren einfachen Spalten zu füllen, die basierend auf dem Typ dynamisch aus strukturierten (bzw. halbstrukturierten) Spalten extrahiert werden. Derzeit werden nur JSON-Spalten unterstützt (sowohl dynamische als auch Zeichenfolgenserialisierung).

* `max_columns=` *int* (Standardwert: 10) 
  
    Die Anzahl von neu hinzugefügten Spalten ist dynamisch und kann sehr hoch sein (Anzahl von einzelnen Schlüsseln in allen JSON-Datensätzen), sodass wir sie beschränken müssen. Die neuen Spalten werden in absteigender Reihenfolge basierend auf ihrer Häufigkeit sortiert, und bis zu „max_columns“ (Zahlenwert) werden der Tabelle hinzugefügt.
  
    `T | evaluate extractcolumns("json_column_name=json", "max_columns=30")`
* `min_percent=` *double* (Standardwert: 10,0) 
  
    Eine weitere Möglichkeit zum Beschränken neuer Spalten, indem Spalten ignoriert werden, deren Häufigkeit unter „min_percent“ liegt.
  
    `T | evaluate extractcolumns("json_column_name=json", "min_percent=60")`
* `add_prefix=` *bool* (Standardwert: true) 
  
    Bei „true“ wird der Name der komplexen Spalte den extrahierten Spaltennamen als Präfix hinzugefügt.
* `prefix_delimiter=` *string* (Standardwert: „_“) 
  
    Wenn „add_prefix=true“ gilt, definiert dieser Parameter das Trennzeichen, das verwendet wird, um die Namen der neuen Spalten zu verketten.
  
    `T | evaluate extractcolumns("json_column_name=json",` <br/>
    `"add_prefix=true", "prefix_delimiter=@")`
* `keep_original=` *bool* (Standardwert: false) 
  
    Bei „true“ werden die ursprünglichen Spalten (JSON) in der Ausgabetabelle beibehalten.
* `output=query | table` 
  
    Das Format der Ergebnisse. 
  
  * `table` – Die Ausgabe entspricht der empfangenen Tabelle abzüglich der angegebenen Eingabespalten und zuzüglich der neuen Spalten, die aus den Eingabespalten extrahiert wurden.
  * `query` – Die Ausgabe ist eine Zeichenfolge, die für die Abfrage steht, die Sie zum Abrufen des Ergebnisses als Tabelle durchführen. 

### <a name="extend-operator"></a>extend-Operator
     T | extend duration = stopTime - startTime

Fügen Sie eine oder mehrere berechnete Spalten an eine Tabelle an. 

**Syntax**

    T | extend ColumnName = Expression [, ...]

**Argumente**

* *T:* Die Eingabetabelle.
* *ColumnName:* Der Name einer hinzuzufügenden Spalte. Bei [Namen](#names) muss die Groß-/Kleinschreibung beachtet werden. Sie können alphabetische oder numerische Zeichen oder Unterstriche („_“) enthalten. Verwenden Sie `['...']` oder `["..."]` zum Angeben von Schlüsselwörtern oder Namen mit anderen Zeichen.
* *Expression:* Eine Berechnung über die vorhandenen Spalten hinweg.

**Rückgabe**

Eine Kopie der Eingabetabelle mit den angegebenen zusätzlichen Spalten.

**Tipps**

* Verwenden Sie stattdessen [`project`](#project-operator) , wenn Sie auch einige Spalten löschen oder umbenennen möchten.
* Verwenden Sie nicht einfach `extend` , um einen kürzeren Namen zur Verwendung in einem langen Ausdruck zu erhalten. `...| extend x = anonymous_user_id_from_client | ... func(x) ...` 
  
    Die systemeigenen Spalten der Tabelle wurden indiziert; der neue Name definiert eine zusätzliche, nicht indizierte Spalte, d. h. die Abfrage wird wahrscheinlich langsamer ausgeführt.

**Beispiel**

```AIQL
traces
| extend
    Age = now() - timestamp
```

### <a name="find-operator"></a>find-Operator

    find in (Table1, Table2, Table3) where id=="a string"
    find in (Table1, Table2, Table3) where id=="a string" project column1, column2
    find in (Table1, Table2, Table3) where * has "a string"
    find in (Table1, Table2, Table3) where appName in ("string 1", "string 2", "string 3")

Sucht nach Zeilen, die einem Prädikat in einer Gruppe von Tabellen entsprechen.

**Syntax**

    find in (Table1, ...) 
    where Predicate 
    [project Column1, ...]

**Argumente**

* *Table1* Tabellenname oder Abfrage. Kann eine let-definierte Tabelle, aber keine Funktion sein. Ein Tabellenname bietet eine bessere Leistung als eine Abfrage.
* *Predicate* Ein boolescher Ausdruck, der für jede Zeile in den angegebenen Tabellen ausgewertet wird.
 * In Zeichenfolgenvergleichen können Sie „*“ anstelle eines Spaltennamens verwenden.
* *Column1* Mit der `project`-Option können Sie angeben, welche Spalten in der Ausgabe immer angezeigt werden müssen. 

**Ergebnis**

Standardmäßig enthält die Ausgabetabelle:

* `source_`: Ein Indikator für die Quelltabelle für jede Zeile Verwenden Sie [as](#as-operator) am Ende jedes Tabellenausdrucks, wenn Sie den Namen angeben möchten, der in dieser Spalte angezeigt wird.
* Im Prädikat explizit erwähnte Spalten
* Nicht leere Spalten, die alle Eingabetabellen gemeinsam haben
* `pack_`: Eine Eigenschaftensammlung mit den Daten aus den anderen Spalten.

Beachten Sie, dass sich dieses Format bei Änderungen in den Eingabedaten oder eines Prädikats ändern kann. Zum angeben eines festen Satzes von Spalten verwenden Sie `project`.

**Beispiel**

Abrufen aller Anforderungen und Ausnahmen, mit Ausnahme derjenigen von Verfügbarkeitstests und Robotern:

```AIQL

    find in (requests, exceptions) where isempty(operation_SyntheticSource)
```

Suchen aller Anforderungen und Ausnahmen aus dem Vereinigten Königreich, mit Ausnahme derjenigen von Verfügbarkeitstests und Robotern:

```AIQL

    let requk = requests
    | where client_CountryOrRegion == "United Kingdom";
    let exuk = exceptions
    | where client_CountryOrRegion == "United Kingdom";
    find in (requk, exuk) where isempty(operation_SyntheticSource)
```

Suchen der aktuellen Telemetriedaten, wobei ein beliebiges Feld den Begriff „test“ enthält:

```AIQL

    find in (traces, requests, pageViews, dependencies, customEvents, availabilityResults, exceptions) 
    where * has 'test' 
    | top 100 by timestamp desc
```

**Leistungstipps**

* Fügen Sie dem `where`-Prädikat zeitbasierte Begriffe hinzu.
* Verwenden Sie `let`-Klauseln anstatt Abfragen inline zu schreiben.

### <a name="getschema-operator"></a>getschema-Operator

   T | getschema
   
Ergibt eine Tabelle mit den Spaltennamen und -typen der Eingabetabelle.

```AIQL
requests
| project appId, appName, customDimensions, duration, iKey, itemCount, success, timestamp 
| getschema 
```

![Ergebnisse von „getschema“](./media/app-insights-analytics-reference/getschema.png)

### <a name="join-operator"></a>join-Operator
    Table1 | join (Table2) on CommonColumn

Führt die Zeilen zweier Tabellen anhand von übereinstimmenden Werten der angegebenen Spalte zusammen.

**Syntax**

    Table1 | join [kind=Kind] (Table2) on CommonColumn [, ...]

**Argumente**

* *Table1:* Die „linke Seite“ der Verknüpfung.
* *Table2:* Die „rechte Seite“ der Verknüpfung. Kann ein geschachtelter Abfrageausdruck sein, der eine Tabelle ausgibt.
* *CommonColumn:* Eine Spalte mit dem gleichen Namen in beiden Tabellen.
* *Kind:* Gibt an, wie Zeilen aus den beiden Tabellen abgeglichen werden.

**Rückgabe**

Eine Tabelle mit:

* Einer Spalte für jede Spalte in jeder der beiden Tabellen, einschließlich der übereinstimmenden Schlüssel. Die Spalten der rechten Seite werden bei Namenskonflikten automatisch umbenannt.
* Einer Zeile für jede Übereinstimmung zwischen den Eingabetabellen. Eine Übereinstimmung ist eine ausgewählte Zeile in einer Tabelle, die in allen `on` -Feldern denselben Wert wie eine Zeile in der anderen Tabelle aufweist. 
* `Kind` ohne Angabe oder `= innerunique`
  
    Nur eine Zeile der linken Seite wird für jeden Wert des `on` -Schlüssels abgeglichen. Die Ausgabe enthält eine Zeile für jede Übereinstimmung dieser Zeile mit Zeilen der rechten Seite.
* `kind=inner`
  
     Der Ausgabe enthält eine Zeile für jede Kombination von übereinstimmenden Zeilen der linken und rechten Seite.
* `kind=leftouter` (oder `kind=rightouter` oder `kind=fullouter`)
  
     Zusätzlich zu den internen Übereinstimmungen ist eine Zeile für jede Zeile auf der linken (und/oder rechten) Seite vorhanden, selbst wenn es keine Übereinstimmung damit gibt. In diesem Fall enthalten die Ausgabezellen ohne Übereinstimmung NULL-Werte.
* `kind=leftanti`
  
     Gibt alle Datensätze von der linken Seite zurück, für die keine Übereinstimmungen auf der rechten Seite vorhanden sind. Die Ergebnistabelle enthält nur die Spalten von der linken Seite. 
* `kind=leftsemi` (oder `leftantisemi`)

    Gibt eine Zeile aus der linken Tabelle zurück, wenn in der rechten Tabelle eine Übereinstimmung dafür vorhanden ist (oder nicht). Das Ergebnis enthält keine Daten aus der rechten Tabelle.


**Tipps**

Für die Ergebnistabelle gilt ein Grenzwert von 64 MB.

Für eine optimale Leistung:

* Verwenden Sie `where` und `project`, um die Anzahl von Zeilen und Spalten in den Eingabetabellen vor der Verknüpfung (`join`) zu reduzieren. 
* Wenn eine Tabelle immer kleiner als die andere ist, verwenden Sie diese als die linke (weitergeleitete) Seite der Verknüpfung.
* Die Spalten für die Verknüpfungsübereinstimmung müssen den gleichen Namen haben. Verwenden Sie ggf. den project-Operator, um eine Spalte in einer der Tabellen umzubenennen.



**Beispiel**

Abrufen erweiterter Aktivitäten aus einem Protokoll, in dem einige Einträge den Start und das Ende einer Aktivität markieren 

```AIQL
    let Events = MyLogTable | where type=="Event" ;
    Events
    | where Name == "Start"
    | project Name, City, ActivityId, StartTime=timestamp
    | join (Events
           | where Name == "Stop"
           | project StopTime=timestamp, ActivityId)
        on ActivityId
    | project City, ActivityId, StartTime, StopTime, Duration=StopTime-StartTime

```


### <a name="limit-operator"></a>limit-Operator
     T | limit 5

Gibt höchstens die angegebene Anzahl von Zeilen aus der Eingabetabelle zurück. Es gibt keine Garantie dafür, welche Datensätze zurückgegeben werden. (Verwenden Sie [`top`](#top-operator), um bestimmte Datensätze zurückzugeben.)

**Alias::** `take`

**Syntax**

    T | limit NumberOfRows


**Tipps**

`Take` ist eine einfache und effiziente Möglichkeit, ein Beispiel für die Ergebnisse anzuzeigen, wenn Sie interaktiv arbeiten. Denken Sie daran, dass es keine Garantie dafür gibt, dass bestimmte Zeilen erzeugt bzw. in einer bestimmten Reihenfolge erzeugt werden.

Für die Anzahl von Zeilen, die an den Client zurückgegeben werden, besteht auch dann eine implizite Begrenzung, wenn Sie `take`nicht verwenden. Um diese Begrenzung aufzuheben, verwenden Sie die Clientanforderungsoption `notruncation` .

### <a name="make-series-operator"></a>make-series-Operator

Führt eine Aggregation aus. Im Gegensatz zu [summarize](#summarize-operator) entsteht hierbei jeweils eine Ausgabezeile pro Gruppe. In den Ergebnisspalten werden die Werte in den einzelnen Gruppen zu Arrays zusammengefasst. 

**Syntax**

    T | 
    make-series [Column =] Aggregation default = DefaultValue [, ...] 
    on AxisColumn in range(start, stop, step) 
    by [Column =] GroupExpression [, ...]


**Argumente**

* *Column:* Optionaler Name für eine Ergebnisspalte. Nimmt standardmäßig den vom Ausdruck abgeleiteten Namen an.
* *DefaultValue:* Ist keine Zeile mit bestimmten AxisColumn- und GroupExpression-Werten vorhanden, wird das entsprechende Element in den Ergebnissen mit einem Standardwert zugewiesen. 
* *Aggregation:* Ein numerischer Ausdruck mit einer [Aggregationsfunktion](#aggregations). 
* *AxisColumn:* Eine Spalte, nach der die Reihe sortiert wird. Sie kann als Zeitachse verwendet werden, es werden jedoch beliebige numerische Typen akzeptiert.
*start, stop, step:* Definiert die Liste mit den AxisColumn-Werten für jede Zeile. Jede andere Ergebnisaggregationsspalte besitzt ein Array gleicher Länge. 
* *GroupExpression:* Ein spaltenübergreifender Ausdruck, mit dem ein Satz von unterschiedlichen Werten bereitgestellt wird. Die Ausgabe enthält jeweils eine Zeile pro GroupExpression-Wert. Hierbei handelt es sich in der Regel um einen Spaltennamen, der bereits einen eingeschränkten Satz von Werten bereitstellt. 

**Tipp**

Die Ergebnisarrays werden genau wie beim entsprechenden summarize-Vorgang in einem Analytics-Diagramm gerendert.

**Beispiel**

```AIQL
requests
| make-series sum(itemCount) default=0, avg(duration) default=0
  on timestamp in range (ago(7d), now(), 1d)
  by client_City
```

![Ergebnisse von „make-series“](./media/app-insights-analytics-reference/make-series.png)

### <a name="mvexpand-operator"></a>mvexpand-Operator
    T | mvexpand listColumn 

Erweitert eine Liste aus einer Zelle mit dynamischer Typisierung (JSON) erweitert, sodass jeder Eintrag eine separate Zeile enthält. Alle anderen Zellen in einer erweiterten Zeile sind dupliziert. 

(Siehe auch [`summarize makelist`](#summarize-operator) , wobei die gegenteilige Funktion durchgeführt wird.)

**Beispiel**

Angenommen, die Eingabetabelle ist:

| A:int | B:string | D:dynamic |
| --- | --- | --- |
| 1 |"hello" |{"key":"value"} |
| 2 |"world" |[0,1,"k","v"] |

    mvexpand D

Das Ergebnis lautet:

| A:int | B:string | D:dynamic |
| --- | --- | --- |
| 1 |"hello" |{"key":"value"} |
| 2 |"world" |0 |
| 2 |"world" |1 |
| 2 |"world" |"k" |
| 2 |"world" |"v" |

**Syntax**

    T | mvexpand  [bagexpansion=(bag | array)] ColumnName [limit Rowlimit]

    T | mvexpand  [bagexpansion=(bag | array)] [Name =] ArrayExpression [to typeof(Typename)] [limit Rowlimit]

**Argumente**

* *ColumnName:* Im Ergebnis werden Arrays in der benannten Spalte auf mehrere Zeilen erweitert. 
* *ArrayExpression:* Ein Ausdruck, der ein Array zurückgibt. Bei Verwendung dieses Formulars wird eine neue Spalte hinzugefügt, und die vorhandene wird beibehalten.
* *Name:* Ein Name für die neue Spalte.
* *Typename:* Wandelt den erweiterten Ausdruck in einen bestimmten Typ um.
* *RowLimit:* Die maximale Anzahl von Zeilen, die aus jeder ursprünglichen Zeile generiert werden. Der Standardwert ist 128.

**Rückgabe**

Mehrere Zeilen für alle Werte in jedem Array in der benannten Spalte oder im Arrayausdruck.

Die erweiterte Spalte ist immer dynamisch typisiert. Verwenden Sie eine Umwandlung wie `todatetime()` oder `toint()`, wenn Sie Werte berechnen oder aggregieren möchten.

Zwei Erweiterungsmodi für Eigenschaftenbehälter werden unterstützt:

* `bagexpansion=bag`: Eigenschaftenbehälter werden zu Eigenschaftenbehältern mit einem einzelnen Eintrag erweitert. Dies ist die Standarderweiterung.
* `bagexpansion=array`: Eigenschaftenbehälter werden zu Arraystrukturen mit den beiden Elementen `[`*Schlüssel*`,`*Wert*`]` erweitert und lassen den einheitlichen Zugriff auf Schlüssel und Werte zu (sowie z. B. auch das Ausführen einer distinct-count-Aggregation über Eigenschaftsnamen).

**Beispiele**

    exceptions | take 1
    | mvexpand details[0]

Teilt einen Ausnahmedatensatz für jedes Element im Feld „Details“ in Zeilen auf.

### <a name="parse-operator"></a>parse-Operator
    T | parse "I got 2 socks for my birthday when I was 63 years old"
    with * "got" counter:long " " present "for" * "was" year:long *


    T | parse kind=relaxed
          "I got no socks for my birthday when I was 63 years old"
    with * "got" counter:long " " present "for" * "was" year:long *

    T |  parse kind=regex "I got socks for my 63rd birthday"
    with "(I|She) got " present " for .*?" year:long *

Extrahiert Werte aus einer Zeichenfolge. Kann einfache oder reguläre Ausdrücke für Übereinstimmungen verwenden.

**Syntax**

    T | parse [kind=regex|relaxed] SourceText
        with [Match | Column [: Type [*]] ]  ...

**Argumente**

* `T`: Die Eingabetabelle.
* `kind`: 
  * `simple` (Standard): Die `Match`-Zeichenfolgen sind unverschlüsselte Zeichenfolgen.
  * `relaxed`: Wenn der Text nicht als der Typ einer Spalte analysiert wird, wird die Spalte auf NULL festgelegt und die Analyse fortgesetzt. 
  * `regex`: Die `Match`-Zeichenfolgen sind reguläre Ausdrücke.
* `Text`: Eine Spalte oder ein anderer Ausdruck, die/der als Zeichenfolge ausgewertet wird oder in eine Zeichenfolge konvertiert werden kann.
* *Übereinstimmung:* Gleichen Sie den nächsten Teil der Zeichenfolge auf Übereinstimmungen ab, und verwerfen Sie sie.
* *Spalte:* Weisen Sie den nächsten Teil der Zeichenfolge dieser Spalte zu. Die Spalte wird erstellt, wenn sie nicht vorhanden ist.
* *Typ:* Analysieren Sie den nächsten Teil der Zeichenfolge als den angegebenen Typ. Beispiele: int, date, double. 

**Rückgabe**

Die Eingabetabelle, erweitert gemäß der Liste der Spalten.

Die Elemente in der `with` -Klausel werden wiederum mit dem Quelltext abgeglichen. Jedes Element entnimmt ein Segment des Quelltexts: 

* Eine Literalzeichenfolge oder ein regulärer Ausdruck verschiebt den entsprechenden Cursor um die Länge der Übereinstimmung.
* Bei der Analyse eines regulären Ausdrucks kann ein regulärer Ausdruck den Minimierungsoperator „?“ verwenden, um so schnell wie möglich zur folgenden Übereinstimmung zu wechseln.
* Ein Spaltenname mit einem Typ analysiert den Text als den angegebenen Typ. Außer bei „kind=relaxed“ macht eine nicht erfolgreiche Analyse Übereinstimmungen mit dem gesamten Muster ungültig.
* Ein Spaltenname ohne einen Typ oder mit dem Typ „string“ kopiert die Mindestanzahl von Zeichen, um die folgende Übereinstimmung abzurufen.
* „*“ überspringt die Mindestanzahl von Zeichen, um die folgende Übereinstimmung zu erhalten. Sie können „*“ am Anfang und Ende des Musters oder hinter einem Typ, der keine Zeichenfolge ist, oder zwischen Zeichenfolgenübereinstimmungen verwenden.

Alle Elemente in einem Analysemuster müssen genau übereinstimmen. Andernfalls werden keine Ergebnisse erzeugt. Die Ausnahme dieser Regel lautet, dass wenn bei „kind=relaxed“ die Analyse einer typisierten Variablen misslingt, die restliche Analyse fortgesetzt wird.

**Beispiele**

*Einfach:*

```AIQL

// Test without reading a table:
 range x from 1 to 1 step 1 
 | parse "I got 2 socks for my birthday when I was 63 years old" 
    with 
     *   // skip until next match
     "got" 
     counter: long // read a number
     " " // separate fields
     present // copy string up to next match
     "for" 
     *  // skip until next match
     "was" 
     year:long // parse number
     *  // skip rest of string
```

| x | Zähler | Geschenk | Jahr |
| --- | --- | --- | --- |
| 1 |2 |socks (Socken) |63 |

*Relaxed:*

Wenn die Eingabe eine ordnungsgemäße Übereinstimmung für jede typisierte Spalte enthält, erzeugt eine Analyse des Typs „Relaxed“ (Ungenau) dieselben Ergebnisse wie eine einfache Analyse. Aber wenn eine der typisierten Spalten nicht ordnungsgemäß analysiert wird, setzt eine ungenaue Analyse das Verarbeiten des Rests des Musters fort, während eine einfache Analyse beendet wird, ohne Ergebnisse zu liefern.

```AIQL

// Test without reading a table:
 range x from 1 to 1 step 1 
 | parse kind="relaxed"
        "I got several socks for my birthday when I was 63 years old" 
    with 
     *   // skip until next match
     "got" 
     counter: long // read a number
     " " // separate fields
     present // copy string up to next match
     "for" 
     *  // skip until next match
     "was" 
     year:long // parse number
     *  // skip rest of string
```


| x | Geschenk | Jahr |
| --- | --- | --- |
| 1 |socks (Socken) |63 |

*Regulärer Ausdruck:*

```AIQL

// Run a test without reading a table:
range x from 1 to 1 step 1 
// Test string:
| extend s = "Event: NotifySliceRelease (resourceName=Scheduler, totalSlices=27, sliceNumber=16, lockTime=02/17/2016 07:31, releaseTime=02/17/2016 08:41:00, previousLockTime=02/17/2016 06:20:00 ) }" 
// Parse it:
| parse kind=regex s 
  with ".*?=" resource 
       ", total.*?sliceNumber=" slice:long *
       "lockTime=" lock
       ",.*?releaseTime=" release 
       ",.*?previousLockTime=" previous:date 
       @".*\)" *
| project-away x, s
```

| Ressource | Slice | Sperre | Freigabe | Vorherige |
| --- | --- | --- | --- | --- |
| Scheduler |16 |02/17/2016 07:31:00 |02/17/2016 08:41 (17.02.2016) |2016-02-17T06:20:00Z |

### <a name="project-operator"></a>project-Operator
    T | project cost=price*quantity, price

Wählen Sie die Spalten aus, die einbezogen, umbenannt oder gelöscht werden sollen, und fügen Sie neue berechnete Spalten ein. Die Reihenfolge der Spalten im Ergebnis wird durch die Reihenfolge der Argumente festgelegt. Nur die in den Argumenten angegebenen Spalten sind im Ergebnis enthalten: alle anderen Spalten in der Eingabe werden gelöscht.  (Siehe auch `extend`.)

**Syntax**

    T | project ColumnName [= Expression] [, ...]

**Argumente**

* *T:* Die Eingabetabelle.
* *ColumnName:* Name einer Spalte, der in der Ausgabe angezeigt wird. Wenn kein *Ausdruck*vorhanden ist, muss die Eingabe eine Spalte mit diesem Namen enthalten. Bei [Namen](#names) muss die Groß-/Kleinschreibung beachtet werden. Sie können alphabetische oder numerische Zeichen oder Unterstriche („_“) enthalten. Verwenden Sie `['...']` oder `["..."]` zum Angeben von Schlüsselwörtern oder Namen mit anderen Zeichen.
* *Expression:* Optionaler skalarer Ausdruck, der auf die Eingabespalten verweist. 
  
    Das Zurückgeben einer neuen berechneten Spalte mit dem gleichen Namen wie eine vorhandene Spalte der Eingabe ist zulässig.

**Rückgabe**

Eine Tabelle, deren Spalten als Argumente benannt sind, und die ebenso viele Zeilen wie die Eingabetabelle aufweist.

**Beispiel**

Das folgende Beispiel zeigt mehrere Arten von Manipulationen, die mithilfe des `project` -Operators durchgeführt werden können. Die Eingabetabelle `T` umfasst drei Spalten vom Typ `int`: `A`, `B` und `C`. 

```AIQL
T
| project
    X=C,               // Rename column C to X
    A=2*B,             // Calculate a new column A from the old B
    C=strcat("-",tostring(C)), // Calculate a new column C from the old C
    B=2*B,              // Calculate a new column B from the old B
    ['where'] = client_City // rename, using a keyword as a column name
```

### <a name="project-away-operator"></a>project-away-Operator
    T | project-away column1, column2, ...

Schließt bestimmte Spalten aus. Das Ergebnis enthält alle Eingabespalten mit Ausnahme der angegebenen Spalten.

### <a name="range-operator"></a>range-Operator
    range LastWeek from ago(7d) to now() step 1d

Erzeugt eine einspaltige Tabelle mit Werten. Beachten Sie, dass keine Pipeline-Eingabe vorhanden ist. 

| LastWeek |
| --- |
| 2015-12-05 09:10:04.627 |
| 2015-12-06 09:10:04.627 |
| ... |
| 2015-12-12 09:10:04.627 |

**Syntax**

    range ColumnName from Start to Stop step Step

**Argumente**

* *ColumnName:* Der Name der einzelnen Spalte in der Ausgabetabelle.
* *Start:* Der kleinste Wert in der Ausgabe.
* *Stop:* Der höchste in der Ausgabe generierte Wert (oder eine Grenze für den höchsten Wert, wenn *step* diesen Wert überschreitet).
* *Step:* Die Differenz zwischen zwei aufeinanderfolgenden Werten. 

Die Argumente müssen numerische Werte, Datums- oder TimeSpan-Werte sein. Sie können nicht auf die Spalten einer Tabelle verweisen. (Wenn Sie den Bereich basierend auf einer Eingabetabelle berechnen möchten, verwenden Sie die [range*-Funktion*](#range), ggf. mit dem [mvexpand-Operator](#mvexpand-operator).) 

**Rückgabe**

Eine Tabelle mit einer einzelnen Spalte namens *ColumnName*, deren Werte *Start*, *Start* + *Step* usw. bis einschließlich *Stop* lauten.

**Beispiel**  

```AIQL
range Steps from 1 to 8 step 3
```

Eine Tabelle mit einer einzelnen Spalte namens `Steps` vom Typ `long`, deren Werte `1`, `4` und `7` sind.

**Beispiel**

    range LastWeek from bin(ago(7d),1d) to now() step 1d

Eine Tabelle von Mitternacht der vergangenen sieben Tage. Die bin (floor)-Funktion reduziert jede Zeit auf den Anfang des Tages.

**Beispiel**  

```AIQL
range timestamp from ago(4h) to now() step 1m
| join kind=fullouter
  (traces
      | where timestamp > ago(4h)
      | summarize Count=count() by bin(timestamp, 1m)
  ) on timestamp
| project Count=iff(isnull(Count), 0, Count), timestamp
| render timechart  
```

Zeigt, wie mit dem `range` -Operator eine kleine Ad-hoc-Dimensionstabelle erstellt werden kann, mit der anschließend Nullen eingefügt werden, wenn die Quelldaten keine Werte aufweisen.

### <a name="reduce-operator"></a>reduce-Operator
    exceptions | reduce by outerMessage

Versucht, ähnliche Datensätze zu gruppieren. Der Operator gibt für jede Gruppe das Muster (`Pattern`) aus, das die Gruppe wahrscheinlich am besten beschreibt, sowie die Anzahl (`Count`) von Datensätzen in dieser Gruppe.

![](./media/app-insights-analytics-reference/reduce.png)

**Syntax**

    T | reduce by  ColumnName [ with threshold=Threshold ]

**Argumente**

* *ColumnName:* Die zu untersuchende Spalte. Sie muss vom Typ „Zeichenfolge“ sein.
* <seg>
  *Threshold:* Ein Wert im Bereich {0..1}.</seg> Der Standardwert ist 0,001. Bei großen Eingaben sollte der Schwellenwert klein sein. 

**Rückgabe**

Zwei Spalten: `Pattern` und `Count`. In vielen Fällen ist das Muster ein vollständiger Wert aus der Spalte. In einigen Fällen kann es allgemeine Begriffe identifizieren und die Variablenteile durch „*“ ersetzen.

Das Ergebnis von `reduce by city` kann z.B. Folgendes enthalten: 

| Muster | Count |
| --- | --- |
| San * |5182 |
| Saint * |2846 |
| Moskau |3726 |
| \* -auf- \* |2730 |
| Paris |27163 |

### <a name="render-directive"></a>render-Anweisung
    T | render [ table | timechart  | barchart | piechart | areachart | scatterchart ] 
        [kind= default|stacked|stacked100|unstacked]

„Render“ weist die Darstellungsschicht an, wie die Tabelle angezeigt werden soll. Es sollte das letzte Element der Pipe sein. Es ist eine praktische Alternative zum Verwenden der Steuerelemente in der Anzeige, und Sie können eine Abfrage mit einer bestimmten Präsentationsmethode speichern.

Für einige Diagrammtypen bietet `kind` weitere Optionen. In einem Balkendiagramm vom Typ `stacked` wird beispielsweise jeder Balken nach einer ausgewählten Dimension segmentiert, sodass der Beitrag der verschiedenen Werte der Dimension zum Gesamtwert veranschaulicht wird. In einem Diagramm vom Typ `stacked100` weist jeder Balken die gleiche Höhe von 100 % auf, sodass Sie die relativen Beiträge vergleichen können.


### <a name="restrict-clause"></a>restrict-Klausel
Gibt die Tabellennamen an, die für die folgenden Operatoren zur Verfügung stehen. Beispiel:

    let e1 = requests | project name, client_City;
    let e2 =  requests | project name, success;
    // Exclude predefined tables from the union:
    restrict access to (e1, e2);
    union * |  take 10 

### <a name="sample-operator"></a>sample-Operator

Gibt gleichmäßig verteilte, zufällige Zeilen aus der Eingabetabelle zurück.


**Syntax**

    T | sample NumerOfRows

* *NumberOfRows:* Die zurückzugebende Zeilenanzahl im Beispiel.

**Tipp**

Verwenden Sie `Take`, wenn Sie kein gleichmäßig verteiltes Beispiel benötigen.


### <a name="sample-distinct-operator"></a>sample-distinct-Operator

Gibt eine einzelne Spalte zurück, die maximal die angegebene Anzahl von unterschiedlichen Werten für die angeforderte Spalte enthält. Gibt derzeit kein relativ verteiltes Beispiel zurück.

**Syntax**

    T | sample-distinct NumberOfValues of ColumnName

* *NumberOfValues* Die gewünschte Tabellenlänge
* *ColumnName:* Die gewünschte Spalte

**Tipps**

Kann hilfreich sein zum Abrufen einer Beispielpopulation durch Einfügen von sample-distinct in einer let-Anweisung und zum späteren Filtern mithilfe des in-Operators (siehe Beispiel).
 
Wenn Sie anstelle von Beispielwerten die ersten Werte abrufen möchten, verwenden Sie den top-hitters-Operator.

Wenn Sie Beispieldatenzeilen (anstelle von Werten einer bestimmten Spalte) abrufen möchten, verwenden Sie den [sample-Operator](#sample-operator).

**Beispiel**

Sie erfassen eine Beispielpopulation und führen weitere Berechnungen durch und wissen dabei, dass die Zusammenfassung die Abfragegrenzwerte nicht überschreitet.

```AIQL
let sampleops = toscalar(requests | sample-distinct 10 of OperationName);
requests | where OperationName in (sampleops) | summarize total=count() by OperationName
```
### <a name="search-operator"></a>search-Operator

Sucht in mehreren Tabellen und Spalten nach Zeichenfolgen.

**Syntax**

    search [kind=case_sensitive] [in (TableName, ...)] SearchToken

    T | search [kind=case_sensitive] SearchToken

    search [kind=case_sensitive] [in (TableName, ...)] SearchPredicate

    T | search [kind=case_sensitive] SearchPredicate

Sucht in beliebigen Spalten von beliebigen Tabellen nach Vorkommen der angegebenen Tokenzeichenfolge.
 
* *TableName:* Der global (Anforderungen, Ausnahmen...) oder durch eine [let-Klausel](#let-clause) definierte Name einer Tabelle. Sie können Platzhalter wie etwa „r*“ verwenden.
* *SearchToken:* Eine Tokenzeichenfolge. Muss einem ganzen Wort entsprechen. Sie können nachgestellte Platzhalter verwenden. „Amster *“ entspricht „Amsterdam“, „Amster“ jedoch nicht.
* *SearchPredicate:* Ein boolescher Ausdruck für die Spalten in den Tabellen. Sie können „*“ als Platzhalter in Spaltennamen verwenden.

**Beispiele**

```AIQL
search "Amster*"  //All columns, all tables

search name has "home"  // one column

search * has "home"     // all columns

search in (requests, exceptions) "Amster*"  // two tables

requests | search "Amster*"

requests | search name has "home"

```




### <a name="sort-operator"></a>sort-Operator
    T | sort by country asc, price desc

Sortiert die Zeilen der Eingabetabelle in Reihenfolge nach einer oder mehreren Spalten.

**Alias::** `order`

**Syntax**

    T  | sort by Column [ asc | desc ] [ , ... ]

**Argumente**

* *T:* Die zu sortierende Tabelleneingabe.
* *Column:* Spalte von *T*, nach der sortiert werden soll. Der Typ der Werte muss „Numerisch“, „Datum“, „Uhrzeit“ oder „Zeichenfolge“ sein.
* `asc` : Sortierung in aufsteigender Reihenfolge. Die Standardeinstellung ist `desc`, also absteigend.

**Beispiel**

```AIQL
Traces
| where ActivityId == "479671d99b7b"
| sort by Timestamp asc
```
Alle Zeilen in der Tabelle „Traces“ mit einer bestimmten Aktivitäts-ID ( `ActivityId`), sortiert nach ihrem Zeitstempel.

### <a name="summarize-operator"></a>summarize-Operator
Erzeugt eine Tabelle, die den Inhalt der Eingabetabelle aggregiert.

    requests
    | summarize count(), avg(duration), makeset(client_City) 
      by client_CountryOrRegion

Tabelle, die die Anzahl, durchschnittliche Anforderungsdauer und Menge von Städten in jedem Land zeigt. Die Ausgabe enthält eine Zeile für jedes unterschiedliche Land. Die Ausgabespalten zeigen die Anzahl, durchschnittliche Dauer, Städte und das Land. Alle anderen Eingabespalten werden ignoriert.

    T | summarize count() by price_range=bin(price, 10.0)

Eine Tabelle, die zeigt, wie viele Elemente in jedem Intervall [0, 10,0][10,0, 20,0] usw. Preise aufweisen. In diesem Beispiel ist eine Spalte für die Anzahl und eine für den Preisbereich vorhanden. Alle anderen Eingabespalten werden ignoriert.

**Syntax**

    T | summarize
         [  [ Column = ] Aggregation [ , ... ] ]
         [ by
            [ Column = ] GroupExpression [ , ... ] ]

**Argumente**

* *Column:* Optionaler Name für eine Ergebnisspalte. Nimmt standardmäßig den vom Ausdruck abgeleiteten Namen an. Bei [Namen](#names) muss die Groß-/Kleinschreibung beachtet werden. Sie können alphabetische oder numerische Zeichen oder Unterstriche („_“) enthalten. Verwenden Sie `['...']` oder `["..."]` zum Angeben von Schlüsselwörtern oder Namen mit anderen Zeichen.
* *Aggregation:* Ein Aufruf einer Aggregationsfunktion, z. B. `count()` oder `avg()`, mit Spaltennamen als Argumente. Siehe [Aggregationen](#aggregations).
* *GroupExpression:* Ein spaltenübergreifender Ausdruck, mit dem ein Satz von unterschiedlichen Werten bereitgestellt wird. Normalerweise handelt es sich entweder um einen Spaltennamen, der bereits einen eingeschränkten Satz von Werten bereitstellt, oder um `bin()` mit einer numerischen Spalte oder Zeitspalte als Argument. 

Wenn Sie einen numerischen Ausdruck oder Zeitausdruck ohne `bin()` bereitstellen, wendet Analytics ihn automatisch mit einem Intervall von `1h` für Uhrzeiten oder von `1.0` für Zahlen an.

Wenn Sie kein *GroupExpression* -Element angeben, wird die gesamte Tabelle in einer einzelnen Ausgabezeile zusammengefasst.

**Rückgabe**

Die Eingabezeilen sind in Gruppen mit denselben Werten der `by` -Ausdrücke angeordnet. Anschließend werden die angegebenen Aggregationsfunktionen über jede Gruppe berechnet, dabei wird eine Zeile für jede Gruppe erzeugt. Das Ergebnis enthält die `by` -Spalten und auch mindestens eine Spalte für jedes berechnete Aggregat. (Einige Aggregationsfunktionen geben mehrere Spalten zurück.)

Das Ergebnis umfasst genauso viele Zeilen, wie unterschiedliche Kombinationen von `by` -Werten vorhanden sind. Wenn Sie Zusammenfassungen über Bereiche von numerischen Werten erstellen möchten, verwenden Sie `bin()` , um Bereiche auf diskrete Werte zu reduzieren.

> [!NOTE]
> Auch wenn Sie beliebige Ausdrücke für die Aggregation und Gruppierung von Ausdrücken bereitstellen können, ist es effizienter, einfache Spaltennamen zu verwenden oder `bin()` auf eine numerische Spalte anzuwenden.

### <a name="table-operator"></a>table-Operator

    table('pageViews')

Die in der Argumentzeichenfolge benannte Tabelle.

**Syntax**

    table(tableName)

**Argumente**

* *tableName:* Eine Zeichenfolge. Der Name einer Tabelle (statisch oder das Ergebnis einer let-Klausel).

**Beispiele**

    table('requests');


    let size = (tableName: string) {
        table(tableName) | summarize sum(itemCount)
    };
    size('pageViews');



### <a name="take-operator"></a>take-Operator
Alias von [limit](#limit-operator)

### <a name="top-operator"></a>top-Operator
    T | top 5 by Name desc nulls first

Gibt die ersten *N* Datensätze nach den angegebenen Spalten sortiert zurück.

**Syntax**

    T | top NumberOfRows by Sort_expression [ asc | desc ] [nulls first|nulls last] [, ... ]

**Argumente**

* *NumberOfRows:* Die zurückzugebende Zeilenanzahl von *T*.
* *Sort_expression:* Ein Ausdruck, nach dem die Zeilen sortiert werden. Dies ist in der Regel nur ein Spaltenname. Sie können mehrere „Sort_expression“-Angaben machen.
* Unter Umständen wird `asc` oder `desc` (Standard) angezeigt, um zu steuern, ob die tatsächliche Auswahl vom „unteren“ oder „oberen“ Ende des Bereichs erfolgt.
* `nulls first` oder `nulls last` steuert, wo Nullwerte angezeigt werden. `First` ist der Standardwert für `asc`, `last` ist der Standardwert für `desc`.

**Tipps**

`top 5 by name` entspricht oberflächlich betrachtet `sort by name | take 5`. Allerdings ist die Ausführung schneller, und es werden immer sortierte Ergebnisse zurückgegeben; dies ist mit `take` nicht garantiert.

### <a name="top-nested-operator"></a>top-nested operator
    requests
    | top-nested 5 of name by count()
    , top-nested 3 of performanceBucket by count()
    , top-nested 3 of client_CountryOrRegion by count()
    | render barchart

Erzeugt die hierarchische Ergebnisse, wobei jede Ebene einen Drilldown der vorherigen Ebene darstellt. Dies ist nützlich für die Beantwortung von Fragen wie „Was sind die Top 5-Anfragen, welches sind für jede von diesen die 3 besten Leistungsbuckets und aus welchen 3 Ländern stammen die meisten Anforderungen für diese?“.

**Syntax**

   T | top-nested N of COLUMN by AGGREGATION [, ...]

**Argumente**

* N:int: Anzahl der Zeilen für die Rückgabe oder die Übergabe an die nächste Ebene. In einer Abfrage mit drei Ebenen mit N = 5, 3 und 3 ist die Gesamtanzahl der Zeilen 45.
* COLUMN: eine Spalte zum Gruppieren für die Aggregation. 
* AGGREGATION: Eine [Aggregationsfunktion](#aggregations) , die auf jede Gruppe von Zeilen angewendet werden soll. Die Ergebnisse dieser Aggregationen bestimmt die obersten Gruppen für die Anzeige.

### <a name="union-operator"></a>union-Operator
     Table1 | union Table2, Table3

Verwendet mindestens zwei Tabellen und gibt die Zeilen aller Tabellen zurück. 

**Syntax**

    T | union [ kind= inner | outer ] [ withsource = ColumnName ] Table2 [ , ...]  

    union [ kind= inner | outer ] [ withsource = ColumnName ] Table1, Table2 [ , ...]  

**Argumente**

* *Table1*, *Table2* ...
  * Der Name einer Tabelle, z. B. `requests`, oder eine in einer [let-Klausel](#let-clause) definierte Tabelle; oder
  * Ein Abfrageausdruck, z.B. `(requests | where success=="True")`.
  * Ein Satz von Tabellen, die mit einem Platzhalterzeichen angegeben sind. `e*` bildet z.B. die Vereinigung aller Tabellen, die in den vorhergehenden let-Klauseln definiert wurden und deren Name mit „e“ beginnt, zusammen mit der Tabelle der Ausnahmen.
* `kind`: 
  * `inner` : Das Ergebnis enthält die Teilmenge der Spalten, die in allen Eingabetabellen vorkommen.
  * `outer` : Das Ergebnis enthält alle Spalten, die in einer der Eingaben vorkommen. Zellen, die nicht durch eine Eingabezeile definiert wurden, werden auf `null`festgelegt.
* `withsource=`*ColumnName:* Wenn diese Einstellung festgelegt ist, enthält die Ausgabe eine Spalte namens *ColumnName*, deren Wert angibt, aus welchen Quelltabellen die einzelnen Zeilen stammen. Verwenden Sie [as](#as-operator) am Ende jedes Tabellenausdrucks, wenn Sie den Namen angeben möchten, der in dieser Spalte angezeigt wird.

**Rückgabe**

Eine Tabelle, deren Anzahl an Zeilen der Anzahl in allen Eingabetabellen entspricht und deren Anzahl an Spalten mit der Anzahl an eindeutigen Spaltennamen in den Eingaben übereinstimmt.

Es gibt keine garantierte Reihenfolge in den Zeilen.


**Beispiel**

Die Anzahl unterschiedlicher Benutzer, die während der letzten 12 Stunden entweder ein `exceptions`- oder ein `traces`-Ereignis ausgelöst haben. Im Ergebnis enthält die Spalte „SourceTable“ entweder Ausnahmen oder Ablaufverfolgungen:

```AIQL
    
    union withsource=SourceTable kind=outer exceptions, traces
    | where timestamp > ago(12h)
    | summarize dcount(user_Id) by SourceTable
```

Mit dieser effizienteren Version wird dasselbe Ergebnis erzielt. Jede Tabelle wird vor dem Erstellen der Vereinigung gefiltert.

```AIQL
    exceptions
    | where timestamp > ago(24h) | as exceptions
    | union withsource=SourceTable kind=outer (requests | where timestamp > ago(12h) | as traces)
    | summarize dcount(user_Id) by SourceTable 
```

Verwenden Sie [as](#as-operator), um den Namen anzugeben, der in der Quellspalte angezeigt wird.

#### <a name="forcing-an-order-of-results"></a>Erzwingen der Reihenfolge der Ergebnisse

„Union“ garantiert keine bestimmte Reihenfolge der Zeilen in den Ergebnissen.
Fügen Sie zum Abrufen derselben Reihenfolge bei jeder Ausführung der Abfrage eine Spalte des Typs „Tag“ an jede Eingabetabelle an:

    let r1 = (traces | count | extend tag = 'r1');
    let r2 = (requests | count| extend tag = 'r2');
    let r3 = (pageViews | count | extend tag = 'r3');
    r1 | union r2,r3 | sort by tag

#### <a name="see-also"></a>Weitere Informationen

Betrachten Sie den [join-Operator](#join-operator) als Alternative.

### <a name="where-operator"></a>where-Operator
     requests | where resultCode=="200"

Filtert eine Tabelle auf die Teilmenge der Zeilen, die ein Prädikat erfüllen.

**Alias::** `filter`

**Syntax**

    T | where Predicate
    T | where * has Term

**Argumente**

* *T* : Die tabellarische Eingabe, deren Datensätze gefiltert werden sollen.
* *Predicate*: Ein `boolean`-[-Ausdruck](#boolean) über die Spalten von *T*. Er wird für jede Zeile in *T* ausgewertet.
* *Term*: Zeichenfolge, die dem gesamten Wort in einer Spalte entsprechen muss.

**Rückgabe**

Zeilen in *T*, für die *Predicate* auf `true` festgelegt ist.

**Tipps**

So erzielen Sie die optimale Leistung:

* **Verwenden Sie einfache Vergleiche** zwischen dem Spaltennamen und Konstanten. („Konstant“ bedeutet konstant innerhalb der Tabelle, d. h. `now()` und `ago()` sind ebenso in Ordnung wie skalare Werte, die mithilfe einer [`let`-Klausel](#let-clause) zugewiesen werden.)
  
    Beispielsweise wird `where Timestamp >= ago(1d)` gegenüber `where floor(Timestamp, 1d) == ago(1d)` bevorzugt.
* **Einfachste Begriffe zuerst**: Wenn Sie mehrere mit `and` verbundene Klauseln haben, stellen Sie die Klauseln, die nur eine Spalte umfassen, an den Anfang. `Timestamp > ago(1d) and OpId == EventId` ist also besser als anders herum.

**Beispiel**

```AIQL
traces
| where Timestamp > ago(1h)
    and Source == "Kuskus"
    and ActivityId == SubActivityIt 
```

Datensätze, die nicht älter als 1 Stunde sind, aus der Quelle namens „Kuskus“ stammen und zwei Spalten mit dem gleichen Wert aufweisen. 

Beachten Sie, dass wir den Vergleich zwischen zwei Spalten an das Ende stellen, da der Index nicht genutzt werden kann und ein Scan erzwungen wird.



## <a name="aggregations"></a>Aggregationen
Aggregationen dienen zum Kombinieren von Werten in Gruppen, die im [summarize-Vorgang](#summarize-operator) erstellt werden. In dieser Abfrage ist z.B. dcount() eine Aggregatfunktion:

    requests | summarize dcount(name) by success

### <a name="any"></a>beliebig
    any(Expression)

Wählt eine Zeile der Gruppe nach dem Zufallsprinzip aus, und gibt den Wert des angegebenen Ausdrucks zurück.

Dies empfiehlt sich beispielsweise, wenn eine Spalte über eine große Anzahl von ähnlichen Werten verfügt (z. B. eine Spalte „Fehlertext“) und Sie einmal pro eindeutigem Wert für den zusammengesetzten Gruppenschlüssel Stichproben aus dieser Spalte abrufen möchten. 

**Beispiel**  

```

traces 
| where timestamp > now(-15min)  
| summarize count(), any(message) by operation_Name 
| top 10 by count_level desc 
```

<a name="argmin"></a>
<a name="argmax"></a>

### <a name="argmin-argmax"></a>argmin, argmax
    argmin(ExprToMinimize, * | ExprToReturn  [ , ... ] )
    argmax(ExprToMaximize, * | ExprToReturn  [ , ... ] ) 

Findet eine Zeile in der Gruppe, die *ExprToMaximize* minimiert/maximiert, und gibt den Wert von *ExprToReturn* zurück (oder `*`, um die gesamte Zeile zurückzugeben).

**Tipp**: Die durchlaufenen Spalten werden automatisch umbenannt. Um sicherzustellen, dass Sie die richtigen Namen verwenden, überprüfen Sie die Ergebnisse mit `take 5` , bevor Sie die Ergebnisse an einen anderen Operator weiterreichen.

**Beispiele**

Zeigen Sie für jeden Anforderungsnamen, wann die längste Anforderung aufgetreten ist:

    requests | summarize argmax(duration, timestamp) by name

Zeigen Sie alle Details der längsten Anforderung, nicht nur den Zeitstempel:

    requests | summarize argmax(duration, *) by name


Suchen Sie den niedrigsten Wert jeder Metrik, zusammen mit dem Zeitstempel und anderen Daten:

    metrics 
    | summarize minValue=argmin(value, *) 
      by name


![](./media/app-insights-analytics-reference/argmin.png)

### <a name="avg"></a>avg
    avg(Expression)

Berechnet den Durchschnitt von *Expression* in der Gruppe.

### <a name="buildschema"></a>buildschema
    buildschema(DynamicExpression)

Gibt das minimale Schema zurück, das alle Werte von *DynamicExpression*zulässt. 

Der Parameterspaltentyp sollte `dynamic` lauten (Array oder ein Eigenschaftenbehälter). 

**Beispiel**

    exceptions | summarize buildschema(details)

Ergebnis:

    { "indexer":
     {"id":"string",
       "parsedStack":
       { "indexer": 
         {  "level":"int",
            "assembly":"string",
            "fileName":"string",
            "method":"string",
            "line":"int"
         }},
      "outerId":"string",
      "message":"string",
      "type":"string",
      "rawStack":"string"
    }}

Beachten Sie, dass mit `indexer` markiert wird, an welcher Stelle Sie einen numerischen Index verwenden sollten. Einige gültige Pfade für dieses Schema (vorausgesetzt diese Beispielindizes befinden sich im Bereich):

    details[0].parsedStack[2].level
    details[0].message
    arraylength(details)
    arraylength(details[0].parsedStack)

**Beispiel**

Wenn die Eingabespalte drei dynamische Werte hat:

|  |
| --- |
| `{"x":1, "y":3.5}` |
| `{"x":"somevalue", "z":[1, 2, 3]}` |
| `{"y":{"w":"zzz"}, "t":["aa", "bb"], "z":["foo"]}` |

Lautet das resultierende Schema folgendermaßen:

    {
      "x":["int", "string"],
      "y":["double", {"w": "string"}],
      "z":{"indexer": ["int", "string"]},
      "t":{"indexer": "string"}
    }

Das Schema weist auf Folgendes hin:

* Das Stammobjekt ist ein Container mit den vier Eigenschaften x, y, z und t.
* Die Eigenschaft „x“ kann entweder den Typ „int“ oder „string“ haben.
* Bei der Eigenschaft „y“ kann es sich entweder um den Typ „double“ handeln oder um einen anderen Container mit einer Eigenschaft namens „w“ vom Typ „string“.
* Das ``indexer`` -Schlüsselwort gibt an, dass „z“ und „t“ Arrays sind.
* Jedes Element im Array „z“ ist entweder eine ganze Zahl oder eine Zeichenfolge (string).
* „t“ ist ein Array von Zeichenfolgen.
* Jede Eigenschaft ist implizit optional, und jedes Array kann leer sein.

##### <a name="schema-model"></a>Schemamodell
Die Syntax des zurückgegebenen Schemas lautet folgendermaßen:

    Container ::= '{' Named-type* '}';
    Named-type ::= (name | '"indexer"') ':' Type;
    Type ::= Primitive-type | Union-type | Container;
    Union-type ::= '[' Type* ']';
    Primitive-type ::= "int" | "string" | ...;

Sie entsprechen einer Teilmenge der TypeScript-Typanmerkungen, die als dynamischer Wert codiert sind. In TypeScript würde das Beispielschema folgendermaßen lauten:

    var someobject:
    {
      x?: (number | string),
      y?: (number | { w?: string}),
      z?: { [n:number] : (int | string)},
      t?: { [n:number]: string }
    }


### <a name="count"></a>count
    count([ Predicate ])

Gibt die Anzahl von Zeilen zurück, für die *Predicate* als `true` ausgewertet wird. Wenn *Predicate* nicht angegeben ist, wird die Gesamtzahl von Datensätzen in der Gruppe zurückgegeben. 

**Leistungstipp**: Verwenden Sie `summarize count(filter)` anstelle von `where filter | summarize count()`.

> [!NOTE]
> Vermeiden Sie count() zum Ermitteln der Anzahl von Anforderungen, Ausnahmen oder anderen Ereignissen, die aufgetreten sind. Wenn gerade eine [Stichprobe](app-insights-sampling.md) erstellt wird, ist die Anzahl von Datenpunkten in Application Insights geringer als die Anzahl von tatsächlichen Ereignissen. Verwenden Sie stattdessen `summarize sum(itemCount)...`. Die Eigenschaft „itemCount“ gibt die Anzahl von ursprünglichen Ereignissen wieder, die von jedem vermerkten Datenpunkt dargestellt werden.
> 
> 

### <a name="countif"></a>countif
    countif(Predicate)

Gibt die Anzahl von Zeilen zurück, für die *Predicate* als `true` ausgewertet wird.

**Leistungstipp**: Verwenden Sie `summarize countif(filter)` anstelle von `where filter | summarize count()`.

> [!NOTE]
> Verwenden Sie „countif()“ nicht zum Ermitteln der Anzahl von Anforderungen, Ausnahmen oder anderen Ereignissen, die aufgetreten sind. Wenn gerade ein [Sampling](app-insights-sampling.md) durchgeführt wird, ist die Anzahl von Datenpunkten geringer als die Anzahl von tatsächlichen Ereignissen. Verwenden Sie stattdessen `summarize sum(itemCount)...`. Die Eigenschaft „itemCount“ gibt die Anzahl von ursprünglichen Ereignissen wieder, die von jedem vermerkten Datenpunkt dargestellt werden.
> 
> 

### <a name="dcount"></a>dcount
    dcount( Expression [ ,  Accuracy ])

Gibt eine Schätzung der Anzahl von unterschiedlichen Werten für *Expr* in der Gruppe zurück. (Verwenden Sie zum Auflisten der unterschiedlichen Werte [`makeset`](#makeset).)

Mit *Accuracy* wird, sofern angegeben, der Ausgleich zwischen Geschwindigkeit und Genauigkeit gesteuert.

* `0` ist die am wenigsten präzise und schnellste Berechnung.
* `1` ist die Standardeinstellung, bei der Genauigkeit und Berechnungszeit ausgeglichen sind; etwa 0,8% Fehlerwahrscheinlichkeit.
* `2` ist die präziseste und langsamste Berechnung; etwa 0,4% Fehlerwahrscheinlichkeit.

**Beispiel**

    pageViews 
    | summarize cities=dcount(client_City) 
      by client_CountryOrRegion

![](./media/app-insights-analytics-reference/dcount.png)

### <a name="dcountif"></a>dcountif
    dcountif( Expression, Predicate [ ,  Accuracy ])

Gibt eine Schätzung der Anzahl von eindeutigen Werten für *Expr* in Zeilen der Gruppe zurück, für die *Predicate* auf „true“ festgelegt ist. (Verwenden Sie zum Auflisten der unterschiedlichen Werte [`makeset`](#makeset).)

Mit *Accuracy* wird, sofern angegeben, der Ausgleich zwischen Geschwindigkeit und Genauigkeit gesteuert.

* `0` ist die am wenigsten präzise und schnellste Berechnung.
* `1` ist die Standardeinstellung, bei der Genauigkeit und Berechnungszeit ausgeglichen sind; etwa 0,8% Fehlerwahrscheinlichkeit.
* `2` ist die präziseste und langsamste Berechnung; etwa 0,4% Fehlerwahrscheinlichkeit.

**Beispiel**

    pageViews 
    | summarize cities=dcountif(client_City, client_City startswith "St") 
      by client_CountryOrRegion


### <a name="makelist"></a>makelist
    makelist(Expr [ ,  MaxListSize ] )

Gibt ein `dynamic` -Array (JSON) aller Werte von *Expr* in der Gruppe zurück. 

* *MaxListSize* ist eine optionale Ganzzahlbegrenzung für die maximale Anzahl von zurückgegebenen Elementen (Standardwert: *128*).

### <a name="makeset"></a>makeset
    makeset(Expression [ , MaxSetSize ] )

Gibt ein `dynamic` -Array (JSON) des Satzes eindeutiger Werte zurück, die *Expr* in der Gruppe annimmt. (Tipp: Verwenden Sie zum Zählen der unterschiedlichen Werte [`dcount`](#dcount).)

* *MaxSetSize* ist eine optionale Ganzzahlbegrenzung für die maximale Anzahl von zurückgegebenen Elementen (Standardwert: *128*).

**Beispiel**

    pageViews 
    | summarize cities=makeset(client_City) 
      by client_CountryOrRegion

![](./media/app-insights-analytics-reference/makeset.png)

Siehe auch den [`mvexpand` -Operator](#mvexpand-operator) für die umgekehrte Funktion.

### <a name="max-min"></a>max, min
    max(Expr)

Berechnet das Maximum von *Expr*.

    min(Expr)

Berechnet das Minimum von *Expr*.

**Tipp:** Hiermit erhalten Sie ausschließlich die Mindest- oder Maximalwerte, z. B. den höchsten oder niedrigsten Preis. Wenn Sie jedoch andere Spalten in der Zeile abrufen möchten, z. B. den Namen des Lieferanten mit dem niedrigsten Preis, verwenden Sie [argmin oder argmax](#argmin-argmax).

<a name="percentile"></a>
<a name="percentiles"></a>
<a name="percentilew"></a>
<a name="percentilesw"></a>

### <a name="percentile-percentiles-percentilew-percentilesw"></a>percentile, percentiles, percentilew, percentilesw
    percentile(Expression, Percentile)

Gibt eine Schätzung für *Expression* des angegebenen Perzentils in der Gruppe zurück. Die Genauigkeit hängt von der Bevölkerungsdichte in der Region des Perzentils ab.

    percentiles(Expression, Percentile1 [ , Percentile2 ...] )

Ähnlich wie `percentile()`, berechnet jedoch eine Reihe von Perzentilwerten (was schneller ist, als jedes Perzentil einzeln zu berechnen).

    percentilew(Expression, WeightExpression, Percentile)

Gewichtetes Perzentil. Verwenden Sie dieses für vorab aggregierte Daten.  `WeightExpression` ist eine Ganzzahl, die angibt, wie viele ursprüngliche Zeilen von jeder aggregierten Zeile dargestellt werden.

    percentilesw(Expression, WeightExpression, Percentile1, [, Percentile2 ...])

Wie `percentilew()`, berechnet aber eine Anzahl von Perzentilwerten.

**Beispiele**

Der Wert von `duration` , der größer als 95% und kleiner als 5% des Stichprobensatzes ist, berechnet für jeden Anforderungsnamen:

    request 
    | summarize percentile(duration, 95)
      by name

Lassen Sie „by...“ aus, um den Wert für die gesamte Tabelle zu berechnen.

Berechnen Sie gleichzeitig mehrere Perzentile für andere Anforderungsnamen:

    requests 
    | summarize 
        percentiles(duration, 5, 20, 50, 80, 95) 
      by name

![](./media/app-insights-analytics-reference/percentiles.png)

Die Ergebnisse zeigen, dass für die Anforderung „/Events/Index“ auf 5 % der Anforderungen in weniger als 2,44 Sekunden reagiert wird, auf die Hälfte in 3,52 Sekunden und auf 5 % langsamer als 6,85 Sekunden.

Berechnen Sie mehrere Statistiken:

    requests 
    | summarize 
        count(), 
        avg(Duration),
        percentiles(Duration, 5, 50, 95)
      by name

#### <a name="weighted-percentiles"></a>Gewichtete Perzentile
Verwenden Sie die Funktionen für gewichtete Perzentile in Fällen, in denen die Daten vorab aggregiert wurden. 

Angenommen, Ihre App führt mehrere Tausend Vorgänge pro Sekunde aus, und Sie möchten die Latenzzeit dieser Vorgänge wissen. Eine einfache Lösung wäre es, eine Application Insights-Anforderung oder ein benutzerdefiniertes Ereignis für jeden Vorgang zu generieren. Das würde zu viel Datenverkehr führen, obwohl dieser durch adaptives Sampling reduziert würde. Wenn Sie jedoch eine bessere Lösung implementieren möchten, schreiben Sie Code in Ihre App, mit dem die Daten vor dem Senden an Application Insights aggregiert werden. Die aggregierte Zusammenfassung wird in regelmäßigen Abständen gesendet, sodass die Datenrate auf wenige Punkte pro Minute reduziert wird.

Ihr Code verwendet einen Datenstrom von Latenzmessungen in Millisekunden. Zum Beispiel:

     { 15, 12, 2, 21, 2, 5, 35, 7, 12, 22, 1, 15, 18, 12, 26, 7 }

Es werden die Messungen in den folgenden Containern gezählt: `{ 10, 20, 30, 40, 50, 100 }`

In regelmäßigen Abständen wird eine Serie von TrackEvent-Aufrufen ausgeführt – einer pro Bucket, mit benutzerdefinierten Messungen in jedem Aufruf: 

    foreach (var latency in bins.Keys)
    { telemetry.TrackEvent("latency", null, 
         new Dictionary<string, double>
         ({"latency", latency}, {"opCount", bins[latency]}}); }

In Analytics wird eine Gruppe von Ereignissen wie die folgende angezeigt:

| `opCount` | `latency` | Bedeutung |
| --- | --- | --- |
| 8 |10 |= 8 Vorgänge im 10-ms-Container |
| 6 |20 |= 6 Vorgänge im 20-ms-Container |
| 3 |30 |= 3 Vorgänge im 30-ms-Container |
| 1 |40 |= 1 Vorgang im 40-ms-Container |

Um ein exaktes Bild der ursprünglichen Verteilung der Ereignislatenzen zu erhalten, verwenden wir `percentilesw`:

    customEvents | summarize percentilesw(latency, opCount, 20, 50, 80)

Die Ergebnisse sind die gleichen, als hätten wir einfache `percentiles` -Elemente im ursprünglichen Messungssatz verwendet.

> [!NOTE]
> Gewichtete Perzentile gelten nicht für [Stichprobendaten](app-insights-sampling.md), bei denen jede erfasste Zeile eine zufällige Stichprobe der ursprünglichen Zeilen darstellt, und keinen Container. Die einfachen Perzentilfunktionen eignen sich für Stichprobendaten.
> 
> 

#### <a name="estimation-error-in-percentiles"></a>Schätzungsfehler in Perzentilen
Das Perzentilaggregat stellt einen ungefähren Wert mithilfe von [T-Digest](https://github.com/tdunning/t-digest/blob/master/docs/t-digest-paper/histo.pdf)bereit. 

Einige wichtige Punkte: 

* Die Grenzen für den Schätzungsfehler variieren je nach dem Wert des angeforderten Perzentils. Die beste Genauigkeit erhalten Sie an den Enden der Skala von [0 bis 100]. Die Perzentile 0 und 100 sind die Mindest- und Maximalwerte für die Verteilung. Die Genauigkeit nimmt zur Mitte der Skala hin ab. Am Mittelpunkt ist die Genauigkeit am unpräzisesten und auf 1 % begrenzt. 
* Fehlergrenzen werden in Bezug auf den Rang, nicht auf den Wert sichtbar. Beispiel: Perzentil(X, 50) hat den Wert Xm zurückgegeben. Die Schätzung garantiert, dass mindestens 49 % und höchstens 51 % der Werte von X kleiner sind als Xm. Es gibt keine theoretische Beschränkung hinsichtlich des Unterschieds zwischen Xm und dem tatsächlichen Mittelwert von X.

### <a name="stdev"></a>stdev
     stdev(Expr)

Gibt die Standardabweichung von *Expr* für die Gruppe zurück.

### <a name="variance"></a>variance
    variance(Expr)

Gibt die Varianz von *Expr* für die Gruppe zurück.

### <a name="sum"></a>sum
    sum(Expr)

Gibt die Summe von *Expr* für die Gruppe zurück.                      

## <a name="scalars"></a>Skalare
[Umwandlungen](#casts) | [Vergleiche](#scalar-comparisons)
<br/>
[gettype](#gettype) | [hash](#hash) | [iff](#iff) |  [isnull](#isnull) | [isnotnull](#isnotnull) | [notnull](#notnull) | [toscalar](#toscalar)

Die unterstützten Typen sind:

| Typ | Weitere(r) Name(n) | Entsprechender .NET-Typ |
| --- | --- | --- |
| `bool` |`boolean` |`System.Boolean` |
| `datetime` |`date` |`System.DateTime` |
| `dynamic` | |`System.Object` |
| `guid` |`uuid`, `uniqueid` |`System.Guid` |
| `int` | |`System.Int32` |
| `long` | |`System.Int64` |
| `double` |`real` |`System.Double` |
| `string` | |`System.String` |
| `timespan` |`time` |`System.TimeSpan` |

### <a name="casts"></a>Typumwandlungen
Sie können einen Typ in einen anderen umwandeln. Wenn die Konvertierung sinnvoll ist, wird sie im Allgemeinen auch funktionieren:

    todouble(10), todouble("10.6")
    toint(10.6) == 11
    floor(10.6) == 10
    toint("200")
    todatetime("2016-04-28 13:02")
    totimespan("1.5d"), totimespan("1.12:00:00")
    toguid("00000000-0000-0000-0000-000000000000")
    tostring(42.5)
    todynamic("{a:10, b:20}")

Überprüfen Sie, ob eine Zeichenfolge in einen bestimmten Typ konvertiert werden kann:

    iff(notnull(todouble(customDimensions.myValue)),
       ..., ...)







### <a name="scalar-comparisons"></a>Skalare Vergleiche
|  |  |
| --- | --- |
| `<` |Kleiner |
| `<=` |Kleiner oder gleich |
| `>` |Größer |
| `>=` |Größer oder gleich |
| `<>` |Not Equals |
| `!=` |Not Equals |
| `in` |Rechter Operand ist ein (dynamisches) Array, und linker Operand entspricht einem seiner Elemente. |
| `!in` |Rechter Operand ist ein (dynamisches) Array, und linker Operand entspricht nicht einem seiner Elemente. |

### <a name="gettype"></a>gettype
**Rückgabe**

Eine Zeichenfolge, die den zugrunde liegenden Speichertyp des einzigen Arguments darstellt. Dies ist besonders nützlich, wenn Sie über Werte vom Typ `dynamic` verfügen: In diesem Fall zeigt `gettype()`, wie ein Wert codiert ist.

**Beispiele**

|  |  |
| --- | --- |
| `gettype("a")` |`"string" ` |
| `gettype(111)` |`"long" ` |
| `gettype(1==1)` |`"int8"` |
| `gettype(now())` |`"datetime" ` |
| `gettype(1s)` |`"timespan" ` |
| `gettype(parsejson('1'))` |`"int" ` |
| `gettype(parsejson(' "abc" '))` |`"string" ` |
| `gettype(parsejson(' {"abc":1} '))` |`"dictionary"` |
| `gettype(parsejson(' [1, 2, 3] '))` |`"array"` |
| `gettype(123.45)` |`"real" ` |
| `gettype(guid(12e8b78d-55b4-46ae-b068-26d7a0080254))` |`"guid"` |
| `gettype(parsejson(''))` |`"null"` |
| `gettype(1.2)==real` |`true` |

### <a name="hash"></a>hash
**Syntax**

    hash(source [, mod])

**Argumente**

* *source:*Der Quellskalar, mit dem der Hash berechnet wird.
* *mod:*Der Modulowert, der auf das Hashergebnis angewendet werden soll.

**Rückgabe**

Der xxhash (long)-Wert des angegebenen Skalars, Modulo des angegebenen mod-Werts (sofern angegeben).

**Beispiele**

```
hash("World")                   // 1846988464401551951
hash("World", 100)              // 51 (1846988464401551951 % 100)
hash(datetime("2015-01-01"))    // 1380966698541616202
```
### <a name="iff"></a>iff
Die `iff()`-Funktion wertet das erste Argument (Prädikat) aus und gibt entweder den Wert des zweiten oder den Wert des dritten Arguments zurück, und zwar abhängig davon, ob das Prädikat `true` oder `false` lautet. Die zweiten und dritten Argumente müssen vom gleichen Typ sein.

**Syntax**

    iff(predicate, ifTrue, ifFalse)


**Argumente**

* *predicate*: Ein Ausdruck, der als `boolean`-Wert ausgewertet wird.
* *ifTrue*: Ein Ausdruck, der ausgewertet und dessen Wert von der Funktion zurückgegeben wird, wenn *predicate* als `true` ausgewertet wird.
* *ifFalse:* Ein Ausdruck, der ausgewertet und dessen Wert von der Funktion zurückgegeben wird, wenn *predicate* als `false` ausgewertet wird.

**Rückgabe**

Diese Funktion gibt den Wert von *ifTrue* zurück, wenn *predicate* als `true` ausgewertet wird, andernfalls den Wert von *ifFalse*.

**Beispiel**

```
iff(floor(timestamp, 1d)==floor(now(), 1d), "today", "anotherday")
```

<a name="isnull"/></a>
<a name="isnotnull"/></a>
<a name="notnull"/></a>

### <a name="isnull-isnotnull-notnull"></a>isnull, isnotnull, notnull
    isnull(parsejson("")) == true

Akzeptiert ein einzelnes Argument und gibt an, ob es null ist.

**Syntax**

    isnull([value])


    isnotnull([value])


    notnull([value])  // alias for isnotnull

**Rückgabe**

True oder False, je nachdem, ob ist der Wert null oder nicht null ist.

| x | isnull(x) |
| --- | --- |
| "" |false |
| "x" |false |
| parsejson("") |true |
| parsejson("[]") |false |
| parsejson("{}") |false |

**Beispiel**

    T | where isnotnull(PossiblyNull) | count

Beachten Sie, dass es andere Möglichkeiten gibt, diesen Effekt zu erreichen:

    T | summarize count(PossiblyNull)

### <a name="toscalar"></a>toscalar
Wertet eine Abfrage oder einen Ausdruck aus und gibt das Ergebnis als einzelnen Wert zurück. Diese Funktion eignet sich für die gestaffelte Berechnungen; z.B. um die Gesamtanzahl von Ereignissen zu berechnen und diese dann als Basislinie zu verwenden.

**Syntax**

    toscalar(query)
    toscalar(scalar)

**Rückgabe**

Das ausgewertete Argument. Wenn das Argument eine Tabelle ist, wird die erste Spalte der ersten Zeile zurückgegeben. (Es empfiehlt sich, dafür zu sorgen, dass das Argument nur eine Spalte und Zeile enthält.)

**Beispiel**

```AIQL

    // Get the count of requests 5 days ago:
    let baseline = toscalar(requests  
        | where floor(timestamp, 1d) == floor(ago(5d),1d) | count);
    // List the counts relative to that baseline:
    requests | summarize daycount = count() by floor(timestamp, 1d)  
    | extend relative = daycount - baseline
```




### <a name="boolean-literals"></a>Boolesche Literale
    true == 1
    false == 0
    gettype(true) == "int8"
    typeof(bool) == typeof(int8)

### <a name="boolean-operators"></a>Boolesche Operatoren
    and 
    or 

### <a name="convert-to-boolean"></a>Konvertieren zu in booleschen Wert

Sie können eine Zeichenfolge `aStringBoolean`, die den Wert „true“ oder „false“ enthält, wie folgt in einen booleschen Wert konvertieren:

    booleanResult = aStringBoolean =~ "true"



## <a name="numbers"></a>Zahlen
[abs](#abs) | [bin](#bin) | [exp](#exp) | [floor](#floor) | [gamma](#gamma) |[log](#log) | [rand](#rand) | [range](#range) | [sqrt](#sqrt) 
| [todouble](#todouble) | [toint](#toint) | [tolong](#tolong)

### <a name="numeric-literals"></a>Numerische Literale
|  |  |
| --- | --- |
| `42` |`long` |
| `42.0` |`real` |

### <a name="arithmetic-operators"></a>Arithmetische Operatoren
|  |  |
| --- | --- |
| + |Hinzufügen |
| - |Subtrahieren |
| * |Multiplizieren |
| / |Dividieren |
| % |Modulo |
| `<` |Kleiner |
| `<=` |Kleiner oder gleich |
| `>` |Größer |
| `>=` |Größer oder gleich |
| `<>` |Not Equals |
| `!=` |Not Equals |

### <a name="abs"></a>abs
**Syntax**

    abs(x)

**Argumente**

* x: ein integer-, real- oder timespan-Wert

**Rückgabe**

    iff(x>0, x, -x)

<a name="bin"></a><a name="floor"></a>

### <a name="bin-floor"></a>bin, floor
Rundet Werte auf eine ganze Zahl ab, die ein Vielfaches der angegebenen bin-Größe ist. Wird häufig in der [`summarize by`](#summarize-operator) -Abfrage verwendet. Wenn Sie über einen verstreuten Satz von Werten verfügen, werden sie zu einem kleineren Satz bestimmter Werte gruppiert.

Alias: `floor`

**Syntax**

     bin(value, roundTo)
     floor(value, roundTo)

**Argumente**

* *value:* Eine Zahl, ein Datum oder ein Zeitraum. 
* *roundTo:* Die bin-Größe. Eine Zahl, ein Datum oder ein Zeitraum zum Teilen des Werts ( *value*). 

**Rückgabe**

Das nächste Vielfache von *roundTo* unter dem Wert (*value*).  

    (toint(value/roundTo)) * roundTo

**Beispiele**

| Expression | Ergebnis |
| --- | --- |
| `bin(4.5, 1)` |`4.0` |
| `bin(time(16d), 7d)` |`14d` |
| `bin(datetime(1953-04-15 22:25:07), 1d)` |`datetime(1953-04-15)` |

Der folgende Ausdruck berechnet ein Histogramm der Dauer mit einer Bucketgröße von 1 Sekunde:

```AIQL

    T | summarize Hits=count() by bin(Duration, 1s)
```

### <a name="exp"></a>exp
    exp(v)   // e raised to the power v
    exp2(v)  // 2 raised to the power v
    exp10(v) // 10 raised to the power v


### <a name="floor"></a>floor
Ein Alias für [`bin()`](#bin).

### <a name="gamma"></a>Gamma
Die [Gammafunktion](https://en.wikipedia.org/wiki/Gamma_function)

**Syntax**

    gamma(x)

**Argumente**

* *x:* Eine reelle Zahl

Bei positiven ganzen Zahlen gilt: `gamma(x) == (x-1)!`, z.B. `gamma(5) == 4 * 3 * 2 * 1`.

Siehe auch [Loggamma](#loggamma).

### <a name="log"></a>log
    log(v)    // Natural logarithm of v
    log2(v)   // Logarithm base 2 of v
    log10(v)  // Logarithm base 10 of v


`v` sollte eine reelle Zahl > 0 sein. Andernfalls wird Null zurückgegeben.

### <a name="loggamma"></a>Loggamma
Der natürliche Logarithmus des absoluten Werts der [Gammafunktion](#gamma)

**Syntax**

    loggamma(x)

**Argumente**

* *x:* Eine reelle Zahl

### <a name="rand"></a>rand
Ein Zufallszahlengenerator.

* `rand()` : Eine reelle Zahl zwischen 0,0 und 1,0.
* `rand(n)` : Eine ganze Zahl zwischen 0 und n-1.

### <a name="sqrt"></a>sqrt
Die Quadratwurzelfunktion.  

**Syntax**

    sqrt(x)

**Argumente**

* *x:* Eine reelle Zahl >= 0.

**Rückgabe**

* Eine positive Zahl, sodass Folgendes gilt: `sqrt(x) * sqrt(x) == x`
* `null`, wenn das Argument negativ ist oder nicht in einen `real`-Wert konvertiert werden kann. 

### <a name="toint"></a>toint
    toint(100)        // cast from long
    toint(20.7) == 20 // nearest int below double
    toint(20.4) == 20 // nearest int below double
    toint("  123  ")  // parse string
    toint(a[0])       // cast from dynamic
    toint(b.c)        // cast from dynamic


### <a name="todouble"></a>todouble
    todouble(20) == 20.0 // conversion from long or int
    todouble(" 12.34 ")  // parse string
    todouble(a[0])       // cast from dynamic
    todouble(b.c)        // cast from dynamic


### <a name="tolong"></a>tolong
    tolong(20.7) == 20 // conversion from double
    tolong(20.4) == 20 // conversion from double
    tolong("  123  ")  // parse string
    tolong(a[0])       // cast from dynamic
    tolong(b.c)        // cast from dynamic

## <a name="numeric-series"></a>Zahlenfolge

[series_fir](#seriesfir) | [series\_fit\_line](#seriesfitline) | [series\_fit\_2lines](#seriesfit2lines) | [series_iir](#seriesiir) |  [series_periods](#seriesperiods) | [series_stats](#seriesstats)  

### <a name="seriesfir"></a>series_fir
Die Funktion „series_fir()“ wendet einen [Filter mit endlicher Impulsantwort](https://wikipedia.org/wiki/Finite_impulse_response) auf eine Reihe an (die von einer dynamischen Spalte mit numerischem Array dargestellt wird).

Durch die Angabe der Filterkoeffizienten kann sie für die Berechnung des gleitenden Durchschnitts, der Glättung, der Erkennung von Änderungen und viele weitere Anwendungsfälle eingesetzt werden.

Die Funktion verwendet die Spalte mit dem dynamischen Array und einem statischen, dynamischen Array der Filterkoeffizienten als Eingabe und wendet die Filter auf die Spalte an. Sie gibt eine neue dynamische Array-Spalte mit der gefilterten Ausgabe aus. 

**Syntax**

`series_fir(x, filter [, normalize[, center]])`

**Argumente**

* *x:* Dynamische Array-Zelle, die ein Array aus numerischen Werten – in der Regel die Ausgabe der Operatoren [make-series](#make-series-operator) oder [makelist](#makelist-operator) – ist.
* *filter:* Ein optionaler boolescher Wert, der angibt, ob die Filterkoeffizienten normalisiert (d.h. durch die Summe dividiert) werden sollen. „normalize“ ist standardmäßig auf „true“ festgelegt. Wenn der Filter negative Werte enthält, kann das automatische Normalisieren nicht durchgeführt werden, und der Wert für das Normalisieren muss explizit auf „false“ festgelegt werden.
* *normalize:* Optionaler boolescher Wert, der angibt, ob der Filter normalisiert werden sollen. „normalize“ ist standardmäßig auf „true“ festgelegt. Wenn der Filter negative Werte enthält, muss „normalize“ auf „false“ festgelegt werden. 
* *center:* Ein optionaler boolescher Wert, der angibt, ob der Filter symmetrisch auf ein Zeitfenster vor und nach dem aktuellen Zeitpunkt oder auf ein Zeitfenster ab dem aktuellen Zeitpunkt rückwärts angewendet wird. Standardmäßig ist „center“ auf „false“ festgelegt, was zum Szenario für das Streaming von Daten passt, wo wir den Filter nur auf aktuelle und ältere Punkte anwendet können. Allerdings können Sie den Wert bei der Ad-hoc-Verarbeitung auf „true“ festlegen, um diese mit der Zeitreihe zu synchronisieren (siehe folgende Beispiele). Technisch gesehen steuert dieser Parameter die Verzögerung der Filtergruppe.

**Beispiele**

Zum Berechnen eines gleitenden Durchschnitts von 5 Punkten legen Sie Folgendes fest: filter=[1,1,1,1,1] und normalize=true (Standard). Beachten Sie die Auswirkung von center=false (Standard) im Vergleich zu „true“:

```AIQL
range t from bin(now(), 1h)-23h to bin(now(), 1h) step 1h
| summarize t=makelist(t)
| project id='TS', val=dynamic([0,0,0,0,0,0,0,0,0,10,20,40,100,40,20,10,0,0,0,0,0,0,0,0]), t
| extend 5h_MovingAvg=series_fir(val, dynamic([1,1,1,1,1])),
         5h_MovingAvg_centered=series_fir(val, dynamic([1,1,1,1,1]), true, true)
| render timechart
```

Diese Abfrage gibt Folgendes zurück:

* *5h_MovingAvg:* Filter für gleitenden Durchschnitt von 5 Punkten. Die Spitze wird geglättet und um (5-1)/2 = 2 Stunden verschoben.
* *5h_MovingAvg_centered:* Identisch, aber die Einstellung „center=true“ bewirkt, dass die Spitze an ihrer ursprünglichen Position bleibt.

![Abfrageergebnisse](./media/app-insights-analytics-reference/series-fir-1.png) (Deaktivieren Sie „split“ in den Diagrammsteuerelementen, um mehrere Zeilen anzuzeigen.)

Zum Berechnen der Differenz zwischen einem Punkt und dem vorherigen Punkt legen Sie „filter=[1,-1]“ fest:

```AIQL
range t from bin(now(), 1h)-11h to bin(now(), 1h) step 1h
| summarize t=makelist(t)
| project id='TS',t,value=dynamic([0,0,0,0,2,2,2,2,3,3,3,3])
| extend diff=series_fir(value, dynamic([1,-1]), false, false)
| render timechart
```


![Abfrageergebnisse](./media/app-insights-analytics-reference/series-fir-2.png)


### <a name="seriesfitline"></a>series\_fit\_line
Die Funktion „series_fit_line()“ erfordert eine Spalte mit einem dynamischen numerischen Array als Eingabe und führt eine lineare Regression aus, um die Zeile zu finden, die am besten geeignet ist. Diese Funktion sollte für Zeitreihenarrays, die der Ausgabe des Operators „make-series“ entsprechen, verwendet werden. Sie generiert eine dynamische Spalte mit den folgenden Feldern:

* *slope:* Steigung der geschätzten Linie (Dies ist `a` aus `y=ax+b`).
* *interception:* Abfangen der geschätzten Linie (Dies ist `b` aus `y=ax+b`).
* *rsquare:* „r-square“ ist ein Standardmaß der Eignungsqualität. Es ist eine Zahl im Bereich [0-1], wobei 1 die beste Option ist und 0 bedeutet, dass die Daten unsortiert sind und nicht jede beliebige Zeile passen.
* *variance:* Varianz der Eingabedaten.
* *rvariance:* Verbleibende Varianz, also die Abweichung zwischen den Eingabedatenwerten und den geschätzten Werten.
* *line_fit:* Numerisches Array, das eine Reihe von Werten der besten Linie enthält. Die Reihenlänge entspricht der Länge des Eingabearrays. Sie wird hauptsächlich für Diagramme verwendet.

Am besten verwenden Sie diese, indem Sie sie auf die Ergebnisse des Operators „make-series“ anwenden.

**Syntax**
    
    series_fit_line(x)

**Argumente**

* `x:` Dynamisches Array von numerischen Werten. Beachten Sie, dass die Funktion erwartet, dass alle Zeilen die gleiche Anzahl von Arrayelementen haben. Andernfalls werden leere Ergebnisse zurückgegeben. 

**Beispiele**

```AIQL
range x from 1 to 1 step 1
| project id=' ', x=range(bin(now(), 1h)-11h, bin(now(), 1h), 1h), y=dynamic([2,5,6,8,11,15,17,18,25,26,30,30])
| extend (s,i,rs,v,rv,LineFit)=series_fit_line(y)
| render timechart 
```

![Abfrageergebnisse](./media/app-insights-analytics-reference/series-fit-line.png)

|Slope|Interception|RSquare|Variance|RVariance|LineFit|
|---|---|---|---|---|---|
|0.982|2.730|98.628|1.686|-1.666| 1064, 3.7945, 6.526, 9.256, 11.987, 14.718, 17.449, 20.180, 22.910, 25.641, 28.371, |

### <a name="seriesfit2lines"></a>series\_fit\_2lines

Die Funktion „series_fit_2lines()“ wendet zwei Segmente der linearen Regression auf eine (Zeit-) Reihe an, um Trendänderungen in einer Reihe zu identifizieren und zu quantifizieren. Die Funktion durchläuft die Reihenindizes und teilt in jeder Iteration die Reihe in zwei Teile, passt eine separate Zeile (mithilfe von series_fit_line()) an die einzelnen Teile an und berechnet den Gesamtwert für „r-square“. Die beste Teilung ist diejenige, die „r-square“ maximiert hat. Die Funktion gibt die dazugehörigen Parameter zurück:

* *rsquare:* „r-square“ ist ein Standardmaß der Eignungsqualität. Es ist eine Zahl im Bereich [0-1], wobei 1 die beste Option ist und 0 bedeutet, dass die Daten unsortiert sind und nicht in jede beliebige Zeile passen.
* *split_idx:* Der Index zum Trennen in 2 Segmente (nullbasiert)
* *variance:* Varianz der Eingabedaten
* *rvariance:* Verbleibende Varianz, also die Abweichung zwischen den Eingabedatenwerten und den geschätzten Werten (durch die „2-lines“-Segmente).
* *line_fit:* Numerisches Array, das eine Reihe von Werten der besten Linie enthält. Die Reihenlänge entspricht der Länge des Eingabearrays. Sie wird hauptsächlich für Diagramme verwendet.
* *right_rsquare:* „r-square“ der Zeile auf der rechten Seite der Teilung, siehe series_fit_line()
* *right_slope:* Steigung der rechts geschätzten Zeile (Dies ist „a“ aus „y=ax+b“)
* *right_interception:* Abfangen der geschätzten linken Linie (Dies ist „b“ aus „y=ax+b“).
* *right_variance:* Varianz der Eingabedaten auf der rechten Seite der Teilung
* *right_variance:* Verbleibende Varianz der Eingabedaten auf der rechten Seite der Teilung
* *left_rsquare:* r-square der Zeile auf der linken Seite der Teilung, siehe „series_fit_line()“
* *left_slope:* Steigung der linken geschätzten Zeile (Dies ist „a“ aus „y=ax+b“)
* *left_interception:* Abfangen der geschätzten linken Linie (Dies ist „b“ aus „y=ax+b“).
* *left_variance:* Varianz der Eingabedaten auf der linken Seite der Teilung
* *left_variance:* Verbleibende Varianz der Eingabedaten auf der linken Seite der Teilung

Beachten Sie, dass diese Funktion mehrere Spalten zurückgibt und daher nicht als Argument für eine andere Funktion verwendet werden kann.

**Syntax**

    project series_fit_2lines(x)

Gibt alle oben genannten Spalten mit den folgenden Namen zurück: `series_fit_2lines_x_rsquare, series_fit_2lines_x_split_idx and etc.`

    project (rs, si, v)=series_fit_2lines(x)

Gibt die folgenden Spalten zurück: `rs (r-square), si (split index), v (variance)` und der Rest wird wie folgt aussehen: `series_fit_2lines_x_rvariance, series_fit_2lines_x_line_fit` usw.

    extend (rs, si, v)=series_fit_2lines(x)

Gibt nur Folgendes zurück: rs (r-square), si (split index) und v (variance).

**Argumente**

* *x* Dynamisches Array von numerischen Werten. 

Am besten verwenden Sie diese, indem Sie sie auf die Ergebnisse des Operators „make-series“ anwenden.

**Beispiele**

```AIQL
range x from 1 to 1 step 1
| project id=' ', x=range(bin(now(), 1h)-11h, bin(now(), 1h), 1h), y=dynamic([1,2.2, 2.5, 4.7, 5.0, 12, 10.3, 10.3, 9, 8.3, 6.2])
| extend (Slope,Interception,RSquare,Variance,RVariance,LineFit)=series_fit_line(y), (RSquare2, SplitIdx, Variance2,RVariance2,LineFit2)=series_fit_2lines(y)
| project id, x, y, LineFit, LineFit2
| render timechart
```


![Abfrageergebnisse](./media/app-insights-analytics-reference/series-fit-2lines.png)

### <a name="seriesiir"></a>series_iir

Die Funktion „series_fir()“ wendet einen Filter mit unendlicher Impulsantwort auf eine Reihe an (die von einer dynamischen Spalte mit numerischem Array dargestellt wird).

Durch Angeben der Filterkoeffizienten können sie z.B. zum Berechnen der kumulative Summe der Reihe, Glättungsmodusvorgänge als auch für verschiedene Hochpass-, Bandpass- und Tiefpass-Filter verwendet werden.

Die Funktion verwendet die Spalte mit dem dynamischen Array und zwei statischen, dynamischen Arrays der Filterkoeffizienten „a“ und „b“ als Eingabe und wendet die Filter auf die Spalte an. Sie gibt eine neue dynamische Array-Spalte mit der gefilterten Ausgabe aus. 

**Syntax**

    series_iir(x, b , a)

**Argumente**


* *x:* Dynamische Array-Zelle, die ein Array aus numerischen Werten und in der Regel die Ausgabe der Operatoren „make-series“ oder „makelist“ ist.
* *b:* Ein konstanter Ausdruck, der die Zählerkoeffizienten des Filters (als dynamisches Array von numerischen Werten gespeichert) enthält.
* *a:* Ein konstanter Ausdruck wie „b“. Enthält die Nennerkoeffizienten des Filters.

    Das erste Element von „a“ (d.h. a[0]) darf nicht NULL sein (um das Dividieren durch 0 zu vermeiden; siehe folgende Formel).

**Weitere Informationen zur rekursiven Formel des Filters**

Mit dem Eingabearray X und den Koeffizientenarrays a, b der Längen `n_a` und `n_b` wird die Übertragungsfunktion des Filters, die das Ausgabearray Y generiert, folgendermaßen definiert (siehe auch Wikipedia): 

    Y[i] = 1/a[0] * ( b[0]*X[i] + b[1]*X[i-1] + … 
                 + b[n_b-1]*X[i-n_b-1] — a[1]*Y[i-1] – a[2]*Y[i-2] – …
                 – a[n_a-1]*Y[i-n_a-1] )


**Beispiele**

Die Berechnung der kumulative Summe kann mit dem Filter „iir“ mit den Koeffizienten „a=[1 -1]“ und „b=[1]“ durchgeführt werden: 

```AIQL
let x = range(1.0, 10, 1);
range t from 1 to 1 step 1
| project x=x, y = series_iir(x, dynamic([1]), dynamic([1,-1]))
| mvexpand x, y
```

|x|y|
|---|---|
|1,0|1,0|
|2,0|3.0|
|3.0|6,0|
|4,0|10,0|
### <a name="seriesoutliers"></a>series_outliers 

Bei der Funktion „series_outliers()“ wird eine Spalte mit einem dynamischen Array als Eingabe verwendet und ein dynamisches numerisches Array gleicher Länge als Eingabe generiert. Jeder Wert des Arrays steht für eine Punktzahl, die eine mögliche Anomalie gemäß Tukey-Test angibt. Ein Wert, der höher als 1,5 oder kleiner als -1,5 ist, weist auf einen Anstieg bzw. einen Abfall der Anomalie in demselben Element der Eingabe hin.  

**Syntax**  

```
series_outliers(x,kind,ignore_val,min_percentile,max_percentile)  
```
**Argumente** 
* *x:* Dynamische Arrayzelle, die ein Array aus numerischen Werten ist. Für die Werte wird angenommen, dass sie äquidistant sind, da es andernfalls zu unerwarteten Ergebnissen kommt.  
* *kind:* Algorithmus der Ausreißererkennung. Derzeit werden „tukey“ und „ctukey“ unterstützt. Der Standardwert ist „ctukey“.  
* *ignore_val:* Numerischer Wert, der auf fehlende Werte der Serie hinweist. Standardwert ist „double(null)“.
* *min_percentile:* Für die Berechnung des normalen Bereichs zwischen Quantilen. Standardwert ist 10 (nur „ctukey“).
* *max_percentile:* Für die Berechnung des normalen Bereichs zwischen Quantilen. Standardwert ist 90 (nur „ctukey“).

In der folgenden Tabelle sind die Unterschiede zwischen „tukey“ und „ctukey“ aufgeführt:

|Algorithmus|Quantil-Standardbereich|Unterstützt benutzerdefinierten Quantilbereich|
|---------|----------------------|------------------------------|
|„tukey“|25%/75%|Nein|
|„ctukey“|10%/90%|Ja|

**Wichtiger Hinweis** Am besten verwenden Sie diese Funktion, indem Sie sie auf die Ergebnisse des Operators `make-series` anwenden.

**Beispiele** 

Folgende Eingabe:   
```
[30,28,5,27,31,38,29,80,25,37,30]
``` 
Rückgabe von „series_outliers()“:  
[0.0,0.0,-3.206896551724138,-0.1724137931034483,0.0,2.6666666666666667,0.0,16.666666666666669,-0.4482758620689655,2.3333333333333337,0.0]

Dies bedeutet, dass – verglichen zum Rest der Serie – 5 eine abnehmende Anomalie und 80 eine zunehmende Anomalie ist. 

### <a name="seriesperiods"></a>series_periods

Die Funktion „series_periods()“ findet die wichtigsten Punkte, die in einer Zeitreihe vorhanden sind.

Beispielsweise zeichnet sich eine Metrik, die den Datenverkehr einer Anwendung misst, durch zwei signifikante Zyklen aus: wöchentlich und täglich. Mit solch einem Zeitreihenmodell muss „series_periods()“ diese beiden dominanten Zeiträume erkennen.

Diese Funktion nimmt eine Spalte mit einem dynamischen Array von Zeitreihen (in der Regel die Ausgabe des Operators „make-series“), zwei echte Zahlen, die die Mindest- und Maximalgröße des Zeitraums (d.h. Anzahl an Containern, für 1h beträgt die Containergröße eines Tageszeitraums z.B. 24) für die Suche und eine lange Zahl, die die Gesamtzahl an Zeiträumen, die die Funktion durchsuchen soll, als Eingabe. Die Ausgabe ist ein dynamisches Array, das die Größe der gefundenen Zeiträume nach der Bedeutung der Zeiträume in den Daten sortiert, enthält.

**Syntax**

    series_periods(x, min_period, max_period, num_periods)`

**Argumente**

* *x:* Dynamische Array-Zelle, die ein Array aus numerischen Werten und in der Regel die Ausgabe der Operatoren „make-series“ oder „makelist“ ist.
* *min_period:* Eine reale Zahl, die den minimalen Zeitraum für die Suche angibt.
* *max_period:* Eine reale Zahl, die den maximalen Zeitraum für die Suche angibt.
* *num_periods:* Eine lange Zahl, die die erforderliche maximale Anzahl an Zeiträumen angibt. Dies wird die Länge des dynamischen Ausgabearrays sein.

**Wichtige Hinweise**

* Der Algorithmus hinter „series\_periods()“ benötigt mindestens 4 Punkte in einem Zeitraum, um ihn zu erkennen. Daher beträgt der Mindestwert für „min_period“ 4. Wenn „min_period“ auf einen niedrigeren Wert festgelegt ist, ersetzt die Funktion den Wert durch 4.
* Der maximale Wert für „max_period“ ist die Hälfte der Länge der Eingabereihe. Wenn „max_period“ auf einen höheren Wert festgelegt ist, schneidet die Funktion diesen Wert ab.
* Wie oben erwähnt, ergeben sich die resultierenden Zeiträume durch die Einheiten der Diskretisierung. Wenn z.B. die ursprüngliche Reihe einen täglichen Zeitraum aufweist und durch stündliche Container aggregiert wurde, beträgt ein täglicher Zeitraum in der Ausgabe 24. Wenn die Daten nach Minute aggregiert werden, beträgt die Ausgabe 60*24=1.440.
* Sie sollten den Mindestzeitraum „min\_period“ etwas unterhalb und den Maximalzeitraum „max\_period“ etwas oberhalb der Zeiträume festlegen, die Sie in der Zeitreihe finden möchten. Wenn Sie z.B. ein stündlich aggregiertes Signal haben und nach täglichen oder wöchentlichen Zeiträume suchen (also 24 bzw. 168), legen Sie min\_period=0,824 und *max\_period=1,2*168 fest.
* Die Länge des dynamischen Ausgabearrays ist „num\_of\_periods“. Wenn die Funktion weniger signifikante Zeiträume als „num\_of\_periods“ findet, wird der Rest der Arrayeinträge auf 0 festgelegt.
* Die eingegebene Zeitreihe muss regulär sein, d.h. in konstanten Containern aggregiert werden (was immer der Fall ist, wenn er mit „make-series“ erstellt wurde). Andernfalls ist die Ausgabe bedeutungslos.

**Beispiel**

Die folgende Abfrage bettet z.B. eine Momentaufnahme eines Monats des Datenverkehrs einer Anwendung ein, die zweimal am Tag (d.h. alle 12 Stunden) aggregiert wird.

```AIQL
range x from 1 to 1 step 1
| project y=dynamic([80,139,87,110,68,54,50,51,53,133,86,141,97,156,94,149,95,140,77,61,50,54,47,133,72,152,94,148,105,162,101,160,87,63,53,55,54,151,103,189,108,183,113,175,113,178,90,71,62,62,65,165,109,181,115,182,121,178,114,170])
| project x=range(1, arraylength(y), 1), y  
| render linechart
```

![Abfrageergebnisse](./media/app-insights-analytics-reference/series-periods1.png)

Das Ausführen von „series_periods()“ auf diese Reihe resultiert im wöchentlichen Zeitraum (14 Punkte lang):

```AIQL
range x from 1 to 1 step 1
| project y=dynamic([80,139,87,110,68,54,50,51,53,133,86,141,97,156,94,149,95,140,77,61,50,54,47,133,72,152,94,148,105,162,101,160,87,63,53,55,54,151,103,189,108,183,113,175,113,178,90,71,62,62,65,165,109,181,115,182,121,178,114,170])
| project x=range(1, arraylength(y), 1), y  
| project periods = series_periods(y, 4.0, 50.0, 2)
```

|Zeiträume|
|---|
|[14.0, 0.0]|

### <a name="seriesstats"></a>series_stats

Die Funktion „series_stats()“ erfordert eine Spalte mit einem dynamischen numerischen Array als Eingabe an und berechnet die folgenden Spalten:

* *min:* Mindestwert im Eingabearray
* *min_idx:* Minimalwert im Eingabearray
* *max:* Maximalwert im Eingabearray
* *max_idx:* Maximalwert im Eingabearray
* *average:* Durchschnittswert des Eingabearrays
* *variance:* Stichprobenvarianz des Eingabearrays
* *stdev:* Stichproben-Standardabweichung des Eingabearrays

Beachten Sie, dass diese Funktion mehrere Spalten zurückgibt und daher nicht als Argument für eine andere Funktion verwendet werden kann.

**Syntax**

    project series_stats(x)

Gibt alle oben genannten Spalten mit den folgenden Namen zurück: serie\_stats\_x\_min, series\_stats\_x\_min\_idx usw.

    project (m, mi)=series_stats(x)

Gibt die folgenden Spalten zurück: `m (min), mi (min_idx)` und der Rest wird wie folgt aussehen: `series_stats_x_max, series_stats_x_line_max_idx` usw.

    extend (m, mi)=series_stats(x)

Gibt nur: „m“ (min.) und „mi“ (min_idx) zurück.

**Argumente**

* *x:* Dynamische Arrayzelle, die ein Array aus numerischen Werten ist. 

**Beispiele**

Für die folgende Eingabe:

` [1,6,11,16,21,26,31,36,41,46,51,56,61,66,71,76,81,86,91,96]`

„series_stats()“ gibt zurück:

|Min|min\_idx|max|max\_idx|average|variance|stdev|
|---|---|---|---|---|---|---|
|1,0|1|96.0|19|48.5|29.58039891549808|875.0|


## <a name="date-and-time"></a>Datum und Uhrzeit
[ago](#ago) | [dayofmonth](#dayofmonth) | [dayofweek](#dayofweek) |  [dayofyear](#dayofyear) |[datepart](#datepart) | [endofday](#endofday) | [endofmonth](#endofmonth) | [endofweek](#endofweek) | [endofyear](#endofyear) | [getmonth](#getmonth)|  [getyear](#getyear) | [now](#now) | [startofday](#startofday) | [startofmonth](#startofmonth) | [startofweek](#startofweek) | [startofyear](#startofyear) | [todatetime](#todatetime) | [totimespan](#totimespan) | [weekofyear](#weekofyear)

Ein timespan-Wert stellt einen Zeitraum wie beispielsweise drei Stunden oder ein Jahr dar.

Ein datetime-Wert stellt eine Datums-/Uhrzeitangabe nach einem bestimmten Kalender/einer bestimmten Uhr in UTC dar.

Es gibt keinen separaten Typ „date“. Verwenden Sie einen Ausdruck wie `bin(timestamp, 1d)`, um die Zeit aus einem datetime-Wert zu entfernen.

### <a name="date-and-time-literals"></a>Datum und Uhrzeit – Literale
|  |  |
| --- | --- |
| **datetime** | |
| `datetime("2015-12-31 23:59:59.9")`<br/>`datetime("2015-12-31")` |Zeiten werden immer in UTC angegeben. Durch das Auslassen des Datums wird eine Zeit am heutigen Tag angegeben. |
| `now()` |Die aktuelle Zeit. |
| `now(`-*timespan*`)` |`now()-`*timespan* |
| `ago(`*timespan*`)` |`now()-`*timespan* |
| **timespan** | |
| `2d` |2 Tage |
| `1.5h` |1,5 Stunden |
| `30m` |30 Minuten |
| `10s` |10 Sekunden |
| `0.1s` |0,1 Sekunde |
| `100ms` |100 Millisekunden |
| `10microsecond` | |
| `1tick` |100 ns |
| `time("15 seconds")` | |
| `time("2")` |2 Tage |
| `time("0.12:34:56.7")` |`0d+12h+34m+56.7s` |

### <a name="date-and-time-expressions"></a>Datum und Uhrzeit – Ausdrücke
| Expression | Ergebnis |Effekt|
| --- | --- |---|
| `datetime("2015-01-02") - datetime("2015-01-01")` |`1d` | Zeitliche Differenz|
| `datetime("2015-01-01") + 1d` |`datetime("2015-01-02")` | Tage addieren |
| `datetime("2015-01-01") - 1d` |`datetime("2014-12-31")` | Tage subtrahieren|
| `2h * 24` |`2d` |Timespan-Vielfache|
| `2d` / `2h` |`24` |Timespan-Division|
| `datetime("2015-04-15T22:33") % 1d` |`timespan("22:33")` |Zeit aus einem datetime-Wert|
| `bin(datetime("2015-04-15T22:33"), 1d)` |`datetime("2015-04-15T00:00")` |Datum aus einem datetime-Wert|
|  | ||
| `<` ||Kleiner |
| `<=` ||Kleiner als oder gleich |
| `>` ||Größer |
| `>=` ||Größer als oder gleich |
| `<>` ||Ungleich |
| `!=` ||Ungleich |

### <a name="ago"></a>ago
Subtrahiert den angegebenen Zeitraum von der aktuellen UTC-Uhrzeit. Wie `now()`kann diese Funktion mehrmals in einer Anweisung verwendet werden, und die UTC-Uhrzeit, auf die verwiesen wird, ist für alle Instanziierungen identisch.

**Syntax**

    ago(a_timespan)

**Argumente**

* *a_timespan:* Intervall, das von der aktuellen UTC-Uhrzeit (`now()`) subtrahiert werden soll.

**Rückgabe**

    now() - a_timespan

**Beispiel**

Alle Zeilen mit einem Zeitstempel der letzten Stunde:

```AIQL

    T | where timestamp > ago(1h)
```

### <a name="datepart"></a>datepart
    datepart("Day", datetime(2015-12-14)) == 14

Extrahiert einen bestimmten Abschnitt eines Datums als ganze Zahl.

**Syntax**

    datepart(part, datetime)

**Argumente**

* `part:String` – {„Jahr“, „Monat“, „Tag“, „Stunde“, „Minute“, „Sekunde“, „Millisekunde“, „Mikrosekunde“, „Nanosekunde“}
* `datetime`

**Rückgabe**

Long-Wert, der den angegebenen Abschnitt darstellt.

### <a name="dayofmonth"></a>dayofmonth
    dayofmonth(datetime("2016-05-15")) == 15 

Die Ordinalzahl des Tags im Monat.

**Syntax**

    dayofmonth(a_date)

**Argumente**

* `a_date`: Ein `datetime`-Wert.

### <a name="dayofweek"></a>dayofweek
    dayofweek(datetime("2015-12-14")) == 1d  // Monday

Die Anzahl von Tagen (als ganze Zahl) seit dem vorherigen Sonntag als `timespan`-Wert.

**Syntax**

    dayofweek(a_date)

**Argumente**

* `a_date`: Ein `datetime`-Wert.

**Rückgabe**

Die Dauer (als `timespan` -Wert) seit Mitternacht zu Beginn des vorhergehenden Sonntags, abgerundet auf die Anzahl von Tagen als ganze Zahl.

**Beispiele**

```AIQL
dayofweek(1947-11-29 10:00:05)  // time(6.00:00:00), indicating Saturday
dayofweek(1970-05-11)           // time(1.00:00:00), indicating Monday
```

### <a name="dayofyear"></a>dayofyear
    dayofyear(datetime("2016-05-31")) == 152 
    dayofyear(datetime("2016-01-01")) == 1 

Die Ordinalzahl des Tags im Jahr.

**Syntax**

    dayofyear(a_date)

**Argumente**

* `a_date`: Ein `datetime`-Wert.

<a name="endofday"></a><a name="endofweek"></a><a name="endofmonth"></a><a name="endofyear"></a>

### <a name="endofday-endofweek-endofmonth-endofyear"></a>endofday, endofweek, endofmonth, endofyear
    dt = datetime("2016-05-23 12:34")

    endofday(dt) == 2016-05-23T23:59:59.999
    endofweek(dt) == 2016-05-28T23:59:59.999 // Saturday
    endofmonth(dt) == 2016-05-31T23:59:59.999 
    endofyear(dt) == 2016-12-31T23:59:59.999 


### <a name="getmonth"></a>getmonth
Rufen Sie die Monatsnummer (1-12) aus einem datetime-Wert ab.

**Beispiel**

    ... | extend month = getmonth(datetime(2015-10-12))

    --> month == 10

### <a name="getyear"></a>getyear
Rufen Sie das Jahr aus einem datetime-Wert ab.

**Beispiel**

    ... | extend year = getyear(datetime(2015-10-12))

    --> year == 2015

### <a name="now"></a>now
    now()
    now(-2d)

Die aktuelle UTC-Uhrzeit, die optional durch einen angegebenen Zeitraum versetzt wird. Diese Funktion kann mehrmals in einer Anweisung verwendet werden, und die Uhrzeit, auf die verwiesen wird, ist für alle Instanzen identisch.

**Syntax**

    now([offset])

**Argumente**

* *offset:* Ein `timespan`-Wert, der der aktuellen UTC-Uhrzeit hinzugefügt wird. Standard: 0.

**Rückgabe**

Die aktuelle UTC-Uhrzeit als `datetime`-Wert.

    now() + offset

**Beispiel**

Bestimmt das Intervall seit dem vom Prädikat identifizierten Ereignis:

```AIQL
T | where ... | extend Elapsed=now() - timestamp
```

<a name="startofday"></a><a name="startofweek"></a><a name="startofmonth"></a><a name="startofyear"></a>

### <a name="startofday-startofweek-startofmonth-startofyear"></a>startofday, startofweek, startofmonth, startofyear
    date=datetime("2016-05-23 12:34:56")

    startofday(date) == datetime("2016-05-23")
    startofweek(date) == datetime("2016-05-22") // Sunday
    startofmonth(date) == datetime("2016-05-01")
    startofyear(date) == datetime("2016-01-01")



### <a name="todatetime"></a>todatetime
Alias: `datetime()`

     todatetime("2016-03-28")
     todatetime("03/28/2016")
     todatetime("2016-03-28 14:34:00")
     todatetime("03/28/2016 2:34pm")
     todatetime("2016-03-28T14:34.5Z")
     todatetime(a[0]) 
     todatetime(b.c) 

Überprüft, ob eine Zeichenfolge ein gültiges Datum ist:

     iff(notnull(todatetime(customDimensions.myDate)),
         ..., ...)


### <a name="totimespan"></a>totimespan
Alias: `timespan()`

    totimespan("21d")
    totimespan("21h")
    totimespan(request.duration)

### <a name="weekofyear"></a>weekofyear
    weekofyear(datetime("2016-05-14")) == 21
    weekofyear(datetime("2016-01-03")) == 1
    weekofyear(datetime("2016-12-31")) == 53

Das ganzzahlige Ergebnis stellt die Wochennummer nach ISO-8601-Standard dar. Der erste Tag einer Woche ist Sonntag, und die erste Woche des Jahres ist die Woche, in die der erste Donnerstag des Jahres fällt. (Die letzten Tage eines Jahres können daher einige Tage der 1. Woche des Folgejahres enthalten, und die ersten Tage können einige Tage der Woche 52 oder 53 des vorherigen Jahres enthalten.)

## <a name="string"></a>String
[countof](#countof) | [extract](#extract) | [extractjson](#extractjson)  | [isempty](#isempty) | [isnotempty](#isnotempty) | [notempty](#notempty) | [parseurl](#parseurl) | [replace](#replace) | [split](#split) | [strcat](#strcat) | [strlen](#strlen) | [substring](#substring) | [tolower](#tolower) | [tostring](#tostring) | [toupper](#toupper)

### <a name="string-literals"></a>Zeichenfolgenliterale
Die Regeln sind mit JavaScript identisch.

Zeichenfolgen können entweder in einfachen oder doppelten Anführungszeichen eingeschlossen sein. 

Es wird ein umgekehrter Schrägstrich (`\`) verwendet, um Zeichen wie z.B. `\t` (Tabstopp), `\n` (Zeilenvorschub) und Instanzen des einschließenden Anführungszeichens mit einem Escapezeichen zu versehen.

* `'this is a "string" literal in single \' quotes'`
* `"this is a 'string' literal in double \" quotes"`
* `@"C:\backslash\not\escaped\with @ prefix"`

### <a name="obfuscated-string-literals"></a>Verborgene Zeichenfolgenliterale
Verborgene Zeichenfolgenliterale sind Zeichenfolgen, die Analytics bei der Ausgabe der Zeichenfolge ausblendet (etwa bei der Ablaufverfolgung). Bei diesem Vorgang werden alle verborgenen Zeichen durch ein Startzeichen (`*`) ersetzt.

Stellen Sie zum Erstellen eines verborgenen Zeichenfolgenliterals `h` oder „H“ voran. Zum Beispiel:

```
h'hello'
h@'world' 
h"hello"
```

### <a name="string-comparisons"></a>Zeichenfolgenvergleiche
| Operators | Beschreibung | Groß-/Kleinschreibung | Beispiel für „True“ |
| --- | --- | --- | --- |
| `==` |Equals |Ja |`"aBc" == "aBc"` |
| `<>` `!=` |Not Equals |Ja |`"abc" <> "ABC"` |
| `=~` |Equals |Nein |`"abc" =~ "ABC"` <br/>`boolAsString =~ "true"` |
| `!~` |Not Equals |Nein |`"aBc" !~ "xyz"` |
| `has` |Rechte Seite (RS) ist ein ganzer Begriff innerhalb der linken Seite (LS) |Nein |`"North America" has "america"` |
| `!has` |RS ist kein vollständiger Begriff innerhalb der LS |Nein |`"North America" !has "amer"` |
| `hasprefix` |RS ist ein Präfix eines Begriffs in LS |Nein |`"North America" hasprefix "ame"` |
| `!hasprefix` |RS ist kein Präfix eines Begriffs in LS |Nein |`"North America" !hasprefix "mer"` |
| `hassuffix` |RS ist ein Suffix eines Begriffs in LS |Nein |`"North America" hassuffix "rth"` |
| `!hassuffix` |RS ist kein Suffix eines Begriffs in LS |Nein |`"North America" !hassuffix "mer"` |
| `contains` |RS tritt als Teilzeichenfolge von LS auf |Nein |`"FabriKam" contains "BRik"` |
| `!contains` |RS tritt nicht in LS auf |Nein |`"Fabrikam" !contains "xyz"` |
| `containscs` |RS tritt als Teilzeichenfolge von LS auf |Ja |`"FabriKam" contains "Kam"` |
| `!containscs` |RS tritt nicht in LS auf |Ja |`"Fabrikam" !contains "Kam"` |
| `startswith` |RS ist eine anfängliche Teilzeichenfolge von LS |Nein |`"Fabrikam" startswith "fab"` |
| `!startswith` |RS ist keine anfängliche Teilzeichenfolge von LS |Nein |`"Fabrikam" !startswith "abr"` |
| `endswith` |RS ist eine abschließende Teilzeichenfolge von LS |Nein |`"Fabrikam" endswith "kam"` |
| `!endswith` |RS ist keine abschließende Teilzeichenfolge von LS |Nein |`"Fabrikam" !endswith "ka"` |
| `matches regex` |LS enthält eine Übereinstimmung für RS |Ja |`"Fabrikam" matches regex "b.*k"` |
| [`in`](#in) |Entspricht allen Elementen |Ja |`"abc" in ("123", "345", "abc")` |
| [`!in`](#in) |Entspricht keinem Element |Ja |`"bc" !in ("123", "345", "abc")` |

Verwenden Sie `has` oder `in`, wenn Sie auf das Vorhandensein eines vollständigen lexikalischen Begriffs hin testen, d.h. ein Symbol oder ein alphanumerisches Wort, begrenzt durch nicht alphanumerische Zeichen oder den Anfang oder das Ende des Felds. `has` ist schneller als `contains`, `startswith` oder `endswith`. Die erste dieser Abfragen wird schneller ausgeführt:

    EventLog | where continent has "North" | count;
    EventLog | where continent contains "nor" | count





### <a name="countof"></a>countof
    countof("The cat sat on the mat", "at") == 3
    countof("The cat sat on the mat", @"\b.at\b", "regex") == 3

Zählt die Vorkommnisse einer Teilzeichenfolge in einer Zeichenfolge. Einfache Zeichenfolgenübereinstimmungen überlappen sich möglicherweise; bei regex-Übereinstimmungen ist dies nicht Fall.

**Syntax**

    countof(text, search [, kind])

**Argumente**

* *text:* Eine Zeichenfolge.
* *search:* Die einfache Zeichenfolge oder der reguläre Ausdruck, die bzw. der in *text* abgeglichen werden soll.
* *kind:* `"normal"|"regex"` Standardwert: `normal`. 

**Rückgabe**

Angabe, wie oft die Suchzeichenfolge im Container abgeglichen werden kann. Einfache Zeichenfolgenübereinstimmungen überlappen sich möglicherweise; bei regex-Übereinstimmungen ist dies nicht Fall.

**Beispiele**

|  |  |
| --- | --- |
| `countof("aaa", "a")` |3 |
| `countof("aaaa", "aa")` |3 (nicht 2!) |
| `countof("ababa", "ab", "normal")` |2 |
| `countof("ababa", "aba")` |2 |
| `countof("ababa", "aba", "regex")` |1 |
| `countof("abcabc", "a.c", "regex")` |2 |

### <a name="extract"></a>extract
    extract("x=([0-9.]+)", 1, "hello x=45.6|wo") == "45.6"

Ruft eine Übereinstimmung für einen [regulären Ausdruck](#regular-expressions) aus einer Textzeichenfolge ab. Optional konvertiert es dann die extrahierte Teilzeichenfolge in den angegebenen Typ.

**Syntax**

    extract(regex, captureGroup, text [, typeLiteral])

**Argumente**

* *regex:* Ein [regulärer Ausdruck](#regular-expressions).
* *captureGroup:* Eine positive `int`-Konstante, die die zu extrahierende Erfassungsgruppe angibt. 0 steht für die vollständige Übereinstimmung, 1 für den mit der ersten „("Klammer")“ übereinstimmenden Wert im regulären Ausdruck, 2 oder höher für nachfolgende Klammern.
* *text:* Ein `string` -Wert.
* *typeLiteral:* Ein optionales Typliteral (z. B. `typeof(long)`). Die extrahierte Teilzeichenfolge wird, sofern angegeben, in diesen Typ konvertiert. 

**Rückgabe**

Wenn mit *regex* eine Übereinstimmung in *text* gefunden wird: die mit der angegebenen Erfassungsgruppe *captureGroup* abgeglichene Teilzeichenfolge, optional konvertiert in *typeLiteral*.

Wenn keine Übereinstimmung vorhanden ist oder bei der Typkonvertierung ein Fehler auftritt: `null`. 

**Beispiele**

Die Beispielzeichenfolge `Trace` wird nach einer Definition für `Duration` durchsucht. Die Übereinstimmung wird in `real` konvertiert und dann mit einer Zeitkonstanten (`1s`) multipliziert, damit `Duration` den Typ `timespan` erhält. In diesem Beispiel entspricht dies 123,45 Sekunden:

```AIQL
...
| extend Trace="A=1, B=2, Duration=123.45, ..."
| extend Duration = extract("Duration=([0-9.]+)", 1, Trace, typeof(real)) * time(1s) 
```

Dieses Beispiel entspricht `substring(Text, 2, 4)`:

```AIQL
extract("^.{2,2}(.{4,4})", 1, Text)
```

<a name="notempty"></a>
<a name="isnotempty"></a>
<a name="isempty"></a>



### <a name="isempty-isnotempty-notempty"></a>isempty, isnotempty, notempty
    isempty("") == true

„True“, wenn das Argument eine leere Zeichenfolge oder null ist.
Siehe auch [isnull](#isnull).

**Syntax**

    isempty([value])


    isnotempty([value])


    notempty([value]) // alias of isnotempty

**Rückgabe**

Gibt an, ob das Argument eine leere Zeichenfolge oder isnull ist.

| x | isempty(x) |
| --- | --- |
| "" |true |
| "x" |false |
| parsejson("") |true |
| parsejson("[]") |false |
| parsejson("{}") |false |

**Beispiel**

    T | where isempty(fieldName) | count


### <a name="parseurl"></a>parseurl
Zerlegen Sie eine URL in ihre Bestandteile.

**Syntax**

    parseurl(urlstring)

**Argumente**

* *urlstring:* Eine URL

**Rückgabe**

Ein Objekt, das die Teile als Zeichenfolgen enthält

**Beispiel**

    parseurl("http://user:pass@contoso.com/icecream/buy.aspx?a=1&b=2#tag")

    {
    "Scheme" : "http",
    "Host" : "contoso.com",
    "Port" : "80",
    "Path" : "/icecream/buy.aspx",
    "Username" : "user",
    "Password" : "pass",
    "Query Parameters" : {"a":"1","b":"2"},
    "Fragment" : "tag"
    }

### <a name="replace"></a>replace
Ersetzen Sie alle regex-Übereinstimmungen mit einer anderen Zeichenfolge.

**Syntax**

    replace(regex, rewrite, text)

**Argumente**

* *regex:* Der [reguläre Ausdruck](https://github.com/google/re2/wiki/Syntax) zum Durchsuchen von *text*. Er kann Erfassungsgruppen in „('Klammern')“ enthalten. 
* *rewrite:* Der reguläre Ersetzungsausdruck für jede Übereinstimmung, die mit *matchingRegex* erzielt wurde. Verwenden Sie `\0`, um auf die gesamte Übereinstimmung zu verweisen: `\1` für die erste Erfassungsgruppe, `\2` usw. für nachfolgende Erfassungsgruppen.
* *text:* Eine Zeichenfolge.

**Rückgabe**

*text* nach dem Ersetzen aller Übereinstimmungen von *regex* durch Auswertungen von *rewrite*. Übereinstimmungen überlappen sich nicht.

**Beispiel**

Diese Anweisung:

```AIQL
range x from 1 to 5 step 1
| extend str=strcat('Number is ', tostring(x))
| extend replaced=replace(@'is (\d+)', @'was: \1', str)
```

Bietet die folgenden Ergebnisse:

| x | str | replaced |
| --- | --- | --- |
| 1 |Nummer lautet 1.000000 |Nummer lautete 1.000000 |
| 2 |Nummer lautet 2.000000 |Nummer lautete 2.000000 |
| 3 |Nummer lautet 3.000000 |Nummer lautete 3.000000 |
| 4 |Nummer lautet 4.000000 |Nummer lautete 4.000000 |
| 5 |Nummer lautet 5.000000 |Nummer lautete 5.000000 |

### <a name="split"></a>split
    split("aaa_bbb_ccc", "_") == ["aaa","bbb","ccc"]

Teilt eine angegebene Zeichenfolge gemäß einem angegebenen Trennzeichen, und gibt ein Zeichenfolgenarray mit den enthaltenen untergeordneten Zeichenfolgen zurück. Optional kann eine bestimmte Teilzeichenfolge zurückgegeben werden, sofern vorhanden.

**Syntax**

    split(source, delimiter [, requestedIndex])

**Argumente**

* *source:*Die Quellzeichenfolge, die dem angegebenen Trennzeichen entsprechend geteilt wird.
* *delimiter:*Das Trennzeichen, das zum Teilen der Quellzeichenfolge verwendet wird.
* *requestedIndex*: Ein optionaler nullbasierter Index (`int`). Sofern angegeben, enthält das zurückgegebene Zeichenfolgenarray die angeforderte Teilzeichenfolge, sofern vorhanden. 

**Rückgabe**

Ein Zeichenfolgenarray, das die Teilzeichenfolgen der angegebenen Quellzeichenfolge enthält, die durch das angegebene Trennzeichen getrennt sind.

**Beispiele**

```
split("aa_bb", "_")           // ["aa","bb"]
split("aaa_bbb_ccc", "_", 1)  // ["bbb"]
split("", "_")                // [""]
split("a__b")                 // ["a","","b"]
split("aabbcc", "bb")         // ["aa","cc"]
```




### <a name="strcat"></a>strcat
    strcat("hello", " ", "world")

Verkettet zwischen 1 und 16 Argumente, bei denen es sich um Zeichenfolgen handeln muss.

### <a name="strlen"></a>strlen
    strlen("hello") == 5

Länge einer Zeichenfolge.

### <a name="substring"></a>substring
    substring("abcdefg", 1, 2) == "bc"

Extrahiert eine Teilzeichenfolge aus einer angegebenen Quellzeichenfolge, beginnend bei einem angegebenen Index. Optional kann die Länge der angeforderten Teilzeichenfolge angegeben werden.

**Syntax**

    substring(source, startingIndex [, length])

**Argumente**

* *source:* Die Quellzeichenfolge, aus der die Teilzeichenfolge entnommen wird.
* *startingIndex:* Die nullbasierte Position des Anfangszeichens der angeforderten Teilzeichenfolge.
* *length:* Ein optionaler Parameter, der zur Angabe der angeforderten Anzahl von Zeichen in der Teilzeichenfolge verwendet werden kann. 

**Rückgabe**

Eine Teilzeichenfolge aus der angegebenen Zeichenfolge. Die Teilzeichenfolge beginnt bei der startingIndex (nullbasierten) Zeichenposition und wird bis zum Ende der Zeichenfolge oder der Längenzeichen fortgesetzt, sofern angegeben.

**Beispiele**

```
substring("123456", 1)        // 23456
substring("123456", 2, 2)     // 34
substring("ABCD", 0, 2)       // AB
```

### <a name="tolower"></a>tolower
    tolower("HELLO") == "hello"

Konvertiert eine Zeichenfolge in Kleinbuchstaben.

### <a name="toupper"></a>toupper
    toupper("hello") == "HELLO"

Konvertiert eine Zeichenfolge in Großbuchstaben.

### <a name="guids"></a>GUIDs
    guid(00000000-1111-2222-3333-055567f333de)


## <a name="arrays-objects-and-dynamic"></a>Arrays, Objekte und Dynamik
[Literale](#dynamic-literals) | [Umwandlung](#casting-dynamic-objects) | [Operatoren](#operators) | [let-Klauseln](#dynamic-objects-in-let-clauses)
<br/>
[arraylength](#arraylength) | [extractjson](#extractjson) | [parsejson](#parsejson) | [range](#range) | [treepath](#treepath) | [todynamic](#todynamic) | [zip](#zip)

Hier ist das Ergebnis einer Abfrage für eine Application Insights-Ausnahme. Der Wert in `details` ist ein Array.

![](./media/app-insights-analytics-reference/310.png)

**Indizierung:** Arrays und Objekte werden wie in JavaScript indiziert:

    exceptions | take 1
    | extend 
        line = details[0].parsedStack[0].line,
        stackdepth = arraylength(details[0].parsedStack)

* Verwenden Sie jedoch `arraylength` und andere Analytics-Funktionen (nicht „.length“!).

**Typumwandlung:** In einigen Fällen ist es erforderlich, ein Element umzuwandeln, das Sie aus einem Objekt extrahieren, da der Typ variieren kann. `summarize...to` benötigt beispielsweise einen bestimmten Typ:

    exceptions 
    | summarize count() 
      by toint(details[0].parsedStack[0].line)

    exceptions
    | summarize count()
      by tostring(details[0].parsedStack[0].assembly)

**Literale:** Um ein explizites Array oder ein Eigenschaftenbehälterobjekt zu erstellen, schreiben Sie es als JSON-Zeichenfolge mit Typumwandlung:

    todynamic('[{"x":"1", "y":"32"}, {"x":"6", "y":"44"}]')


**mvexpand:** Verwenden Sie „mvexpand“, um die Eigenschaften eines Objekts in separate Zeilen aufzuteilen:

    exceptions | take 1
    | mvexpand details[0].parsedStack[0]


![](./media/app-insights-analytics-reference/410.png)

**treepath:** Zum Auffinden aller Pfade in einem komplexen Objekt:

    exceptions | take 1 | project timestamp, details
    | extend path = treepath(details)
    | mvexpand path


![](./media/app-insights-analytics-reference/420.png)

**buildschema:** Zum Auffinden des minimalen Schemas, das alle Werte des Ausdrucks in der Tabelle zulässt:

    exceptions | summarize buildschema(details)

Ergebnis:

    { "indexer":
     {"id":"string",
       "parsedStack":
       { "indexer":
         {  "level":"int",
            "assembly":"string",
            "fileName":"string",
            "method":"string",
            "line":"int"
         }},
      "outerId":"string",
      "message":"string",
      "type":"string",
      "rawStack":"string"
    }}

Beachten Sie, dass mit `indexer` markiert wird, an welcher Stelle Sie einen numerischen Index verwenden sollten. Einige gültige Pfade für dieses Schema (vorausgesetzt diese Beispielindizes befinden sich im Bereich):

    details[0].parsedStack[2].level
    details[0].message
    arraylength(details)
    arraylength(details[0].parsedStack)



### <a name="array-and-object-literals"></a>Array- und Objektliterale
Verwenden Sie `parsejson` zum Erstellen eines dynamischen Literals (Alias: `todynamic`) mit einem JSON-Zeichenfolgenargument:

* `parsejson('[43, 21, 65]')` : ein Array mit Zahlen
* `parsejson('{"name":"Alan", "age":21, "address":{"street":432,"postcode":"JLK32P"}}')`
* `parsejson('21')` : ein einzelner Wert vom Typ „dynamic“ mit einer Zahl
* `parsejson('"21"')` : ein einzelner Wert vom Typ „dynamic“ mit einer Zeichenfolge

> [!NOTE]
> Doppelte Anführungszeichen (`"`) müssen zum Einschließen von Bezeichnungen und Zeichenfolgenwerten in JSON-Code verwendet werden. Daher ist es im Allgemeinen einfacher, ein JSON-codiertes Zeichenfolgenliteral mit einfachen Anführungszeichen (`'`) zu kennzeichnen.
> 

In diesem Beispiel wird ein dynamischer Wert erstellt, und anschließend werden dessen Felder verwendet:

```

T
| extend person = parsejson('{"name":"Alan", "age":21, "address":{"street":432,"postcode":"JLK32P"}}')
| extend n = person.name, add = person.address.street
```


### <a name="dynamic-object-functions"></a>Dynamische Objektfunktionen
|  |  |
| --- | --- |
| [*value* `in` *array*](#in) |*array* enthält *value* |
| [*value* `!in` *array*](#in) |*array* enthält *value* nicht |
| [`arraylength(`array`)`](#arraylength) |Null, wenn es sich nicht um ein Array handelt. |
| [`extractjson(`path,object`)`](#extractjson) |Verwendet den Pfad zum Navigieren in das Objekt. |
| [`parsejson(`source::`)`](#parsejson) |Wandelt eine JSON-Zeichenfolge in ein dynamisches Objekt um. |
| [`range(`from,to,step`)`](#range) |Ein Array von Werten |
| [`mvexpand` listColumn](#mvexpand-operator) |Repliziert eine Zeile für jeden Wert in einer Liste in eine angegebene Zelle. |
| [`summarize buildschema(`column`)`](#buildschema) |Leitet das Typschema aus dem Spalteninhalt ab. |
| [`summarize makelist(`column`)` ](#makelist) |Reduziert die Zeilengruppen und setzt die Werte der Spalte in ein Array. |
| [`summarize makeset(`column`)`](#makeset) |Reduziert die Zeilengruppen und setzt die Werte der Spalte in ein Array ohne Duplizierung. |

### <a name="dynamic-objects-in-let-clauses"></a>Dynamische Objekte in let-Klauseln
[let-Klauseln](#let-clause) speichern dynamische Werte als Zeichenfolgen, sodass diese beiden Klauseln gleichwertig sind. Beide benötigen vor der Verwendung `parsejson` (oder `todynamic`):

    let list1 = '{"a" : "somevalue"}';
    let list2 = parsejson('{"a" : "somevalue"}');

    T | project parsejson(list1).a, parsejson(list2).a


### <a name="in"></a>in
    value in (listExpression)
    value !in (listExpression)

Bestimmt, ob in der Liste ein Element (nicht) vorhanden ist, das dem Wert entspricht. Die Groß-/Kleinschreibung wird beachtet, wenn der Wert eine Zeichenfolge ist.

**Argumente**

* `value`: Ein skalarer Ausdruck.
* `listExpression`...: Eine Liste von skalaren Ausdrücken oder ein Ausdruck, der als Liste ausgewertet wird. 

Ein geschachteltes Array wird in eine einzelne Liste vereinfacht. `where x in (dynamic([1,[2,3]]))` wird beispielsweise `where x in (1,2,3)`.  

**Beispiele**

```AIQL
    requests | where client_City in ("London", "Paris", "Rome")
```

```AIQL
let cities = dynamic(['Dublin','Redmond','Amsterdam']);
requests | where client_City in (cities) 
|  summarize count() by client_City
```

Berechnete Liste:

```AIQL
let topCities =  toscalar ( // convert single column to value
   requests
   | summarize count() by client_City 
   | top 4 by count_ 
   | summarize makeset(client_City)) ;
requests
| where client_City in (topCities) 
| summarize count() by client_City;
```

Verwendung eines Funktionsaufrufs als Listenausdruck:

```AIQL
let topCities =  (n:int) {toscalar (
   requests
   | summarize count() by client_City 
   | top n by count_ 
   | summarize makeset(client_City)) };
requests
| where client_City in (topCities(3)) 
| summarize count() by client_City;
```
 

### <a name="arraylength"></a>arraylength
Die Anzahl der Elemente in einem dynamischen Array.

**Syntax**

    arraylength(array)

**Argumente**

* *array:* Ein `dynamic`-Wert.

**Rückgabe**

Die Anzahl von Elementen in *array* oder `null`, wenn *array* kein Array ist.

**Beispiele**

```
arraylength(parsejson('[1, 2, 3, "four"]')) == 4
arraylength(parsejson('[8]')) == 1
arraylength(parsejson('[{}]')) == 1
arraylength(parsejson('[]')) == 0
arraylength(parsejson('{}')) == null
arraylength(parsejson('21')) == null
```



### <a name="extractjson"></a>extractjson
    extractjson("$.hosts[1].AvailableMB", EventText, typeof(int))

Rufen Sie ein angegebenes Element aus einem JSON-Text mit einem Pfadausdruck ab. Konvertieren Sie optional die extrahierte Zeichenfolge in einen bestimmten Typ.

**Syntax**

```

    string extractjson(jsonPath, dataSource) 
    resulttype extractjson(jsonPath, dataSource, typeof(resulttype))
```


**Rückgabe**

Diese Funktion führt eine JsonPath-Abfrage in dataSource durch, die eine gültige JSON-Zeichenfolge enthält. Optional wird dieser Wert, je nach drittem Argument, in einen anderen Typ konvertiert.

**Beispiel**

Die [Klammer]-Notation und die Punktnotation sind gleichwertig:

    ... | extend AvailableMB = extractjson("$.hosts[1].AvailableMB", EventText, typeof(int)) | ...

    ... | extend AvailableMD = extractjson("$['hosts'][1]['AvailableMB']", EventText, typeof(int)) | ...



**Leistungstipps**

* Wenden Sie vor der Verwendung von `extractjson()`
* Erwägen Sie stattdessen den Abgleich mit einem regulären Ausdruck mit [extract](#extract) . Dies kann sehr viel schneller ausgeführt werden und ist effektiv, wenn die JSON aus einer Vorlage erstellt wird.
* Verwenden Sie `parsejson()` , wenn Sie mehr als einen Wert aus dem JSON-Code extrahieren müssen.
* Ziehen Sie es in Betracht, die JSON zum Zeitpunkt der Erfassung zu analysieren, indem Sie den Typ der Spalte als dynamisch deklarieren.

### <a name="json-path-expressions"></a>JSON Path-Ausdrücke
|  |  |
| --- | --- |
| `$` |Stammobjekt |
| `@` |Aktuelles Objekt |
| `[0]` |Array-Subscript |
| `.` oder `[0]` |Untergeordnet |

*(Derzeit werden keine Platzhalter, Rekursionen, Vereinigungen oder Segmente implementiert.)*

### <a name="parsejson"></a>parsejson
Interpretiert `string` als [JSON-Wert](http://json.org/) und gibt den Wert als `dynamic` zurück. Dies ist der Nutzung von `extractjson()` vorzuziehen, wenn Sie mehrere Elemente eines zusammengesetzten JSON-Objekts extrahieren müssen.

**Syntax**

    parsejson(json)

**Argumente**

* *json:* Ein JSON-Dokument.

**Rückgabe**

Ein Objekt vom Typ `dynamic` , angegeben durch *json*.

**Beispiel**

Für das folgende Beispiel gilt, dass `customDimensions.person` ein `string`-Element ist, das wie folgt aussieht: 

```
"\"addresses\":[{\"postcode\":\"C789\",\"street\":\"high st\",\"town\":\"Cardigan\"},{\"postcode\":\"J456\",\"street\":\"low st\",\"town\":\"Jumper\"}],\"name\":\"Ada\""
```

dann ruft das folgende Fragment zunächst den Wert des `duration`-Slots im Objekt und daraus zwei Slots ab: `duration.value` und `duration.min` (bzw. `118.0` und `110.0`).

```AIQL
customEvents
| where name == "newMember"
| extend d=parsejson(context_custom_metrics) 
| extend duration_value=d.duration.value, duration_min=d["duration"]["min"]
```

> [!NOTE]
> Doppelte Anführungszeichen müssen zum Einschließen von Bezeichnungen und Zeichenfolgenwerten in JSON-Code verwendet werden. 
>


### <a name="range"></a>range
Die `range()`-Funktion (nicht zu verwechseln mit dem `range`-Operator) erzeugt ein dynamisches Array mit einer Reihe gleichmäßig verteilter Werte.

**Syntax**

    range(start, stop, step)

**Argumente**

* *start:* Der Wert des ersten Elements im resultierenden Array. 
* *stop:* Der Wert des letzten Elements im resultierenden Array oder der kleinste Wert, der größer ist als das letzte Element im resultierenden Array und in einem ganzzahligen Vielfachen von *step* von *start* enthalten ist.
* *step:* Die Differenz zwischen zwei aufeinanderfolgenden Elementen des Arrays.

**Beispiele**

Das folgende Beispiel gibt `[1, 4, 7]`zurück:

```AIQL
range(1, 8, 3)
```

Das folgende Beispiel gibt ein Array mit allen Tagen im Jahr 2015 zurück:

```AIQL

    range(datetime(2015-01-01), datetime(2015-12-31), 1d)
```

### <a name="todynamic"></a>todynamic
    todynamic('{"a":"a1", "b":["b1", "b2"]}')

Konvertiert eine Zeichenfolge in einen dynamischen Wert.

### <a name="treepath"></a>treepath
    treepath(dynamic_object)

Listet alle Path-Ausdrücke auf, die Verzweigungen in einem dynamischen Objekt identifizieren. 

**Rückgabe**

Ein Array von Path-Ausdrücken.

**Beispiele**

    treepath(parsejson('{"a":"b", "c":123}')) 
    =>       ["['a']","['c']"]
    treepath(parsejson('{"prop1":[1,2,3,4], "prop2":"value2"}'))
    =>       ["['prop1']","['prop1'][0]","['prop2']"]
    treepath(parsejson('{"listProperty":[100,200,300,"abcde",{"x":"y"}]}'))
    =>       ["['listProperty']","['listProperty'][0]","['listProperty'][0]['x']"]

Beachten Sie, dass „[0]“ auf das Vorhandensein eines Arrays hinweist, aber nicht den von einem bestimmten Pfad verwendeten Index angibt.

### <a name="zip"></a>zip
    zip(list1, list2, ...)

Kombiniert eine Gruppe von Listen in einer Tupelliste.

* `list1...`: Eine Liste von Werten

**Beispiele**

    zip(parsejson('[1,3,5]'), parsejson('[2,4,6]'))
    => [ [1,2], [3,4], [5,6] ]


    zip(parsejson('[1,3,5]'), parsejson('[2,4]'))
    => [ [1,2], [3,4], [5,null] ]


### <a name="names"></a>Namen
Namen können bis zu 1024 Zeichen lang sein. Die Groß-/Kleinschreibung wird beachtet, und sie können Buchstaben, Ziffern und Unterstriche (`_`) enthalten. 

Geben Sie einen Namen mit ['... '] oder [" ... "] an, um andere Zeichen einzubeziehen oder ein Schlüsselwort als Name zu verwenden. Beispiel:

```AIQL

    requests | 
    summarize  ["distinct urls"] = dcount(name) // non-alphanumerics
    by  ['where'] = client_City, // using a keyword as a name
        ['outcome!'] = success // non-alphanumerics
```


|  |  |
| --- | --- |
| ['path\\file\n\'x\''] |Verwenden Sie \ für Zeichen als Escapezeichen. |
| ["d-e.=/f#\n"] | |
| [@'path\file'] |Keine Escapezeichen – \ ist literal. |
| [@"\now & then\"] | |
| [where] |Verwenden eines Programmiersprachenschlüsselworts als Name |

[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]


