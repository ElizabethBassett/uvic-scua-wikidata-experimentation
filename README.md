# UVic Special Collections and University Archives Wikidata Project
## Visualization Experimentation

Project by Elizabeth Bassett, Special Collections and Archives Assistant (YCW) | July, 2020

The goal of this project is to experiment with ways that UVic Libraries can utilize Wikidata to promote interest in the holdings at Special Collections and University Archives (SCUA). The following visualizations use SPARQL queries and the [Wikidata Query Service](https://query.wikidata.org/) to compile information about people and institutions that have archives and correspondence held at UVIC SCUA. As more instances of the "archives at" property are used to connect SCUA with people and institutions with pages on Wikidata, the visualizations will become more representative of the Archives' holdings.

### General Queries
**The following visualizations provide an overview of SCUA holdings**

#### Query: Creators with archives or correspondence at UVic SCUA

<iframe style="width: 80vw; height: 50vh; border: none;" src="https://query.wikidata.org/embed.html#%23defaultView%3AMap%0ASELECT%20%3FCreator%20%3FCreatorLabel%20%3FCorrespondenceAtLabel%20%3FDateofBirthLabel%20%3FCountryLabel%20%3FCoordinates%20%3FResidenceLabel%0AWHERE%0A%7B%0A%20%20%3FCreator%20wdt%3AP485%20wd%3AQ47518588.%0A%20%20%0A%20%20OPTIONAL%20%7B%3FCreator%20wdt%3AP569%20%3FDateofBirth.%20%7D%0A%20%20%0A%20%20OPTIONAL%20%7B%3FCreator%20wdt%3AP27%20%3FCountry.%20%7D%0A%20%20%0A%20%20OPTIONAL%20%7B%3FCreator%20wdt%3AP551%20%3FResidence.%0A%20%20%20%20%20%20%20%20%20%20%20%20%3FResidence%20wdt%3AP625%20%3FCoordinates.%7D%0A%20%20%0A%20%20OPTIONAL%20%7B%3FCreator%20wdt%3AP485%20wd%3AQ47518588%3B%0A%20%20%20%20%20%20%20%20%20%20%20p%3AP485%20%5B%20ps%3AP485%20%3FCorrespondenceAt%3B%20pq%3AP518%20wd%3AQ1277575%20%5D.%0A%20%20%7D%20%0A%20%20%20%20%20%20%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22%5BAUTO_LANGUAGE%5D%22.%7D%0A%7D%0A%0AORDER%20BY%20%28%3FDateofBirth%29%0A" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups" ></iframe>

#### SPARQL:

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


