---
title       : Improved data management with LivingNorwayR
subtitle    : 
author      : Matt Grainger
job         : Postdoctoral Fellow NINA
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : []            # {mathjax, quiz, bootstrap}
ext_widgets : {rCharts: [libraries/htmlwidgets, libraries/circlepackeR]}
mode        : selfcontained # {standalone, draft}
logo        : LNWhite.png
biglogo     : LNWhite.png
knit        : slidify::knit2slides
assets      : {assets: ../../assets}
---

<!-- Limit image width and height -->
<style type='text/css'>
img {
    max-height: 560px;
    max-width: 964px;
}
</style>

<!-- Center image on slide -->
<script src="http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.min.js"></script>
<script type='text/javascript'>
$(function() {
    $("p:has(img)").addClass('centered');
});
</script>

## Schematic of current workflow
 
![](assets/img/Workflow1.png)


--- .class #id 

## Data sharing 

![](assets/img/sorry_no.png)


--- .class #id 

## Code sharing 

![](assets/img/data&code.png) 


--- .class #id 

## We are sharing data - but not code

Culina et al. (2020) PLoS Biol 18(7): e3000763. (n=346)


![](assets/img/Culina.PNG) 

--- .class #id 

## Although data sharing may not be complete 
"56% were incomplete" (n= 100)

![plot of chunk unnamed-chunk-1](assets/fig/unnamed-chunk-1-1.png)


--- .class #id

## And reuse is prevented
"64% were archived in a way that prevented reuse" (n= 100)

![plot of chunk unnamed-chunk-2](assets/fig/unnamed-chunk-2-1.png)


--- .class #id

##  Barriers to data sharing
Wiley survey 2014 (n=2250)

<style type="text/css"> body {background:none transparent; } </style>




<iframe src="C:/Users/matthew.grainger/Documents/Projects_in_development/LNC2020_presentation/slides/assets/widgets/wiley.html" width=100% height=100% allowtransparency="true"> </iframe>

--- .class #id

## Schematic of future workflow

![](assets/img/Workflow2.png)

--- .class #id 

## Introducing {LivingNorwayR}

https://github.com/LivingNorway/LivingNorwayR

- An R package designed to facilitate the future workflow
- Main features 
  - Import & Export Darwin Core Archive
  - Mapping data (with reduced pain) to DWC terms
  - Metadata extraction/writing functions
  - Plotting functions
  - Modelling functions 

--- .class #id

## Toolchain walkthrough

We will import this data and use it to demonstrate some of the workflow

Nilsen E B, Pedersen H C, Brøseth H, Moa P F, Vang R (2019). Rock ptarmigan (Lagopus muta) radio telemetry in Lierne, Norway. Version 1.2. Norwegian Institute for Nature Research. Occurrence dataset https://doi.org/10.15468/o4zcd3 accessed via GBIF.org on 2020-10-10.
https://www.gbif.org/dataset/b848f1f3-3955-4725-8ad8-e711e4a9e0ac#

![](assets/img/37755781.jpg)

--- .class #id

## Set up the "Living Norway data package" structure


```r
library(LivingNorwayR)
build_folder_structure(project_name = "Tetraonidae_Lagopus")
map_folders(project_name = "Tetraonidae_Lagopus")
#map_files(project_name = "Tetraonidae_Lagopus")
```



<iframe src="./assets/widgets/plot.html" width=100% height=100% allowtransparency="true"> </iframe>

--- .class #id

## Import the data and map to DwCObject 






```r
Rock<-DwCOccurence$new(
  id<-occurrence$id,
  ownerInstitutionCode<-occurrence$ownerInstitutionCode,
  basisOfRecord<-occurrence$basisOfRecord,
  dynamicProperties<-occurrence$dynamicProperties,
  occurrenceID<-occurrence$occurrenceID,
  sex<-occurrence$sex,
  lifeStage<-occurrence$lifeStage,
  organismID<-occurrence$organismID,
  organismName<-occurrence$organismName,
  eventDate<-occurrence$eventDate,
  ...)
```

--- .class #id

## Helper functions


```r
DwCClassList$`dwc:Occurrence`$termInfo
```

