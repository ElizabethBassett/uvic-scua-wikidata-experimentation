Project by Elizabeth Bassett, Special Collections and Archives Assistant (YCW) | July 2020

The goal of this project is to experiment with ways that the University of Victoria (UVic) Libraries can utilize Wikidata to promote interest in the holdings at Special Collections and University Archives (SCUA). The following visualizations use SPARQL queries and the [Wikidata Query Service](https://query.wikidata.org/) to compile information about people and institutions that have fonds, collections, and correspondence held at UVIC SCUA. As more instances of the "archives at" (P485) property are used to connect SCUA with people and institutions with pages on Wikidata, the visualizations will become more representative of the Archives' holdings.

<br>

## Visualizing the Archives' Holdings through Wikidata Queries
----  

<br>

### _**Who has holdings in the Archives?**_ 

<iframe style="width: 55vw; height: 50vh; border: none;" src="https://query.wikidata.org/embed.html#SELECT%20%3FCreator%20%3FCreatorLabel%0AWHERE%0A%7B%0A%20%20%3FCreator%20wdt%3AP485%20wd%3AQ47518588.%0A%20%20%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22%5BAUTO_LANGUAGE%5D%22.%7D%0A%7D%0A%0A%20ORDER%20BY%20%28%3FCreatorLabel%29" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups" ></iframe>

<br>

This table includes both people and organizations that have archival fonds, collections, or correspondence held at UVic SCUA. Note that the list is not exhaustive, and only includes the records creators that have been linked to UVic through the "archives at" (P485) property on Wikidata.

<br>

_SPARQL query used to generate the table:_

```
SELECT ?Creator ?CreatorLabel
WHERE
{
  ?Creator wdt:P485 wd:Q47518588.
  
  SERVICE wikibase:label { bd:serviceParam wikibase:language "[AUTO_LANGUAGE]".}
}

 ORDER BY (?CreatorLabel)
```

<br>

### _**Where are these records creators from?**_

<iframe style="width: 55vw; height: 50vh; border-style: solid; border-width: thin;" src="https://query.wikidata.org/embed.html#%23defaultView%3AMap%0ASELECT%20%3FCreator%20%3FCreatorLabel%20%3FCorrespondenceAtLabel%20%3FDateofBirthLabel%20%3FResidenceLabel%20%3FLocationLabel%20%3FCountryOfCitizenship%20%3FCountry%20%3FCoordinates%20%0AWHERE%0A%7B%0A%20%20%3FCreator%20wdt%3AP485%20wd%3AQ47518588.%0A%20%20%0A%20%20OPTIONAL%20%7B%3FCreator%20wdt%3AP569%20%3FDateofBirth.%20%7D%0A%20%20%0A%20%20OPTIONAL%20%7B%3FCreator%20wdt%3AP27%20%3FCountryOfCitizenship.%20%7D%0A%20%20%0A%20%20OPTIONAL%20%7B%3FCreator%20wdt%3AP551%20%3FResidence.%0A%20%20%20%20%20%20%20%20%20%20%20%20%3FResidence%20wdt%3AP625%20%3FCoordinates.%7D%0A%20%20%0A%20%20OPTIONAL%20%7B%3FCreator%20wdt%3AP131%20%3FLocation.%0A%20%20%20%20%20%20%20%20%20%20%20%20%3FLocation%20wdt%3AP625%20%3FCoordinates.%7D%0A%20%20%0A%20%20OPTIONAL%20%7B%3FCreator%20wdt%3AP17%20%3FCountry.%0A%20%20%20%20%20%20%20%20%20%20%20%20%3FCountry%20wdt%3A625%20%3FCoordinates.%7D%0A%20%20%0A%20%20OPTIONAL%20%7B%3FCreator%20wdt%3AP485%20wd%3AQ47518588%3B%0A%20%20%20%20%20%20%20%20%20%20%20p%3AP485%20%5B%20ps%3AP485%20%3FCorrespondenceAt%3B%20pq%3AP518%20wd%3AQ1277575%20%5D.%0A%20%20%7D%20%0A%20%20%20%20%20%20%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22%5BAUTO_LANGUAGE%5D%22.%7D%0A%7D%0A%0AORDER%20BY%20%28%3FDateofBirth%29%0A" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups" ></iframe>

<br>

Click the red dots on the map to see the names of records creators who have holdings at UVic SCUA, and to see where they are from. Note that some creators show up multiple times on the map, as they have lived in many locations.

<br>

_SPARQL query used to generate the map:_

```
#defaultView:Map
SELECT ?Creator ?CreatorLabel ?CorrespondenceAtLabel ?DateofBirthLabel ?ResidenceLabel ?LocationLabel ?CountryOfCitizenship ?Country ?Coordinates 
WHERE
{
  ?Creator wdt:P485 wd:Q47518588.
  
  OPTIONAL {?Creator wdt:P569 ?DateofBirth. }
  
  OPTIONAL {?Creator wdt:P27 ?CountryOfCitizenship. }
  
  OPTIONAL {?Creator wdt:P551 ?Residence.
            ?Residence wdt:P625 ?Coordinates.}
  
  OPTIONAL {?Creator wdt:P131 ?Location.
            ?Location wdt:P625 ?Coordinates.}
  
  OPTIONAL {?Creator wdt:P17 ?Country.
            ?Country wdt:625 ?Coordinates.}
  
  OPTIONAL {?Creator wdt:P485 wd:Q47518588;
           p:P485 [ ps:P485 ?CorrespondenceAt; pq:P518 wd:Q1277575 ].
  } 
      
  SERVICE wikibase:label { bd:serviceParam wikibase:language "[AUTO_LANGUAGE]".}
}

ORDER BY (?DateofBirth)
```
_*Using the [Wikidata Query Service](https://query.wikidata.org/), the results of this query can also be viewed as a table._

<br>

### _**When and where were these records creators born?**_

<iframe style="width: 55vw; height: 50vh; border: none;" src="https://query.wikidata.org/embed.html#%23defaultView%3ATimeline%0ASELECT%20%3FCreator%20%3FCreatorLabel%20%3FDateOfBirth%20%3FBirthPlace%20%3FBirthPlaceLabel%20%3FCoordinates%0A%7B%0A%20%20%3FCreator%20wdt%3AP485%20wd%3AQ47518588%3B%0A%20%20%20%20%20%20%20%20%20%20%20wdt%3AP569%20%3FDateOfBirth.%0A%20%20%0A%20%20OPTIONAL%20%7B%3FCreator%20wdt%3AP19%20%3FBirthPlace.%0A%20%20%20%20%20%20%20%20%20%20%20%20%3FBirthPlace%20wdt%3AP625%20%3FCoordinates.%7D%0A%20%20%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22%5BAUTO_LANGUAGE%5D%22.%7D%0A%7D%0AORDER%20BY%20%28%3FDateOfBirth%29%0A%0A" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups" ></iframe>

<br>

_SPARQL query used to generate the timeline:_
```
#defaultView:Timeline
SELECT ?Creator ?CreatorLabel ?DateOfBirth ?BirthPlace ?BirthPlaceLabel ?Coordinates
{
  ?Creator wdt:P485 wd:Q47518588;
           wdt:P569 ?DateOfBirth.
  
  OPTIONAL {?Creator wdt:P19 ?BirthPlace.
            ?BirthPlace wdt:P625 ?Coordinates.}
  
  SERVICE wikibase:label { bd:serviceParam wikibase:language "[AUTO_LANGUAGE]".}
}
ORDER BY (?DateOfBirth)
```
_*Using the [Wikidata Query Service](https://query.wikidata.org/), the results of this query can also be viewed as a table, a map, or a graph._

<br>

### _**What occupations do these records creators have?**_

<iframe style="width: 55vw; height: 50vh; border-style: solid; border-width: thin;" src="https://query.wikidata.org/embed.html#%23defaultView%3ABubbleChart%0ASELECT%20DISTINCT%20%3FOccupationLabel%20%28COUNT%20%28%3FCreator%29%20as%20%3FCount%29%0AWHERE%0A%7B%0A%20%20%3FCreator%20wdt%3AP485%20wd%3AQ47518588.%0A%20%20%3FCreator%20wdt%3AP106%20%3FOccupation.%0A%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22%5BAUTO_LANGUAGE%5D%22.%20%7D%0A%7D%0AGROUP%20BY%20%3FOccupationLabel%0AORDER%20BY%20DESC%20%28%3FCount%29%0A" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups" ></iframe>

<br>

_SPARQL query used to generate the bubble chart:_
```
#defaultView:BubbleChart
SELECT DISTINCT ?OccupationLabel (COUNT (?Creator) as ?Count)
WHERE
{
  ?Creator wdt:P485 wd:Q47518588.
  ?Creator wdt:P106 ?Occupation.

  SERVICE wikibase:label { bd:serviceParam wikibase:language "[AUTO_LANGUAGE]". }
}
GROUP BY ?OccupationLabel
ORDER BY DESC (?Count)
```
_*Using the [Wikidata Query Service](https://query.wikidata.org/), the results of this query can also be viewed as a table._

<br>

### _**Which records creators have which occupations?**_

<iframe style="width: 55vw; height: 50vh; border: none;" src="https://query.wikidata.org/embed.html#SELECT%20%3FOccupationLabel%20%3FCreatorLabel%20%3FCreator%20%3FDateOfBirth%20%0A%7B%0A%20%20%3FCreator%20wdt%3AP485%20wd%3AQ47518588%3B%0A%20%20%20%20%20%20%20%20%20%20%20wdt%3AP569%20%3FDateOfBirth.%0A%20%20%0A%20%20OPTIONAL%20%7B%3FCreator%20wdt%3AP106%20%3FOccupation.%7D%0A%20%20%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22%5BAUTO_LANGUAGE%5D%22.%7D%0A%7D%0AORDER%20BY%20%28%3FOccupationLabel%29" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups" ></iframe>

<br>

_SPARQL query used to generate the table:_
```
SELECT ?OccupationLabel ?CreatorLabel ?Creator ?DateOfBirth 
{
  ?Creator wdt:P485 wd:Q47518588;
           wdt:P569 ?DateOfBirth.
  
  OPTIONAL {?Creator wdt:P106 ?Occupation.}
  
  SERVICE wikibase:label { bd:serviceParam wikibase:language "[AUTO_LANGUAGE]".}
}
ORDER BY (?OccupationLabel)
```
_*Using the [Wikidata Query Service](https://query.wikidata.org/), the results of this query can also be viewed as a tree map, and a timeline._

<br>

### _**What are the languages spoken by the records creators?**_

<iframe style="width: 55vw; height: 50vh; border-style: solid; border-width: thin;" src="https://query.wikidata.org/embed.html#%23defaultView%3ABubbleChart%20%0ASELECT%20DISTINCT%20%3FLanguageLabel%20%28COUNT%20%28%3FCreator%29%20as%20%3FCount%29%0AWHERE%0A%7B%0A%20%20%3FCreator%20wdt%3AP485%20wd%3AQ47518588.%0A%20%20%3FCreator%20wdt%3AP1412%20%3FLanguage.%0A%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22%5BAUTO_LANGUAGE%5D%22.%20%7D%0A%7D%0AGROUP%20BY%20%3FLanguageLabel%0AORDER%20BY%20DESC%20%28%3FCount%29" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups" ></iframe>

<br>

_SPARQL query used to generate the bubble chart:_
```
#defaultView:BubbleChart 
SELECT DISTINCT ?LanguageLabel (COUNT (?Creator) as ?Count)
WHERE
{
  ?Creator wdt:P485 wd:Q47518588.
  ?Creator wdt:P1412 ?Language.

  SERVICE wikibase:label { bd:serviceParam wikibase:language "[AUTO_LANGUAGE]". }
}
GROUP BY ?LanguageLabel
ORDER BY DESC (?Count)
```
_*Using the [Wikidata Query Service](https://query.wikidata.org/), the results of this query can also be viewed as a table._

<br>

### _**Which records creators speak which languages?**_

<iframe style="width: 55vw; height: 50vh; border: none;" src="https://query.wikidata.org/embed.html#SELECT%20%3FLanguageLabel%20%3FCreatorLabel%20%3FCreator%20%3FDateOfBirth%20%0A%7B%0A%20%20%3FCreator%20wdt%3AP485%20wd%3AQ47518588%3B%0A%20%20%20%20%20%20%20%20%20%20%20wdt%3AP569%20%3FDateOfBirth.%0A%20%20%0A%20%20OPTIONAL%20%7B%3FCreator%20wdt%3AP1412%20%3FLanguage.%7D%0A%20%20%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22%5BAUTO_LANGUAGE%5D%22.%7D%0A%7D%0AORDER%20BY%20%28%3FLanguageLabel%29%0A" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups" ></iframe>

<br>

_SPARQL query used to generate the table:_
```
SELECT ?LanguageLabel ?CreatorLabel ?Creator ?DateOfBirth 
{
  ?Creator wdt:P485 wd:Q47518588;
           wdt:P569 ?DateOfBirth.
  
  OPTIONAL {?Creator wdt:P1412 ?Language.}
  
  SERVICE wikibase:label { bd:serviceParam wikibase:language "[AUTO_LANGUAGE]".}
}
ORDER BY (?LanguageLabel)
```

_*Using the [Wikidata Query Service](https://query.wikidata.org/), the results of this query can also be viewed as a tree map, and a timeline.*_

<br>

---

<br>

### **Experiment: Using Wikidata to identify correspondence held in archival fonds**
As part of this Wikidata project, I experimented with ways to highlight the relationships between creators who have fonds at UVic and their correspondents. Using the [Else Lübcke Seel fonds](https://uvic2.coppul.archivematica.org/else-lubcke-seel-fonds) as a case study, I identified all individuals who have correspondence held in Seel's fonds. I added the "archives at" (P485) property to each of Seel's correspondent's Wikidata pages, qualified by "applies to part, aspect, or form" (P518) → "correspondence" (Q1277575). I further qualified the "archives at" statement by listing Else Seel (Q94514551) as the "collection creator" (P6241). See the "archives at" statements section on [Ezra Pound's Wikidata page](https://www.wikidata.org/wiki/Q163366) for an example.

The following visualizaton results from this experimentation, highlighting that Else Seel corresponded with a variety of people, and that the resulting letters (addressed to Seel) are held together in Seel's fonds at UVic.

<iframe style="width: 74vw; height: 70vh; border-style: solid; border-width: thin;" src="https://query.wikidata.org/embed.html#%23defaultView%3ADimensions%0ASELECT%20%3FAddresseeLabel%20%3FCorrespondentLabel%20%3FCorrespondenceAtLabel%20%0AWHERE%0A%7B%0A%20%20%3FCorrespondent%20wdt%3AP485%20wd%3AQ47518588%3B%0A%20%20%20%20%20%20%20%20%20%20%20p%3AP485%20%5B%20ps%3AP485%20%3FCorrespondenceAt%3B%20pq%3AP518%20wd%3AQ1277575%20%5D.%0A%20%20VALUES%20%3FAddressee%20%7B%20wd%3AQ94514551%20%7D.%0A%20%20%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22%5BAUTO_LANGUAGE%5D%22.%7D%0A%7D%0A" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups" ></iframe>

<br>

_SPARQL query used to generate the dimensions:_
```
#defaultView:Dimensions
SELECT ?AddresseeLabel ?CorrespondentLabel ?CorrespondenceAtLabel 
WHERE
{
  ?Correspondent wdt:P485 wd:Q47518588;
           p:P485 [ ps:P485 ?CorrespondenceAt; pq:P518 wd:Q1277575 ].
  VALUES ?Addressee { wd:Q94514551 }.
  
  SERVICE wikibase:label { bd:serviceParam wikibase:language "[AUTO_LANGUAGE]".}
}
```
_*Using the [Wikidata Query Service](https://query.wikidata.org/), the results of this query can also be viewed as a table._
