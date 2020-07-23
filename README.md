Project by Elizabeth Bassett, Special Collections and Archives Assistant (YCW) | July 2020

The goal of this project is to experiment with ways that the University of Victoria (UVic) Libraries can utilize Wikidata to promote interest in the holdings at Special Collections and University Archives (SCUA). The following visualizations use SPARQL queries and the [Wikidata Query Service](https://query.wikidata.org/) to compile information about people and institutions that have archives and correspondence held at UVIC SCUA. As more instances of the "archives at" (P485) property are used to connect SCUA with people and institutions with pages on Wikidata, the visualizations will become more representative of the Archives' holdings.

----

### Visualizing the Archives' Holdings through Wikidata Queries

_**Who has holdings in the Archives?**_ 

<iframe style="width: 55vw; height: 50vh; border: none;" src="https://query.wikidata.org/embed.html#SELECT%20%3FCreator%20%3FCreatorLabel%0AWHERE%0A%7B%0A%20%20%3FCreator%20wdt%3AP485%20wd%3AQ47518588.%0A%20%20%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22%5BAUTO_LANGUAGE%5D%22.%7D%0A%7D%0A%0A%20ORDER%20BY%20%28%3FCreatorLabel%29" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups" ></iframe>

This table includes both people and organizations that have archival fonds, collections, or correspondence held at UVic SCUA. Note that the list is not exhaustive, and only includes the records creators that have been linked to UVic through the "archives at" (P485) property on Wikidata.

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

_**Where are these records creators from?**_

<iframe style="width: 55vw; height: 50vh; border: none;" src="https://query.wikidata.org/embed.html#%23defaultView%3AMap%0ASELECT%20%3FCreator%20%3FCreatorLabel%20%3FCorrespondenceAtLabel%20%3FDateofBirthLabel%20%3FCountryLabel%20%3FCoordinates%20%3FResidenceLabel%0AWHERE%0A%7B%0A%20%20%3FCreator%20wdt%3AP485%20wd%3AQ47518588.%0A%20%20%0A%20%20OPTIONAL%20%7B%3FCreator%20wdt%3AP569%20%3FDateofBirth.%20%7D%0A%20%20%0A%20%20OPTIONAL%20%7B%3FCreator%20wdt%3AP27%20%3FCountry.%20%7D%0A%20%20%0A%20%20OPTIONAL%20%7B%3FCreator%20wdt%3AP551%20%3FResidence.%0A%20%20%20%20%20%20%20%20%20%20%20%20%3FResidence%20wdt%3AP625%20%3FCoordinates.%7D%0A%20%20%0A%20%20OPTIONAL%20%7B%3FCreator%20wdt%3AP485%20wd%3AQ47518588%3B%0A%20%20%20%20%20%20%20%20%20%20%20p%3AP485%20%5B%20ps%3AP485%20%3FCorrespondenceAt%3B%20pq%3AP518%20wd%3AQ1277575%20%5D.%0A%20%20%7D%20%0A%20%20%20%20%20%20%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22%5BAUTO_LANGUAGE%5D%22.%7D%0A%7D%0A%0AORDER%20BY%20%28%3FDateofBirth%29%0A" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups" ></iframe>

Click the red dots on the map to see the names of records creators who have holdings at UVic SCUA, and to see the cities that they lived in. Note that some creators show up multiple times on the map, as they have lived in many locations.

_SPARQL query used to generate the map:_

```
#defaultView:Map
SELECT ?Creator ?CreatorLabel ?CorrespondenceAtLabel ?DateofBirthLabel ?CountryLabel ?Coordinates ?ResidenceLabel
WHERE
{
  ?Creator wdt:P485 wd:Q47518588.
  
  OPTIONAL {?Creator wdt:P569 ?DateofBirth. }
  
  OPTIONAL {?Creator wdt:P27 ?Country. }
  
  OPTIONAL {?Creator wdt:P551 ?Residence.
            ?Residence wdt:P625 ?Coordinates.}
  
  OPTIONAL {?Creator wdt:P485 wd:Q47518588;
           p:P485 [ ps:P485 ?CorrespondenceAt; pq:P518 wd:Q1277575 ].
  } 
      
  SERVICE wikibase:label { bd:serviceParam wikibase:language "[AUTO_LANGUAGE]".}
}

ORDER BY (?DateofBirth)

```
_*Using the [Wikidata Query Service](https://query.wikidata.org/), the results of this query can also be viewed as a table._


_**What occupations do these records creators have?**_
<iframe style="width: 55vw; height: 50vh; border: none;" src="https://query.wikidata.org/embed.html#%23defaultView%3ABubbleChart%0ASELECT%20DISTINCT%20%3FOccupationLabel%20%28COUNT%20%28%3FCreator%29%20as%20%3FCount%29%0AWHERE%0A%7B%0A%20%20%3FCreator%20wdt%3AP485%20wd%3AQ47518588.%0A%20%20%3FCreator%20wdt%3AP106%20%3FOccupation.%0A%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22%5BAUTO_LANGUAGE%5D%22.%20%7D%0A%7D%0AGROUP%20BY%20%3FOccupationLabel%0AORDER%20BY%20DESC%20%28%3FCount%29%0A" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups" ></iframe>

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
