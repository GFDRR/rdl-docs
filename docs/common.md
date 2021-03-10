
## Common tables
Each schema has specific tables, but as part of the database schema harmonization process, the _cf\_common_ schema contains tables that are shared among each schema. This ensures consistent hazard naming, intensity parameters and licences within each schema.

###Table: _cf\_common.contribution_

The _hazard.contribution_ table includes general information about the dataset, such as the name of the source model which identifies the data, the name of project that produced the data, the purpose of the data, additional notes, model version (for data version control) and data license.

| **Req** | **Field name** | **Type** | **Reference table** | **Description** |
|:---:| --- | --- | --- | --- |
| **\*** | id | INT || Unique number ID |
| **\*** | component | ENUM | _cf\_common.component_enum_ | Unique number ID |
| **\*** | set\_id | INT || Unique number ID of set |
| **\*** | model\_source | VARCHAR || Name of source model |
| **\*** | model\_date | DATE || Model release date |
| | project | VARCHAR | | Project under which data has been produced |
| | purpose | TEXT | | Purpose for what the data has been produced |
| | notes | TEXT | | Details about the dataset |
| | bibliography | TEXT | | Title and authors of documents containing relevant information |
| | version | VARCHAR | | Version of the dataset |
| **\*** | geo\_coverage | VARCHAR | _cf\_common.iso_ | ISO code(s) of countries covered by the dataset, comma-separated |
| **\*** | contributed\_at | timestamp | | Date of contribution |
| **\*** | license\_code | VARCHAR | _cf\_common.license_ | Type of license |
| **\*** | publish | BOOLEAN | | Show/Hide dataset from webpage |

<br/>

Five additional tables provide the code and name for specific hazard and process, intensity measures, license types and country coverage.

1. The _cf\_common.hazard\_type_ table contains the hazard codes and related names.
2. The _cf\_common.process\_type_ table contains the process type codes and related names (each hazard may have more than one process).
3. The _cf\_common.imt_ table contains the intensity measure for each process and its description.
4. The _cf\_common.license_ table provides a list of supported open-data licenses and url for more detailed information.
5. The _cf\_common.iso_ table lists the ISO 3166 alpha-3 codes for countries, to specify datasets coverage.

|     Table name                |     Required    |     Field name      |     Type       |     Description                         |
|-------------------------------|:---------------:|:-------------------:|:--------------:|:---------------------------------------:|
|     cf_common.hazard_type     |         *       |     code            |     VARCHAR    |     Unique 2-char code                  |
|                               |         *       |     name            |     VARCHAR    |     Name of hazard                      |
|-------------------------------|-----------------|---------------------|----------------|-----------------------------------------|
|     cf_common.process_type    |         *       |     hazard_code     |     VARCHAR    |     Unique 2-char code                  |
|                               |         *       |     code            |     VARCHAR    |     Unique 3-char code                  |
|                               |         *       |     name            |     VARCHAR    |     Name of hazard process              |
|-------------------------------|-----------------|---------------------|----------------|-----------------------------------------|
|     cf_common.imt             |         *       |     process_code    |     VARCHAR    |     Unique 3-char code                  |
|                               |         *       |     hazard_code     |     VARCHAR    |     Unique 2-char code                  |
|                               |         *       |     im_code         |     VARCHAR    |     Alphanumeric code                   |
|                               |         *       |     description     |     VARCHAR    |     Description of unit of measure      |
|                               |         *       |     units           |     VARCHAR    |     Unit of measure                     |
|-------------------------------|-----------------|---------------------|----------------|-----------------------------------------|
|     cf_common.license         |         *       |     code            |     VARCHAR    |     Alphanumeric code                   |
|                               |         *       |     name            |     VARCHAR    |     Name of license                     |
|                               |                 |     notes           |     TEXT       |     Additional notes                    |
|                               |         *       |     url             |     VARCHAR    |     License url reference               |
|-------------------------------|-----------------|---------------------|----------------|-----------------------------------------|
|     cf_common.iso             |         *       |     code            |     VARCHAR    |     ISO 3166 ALPHA-3 country code       |
|                               |         *       |     name            |     VARCHAR    |     Country name			   |

