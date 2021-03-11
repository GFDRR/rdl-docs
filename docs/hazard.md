# Hazard
The hazard schema stores data about the intensity and occurrance probability of physical hazard phenomena such as floods, eartquakes, wildfires or others. The specific hazard process can be defined and measured with a specific intensity unit. For example, earthquake hazard may be represented as ground shaking, liquefaction or ground displacement.

Hazard data are most often represented by geospatial grids (raster).

Some figures as data example?
[ex_hazards1] [ex_hazards2] [ex_hazards3]

The schema specifies which type of analysis and data methodology that has generated the dataset. It supports either simulated probabilistic scenarios and empirical observations. If the dataset has been produced for a specific location, such a city, the name of the location can be included.

|**Required**| **Attribute** | **Description** | **Type** |
|:---:| --- | --- | --- |
|*| Hazard type | Main hazard type from list of options | <ul><li>Coastal Flood<li>Convective Storm<li>Drought<li>Earthquake<li>Extreme Temperature<li>Flood<li>Landslide<li>Tsunami<li>Volcanic<li>Wildfire<li>Strong Wind<li>Multi-Hazard</ul> |
|*| Analysis type | Type of analysis that generated the data | <ul><li>Deterministic<li>Probabilistic |
|*| Calculation method | The methodology used for the modelling of hazard | <ul><li>Simulated<li>Observed<li>Inferred |
|| Geographic area | Specific location for which the dataset has been developed | Name of location |

<br>When the scenario modelled refers to a specific period of time, this can be specified in terms of dates, period span and reference year. For example, an observed flood event that occurred from 1.10.2009 (time start) to 3.10.2009 (time end), spanning over 3 days (time span). When precise time collocation is unknow or inappkicabile, a general reference date such as "2009" is used to identify events (time year). This is also useful to specify future scenario, e.g. time year: 2050.

|**Required**| **Attribute** | **Description** | **Type** |
|:---:| --- | --- | --- |
|| Time start | The time at which the modelled scenario starts | Date |
|| Time end | The time at which the modelled scenario ends | Date |
|| Time span | The duration of the modelled period | Number |
|| Time year | One reference year to univocally identify the scenario | Date (year) |

<br>When the hazard scenario is represented in probabilistic terms, the occurrance probability (frequency distribution) of hazard can be expressed in different ways. The most common way to communicate this is the "return period", expressed as the number of years after which a given hazard intensity could occurr again: RP 100 indicates that that event has a probability of once in 100 years. This attirbute can indicate individual layer frequency (RP100) or a range of frequencies for a collection of layers (RP10-100) The probability of occurrance is usually calculated on the basis of a reference period that provides observations: this period can be specified by start date, end date and time span. For example, an analysis of eartquake frequency based on seismic observations from 1934 (occurrance time start) to 2001 (occurrance time end), for a total count of 66 years (occurrance time span).

|**Required**| **Attribute** | **Description** | **Type** |
|:---:| --- | --- | --- |
|| Frequency type | The frequency of occurrence of the present event | <ul><li>Rate of Exceedence<li>Probability of Exceedence<li>Return Period</ul> |
|| Occurrance probability | For probabilistic scenario, the occurrance probability is expressed accordig to frequency type | Text |
|| Occurence time (start) | Start date of the period used to infer the occurrence probability | Date (year) |
|| Occurence time (end) | End date of the period used to specify the occurrence probability | Date (year) |
|| Occurence time (span) | The duration of the period used to specify either the frequency or the occurrence\_probability | Number of years |

<br>The schema distinguish between the hazard and process represented and the hazard and process identified as the cause, or concause for the manifestation of the represented hazard. For example, a dataset represent landslide hazard that is triggered by an earthquake will have Hazard type: Landslide; Trigger hazard type: Earthquake. The unit of measure refers to the represented hazard and process. A description can be added to cover additional information not included in the schema.

|**Required**| **Attribute** | **Description** | **Type** |
|:---:| --- | --- | --- |
|| Trigger hazard type | The hazard type that has triggered the event (if any) | Hazard type |
|| Trigger process type |  The process type that triggered the event (if any) | Process type |

<br>The hazard dataset could include one or more footprints for the same event, where each is one possible realisation (i.e. one footprint could represent minimum, another footprint the average and another one the maximum). The event uncertainty can be represented explicitly, through the inclusion of multiple footprints per event.

|**Required**| **Attribute** | **Description** | **Type** |
|:---:| --- | --- | --- |
|*| Hazard process | Specific hazard process | Process type |
|*| Unit of measure | Intensity measure of the process | Option list |
|| Description | Provides additional information about a specific event | Text |
|| Data uncertainty | The typology of uncertainty, if considered | Text |

<br><hr>

##Examples

Schema attributes for flood hazard maps related to occurrance probability of a river flood event of once in 100 years over Kabul, Afghanistan. The hydrological data used for modelling the intensity of floods is derived from observations over the period 1958-2001 (44 years). The intensity of hazard is measured as water depth in meters. These information cover all mandatory fields, and few optional fields.