dwc:Occurrence - Occurrence
An existence of an Organism (sensu http://rs.tdwg.org/dwc/terms/Organism) at a particular place at a particular time.

	Defined in: https://dwc.tdwg.org/
	IRI: http://rs.tdwg.org/dwc/terms/Occurrence
	Version IRI: http://rs.tdwg.org/dwc/terms/version/Occurrence-2020-08-20
	Type: Class
	Date modified: 2020-08-20
	Executive committee decisions:
		http://rs.tdwg.org/decisions/decision-2014-10-26_15
	Examples:
		A wolf pack on the shore of Kluane Lake in 1988. A virus in a plant leaf in the New York Botanical Garden at 15:29 on 2014-10-23. A fungus in Central Park in the summer of 1929.

--- .class #id


## Make use of the data 


```r
df<-Rock$object()
summary(df$sex)
```

```
##   F   M 
## 180 198
```

```r
summary(df$lifeStage)
```

```
##    adult juvenile 
##      211      167
```

```r
bb<-Rock$get_bounding_box()
```

```
##     minX     maxX     minY     maxY 
## 12.65946 14.65305 64.03308 64.77377
```

--- .class #id

## Produce maps 


```r
Map<-Rock$plotmap()
Map
```

![plot of chunk unnamed-chunk-12](assets/fig/unnamed-chunk-12-1.png)

--- .class #id

## Explore the metadata

**Early stage of development**





```r
RockXML<-("C:/Users/matthew.grainger/Documents/Projects_in_development/LNC2020_presentation/slides/Tetraonidae_Lagopus/metadata/eml.xml")

metadata<-DwCMetaData$new(RockXML)
#metadata$get_eml()
metadata$get_abstract(RockXML)
```

```
## <abstract>
##   <para>This data set is based on a small radio telemetry project on rock ptarmigan (Lagopus muta) in Lierne municipality, central Norway. In total, 85 rock ptarmigans were captured and radio-collared. After release, the birds were re-located with variable geographical precision (noted in the data). When mortality were detected, cause of death was as far as possible recorded. 
## 
## In the published data, cause of death is attributed to one of two causes (hunting OR other causes), and this information is available in the field "dynamicProperties" together with information about the event (capture OR radiotelemetry/recature). In some cases more detailed information about the event and state is available in the raw data.</para>
## </abstract>
```

--- .class #id

## Do some analysis
**Early stage of development**





```r
DwCOccurence$run_survival()
```




```
## Call: survfit(formula = Surv(entry, exit, event) ~ 1, data = CH)
## 
##  time n.risk n.event censored survival std.err lower 95% CI upper 95% CI
##     4     81       5        1    0.938  0.0267        0.887        0.992
##     5     76       6        0    0.864  0.0381        0.793        0.942
##     6     70       6        1    0.790  0.0452        0.706        0.884
##     7     63       1        0    0.778  0.0462        0.692        0.874
##    10     57       2        9    0.750  0.0485        0.661        0.852
##    11     55       4        6    0.696  0.0521        0.601        0.806
##    15     38       2        7    0.659  0.0554        0.559        0.777
##    16     36       2        0    0.622  0.0580        0.519        0.747
##    17     34       1        0    0.604  0.0592        0.499        0.732
##    18     33       1        1    0.586  0.0601        0.479        0.716
##    19     31       1        0    0.567  0.0611        0.459        0.700
##    20     30       1        5    0.548  0.0619        0.439        0.684
##    22     24       2        0    0.502  0.0646        0.390        0.646
##    25     19       2        3    0.450  0.0678        0.335        0.604
```

```
## Call: survfit(formula = Surv(entry, exit2, event2) ~ 1, data = CH_h)
## 
##  time n.risk n.event censored survival std.err lower 95% CI upper 95% CI
##     4     81       7       75    0.914  0.0312        0.854        0.977
```

```
## Call: survfit(formula = Surv(entry, exit2, event2) ~ 1, data = CH_e)
## 
##  time n.risk n.event censored survival std.err lower 95% CI upper 95% CI
##     4     81       5        1    0.938  0.0267        0.887        0.992
##     5     76       6        0    0.864  0.0381        0.793        0.942
##     6     70       6        1    0.790  0.0452        0.706        0.884
##     7     63       1        0    0.778  0.0462        0.692        0.874
##    10     57       2        9    0.750  0.0485        0.661        0.852
##    11     55       4        6    0.696  0.0521        0.601        0.806
```

```
## Call: survfit(formula = Surv(entry2, exit, event) ~ 1, data = CH_l)
## 
##  time n.risk n.event censored survival std.err lower 95% CI upper 95% CI
##    15     38       2        0    0.947  0.0362        0.879        1.000
##    16     36       2        0    0.895  0.0498        0.802        0.998
##    17     34       1        0    0.868  0.0548        0.767        0.983
##    18     33       1        1    0.842  0.0592        0.734        0.966
##    19     31       1        0    0.815  0.0632        0.700        0.949
##    20     30       1        5    0.788  0.0667        0.667        0.930
##    22     24       2        0    0.722  0.0756        0.588        0.886
##    25     19       2        3    0.646  0.0846        0.500        0.835
```

--- .class #id


### Then add a plot



![](assets/img/ggsurv.png)

--- .class #id

## Write it up

### Results

Out of 84 radio marked rock ptarmigans, 33 were shot by hunters in the study area, and 9 were recorded as dead due to other causes (mostly predation). 

### Results (under the covers)

Out of ``r length(unique(d$organismName))`` radio marked rock ptarmigans, ``r  Deaths[1,2]`` were shot by hunters in the study area, and ``r Deaths[2,2]`` were recorded as dead due to other causes (mostly predation). 

--- .class #id

## {LivingNorwayR}

- {LivingNorwayR} is still in development
  - Please let us know what functionality you need
    - Github issues: https://github.com/LivingNorway/LivingNorwayR/issues
    - Slack: Joseph Chipperfield, Matt Grainger, Erlend Nilsen
    - Email: matthew.grainger@nina.no
    
![](https://media.giphy.com/media/vJTzaVE5YZf4k/giphy.gif)

--- .class id#

![](assets/img/LNWhite.png)