<br/>
The content of these common tables is as follows:

###Table: _cf\_common.hazard\_type_

| **code** | **name** |
|---|---|
| **CF** | Coastal Flood |
| **CS** | Convective Storm |
| **DR** | Drought |
| **EQ** | Earthquake |
| **ET** | Extreme Temperature |
| **FL** | Flood |
| **LS** | Landslide |
| **MH** | Multi-Hazard |
| **TS** | Tsunami |
| **VO** | Volcanic |
| **WF** | Wildfire |
| **WI** | Strong Wind |

<br/>

###Table: _cf\_common.process\_type_

| **code** | **hazard\_code** | **name** |
|---|---|---|
| **FCF** | CF | Coastal Flood |
| **FSS** | CF | Storm Surge |
| **TOR** | CS | Tornado |
| **DTA** | DR | Agricultural Drought |
| **DTH** | DR | Hydrological Drought |
| **DTM** | DR | Meteorological Drought |
| **DTS** | DR | Socio-economic Drought |
| **Q1R** | EQ | Primary Rupture |
| **Q2R** | EQ | Secondary Rupture |
| **QGM** | EQ | Ground Motion |
| **QLI** | EQ | Liquefaction |
| **ECD** | ET | Extreme cold |
| **EHT** | ET | Extreme heat |
| **FFF** | FL | Fluvial Flood |
| **FPF** | FL | Pluvial Flood |
| **LAV** | LS | Snow Avalanche |
| **LSL** | LS | Landslide (general) |
| **TSI** | TS | Tsunami |
| **VAF** | VO | Ashfall |
| **VBL** | VO | Ballistics |
| **VFH** | VO | Proximal hazards |
| **VLH** | VO | Lahar |
| **VLV** | VO | Lava |
| **VPF** | VO | Pyroclastic Flow |
| **WFI** | WF | Wildfire |
| **ETC** | WI | Extratropical cyclone |
| **TCY** | WI | Tropical cyclone |

<br/>

###Table: _cf\_common.imt_

