## Loss DB schema

The modelled loss schema enables return period loss estimates and annual average loss to be stored and linked to a geographic unit. 
Loss datasets can be directly linked to the hazard, exposure, and vulnerability datasets which were used to create the modelled losses via fields in _loss.model_. 
The dataset also summarises the exposure and hazard types to which the losses relate, independent of those links. 

Enumerated types provide consistent categories for referencing losses as:
- Category: Buildings, Contents, Direct Damage to other Asset, or Business Interruption
- Frequency: Return Period, Probability of exceedance, or Rate of exceedance
- Loss type: Ground Up (economic) or Insured
- Metric: Annual average loss, Annual average loss ratio, or Probable maximum loss.

Each model has any number of loss maps which in turn have any number of geospatially referenced loss values. 
The meta-data in the loss map table describes the type of losses, occupancy, return period, metric used and so on. 
Similarly, a model can also have any number of loss curve maps, with any number of geospatially referenced loss curve value arrays. 
The associated loss and loss curve values may optionally include an asset reference to link to elements from an exposure model.

![Screenshot](img/loss.png)
ERD (modeled loss schema): loss table contents (violet) and links to common tables (yellow). The schema includes a SQL view (pink).

###Table: _loss.model_
Each entry in this table represents a single loss model, describing the hazard and process, and data used to generate the losses.

| **Req** | **Field name** | **Type** | **Reference table** | **Description** |
|:---:| --- | --- | --- | --- |
| **_\*_** | id | INT | | Unique number ID |
| **\*** | name | VARCHAR | _loss.model_ | Name of source model |
| | description | TEXT | | Description of source model |
| | hazard\_type | VARCHAR | _hazard.hazard\_type_ | 2-digit code |
| | process\_type | VARCHAR | _hazard.process\_type_ | 3-digit code |
| | hazard\_link | VARCHAR | | |
| | exposure\_link | VARCHAR | | |
| | vulnerability\_link | VARCHAR | | |

<br/>
###Table: _loss.map_
Each entry in this table represents a collection of loss values with unit and loss type and metric, for a given occupancy type, return period and loss component (building, contents) produced by a loss model. 
Loss exceedance curves are contained elsewhere, in _loss.curve\_map_.

| **Req** | **Field name** | **Type** | **Reference table** | **Description** |
|:---:| --- | --- | --- | --- |
| **\*** | id | INT | | Unique number ID |
| **\*** | loss\_model\_id | INT | _loss.model_ | Unique number ID of source loss model |
| **\*** | occupancy | _cf\_common.occupancy\_enum_ | | Destination of use of the asset |
| **\*** | component | _loss.component\_enum_ | | Type of affected component (e.g. buildings) |
| **\*** | loss\_type | _loss.loss\_type\_enum_ | | Type of loss (e.g. ground-up) |
| | return\_period | INT | | Number of return period in years |
| **\*** | units | VARCHAR | | Cost unit of measure |
| **\*** | metric | _loss.metric\_enum_ | | Type of loss metric (e.g. AAL) |

<br/>
###Table: _loss.map\_values_
Each entry in this table represents the loss value and location of the value, with the value relating to the information in _loss.map_.

| **Req** | **Field name** | **Type** | **Reference table** | **Description** |
|:---:| --- | --- | --- | --- |
| **\*** | id | BIGINT | | Unique number ID |
| **\*** | loss\_map\_id | INT | _loss.map_ | Unique number ID of reference loss map |
| | asset\_ref | VARCHAR | | Alphanumeric code that identifies asset from exposure model |
| **\*** | loss | FLOAT | | Loss value in the unit specified in loss\_map |
| **\*** | the\_geom | GEOM | | Associated geometry |

<br/>
###Table: _loss.curve\_map_
Each entry in this table represents a collection of loss exceedance curves associated with the loss model. 
It describes the unit, type and metric of the loss, which is provided for a given occupancy type, and loss component (building, contents) produced by a loss model. 

| **Req** | **Field name** | **Type** | **Reference table** | **Description** |
|:---:| --- | --- | --- | --- |
| **\*** | id | INT | | Unique number ID |
| **\*** | loss\_model\_id | INT | _loss.model_ | Unique number ID of reference loss model |
| **\*** | occupancy | cf\_common.occupancy\_enum | | Destination of use of the asset |
| **\*** | component | loss.component\_enum | | Component affected by loss |
| **\*** | loss\_type | loss.loss\_type\_enum | | Type of loss |
| **\*** | frequency | loss.frequency\_enum | | Frequency representation type |
| | investigation\_time | INT | | Investigation time in years (required if frequency is different from &#39;Return Period&#39;) |
| **\*** | units | VARCHAR | | Unit of measure of loss (e.g. USD, tons, etc) |

<br/>
###Table: _loss.curve\_map\_values_
Each entry in this table provides the values for a loss esceedance curve and location to which the curve relates, with the value relating to the information in _loss.curve\_map_.

| **Req** | **Field name** | **Type** | **Reference table** | **Description** |
|:---:| --- | --- | --- | --- |
| **\*** | id | BIGINT | | Unique number ID |
| **\*** | loss\_curve\_map\_id | INT | _loss.map_ | Unique number ID of reference loss curve map |
| | asset\_ref | VARCHAR | | Alphanumeric code that identifies asset from exposure model |
| **\*** | losses | VARCHAR | | Loss values in the unit specified in _loss\_curve\_map_ |
| **\*** | rates | FLOAT | | Rate values associates with losses |
| **\*** | the\_geom | GEOM | | Associated geometry |

<br/>
###Types

Includes 4 types including the options for asset categories to which loss refers to, how the frequency is expressed, what is the metric in use and the types of losses.

| **ENUM name** | Types | Description |
| --- | --- | --- |
| Category\_enum | <ul><li>Buildings<li>Indicator<li>Infrastructure<li>Crops, livestock and forestry | Types of possible asset categories, consistent with the exposure schema. Indicators refers for example to population density or GDP; infrastructure refers for example to roads, or electricity grid. |
| frequency\_enum | <ul><li>Rate of Exceedence<li>Probability of Exceedence<li>Return Period | How the frequency value reported in _loss.curve\_map_ is expressed.|
| metric\_enum | <ul><li>AAL<li>AALR<li>PML | Type of loss metric used in _loss.curve\_map_ and _loss.map_<br/><br/>Note:<br>AAL = Annual Average Losses<br>AALR = Average Annual Loss Ratio<br>PML = Probable Maximal Loss (also known as Return Period Loss) |
| loss\_type\_enum | <ul><li>Ground Up<li>Insured | Type of losses in _loss.curve\_map_ and _loss.map_.|

<br/>