![Screenshot](img/hzd_fl_kabul.jpg)

|**Required**| **Attribute** | **Example** |
|:---:| --- | --- |
|*| Hazard type | Flood |
|*| Analysis type | Probabilistic |
|*| Calculation method | Simulated |
|| Geographic area | Kabul |
|| Frequency type | Return Period |
|| Occurrance probability | 10 years |
|| Occurence time (start) | 1958 |
|| Occurence time (end) | 2001 |
|| Occurence time (span) | 44 years |
|*| Hazard process | River flood |
|*| Unit of measure | Water depth (m) |


<br><hr>

## Previous version (<a href="https://github.com/GFDRR/rdl-doc/issues/6">as in the GH issue</a>)
The _**Event set**_ stores one or more scenarios for a specific hazard. The main hazard type is defined by a specific code defined in common tables. Key attributes are:

|**Required**| **Attribute** | **Description** | **Example** |
|:---:| --- | --- | --- |
|*| Hazard type | Code provided in common tables | _FL_ for Floods  |
|| description | General details about this set of layers | _Simulated flood depth at country scale_ |
|*| is\_prob | Probabilistic or deterministic analysis. | _TRUE_ for probabilistic |

<br>Each **_Event_** is characterised by three main parameters: the methodology which originated the dataset; the specific occurrance probability, or frequency; and the main and secondary trigger processes which comes before the rapresented hazard in the cascade of events, and are identified as cause, or concause for the manifestation of the represented hazard.

|| **Field name** | **Description** | **Example** |
|:---:|---| --- | --- | 
|*| calculation\_method | The methodology used for the calculation of this event  | _Simulated_ for model simulations; _Observed_ for empirical data; _Inferred_ for models elaborated on empirical data (?) |
|| frequency | The frequency of occurrence of the present event | _0.01_ meaning probability of once in 100 years |
|| occurrence\_probability | The occurrance probability | ?? |
|| occurence\_time\_span | The duration (years) of the period used to specify either the frequency or the occurrence\_probability | _100_ |
|| trigger\_hazard\_type | Hazard type that triggered the event | _CS_ (Convective Storm) |
|| trigger\_process\_type |  Process type that triggered the event | _TCY_  (Tropical Cyclone) |
|| description | Provides additional information about this specific event | _The flood has been caused by heavy rainfall during cyclone Karen_ |

<br>For each **_Event_**, one more **_Footprint_set_** can be available, where each is one possible realisation of the event, i.e. one footprint could represent minimum, another footprint the average and another one the maximum. In this way, the event uncertainty can be represented explicitly, through the inclusion of multiple footprints per event. Hazard footprints can be assigned an occurrence frequency, and can represent a scenario footprint or return period hazard map. Inclusion of an event start and end time enables description of long-duration events.

|| **Field name** |  **Description** | **Example** |
|:---:| --- | --- | --- |
|*| process\_type | The typology of hazard process | _FPF_ for Pluvial flood |
|*| imt | Intensity measure types | _d_fpf:m_ for water depth |
|| data\_uncertainty | This attribute describes the typology of uncertainty | _Min to Max range_ |

<br><hr>
##Original version (<a href="https://github.com/GFDRR/rdl-doc">as from the other repo</a>)
The data structure contains entities nested as follows:

```
Event_set ( Event ( Footprint_set ( Footprint ( Footprint_data) ) ) )
```

The &quot;Event set&quot; stores one or more scenarios for a specific hazard. 
One &quot;Event&quot; represents one specific scenario (e.g. RP100, or one historical event). 
For each Event, one more &quot;Footprint\_set&quot; can be available.  This is a container for one or several &quot;Footprints&quot; where each is one possible realisation of an event. 
Uncertainty in the event characteristics and hazard footprint can be represented explicitly, through the inclusion of multiple events in an event set, and many footprints per event. 
Hazard footprints can be linked to another &#39;trigger event&#39; footprint to represent cascading hazards. 
Hazard footprints can be assigned an occurrence frequency, and can represent a scenario footprint or return period hazard map. 
Inclusion of an event start and end time enables description of long-duration events.

![Screenshot](img/hazard.png)
ERD (hazard schema): hazard table contents (red) and links to common tables (yellow).

###Table: _hazard.event\_set_

The &quot;event.set&quot; entity contains information on a set of events for a given area, with event set duration, description, bibliography and defines the event set as probabilistic or deterministic.
<div class="scrollbar table-scroll" markdown="1">

| **Req** | **Field name** | **Type** | **Reference table** | **Description** |
|:---:| --- | --- | --- | --- |
| **\*** | id | INT | | Unique number ID |
| **\*** | hazard\_type | VARCHAR | _cf\_common.hazard\_type_ | Unique 2-char code |
| **\*** | creation\_date | date | | The date of creation [ISO 8601 format] |
| | time\_start | timestamp | | The time at which the modelled scenario(s) starts [ISO 8601 format] |
| | time\_end | timestamp | | The time at which the modelled scenario(s) ends [ISO 8601 format] |
| | time\_duration | interval | | The extent of the time period covered by the events included in the current scenario hazard analysis [ISO 8601 format] |
| | description | TEXT | | General information about this specific scenario hazard analysis |
| | bibliography | TEXT | | Title and authors of studies containing relevant information |
| **\*** | is\_prob | BOOL | | Wheter the event set represents a probabilistic (TRUE) or a deterministic (FALSE) analysis. |
| **\*** | the\_geom | GEOM | | Associated geometry data (bounding box of data) |