| **_process\_code_** | **_hazard\_code_** | **_im\_code_** | **_description_** |
|---|---|---|---|
| **QGM** | EQ | PGA:g | Peak ground acceleration in g |
| **QGM** | EQ | PGA:m/s2 | Peak ground acceleration in m/s2 |
| **QGM** | EQ | PGV:m/s | Peak ground velocity in m/s |
| **QGM** | EQ | SA(0.2):g | Spectral acceleration with 0.2s period |
| **QGM** | EQ | SA(0.3):g | Spectral acceleration with 0.3s period |
| **QGM** | EQ | SA(1.0):g | Spectral acceleration with 1.0s period |
| **QGM** | EQ | SA(3.0):g | Spectral acceleration with 3.0s period |
| **QGM** | EQ | SA(0.2):m/s2 | Spectral acceleration with 0.2s period |
| **QGM** | EQ | SA(0.3):m/s2 | Spectral acceleration with 0.3s period |
| **QGM** | EQ | SA(1.0):m/s2 | Spectral acceleration with 1.0s period |
| **QGM** | EQ | SA(3.0):m/s2 | Spectral acceleration with 3.0s period |
| **QGM** | EQ | Sd(T1):m | Spectral displacement |
| **QGM** | EQ | Sv(T1):m/s | Spectral velocity |
| **QGM** | EQ | PGDf:m | Permanent ground deformation |
| **QGM** | EQ | D\_a5-95:s | Significant duration a5-95 |
| **QGM** | EQ | D\_a5-75 :s | Significant duration a5-75 |
| **QGM** | EQ | IA:m/s | Arias intensity (IÎ±) or (IA) or (Ia) |
| **QGM** | EQ | Neq:- | Effective number of cycles |
| **QGM** | EQ | EMS:- | European macroseismic scale |
| **QGM** | EQ | AvgSa:m/s2 | Average spectral acceleration |
| **QGM** | EQ | I\_Np:m/s2 | I\_Np by BojÃ³rquez and Iervolino |
| **QGM** | EQ | MMI:- | Modified Mercalli Intensity |
| **QGM** | EQ | CAV:m/s | Cumulative absolute velocity |
| **QGM** | EQ | D\_B:s | Bracketed duration |
| **FFF** | FL | d\_fff:m | Flood water depth |
| **FPF** | FL | d\_fpf:m | Flood water depth |
| **FFF** | FL | v\_fff:m/s | Flood flow velocity |
| **FPF** | FL | v\_fpf:m/s | Flood flow velocity |
| **TCY** | WI | v\_tcy(3s):km/h | 3-sec at 10m sustained wind speed (kph) |
| **ETC** | WI | v\_ect(3s):km/h | 3-sec at 10m sustained wind speed (kph) |
| **TCY** | WI | v\_tcy(1m):km/h | 1-min at 10m sustained wind speed (kph) |
| **ETC** | WI | v\_ect(1m):km/h | 1-min at 10m sustained wind speed (kph) |
| **TCY** | WI | v\_tcy(10m):km/h | 10-min sustained wind speed (kph) |
| **ETC** | WI | v\_etc(10m):km/h | 10-min sustained wind speed (kph) |
| **TCY** | WI | PGWS\_tcy:km/h | Peak gust wind speed |
| **ETC** | WI | PGWS\_ect:km/h | Peak gust wind speed |
| **LSL** | LS | d\_lsl:m | Landslide flow depth |
| **LSL** | LS | I\_DF:m3/s2 | Debris-flow intensity index |
| **LSL** | LS | v\_lsl:m/s2 | Landslide flow velocity |
| **LSL** | LS | MFD\_lsl:m | Maximum foundation displacement |
| **LSL** | LS | SD\_lsl:m | Landslide displacement |
| **LSL** | LS | LSI:- | Landslide susceptibility Index |
| **LSL** | LS | haz\_lsl:- | Landslide hazard index |
| **TSI** | TS | Rh\_tsi:m | Tsunami wave runup height |
| **TSI** | TS | d\_tsi:m | Tsunami inundation depth |
| **TSI** | TS | MMF:m4/s2 | Modified momentum flux |
| **TSI** | TS | F\_drag:kN | Drag force |
| **TSI** | TS | Fr:- | Froude number |
| **TSI** | TS | v\_tsi:m/s | Tsunami velocity |
| **TSI** | TS | F\_QS:kN | Quasi-steady force |
| **TSI** | TS | MF:m3/s2 | Momentum flux |
| **TSI** | TS | h\_tsi:m | Tsunami wave height |
| **TSI** | TS | Fh\_tsi:m | Tsunami Horizontal Force |
| **VAF** | VO | h\_vaf:m | Ash fall thickness |
| **VAF** | VO | L\_vaf:kg/m2 | Ash loading |
| **FSS** | CF | v\_fss:m/s | Maximum water velocity |
| **FSS** | CF | d\_fss:m | Storm surge inundation depth |
| **DTA** | DR | CMI:- | Crop Moisture Index |
| **DTM** | DR | PDSI:- | Palmer Drought Severity Index |
| **DTM** | DR | SPI:- | Standard Precipitation Index |

<br/>

###Table: _cf\_common.license_

| **code** | **name** | **description** | **url** |
|---|---|---|---|
| **CC0** | Creative Commons CCZero (CC0) | Dedicate to the Public Domain (all rights waived) | https://creativecommons.org/publicdomain/zero/1.0/ |
| **CC BY 4.0** | Creative Commons Attribution 4.0 (CC-BY-4.0) | | https://creativecommons.org/licenses/by/4.0/ |
| **CC BY-SA 4.0** | Creative Commons Attribution Share-Alike 4.0 (CC-BY-SA-4.0) | | http://creativecommons.org/licenses/by-sa/4.0/ |
| **ODbL** | Open Data Commons Open Database License (ODbL) | Attribution-ShareAlike for data(bases) | https://opendatacommons.org/licenses/odbl/summary/ |
| **ODC-By** | Open Data Commons Attribution License(ODC-BY) | Attribution for data(bases) | https://opendatacommons.org/licenses/by/summary/ |

