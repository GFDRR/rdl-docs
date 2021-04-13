# Taxonomy

*Suggest having an overview page, plus one page for taxonomy details. For each taxonomy provide:*

 - a description of its scope and purpose
 - which existing taxonomy it is based on
 - a table of values, with relevant codes/identifiers, names and a description
 - a CSV download of the vocabulary (and possibly other formats in future)
 - any notes about mapping to/from other taxonomies to help people use them

<hr>

##Hazard taxonony

There are several existing taxonomies that could be adopted to descibe hazard data. Some examples:

- [**UNDRR**](https://www.undrr.org/publication/hazard-definition-and-classification-review) (formerly UNISDR) recently proposed an extended taxonomy that covers 300 natural and anthropogenic hazards in 8 categories (Meteo-Hydrological, Geohazard, Environmental, Extraterrestrial, Chemical, Biological, Technological, Societal).
<br><br>

- [**Disaster Risk Management Knowledge Centre**](https://drmkc.jrc.ec.europa.eu/risk-data-hub) covers 32 natural and anthropogenic hazards in 8 categories (Geophysical, Hydrological, Meteorological, Climatological, Biological, Technological, Transportation, Malicious).
<br><br>

- [**Inspire**](https://inspire.ec.europa.eu/codelist/NaturalHazardCategoryValue) covers 25 natural hazards in 6 categories (Geological/hydrological, Meteorological/climatological, Fires, Biological, Cosmic, Other).
<br><br>

- [**EM-DAT**](https://www.emdat.be/classification) covers 34 natural and technological hazards in 9 categories (Geophysical, Meteorological, Hydrological, Climatological, Biological, Extraterrestrial, Industrial accident, Transport accident, Miscelleanous accident).
<br><br>

- [**Munich-RE**](https://www.cred.be/downloadFile.php?file=sites/default/files/DisCatClass_264.pdf) covers 27 natural hazards 13 main categories (Geophysical, Meteorological, Hydrological, Climatological, Biological, Extraterrestrial).
<br><br>

The RDL project performed a long review of all the proposed alternatives, and collected numerous feedbacks from risk data scientists and users.
This resulted in an new effort which aims to unify the existing taxonomies for the purpose of risk data classification, focusing on those hazards and processes that are more often required in disaster risk assessments while mapping and matching alternative definitions into one consistent framework.
The **RDL hazard taxonomy** classifies hazard phenomena as main hazard (8 categories) and hazard process (27 categories).

**DRAFT**

<div class="scrollbar table-scroll" markdown="1">

| **Hazard type** | **Process type** |
|---|---|
| Coastal Flood | Coastal Flood |
| Coastal Flood | Storm Surge |
| Convective Storm | Tornado |
| Drought | Agricultural Drought |
| Drought | Hydrological Drought |
| Drought | Meteorological Drought |
| Drought | Socio-economic Drought |
| Earthquake | Primary Rupture |
| Earthquake | Secondary Rupture |
| Earthquake | Ground Motion |
| Earthquake | Liquefaction |
| Extreme Temperature | Extreme cold |
| Extreme Temperature | Extreme heat |
| Flood | Fluvial Flood |
| Flood | Pluvial Flood |
| Landslide | Landslide |
| Landslide | Snow Avalanche |
| Tsunami | Tsunami |
| Volcanic | Ashfall |
| Volcanic | Ballistics |
| Volcanic | Proximal hazards |
| Volcanic | Lahar |
| Volcanic | Lava |
| Volcanic | Pyroclastic Flow |
| Wildfire | Wildfire |
| Strong Wind | Extratropical cyclone |
| Strong Wind | Tropical cyclone |

</div>

<br>
[**Datasheet with mapping of hazard taxonomies**]()

<hr>

##Exposure taxonomy 

The exposure schema can accomodate different descriptions of assets using a taxonomy which describes their characteristics (e.g. building occupancy, construction, age, height, etc. or road surface type).

- [**GED4all**](ged4all.md): developed by GFDRR under the UK-DFID Challenge Fund, this open exposure database schema is meant for multi-hazard risk analysis. GED4ALL can be populated with building-level data from OpenStreetMap (OSM) following the [guidance](https://wiki.openstreetmap.org/wiki/GED4ALL) from the Humanitarian OSM Team, which collects contributions from the community on how OSM tags can be best aligned with the GED4ALL taxonomy. This is the suggested option for classification of exposure data in the RDL.
<br><br>

- [**GEM-OpenQuake**](https://platform.openquake.org/taxtweb): developed specifically for the Global Earthquake Model (GEM), this taxonomy is dedicated to buildings for which it describe the size and properties (height, number of storeys, age, occupancy, material, type of roof, floor and foundations).
<br><hr>