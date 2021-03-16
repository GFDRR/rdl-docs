## Folder tree and file naming

To help univocally identify the content of a dataset, the filename must summarise all the key information that allow to distinquish it from the others. 
 The general format, all in lower caps, is:

      `[component_code]-{project_name}-[country_iso]-{schema_specifics}-{time}`

 The name is made of [required] and {optional} attributes. Each component uses the most relevant attribute as schema_specifics, for example:

 - hzd-[country_iso]-{project_name}-{hazard_type}-{process_type}-{hazard_trigger}-{frequency}-{time}
         Example: pluvial flood hazard scenario with return period 10 years in 2050 for Afghanistan is named:
         **hzd-afg-mhra-fl-fpf-rp10-2050**
  
 - exp-[country_iso]-{project_name}-{occupancy}-{exposure_model}-{time}
         Example: residential exposure in Madagascar from Open Street Map 2015 is named:
         **exp-mdg-swio_rafi-residential-osm-2015**

 - vln-[country_iso]-{project_name}-{hazard_type}-{occupancy}-{vulnerability_model}
         Example: flood depth-damage function developed for India by JRC over industrial land cover is named:
         **vln-ind-fl-industrial-jrc**

 - lss-[country_iso]-{project_name}-{hazard_type}-{occupancy}-{time}
   Example: eartquake losses over Madagascar infrastructures over the period 1920-2012 is named:
   **lss-mdg-eq-infrastructrure-1920_2012**