Contributing to the GEM Global Active Faults Database
=====================================================

The GEM GAF-DB is a public, open-data project and contribution is quite welcome.

The GEM GAF-DB is a compilation of a set of regional and global fault datasets;
most of these are not produced by GEM, but instead have been collected from
external sources. The final database is built with a Python script that handles
the compilation. Therefore, there is no single, permanent dataset that one can
modify to contribute.

Instead, contribution can take several forms:
1. *The addition to the 'miscellaneous' dataset*

   This [dataset][misc] is intended to capture individual faults that are not present
   in the regional dataset for an area, though the dataset has worldwide scope.
   If you have studied a fault that isn't present, or you have new data on a
   fault that is already present, this is likely the best option. 

2. *The modification of a regional dataset*

   This option is best if you have data for faults in an area
   that is covered by one of the fault catalogs maintained by GEM or that is
   otherwise open for modification (e.g., HimaTibetMap or the Active Tectonics
   of the Andes catalogs).

3. *The addition of a new regional dataset*

    If you have a dataset that covers some region with higher fidelity or more
    data than the existing coverage of that region, it's easy to incorporate
    this data into the GAF-DB compilation. 


### Addition to the miscellaneous dataset
The miscellaneous fault dataset can be found [here][misc]. If you want to
contribute to it, one easy method for those familiar with git and GitHub is
to clone that repository, make a new branch, and then add your mapping to the
`.geojson` file. Once your edits are complete, you can submit the changes as
a pull request to the repository.

If you're not familiar with git and GitHub, you can just email [Richard
Styron](mailto:richard.styron@globalquakemodel.org) with the dataset. Ideally
you would be able to send it as a `.geojson` file and use the format of the
GAF-DB (described below, and available [here][blank] as a geopackage template,
or you can use the GAF-DB or the [miscellaneous][misc] file as a template)
but we can work with just about anything.


[blank]: https://blogs.openquake.org/hazard/uploads/master_df_schema.gpkg
[misc]: https://github.com/GEMScienceTools/gem_gaf_misc_faults


### Modification of a regional dataset

If you have fault data for a region that is covered by a GEM dataset or a
dataset that we (or you!) have administrative access to, it could be better to
add to or modify this dataset instead of adding data to the miscellaneous
dataset. This way, users of the regional dataset will be able to use your
updates in addition to users of the global database. 

