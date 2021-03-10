# DATABASE SCHEMA OVERVIEW

The unified database hosting the schema and the risk data is stored at [https://github.com/GFDRR/rdl-data](https://github.com/GFDRR/rdl-data).

--WIP--
The database is implemented in PostgreSQL, using PostGIS for geospatial operations.
--WIP

The Risk DB schema includes four components:

- **Hazard** DB schema: describes hazard scenario footprints and return period hazard maps 
- **Exposure** DB schema: describes exposed assets and population
- **Vulnerability** DB schema: describes physical vulnerbaility, fragility and damage-to-loss models
- **Loss** DB schema: describes modelled damage and losses produced in a risk assessment

Below is a simplified entity-relationship diagram of the whole database schema. All tables are shown but only key fields are included in each table.
![Screenshot](img/all.png)
ERD for Risk Data schema including all components (Hazard, Exposure, Vulnerability and Loss). Yellow = common tables; Red = hazard tables; Green = Exposure tables; Purple = vulnerability tables; Violet = loss table.