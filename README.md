# GEM Global Active Faults

*Please note this is a work in progress; version 1 should be complete by the 
end of 2018.*

The [GEM Foundation's][gem] Global Active Faults project (GEM-GAF) is building 
a comprehensive, global dataset of active fault traces of seismogenic concern. 
The dataset comprises GIS files hosted here of fault traces and small amount of 
relevant attributes or metadata (fault geometry, kinematics, slip rate, etc.) 
useful for seismic hazard modeling and other tectonic applications. The dataset 
is being assembled primarily as a part of GEM's global Probabilistic Seismic 
Hazard Modeling efforts, although we hope that the data find wide use in 
research, education and general interest among many users.

The dataset is freely and publicly available here, under a Creative Commons 
attribution license.

The dataset currently covers most of the deforming continental regions on earth 
with the exceptions of, the Malay Archipelago, Madagascar, Canada, and a few 
other regions. These are to be added progressively through 2018.

The data is viewable in an interactive map [here][gaf-viewer].

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

[gem]: globalquakemodel.org
[gaf-viewer]: https://blogs.openquake.org/hazard/global-active-fault-viewer/
[tuple]: https://en.wikipedia.org/wiki/Tuple