</div>
<br/>
###Table: _hazard.event_

The &quot;Event&quot; entity contains information about one specific scenario or hazard map included in an &quot;Event Set&quot;. 
The information comprises event duration, occurrence probability or frequency, the hazard and process type, a link to a possible triggering event (for cascading events) and a text description for more context about magnitude, for example.
<div class="scrollbar table-scroll" markdown="1">

| **Req** | **Field name** | **Type** | **Reference table** | **Description** |
|:---:| --- | --- | --- | --- |
| **\*** | id | INT | | Unique number ID |
| **\*** | event\_set\_id | INT | _hazard.event\_set_ | Unique number ID of source exposure model |
| **\*** | calculation\_method | ENUM | | The methodology used for the calculation of this event |
| | frequency | FLOAT | | The frequency of occurrence of the present event (for the reference period see occurrence\_time\_span or occurrence\_time\_start and occurrence\_time\_end). |
| | occurrence\_probability | FLOAT | | The probability of occurrence in a given time interval defined either through the occurrence\_time\_start and occurrence\_time\_end or through the occurrence\_time\_span parameter. [float, adimensional]] |
| | occurence\_time\_start | timestamp | | The start date (and possibly time) of the time period used to specify either the frequency or the occurrence\_probability [ISO 8601 format] |
| | occurence\_time\_end | timestamp | | The end date (and possibly time) of the time period used to specify either the frequency or the occurrence\_probability [ISO 8601 format] |
| | occurence\_time\_span | interval | | The duration (years) of the period used to specify either the frequency or the occurrence\_probability |
| | trigger\_hazard\_type | VARCHAR | _cf\_common.hazard\_type_ | Hazard type that triggered the event |
| | trigger\_process\_type | VARCHAR | _cf\_common.process\_type_ | Process type that triggered the event |
| | trigger\_event\_id | INT | | The ID of a event which is trigger for the simulation of the corresponding footprints |
| | description | TEXT | | Provides additional information about this specific event |

</div>
<br/>
###Table: _hazard.footprint\_set_

The &quot;Footprint set&quot; entity contains a sub-group of the &quot;Footprints&quot; computed for an &quot;Event&quot;; all the &quot;Footprint&quot; in a &quot;Footprint Set&quot; have the same unit of measure, represent the same process type and their uncertainty is described in a homogenous way. Every &quot;Footprint Set&quot; instance will have the following attributes.

| **Req** | **Field name** | **Type** | **Reference table** | **Description** |
|:---:| --- | --- | --- | --- |
| **\*** | id | INT | | Unique number ID |
| **\*** | event\_id | INT | _hazard.event_ | The event.id parameter to which this footprint is associated |
| **\*** | process\_type | VARCHAR | _cf\_common.process\_type_ | The typology of hazard process |
| **\*** | imt | VARCHAR | | Intensity measure types |
| | data\_uncertainty | VARCHAR | | This attribute describes the typology of uncertainty |

<br/>
###Table: _hazard.footprint_

The &quot;Footprint&quot; entity contains information on a specific realisation of an &quot;Event&quot;. 
The uncertainty of a particular event is captured either by the construction of many footprints or by a single footprint which contains information about uncertainty.

| **Req** | **Field name** | **Type** | **Reference table** | **Description** |
|:---:| --- | --- | --- | --- |
| **\*** | id | INT | | Unique number ID |
| **\*** | footprint\_set\_id | INT | _hazard.footprint\_set_ | The footprint\_set.id parameter to which this footprint is associated |
| | trigger\_footprint | INT | | |
| | uncertainty\_2nd\_moment | FLOAT | | |

<br/>
###Table: _hazard.footprint\_data_

The &quot;Footprint\_data&quot; entity contains the footprint data: the value of intensity according to the intensity measure (IMT) described in &quot;Footprint set&quot;, and the point location of the intensity value.

| **Req** | **Field name** | **Type** | **Reference table** | **Description** |
|:---:| --- | --- | --- | --- |
| **\*** | id | INT | | Unique number ID |
| **\*** | footprint\_id | INT | _hazard.footprint_ | The footprint.id parameter to which this footprint data is associated |
| **\*** | the\_geom | GEOM | | Associated geometry data (point location) |
| **\*** | intensity | FLOAT | | The hazad process intensity value in the IMT described in &quot;Footprint set&quot; |

<br/>
###Types

| **ENUM name** | Types | Description |
| --- | --- | --- |
| calc\_method\_enum | <ul><li>Inferred<li>Simulated<li>Observed | Type of calculation method applied to produce hazard footprint. |

<br/>