<br/>

###Table: _cf\_common.iso_

| **code** | **name** |
|---|---|
| ABW | Aruba |
| AFG | Afghanistan |
| AGO | Angola |
| AIA | Anguilla |
| ALB | Albania |
| AND | Andorra |
| ARE | United Arab Emirates |
| ARG | Argentina |
| ARM | Armenia |
| ASM | American Samoa |
| ATG | Antigua and Barbuda |
| AUS | Australia |
| AUT | Austria |
| AZE | Azerbaijan |
| BDI | Burundi |
| BEL | Belgium |
| BEN | Benin |
| BFA | Burkina Faso |
| BGD | Bangladesh |
| BGR | Bulgaria |
| BHR | Bahrain |
| BHS | The Bahamas |
| BIH | Bosnia and Herzegovina |
| BLM | Saint-Barthélemy |
| BLR | Belarus |
| BLZ | Belize |
| BMU | Bermuda |
| BOL | Bolivia |
| BRA | Brazil |
| BRB | Barbados |
| BRN | Brunei |
| BTN | Bhutan |
| BWA | Botswana |
| CAF | Central African Republic |
| CAN | Canada |
| CHE | Switzerland |
| CHL | Chile |
| CHN | People's Republic of China |
| CIV | Ivory Coast |
| CMR | Cameroon |
| COD | Democratic Republic of the Congo |
| COG | Republic of the Congo |
| COK | Cook Islands |
| COL | Colombia |
| COM | Comoros |
| CPV | Cape Verde |
| CRI | Costa Rica |
| CUB | Cuba |
| CUW | Curaçao |
| CYM | Cayman Islands |
| CYP | Cyprus |
| CZE | Czech Republic |
| DEU | Germany |
| DJI | Djibouti |
| DMA | Dominica |
| DNK | Denmark |
| DOM | Dominican Republic |
| DZA | Algeria |
| ECU | Ecuador |
| EGY | Egypt |
| ERI | Eritrea |
| ESP | Spain |
| EST | Estonia |
| ETH | Ethiopia |
| FIN | Finland |
| FJI | Fiji |
| FLK | Falkland Islands |
| FRA | France |
| FRO | Faroe Islands |
| FSM | Federated States of Micronesia |
| GAB | Gabon |
| GBR | United Kingdom |
| GEO | Georgia |
| GGY | Guernsey |
| GHA | Ghana |
| GIB | Gibraltar |
| GIN | Guinea |
| GMB | The Gambia |
| GNB | Guinea-Bissau |
| GNQ | Equatorial Guinea |
| GRC | Greece |
| GRD | Grenada |
| GRL | Greenland |
| GTM | Guatemala |
| GUM | Guam |
| GUY | Guyana |
| HKG | Hong Kong |
| HMD | Heard Island and McDonald Islands |
| HND | Honduras |
| HRV | Croatia |
| HTI | Haiti |
| HUN | Hungary |
| IDN | Indonesia |
| IMN | Isle of Man |
| IND | India |
| IRL | Ireland |
| IRN | Iran |
| IRQ | Iraq |
| ISL | Iceland |
| ISR | Israel |
| ITA | Italy |
| JAM | Jamaica |
| JEY | Jersey |
| JOR | Jordan |
| JPN | Japan |
| KAZ | Kazakhstan |
| KEN | Kenya |
| KGZ | Kyrgyzstan |
| KHM | Cambodia |
| KIR | Kiribati |
| KNA | Saint Kitts and Nevis |
| KOR | South Korea |
| KWT | Kuwait |
| LAO | Laos |
| LBN | Lebanon |
| LBR | Liberia |
| LBY | Libya |
| LCA | Saint Lucia |
| LIE | Liechtenstein |
| LKA | Sri Lanka |
| LSO | Lesotho |
| LTU | Lithuania |
| LUX | Luxembourg |
| LVA | Latvia |
| MAC | Macau |
| MAF | Saint Martin |
| MAR | Morocco |
| MCO | Monaco |
| MDA | Moldova |
| MDG | Madagascar |
| MDV | Maldives |
| MEX | Mexico |
| MHL | Marshall Islands |
| MKD | Republic of Macedonia |
| MLI | Mali |
| MLT | Malta |
| MMR | Myanmar |
| MNE | Montenegro |
| MNG | Mongolia |
| MNP | Northern Mariana Islands |
| MOZ | Mozambique |
| MRT | Mauritania |
| MSR | Montserrat |
| MUS | Mauritius |
| MWI | Malawi |
| MYS | Malaysia |
| NAM | Namibia |
| NCL | New Caledonia |
| NER | Niger |
| NFK | Norfolk Island |
| NGA | Nigeria |
| NIC | Nicaragua |
| NIU | Niue |
| NLD | Netherlands |
| NOR | Norway |
| NPL | Nepal |
| NRU | Nauru |
| NZL | New Zealand |
| OMN | Oman |
| PAK | Pakistan |
| PAN | Panama |
| PCN | Pitcairn Islands |
| PER | Peru |
| PHL | Philippines |
| PLW | Palau |
| PNG | Papua New Guinea |
| POL | Poland |
| PRI | Puerto Rico |
| PRK | North Korea |
| PRT | Portugal |
| PRY | Paraguay |
| PSE | Palestine |
| PYF | French Polynesia |
| QAT | Qatar |
| ROU | Romania |
| RUS | Russia |
| RWA | Rwanda |
| SAU | Saudi Arabia |
| SDN | Sudan |
| SEN | Senegal |
| SGP | Singapore |
| SGS | South Georgia and the South Sandwich Islands |
| SHN | Saint Helena |
| SLB | Solomon Islands |
| SLE | Sierra Leone |
| SLV | El Salvador |
| SMR | San Marino |
| SOM | Somalia |
| SPM | Saint Pierre and Miquelon |
| SRB | Serbia |
| SSD | South Sudan |
| STP | São Tomé and Príncipe |
| SUR | Suriname |
| SVK | Slovakia |
| SVN | Slovenia |
| SWE | Sweden |
| SWZ | eSwatini |
| SXM | Sint Maarten |
| SYC | Seychelles |
| SYR | Syria |
| TCA | Turks and Caicos Islands |
| TCD | Chad |
| TGO | Togo |
| THA | Thailand |
| TJK | Tajikistan |
| TKM | Turkmenistan |
| TLS | East Timor |
| TON | Tonga |
| TTO | Trinidad and Tobago |
| TUN | Tunisia |
| TUR | Turkey |
| TUV | Tuvalu |
| TZA | Tanzania |
| UGA | Uganda |
| UKR | Ukraine |
| URY | Uruguay |
| USA | United States of America |
| UZB | Uzbekistan |
| VAT | Vatican City |
| VCT | Saint Vincent and the Grenadines |
| VEN | Venezuela |
| VGB | British Virgin Islands |
| VIR | United States Virgin Islands |
| VNM | Vietnam |
| VUT | Vanuatu |
| WLF | Wallis and Futuna |
| WSM | Samoa |
| XXK | Kosovo |
| YEM | Yemen |
| ZAF | South Africa |
| ZMB | Zambia |
| ZWE | Zimbabwe |

<br/>
###Types

| **ENUM name** | Types | Description |
| --- | --- | --- |
| component\_enum | <ul><li>Hazard<li>Exposure<li>Vulnerability<li>Loss | Which schema component the contribution refers to.|
| occupancy\_enum | <ul><li>Residential<li>Commercial<li>Industrial<li>Infrastructure<li>Healthcare<li>Educational<li>Government<li>Crop<li>Livestock<li>Forestry<li>Mixed occupancy| Common types related to asset occupancy. |

<br/>
