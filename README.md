 
## Overview

The purpose of this project is to assess the reliability of official COVID-19 mortality numbers, by comparing them to 
estimated excess mortality observed during the pandemic.  
It stems from the striking observed difference between Belgium and other countries, according to official COVID-19 
numbers.

The analysis is carried on for England & Wales, France, Netherlands and Belgium.  

**Last update**: 22-04-2020  
**Data available up to**: 05-04-2020 (12-04-2020 for NL and E&W)

## TL;DR : Results

 As of week 14 (ending 05-04-2020), the analysis yields (see [here](#computing-excess-mortality) for the explanation 
 of the cumulation period) :
 
 | Country        | Weeks      | Excess deaths per M | Excess deaths | Official COVID-19 deaths  | Underestimation   |
 | -------------  | ---------- | -------------       | -----         | -----                     | ----              |
 | Belgium        | 11-14      | 280.71              | 3231          | 2373                      | 26.56%            |
 | Netherlands    | 11-14      | 279.09              | 4832          | 2203                      | 54.41%            |
 | France         | 11-14      | 213.63              | 14327         | 7560                      | 47.23%            |
 | E&W            | 12-14      | 147.46              | 8853          | 4971                      | 43.85%            |

So, if the excess mortality estimate is deemed reliable, and attributable to COVID-19, it appears Belgium official numbers
are closer to the reality (off by 26%), while other countries tend to underestimate by a factor 2 (42-54 %).  
 
 Since E&W are 1 week earlier in the evolution of the pandemic, the numbers for Week 15 (already available for E&W) are
 more relevant for a comparison of these countries :
 
  | Country        | Weeks      | Excess deaths per M | Excess deaths | Official COVID-19 deaths  | Underestimation   |
  | -------------  | ---------- | -------------       | -----         | -----                     | ----              |
  | E&W (W15)      | 12-15      | 294.17              | 17660         | 10122                     | 42.68%            |

Taking this into account and aligning numbers on the observed start of the death rate increase (as explained 
[here](#computing-excess-mortality)), it appears Belgium, Netherlands and E&W are very close in terms of excess death 
rate (280-290 per M), while France has a lower excess death rate (213 per M).  
However, it must be noted that aligning weekly data like this is very hazardous, as the error margin for such an 
alignment is of several days.

## Produced datasets

The results consist of several data files, published in this repository :
 * [summary.csv](./data/summary.csv) : a summarized view, starting on week 10, with key values as in the table above
 * [weekly-raw-data.csv](./data/weekly-raw-data.csv)  : all weekly data from 2010 until today, for all countries, 
 absolute and normalized against population
 * [weekly-mortality-BE.csv](./data/weekly-mortality-BE.csv), [weekly-mortality-FR.csv](./data/weekly-mortality-FR.csv), 
 [weekly-mortality-NL.csv](./data/weekly-mortality-NL.csv), [weekly-mortality-EW.csv](./data/weekly-mortality-EW.csv) : 
 per country ; weekly data aligned on week number for every year, averaged over 10 years, computed 2020 difference 
 (per M and absolute), comparison with official COVID-19 numbers
 
## Collecting raw data

The data used to produce these aggregated datasets is of four kinds :
 * weekly or daily deaths statistics, from 2010 onwards [[1](#f1), [6](#f6), [8](#f8), [10](#f10), [12](#f12), 
 [14](#f14)]
 * yearly population, from 2010 onwards [[2](#f2), [3](#f3), [9](#f9)]
 * recent deaths counts from all causes, for 2020 and until now [[1](#f1), [7](#f7), [10](#f10), [12](#f12)]
 * Official COVID mortality [[4](#f4), [5](#f5), [11](#f11), [13](#f13), [15](#f15), [16](#f16)]

#### Remarks
 * The yearly population for 2020 was extrapolated from the 10 previous years.

 * Week boundaries differ between countries : BE, NL, FR compute statistics from Monday to Sunday, 
while UK statistics are computed from Saturday to Friday.  
The data produced here are aligned on monday-sunday. As a result, UK data is offset by two days 
if compared to other countries. E.g. UK data for week 14, 2020 actually ends on March 3rd, while it ends on March 5th 
for other countries.

## Computing excess mortality
For every country, weekly mortality is normalized by population of the respective year, then averaged 
over the last 10 years.  
This average, normalized weekly mortality is used as a baseline to compute the apparent excess mortality in 2020, 
per million.

The date to start summing up the excess deaths (the hypothetic pandemic start date) is the week before the first week 
that exceeds the mean mortality by 1 sigma. This yields :

 | Country        | WeekNb | 
 | -------------  | ------ | 
 | Belgium        | 11     |
 | Netherlands    | 11     | 
 | France         | 11     |
 | E&W            | 12     | 

The total number of excess deaths is computed by summing up weekly excess deaths since those dates. 

This number can be then compared with the official COVID-19 death numbers.

## Licenses
The datasets produced in this project are licensed under CC BY 4.0 .

All source datasets (below) are exposed with a license at least as permissive as a CC-BY license : 
 - https://www.ons.gov.uk :  Open Government Licence v3.0
 - https://www.nhs.uk/ : Open Government Licence v3.0 (as per https://www.nhs.uk/our-policies/terms-and-conditions)
 - https://www.insee.fr : [INSEE License](https://www.insee.fr/fr/information/2381863)
 - https://opendata.cbs.nl : CC BY 4.0
 - https://www.rivm.nl : [CC-BY equivalent license](https://www.rivm.nl/copyright)
 - https://sciensano.be : [CC-BY equivalent license](https://epistat.wiv-isp.be/momo/#copyright)
 - https://statbel.fgov.be : [Statbel license](https://statbel.fgov.be/sites/default/files/files/opendata/Licence%20open%20data_FR.pdf) 

Remark : Although NHS UK advertises an open data license (above), the England and Wales NHS portals (used in this 
project) are less clear on that subject.

## Disclaimer
While being done in good faith and with best efforts, the datasets produced are provided "as is", 
with no warranty of accuracy, completeness, or usefulness.  
The author shall not be held liable for misuse or damage resulting from the use of this data. 

## Data Sources

   #### &nbsp;&nbsp;&nbsp;&nbsp; UK (England & Wales)   
1. <a id="f1"></a> [Deaths registered weekly in England and Wales, provisional](https://www.ons.gov.uk/peoplepopulationandcommunity/birthsdeathsandmarriages/deaths/datasets/weeklyprovisionalfiguresondeathsregisteredinenglandandwales),
   https://www.ons.gov.uk/, Open Government Licence v3.0
2. <a id="f2"></a> [England population mid-year estimate](https://www.ons.gov.uk/peoplepopulationandcommunity/populationandmigration/populationestimates/timeseries/enpop/pop),
   https://www.ons.gov.uk/, Open Government Licence v3.0
3. <a id="f3"></a> [Wales population mid-year estimate](https://www.ons.gov.uk/peoplepopulationandcommunity/populationandmigration/populationestimates/timeseries/wapop/pop),
   https://www.ons.gov.uk/, Open Government Licence v3.0       
4. <a id="f4"></a> [Public Health Wales - Rapid COVID-19 Surveillance](https://public.tableau.com/profile/public.health.wales.health.protection#!/vizhome/RapidCOVID-19virology-Public/Headlinesummary),
   https://phw.nhs.wales, Open Government Licence v3.0   
5. <a id="f5"></a> [Public Health England - COVID-19 Daily Deaths](https://www.england.nhs.uk/statistics/statistical-work-areas/covid-19-daily-deaths/),
   https://www.england.nhs.uk, Open Government Licence v3.0   
   
   #### France   
6. <a id="f6"></a> [T79JDEC – Répartition quotidienne des décès (Séries depuis 1968 pour la France métropolitaine, 1998 pour la France entière)](https://www.insee.fr/fr/statistiques/fichier/4204054/T79JDEC.xls),
   https://www.insee.fr/fr/statistiques/4204054, [INSEE License](https://www.insee.fr/fr/information/2381863)
7. <a id="f7"></a> [Nombre de décès quotidiens par département](https://www.insee.fr/fr/information/4470857),
   https://www.insee.fr/fr/information/4470857, [INSEE License](https://www.insee.fr/fr/information/2381863)
8. <a id="f8"></a> [Démographie - Nombre de décès - France (inclus Mayotte à partir de 2014)](https://www.insee.fr/fr/statistiques/serie/001641603),
   https://www.insee.fr/fr/statistiques/serie/001641603, [INSEE License](https://www.insee.fr/fr/information/2381863)
9. <a id="f9"></a> [Estimation de la population au 1ᵉʳ janvier 2020](https://www.insee.fr/fr/statistiques/1893198), 
   https://www.insee.fr/fr/statistiques/1893198, [INSEE License](https://www.insee.fr/fr/information/2381863)
   
   #### Netherlands   
10. <a id="f10"></a> [Overledenen; geslacht en leeftijd, per week](https://opendata.cbs.nl/statline/#/CBS/nl/dataset/70895ned), 
   https://opendata.cbs.nl, CC BY 4.0
11. <a id="f11"></a> [Aantal overledenen naar datum van overlijden](https://www.rivm.nl/coronavirus-covid-19/grafieken), 
   https://www.rivm.nl, [CC-BY equivalent license](https://www.rivm.nl/copyright)
   
    #### Belgium   
12. <a id="f12"></a> [BE-MoMo daily deaths](https://epistat.wiv-isp.be/data/Belgium_DailyepistatPub.csv), 
   [Belgian Mortality Monitoring - Sciensano](https://epistat.wiv-isp.be/momo), [CC-BY equivalent license](https://epistat.wiv-isp.be/momo/#copyright) 
13. <a id="f13"></a> [COVID-19 – Bulletin Epidémiologique Hebdomadaire](https://covid-19.sciensano.be/fr/covid-19-situation-epidemiologique), 
   [COVID-19 Monitoring - Sciensano](https://covid-19.sciensano.be), [CC-BY equivalent license](https://epistat.wiv-isp.be/momo/#copyright)
14. <a id="f14"></a> [Number of deaths per day (2008-2018)](https://statbel.fgov.be/en/open-data/number-deaths-day),
   https://statbel.fgov.be, [Statbel license](https://statbel.fgov.be/sites/default/files/files/opendata/Licence%20open%20data_FR.pdf)
15. <a id="f15"></a> [Dataset of mortality by date, age, sex, and region](https://epistat.sciensano.be/Data/COVID19BE_MORT.csv),
   [COVID-19 Monitoring - Sciensano](https://epistat.wiv-isp.be/covid/), [CC-BY equivalent license](https://epistat.wiv-isp.be/momo/#copyright) 
    
    #### Other   
16. <a id="f16"></a> [Data on COVID-19 by Our World in Data](https://github.com/owid/covid-19-data/tree/master/public/data), 
  https://ourworldindata.org, CC-BY