Current GEM regional datasets include:
- [Central America and the Caribbean](https://github.com/GEMScienceTools/central_am_carib_faults)
- [North Africa](https://github.com/GEMScienceTools/n_africa_active_faults)
- [Northeast Asia](https://github.com/GEMScienceTools/ne-asia-active-faults)
- [South America](https://github.com/GEMScienceTools/SARA-Active-Faults)

with Canada and East Africa slated for mapping in 2019.

The [HimaTibetMap][htm] and [Active Tectonics of the Andes][ata] datasets are
also administered by Richard Styron, GEM's active fault scientist, and additions
or modifications to this dataset may also be incorporated. Finally, if you
administer one of the other regional datasets used by GEM, we would be happy to
work with you on incorporating any improvements.

The process for addition or modification of these datasets is the same as for
the miscellaneous datasets mentioned above: if you are comfortable with GitHub,
updates can be done to the geojson file in a branch and merged through pull
requests. If you're not, then just email me the data
(richard.styron@globalquakemodel.org).


### Addition of a new regional dataset

If you have a comprehensive dataset that covers some region better than what we
have, we can incorporate that data directly, and basically remove the existing
faults from the region during the data harmonization step of the GAF-DB
compilation. If you want to do this, email richard.styron@globalquakemodel.org
and we can discuss the best way to make the data available.


### Data licensing

The GEM GAF-DB is licensed under a [Creative Commons Attribution License][cc].
Any new data or modifications to existing data will have to comply with this
license. 

### Referencing and acknowledgement

We want the scientists who produce the fault data used in the GEM GAF-DB to be
recognized for their efforts. Any data that you contribute will cite you in the
metadata for that structure, though it is up to you how exactly you would prefer
to be cited--whether as an individual (or group of individuals), as your
institution, or through a publication or report that describes the data.

## Data format
The GEM GAF-DB is a vector GIS file with lines representing the traces of active
faults, and attributes (metadata) providing information on fault geometry,
kinematics, slip rate, references, and other relevant information.

### Mapping style

Geologic mapping involves a component of interpretation that is a bit
subjective, and with structural mapping of fault systems, the geologist has to
make some decisions about how to best represent complicated, fractal structures
on a map. There is no unique right way to represent structures (though there are
certainly wrong ways), and there is real variation in the spatial layout and
connectivity of fault systems throughout the world's deforming regions.

Given GEM's focus on seismic hazard and risk, we have chosen a mapping style
that considers each structure to be an independent seismic source, and do not
include structures too small to cause damaging earthquakes or those that are
obviously subsidiary to larger structures and surely linked at shallow depths.
Each structure should be represented by a single GIS line that has no branches
and represents a full rupture on that fault or fault segment. Mapped fault
segments may link if attributes such as dip or slip rate changes along strike.

We acknowledge that the science on some of these issues is not settled and we
emphasize that the rules for what faults get included are not set in stone (ha
ha) but should reflect the geologic and societal context of the structures as
well as the expediency and clarity of the map. For example, a 6 km long normal
fault with an estimated 0.1 mm/yr slip rate may not be included if it is hard to
distinguish in the field and remote sensing imagery, and lies in an uninhabited
region with larger and faster-slipping faults around; however the same fault
should be included if it lies beneath a city, can be quickly and accurately
mapped, or is one of the major structures of a deforming zone.

Faults that are mapped in the style of the USGS Quaternary Faults and Folds
database are not ideal for the GEM GAF-DB: this style of fault data has many
small fault traces that do not each characterize a single seismic source, so it
is quite difficult to incorporate these structures into seismic hazard analysis,
or any other quantitative analysis of the data. 

A longer discussion of these issues is present in [this blog
post][map_criteria]. Please review it before contributing, or if you are
interested in neotectonic mapping in general.


### Attributes

The metadata (GIS attributes) for the GAF-DB are given in the table below. It is
not expected that each fault will have all of this information, but at minimum a
fault will need kinematic and geometric data (dip direction, etc.) to be
included. If the data is present in a different format, that is fine, and we
will get it in shape for inclusion.

The following table and data types description are copied verbatim from [this
blog post][map_criteria]; please read that post for a more full description, and
email richard.styron@globalquakemodel.org with any questions.

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
upper_seis_depth    | tuple   | Upper depth of sesmic release |(0.,,)
lower_seis_depth    | tuple   | Lower depth of sesmic release |(12.,,)
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

#### Data types

There are a few data types given here:

  - `tuple`: This data type represents *continuous random variables*[^1] in a 
    tuple (ordered sequence) format. In the GEM databases, tuples are given 
    values for the `(most likely, minimum, maximum)` for each variable, which 
    more or less represent a triangular probability distribution. If no 
    variability is necessary, the tuple is represented as `(most likely,,)`. 
    The use of a tuple instead of a single field for each parameter lets us 
    keep the number of fields in the database down, which reduces file size and 
    makes data entry faster. It does mean that some additional parsing 
    functions have to be written to perform quantitative analysis. Individuals 
    or organizations with different needs can choose a format that suits their 
    needs.

  - `string`: Strings (i.e. a sequence of characters in computer science terms) 
    represent textual data of any sort.

  - `integer`: Integers in the GEM fault datasets are for categorical variables 
    or indices. The categorical variables define levels of uncertainty: `0` is 
    well known, `1` less so, and `2` very poorly known.

[^1]: A *continuous random variable* is a number that may take any value 
between some minimum and maximum including negative and positive infinity. This 
may be due to either a lack of firm knowledge (epistemic uncertainty) or 
natural variability (aleatoric variability). A *discrete random variable* is a 
random variable that may take a value from some discrete (non-continuous) set 
of values, but no values in between (if they exist). A dice roll, for example, 
is a discrete random variable. Categorical random variables are as well; an 
example is the day of the week I was born on—I don't know this off-hand but it 
was almost certainly one of the seven days I learned in school.

## Data review and approval

All submitted data will, of course, need to be reviewed for accuracy and
consistency with the GEM GAF-DB. There is no formal review process, but we will
look the data over and reserve the right to make the final decision on what is
included and what is not. If you are willing to contribute, we will be happy to
work with you to make sure that the contributions are acceptable.


[cc]: https://creativecommons.org/licenses/by/4.0/
[htm]: https://github.com/HimaTibetMap/HimaTibetMap
[ata]: https://github.com/ActiveTectonicsAndes/ATA
[map_criteria]: https://blogs.openquake.org/hazard/2018/07/18/mapping-active-faults-for-fault-databases-and-seismic-hazard-analysis/
