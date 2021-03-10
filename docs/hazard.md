## Hazard DB schema
The hazard schema stores hazard scenario footprints and probabilistic hazard maps for multiple hazards. 
Hazards can be further defined into process types, each with a defined intensity unit as in _cf\_common.imt_. 
For example, earthquake hazard may be represented as ground shaking, liquefaction or ground displacement.

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

<br/>
###Table: _hazard.event_

The &quot;Event&quot; entity contains information about one specific scenario or hazard map included in an &quot;Event Set&quot;. 
The information comprises event duration, occurrence probability or frequency, the hazard and process type, a link to a possible triggering event (for cascading events) and a text description for more context about magnitude, for example.

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
