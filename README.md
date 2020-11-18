# GEM Global Active Faults Database (GEM GAF-DB)

[![DOI](https://zenodo.org/badge/91775241.svg)](https://zenodo.org/badge/latestdoi/91775241)


The [GEM Foundation's][gem] Global Active Faults is building a comprehensive, 
global dataset of active fault traces of seismogenic concern. The GEM GAF-DB 
comprises GIS files hosted here of fault traces and small amount of relevant 
attributes or metadata (fault geometry, kinematics, slip rate, etc.) useful for 
seismic hazard modeling and other tectonic applications. The dataset is being 
assembled primarily as a part of GEM's global Probabilistic Seismic Hazard 
Modeling efforts, although we hope that the data find wide use in research, 
education and general interest among many users.

The dataset is freely and publicly available here, under a Creative Commons 
attribution sharealike license.

The dataset currently covers most of the deforming continental regions on earth 
with the exceptions of the Malay Archipelago, Madagascar, Canada, and a few 
other regions.

The data is viewable in an interactive map [here][gaf-viewer].

## Citation

The GEM GAF-DB has been published in *Earthquake Spectra*.  The citation
is:

Styron, Richard, and Marco Pagani. “The GEM Global Active Faults Database.” 
*Earthquake Spectra*, vol. 36, no. 1_suppl, Oct. 2020, pp. 160–180, 
doi:10.1177/8755293020944182.

The link to the publication is here: 
<https://journals.sagepub.com/doi/abs/10.1177/8755293020944182>

## Data Format

### Data Table
Attribute            | Data Type | Description                  | Example
---------------------|-----------|------------------------------|------------
dip                  | tuple     | Dip                           | (40,30,50)
dip_dir             | string    | Dip direction                 |         W 
downthrown_side_id | string    | direction of downthrown side  |        NE 
average_rake        | tuple     | Slip rake of fault            | (45,25,55)
slip_type           | string    | Kinematic type                | Sinistral  
strike_slip_rate   | tuple     | Strike slip rate on fault   |(1.5,0.5,2.5)
dip_slip_rate      | tuple     | Dip slip rate               |(1.5,0.5,2.5)
vert_slip_rate     | tuple     | Vertial slip rate           |(1.5,0.5,2.5)
shortening_rate     | tuple     | Horizontal shortening rate  |(1.5,0.5,2.5)
accuracy            | integer   | Denominator of map scale    |       40000
activity_confidence | integer   | Certainty of neotectonic activity |     1 
exposure_quality    | integer   | How well exposed (visible) fault is |   2 
epistemic_quality   | integer   | Certainty that fault exists here |      1 
last_movement       | string    | Date of last earthquake       |     1865  
name                 | string    | Name of fault zone            | Polochic  
fz_name             | string    | Name of fault zone    | Motagua-Polochic   
reference            | string    | Paper used        | Rogers and Mann, 2007 
notes                | string    | Any relevant info | May be creeping
ogc_fid              | integer   | ID used by GIS    |                    8
catalog_id           | string    | Global ID         |               CCARA_8

### Data Types

There are three main data types used in the GAF attribute table, `tuple`, 
`integer` and `string`.

A `tuple` is a 3-[tuple] of real (floating-point or integer) numbers 
representing continuous random variables such as slip rate. The tuple has the 
format `(most-likely, min, max)`. In some instances where there is no estimated 
uncertainty in the parameter of interest, the tuple may be simply given as 
`(most-likely,,)`; this is most common for the dip of purely strike-slip 
faults. In typed databases it is actually represented by a string, so the 
parentheses and commas will be preserved.  `Rake` is in Aki-Richards 
convention. All slip rate fields except `shortening_rate` describe the slip 
rate or component on the actual fault, and are in magnitudes, i.e. are always 
positive. `shortening_rate` describes the horizontal contraction rate (heave) 
of a fault (such as a GPS measurement); this is not the dip slip rate. 
Extension across a fault is negative.

An `Integer` is used as a categorical variable in this database, typically to 
denote the relative epistemic uncertainty in a parameter.  `1` is most certain, 
`2` is moderately uncertain, and `3` is highly uncertain.  The other uses of 
`Integer` types are for table indices in many constituent datasets, and in the 
`accuracy` attribute which denotes the denominator of the map scale during 
fault mapping and digitization; for example, a fault that was mapped in GIS at 
a 1/40,000 (or 1:40,000) scale will have an accuracy of `40000`.

`String`s for fields with words.


# Constituent Datasets
The GEM GAF-DB is compiled from a variety of regional to global active fault 
datasets. These are given here:

  Coverage Region               |Reference                 |Peer-Review|Dataset Name (if any)
  ------------------------------|--------------------------|-----------|-----------------------------
  New Zealand                   |Litchfield et al., 2014   |Yes        |*none*
  Australia                     |Allen et al., 2018        |Yes        |*none*
  East Africa                   |Macgregor, 2014           |Yes        |*none*
  Middle East                   |Danciu et al., 2018       |Yes        |EMME
  South America                 |Alvarado et al., 2017     |No         |SARA
  Europe                        |Woessner et al., 2015     |Yes        |SHARE
  Northern Andes                |Veloza et al., 2012       |Yes        |Active Tectonics of the Andes
  Indo-Asian Collision Zone     |Styron et al., 2010       |Yes        |HimaTibetMap
  Philippines                   |Penarubia et al., 2019    |Yes        |*none*
  US mainland                   |Petersen et al., 2014     |Yes        |HazFaults
  California                    |Dawson and Weldon, 2013   |Yes        |UCERF3
  Taiwan                        |Shyu et al., 2016         |Yes        |*none*
  Mexico                        |Villegas et al., 2017     |Yes        |*none*
  Southeast Asia                |Chan et al., 2017         |No         |*none*
  Northeast Asia                |Styron et al., 2018       |No         |*none*
  North Africa                  |Styron and Poggi, 2018    |Yes        |*none*
  Central America and Caribbean |Styron et al., 2020       |Yes        |CCAF
  Global (various regions)      |Christophersen et al. 2015|Yes        |Faulted Earth
  Global (plate boundaries)     |Bird, 3002                |Yes        |PB2002

Full reference information is given below.  Please note that these are subject 
to regular change.

# File Formats

The database is currently available in 4 formats, [GeoJSON], [GeoPackage], KML, 
and [ESRI ShapeFile]. Which file format is most appropriate depends on the 
software package that is being used. QGIS users and anyone making webmaps or an 
API will find the GeoJSON format most useful. This is also the version of 
record as it is tracked best with version control. However, ESRI does not seem 
to provide acceptable GeoJSON support; ArcGIS users should be able to use the 
GeoPackage format (note that we have no access to ArcGIS and are unable to test 
these files for compatibility). ESRI's legacy ShapeFile format is also provided 
but this is not a good choice as that format truncates both column names and 
longer text fields such as `Notes`.

**If you are downloading individual files instead of cloning the repository:** 
Please note that GitHub may display a version of the data that is formatted for 
viewing within its built-in webmap, and not display the actual data. If you 
press the 'Download' button, however, you may download the real file.


Additional file formats will be provided once the Version 1 of the database is 
complete; if you have specific needs, please contact richard dot styron at 
globalquakemodel.org.

# Contributing

Contributions to the GEM GAF-DB are highly encouraged. Please see the page on
[contributing] for more details.

[contribuing]: ./contributing.md

# References

Allen TI, Griffin J, Ghasemi H, Leonard M, Clark D and Geoscience Australia 
(2018) The 2018 National Seismic Hazard Assessment for Australia: model 
overview. ISBN 978-1-925848-00-7. URL https://doi.org/10.11636/Record.2018.027. 
OCLC: 1089757486.

Alvarado A, Audemard F, Benavente Escobar C, Santibanez Boric I, Cembrano 
Perasso J, Costa C, Delgado Madera GF, García-Pelaez JA, Masquelin E, Minaya E, 
López MC, Paolini M, Perez I, Grupo de Neotectónica de SEGEMAR and Styron R 
(2017) the South American Risk Assessment Active Fault Database. 
DOI:10.13117/SARA-ACTIVE-FAULTS. URL https://github.com/ 
GEMScienceTools/SARA-Active-Faults.

Bird P (2003) An updated digital model of plate boundaries. Geochemistry, 
Geophysics, Geosystems 4(3): 1027. DOI:10.1029/
2001GC000252. URL 
http://onlinelibrary.wiley.com/doi/10.1029/2001GC000252/abstract.

Chan CH, Wang Y, Shi X, Ornthammarath T, Warnitchai P, Kosuwan S, Thant M, 
Nguyen PH, Nguyen LM, Solidum Jr R and others
(2017) Toward uniform probabilistic seismic hazard assessments for Southeast 
       Asia. In: AGU Fall Meeting Abstracts.

Christophersen A, Litchfield N, Berryman K, Thomas R, Basili R, Wallace L, Ries 
W, Hayes GP, Haller KM, Yoshioka T, Koehler
RD, Clark D, Wolfson-Schwehr M, Boettcher MS, Villamor P, Horspool N, 
Ornthammarath T, Zuñiga R, Langridge RM, Stirling MW, Goded T, Costa C and 
Yeats R (2015b) Development of the Global Earthquake Model’s neotectonic fault 
database. Natural Hazards 79(1): 111–135. DOI:10.1007/s11069-015-1831-6. URL 
https://link.springer.com/article/10.1007/ s11069-015-1831-6.

Danciu L, S ̧es ̧etyan K, Demircioglu M, Gülen L, Zare M, Basili R, Elias A, 
Adamia S, Tsereteli N, Yalçın H, Utkucu M, Khan MA,
Sayab M, Hessami K, Rovida AN, Stucchi M, Burg JP, Karakhanian A, Babayan H, 
Avanesyan M, Mammadli T, Al-Qaryouti M, Kalafat D, Varazanashvili O, Erdik M 
and Giardini D (2018) The 2014 Earthquake Model of the Middle East: seismogenic 
sources. Bulletin of Earthquake Engineering 16(8): 3465–3496. 
DOI:10.1007/s10518-017-0096-8. URL https://doi.org/10.1007/

Dawson T and Weldon R (2013) Geologic-Slip-Rate Data and Geologic Deformation 
Model. In: Uniform California earthquake rupture
forecast, version 3 (UCERF3), number 228 in California Geological Survey 
Special Report.

Litchfield NJ, Dissen RV, Sutherland R, Barnes PM, Cox SC, Norris R, Beavan RJ, 
Langridge R, Villamor P, Berryman K, Stirling M, Nicol A, Nodder S, Lamarche G, 
Barrell DJA, Pettinga JR, Little T, Pondard N, Mountjoy JJ and Clark K (2014) A 
model of active faulting in New Zealand. New Zealand Journal of Geology and 
Geophysics 57(1): 32–56. DOI:10.1080/00288306.2013.854256. URL 
https://doi.org/10.1080/00288306.2013.854256.

Macgregor D (2015) History of the development of the East African Rift System: 
A series of interpreted maps through time. Journal of African Earth Sciences 
101: 232–252. DOI:10.1016/j.jafrearsci.2014.09.016. URL 
http://www.sciencedirect.com/ science/article/pii/S1464343X14003240.

Peñarubia C, Kendra Johnson, Styron RH, Sevilla WIG, Perez JS, Bonita JD, Narag 
IC, Solidum Jr RU, Pagani MM, Allen TI and Allen TI (2019) Probabilistic 
Seismic Hazard Analysis model for the Philippines. Earthquake Spectra. In 
press.

Petersen MD, Moschetti MP, Powers PM, Mueller CS, Haller KM, Frankel AD, Zeng 
Y, Rezaeian S, Harmsen S, Boyd O and others (2014) Documentation for the 2014 
update of the United States national seismic hazard maps, Open-File Report 
2014-1091. Technical Report 2014-1091, U.S. Geological Survey, Reston, VA. URL 
https://dx.doi.org/10.3133/ofr20141091.

Shyu JBH, Chuang YR, Chen YL, Lee YR and Cheng CT (2016) A New On-Land 
Seismogenic Structure Source Database from the Taiwan Earthquake Model (TEM) 
Project for Seismic Hazard Analysis of Taiwan. Terrestrial, Atmospheric and 
Oceanic Sciences 27(3): 311. DOI:10.3319/TAO.2015.11.27.02(TEM). URL 
http://tao.cgu.org.tw/index.php/articles/archive/ geophysics/item/1376.

Styron R and Poggi V (2018) GEM North Africa Active Fault Database. 
DOI:10.13117/N-AFRICA-ACTIVE-FAULTS. URL 
https://github.com/GEMScienceTools/n_africa_active_faults.

Styron R, Garcia-Pelaez J and Pagani M (????) CCAF-DB: The Caribbean and 
Central American Active Fault Database. Natural Hazards and Earth System 
Science, In revision

Styron R, Poggi V and Lunina OV (2018) GEM Northeastern Asia Active Fault 
Database. DOI:10.13117/NE-ASIA-ACTIVE-FAULTS. URL 
https://github.com/GEMScienceTools/ne-asia-active-faults.

Styron R, Taylor M and Okoronkwo K (2010) Database of Active Structures From 
the Indo-Asian Collision. Eos, Transactions American Geophysical Union 91(20): 
181–182. DOI:10.1029/2010EO200001. URL http://onlinelibrary.wiley.com/doi/10. 
1029/2010EO200001/abstract.

Veloza G, Styron R, Taylor M and Mora A (2012) Open-source archive of active 
faults for northwest South America. GSA Today 22(10): 4–10. 
DOI:10.1130/GSAT-G156A.1. URL 
http://www.geosociety.org/gsatoday/archive/22/10/abstract/
i1052-5173-22-10-4.htm.

Woessner J, Laurentiu D, Giardini D, Crowley H, Cotton F, Grünthal G, Valensise 
G, Arvidsson R, Basili R, Demircioglu MB, Hiemer S, Meletti C, Musson RW, 
Rovida AN, Sesetyan K, Stucchi M and The SHARE Consortium (2015) The 2013 
European Seismic Hazard Model: key components and results. Bulletin of 
Earthquake Engineering 13(12): 3553–3596. DOI:10.1007/s10518-015-9795-1. URL
https://doi.org/10.1007/s10518- 015- 9795- 1.


[gem]: globalquakemodel.org
[gaf-viewer]: https://blogs.openquake.org/hazard/global-active-fault-viewer/
[tuple]: https://en.wikipedia.org/wiki/Tuple
[GeoJSON]: http://geojson.org/
[GeoPackage]: https://www.geopackage.org/
[ESRI ShapeFile]: https://support.esri.com/en/white-paper/279

