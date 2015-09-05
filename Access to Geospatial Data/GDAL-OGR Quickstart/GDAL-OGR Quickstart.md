
#[Notebooks](../../)/[Access to Geospatial data](../README.md)

<b><h1 style="margin: 0.0px 0.0px 0.0px 0.0px; line-height: 15.4px; font: 22.0px 'Lucida Sans'; color: #004d87; -webkit-text-stroke: #004d87; background-color: #ffffff"><span class="s1">GDAL-OGR Quickstart</span></h1></b>

The first Notebook is dedicared to the use of the Geospatial Data Abstraction Library **GDAL** from the bash command line. GDAL is a powerful translator library for raster and vector geospatial data formats it presents a single raster abstract data model and vector abstract data model to the calling application for all supported formats.

This Notebook is derived from the original [GDAL-OGR quickstart](../doc/en/quickstart/gdal_quickstart.html)  adapted to run interactively in a IPython notebook and is composed by two main parts **GDAL** (to handle raster data) and **OGR** (to work with vector data)

<h1 style="margin: 0.0px 0.0px 0.0px 0.0px; line-height: 15.4px; font: 18.0px 'Lucida Sans'; color: #004d87; -webkit-text-stroke: #004d87; background-color: #ffffff"><span class="s1">GDAL</span></h1>

* Explore your image data with [```gdalinfo```](gdalinfo.md)
* Format translations, Rescaling, Resizing, Splitting with [```gdal_translate```](gdal_translate.md)

    * [```Format translations```](gdal_translate.md#Format-translation), [```Resizing```](gdal_translate.md#resizing), [```Rescaling```](gdal_translate.md#rescaling), [```Splitting```](gdal_translate.md#splitting)


* Reproject  with [```gdalwarp```](gdalwarp.md#reprojecting)
* Raster tileindex with [```gdaltindex```](gdaltindex.md)
* Image Mosaic with ```gdal_warp``` or [```gdal_merge.py```](#Mosaicking)

<h1 style="margin: 0.0px 0.0px 0.0px 0.0px; line-height: 15.4px; font: 18.0px 'Lucida Sans'; color: #004d87; -webkit-text-stroke: #004d87; background-color: #ffffff"><span class="s1">OGR </span></h1>
* get information about your data with [```ogrinfo```](#ogrinfo)
* use [```ogr2ogr```](#ogr2ogr) to transform your data to other formats

<b><h1 style="margin: 0.0px 0.0px 0.0px 0.0px; line-height: 15.4px; font: 18.0px 'Lucida Sans'; color: #004d87; -webkit-text-stroke: #004d87; background-color: #ffffff"><span class="s1">Get to know GDAL</span></h1></b> 


You will find the demo data at ```/usr/local/share/data```. We want to have a look at the [naturalearth dataset](../doc/en/overview/naturalearth_overview.html) data in this quickstart. We want to work with a copy of the data. So the first step is to copy the data to your home directory.

```python
# Import IPython utility to display images
from IPython.core.display import Image
    
cd /home/user
!rm -rf /home/user/gdal_natural_earth
!cp -R /usr/local/share/data/natural_earth2/ /home/user/gdal_natural_earth
```

You will then find a series of geotiff file:
```
ls /home/user/gdal_natural_earth/HYP_50M_SR_W.*
```
```
/home/user/gdal_natural_earth/HYP_50M_SR_W.prj
/home/user/gdal_natural_earth/HYP_50M_SR_W.README.html
/home/user/gdal_natural_earth/HYP_50M_SR_W.tfw
/home/user/gdal_natural_earth/HYP_50M_SR_W.tif
/home/user/gdal_natural_earth/HYP_50M_SR_W.VERSION.txt
```


<b><h1 style="margin: 0.0px 0.0px 0.0px 0.0px; line-height: 15.4px; font: 18.0px 'Lucida Sans'; color: #004d87; -webkit-text-stroke: #004d87; background-color: #ffffff"><span class="s1">gdaltindex</span></h1></b>  


<b><h1 style="margin: 0.0px 0.0px 0.0px 0.0px; line-height: 15.4px; font: 16.0px 'Lucida Sans'; color: #004d87; -webkit-text-stroke: #004d87; background-color: #ffffff"><span class="s1">Raster tileindex with gdaltindex</span></h1></b> 
You can build a shapefile as a raster tileindex. For every image a polygon is generated with the bounds of the extent of the polygon and the path to the file.


    !gdaltindex /home/user/gdal_natural_earth/index_natural_earth.shp /home/user/gdal_natural_earth/*st.tif

    Creating new index file...


The command above just created a new ESRI Shape File (default vector format), we will see how to work on vector files later on in the **OGR** section.

<b><h1 style="margin: 0.0px 0.0px 0.0px 0.0px; line-height: 15.4px; font: 18.0px 'Lucida Sans'; color: #004d87; -webkit-text-stroke: #004d87; background-color: #ffffff"><span class="s1">Mosaicking</span></h1></b>   

```gdal_merge.py``` is a python script that can be used for simple mosaicking tasks. Mosaic the east.tif and west.tif into a single file:


    !gdal_merge.py  /home/user/gdal_natural_earth/east.tif /home/user/gdal_natural_earth/west.tif -o /home/user/gdal_natural_earth/merged.tif

    0...10...20...30...40...50...60...70...80...90...100 - done.


Convert to jpg to display in the notebook and you can see the original image recomposed


    !gdal_translate -of JPEG -co QUALITY=40 /home/user/gdal_natural_earth/merged.tif /home/user/gdal_natural_earth/merged.jpg

    Input file size is 10800, 5400
    0...10...20...30...40...50...60...70...80...90...100 - done.



    Image('/home/user/gdal_natural_earth/merged.jpg')




![jpeg](output_65_0.jpeg)



The same task can be accomplished with gdalwarp. gdalwarp has a variety of advantages over gdal_merge, but can be slow to merge many files:

    gdalwarp east.tif west.tif warpmerged.tif

<b><h1 style="margin: 0.0px 0.0px 0.0px 0.0px; line-height: 15.4px; font: 18.0px 'Lucida Sans'; color: #004d87; -webkit-text-stroke: #004d87; background-color: #ffffff"><span class="s1">Get to know OGR</span></h1></b>  


<b><h1 style="margin: 0.0px 0.0px 0.0px 0.0px; line-height: 15.4px; font: 16.0px 'Lucida Sans'; color: #004d87; -webkit-text-stroke: #004d87; background-color: #ffffff"><span class="s1">ogrinfo</span></h1></b>  

Like we did with raster using ```gdalinfo```, is possible to retrieve descriptive information from a vector datasource using the command line too ```ogrinfo```.
Let's run ```ogrinfo``` on the previously generated shapefile ```index_natural_earth.shp```:


    !ogrinfo /home/user/gdal_natural_earth/index_natural_earth.shp index_natural_earth

    INFO: Open of `/home/user/gdal_natural_earth/index_natural_earth.shp'
          using driver `ESRI Shapefile' successful.
    
    Layer name: index_natural_earth
    Geometry: Polygon
    Feature Count: 2
    Extent: (-180.000000, -90.000000) - (180.000000, 90.000000)
    Layer SRS WKT:
    GEOGCS["GCS_WGS_1984",
        DATUM["WGS_1984",
            SPHEROID["WGS_84",6378137,298.257223563]],
        PRIMEM["Greenwich",0],
        UNIT["Degree",0.017453292519943295]]
    location: String (254.0)
    OGRFeature(index_natural_earth):0
      location (String) = /home/user/gdal_natural_earth/east.tif
      POLYGON ((-0.000000000017963 90.0,179.999999999964047 90.0,179.999999999964047 -89.999999999982009,-0.000000000017963 -89.999999999982009,-0.000000000017963 90.0))
    
    OGRFeature(index_natural_earth):1
      location (String) = /home/user/gdal_natural_earth/west.tif
      POLYGON ((-180.0 90.0,-0.000000000017963 90.0,-0.000000000017963 -89.999999999982009,-180.0 -89.999999999982009,-180.0 90.0))
    


Get a summary about your data with ogrinfo together with -so.


    !ogrinfo -ro -so /home/user/gdal_natural_earth/ne_10m_admin_0_countries.shp ne_10m_admin_0_countries

    INFO: Open of `/home/user/gdal_natural_earth/ne_10m_admin_0_countries.shp'
          using driver `ESRI Shapefile' successful.
    
    Layer name: ne_10m_admin_0_countries
    Geometry: Polygon
    Feature Count: 254
    Extent: (-180.000000, -90.000000) - (180.000000, 83.634101)
    Layer SRS WKT:
    GEOGCS["GCS_WGS_1984",
        DATUM["WGS_1984",
            SPHEROID["WGS_84",6378137.0,298.257223563]],
        PRIMEM["Greenwich",0.0],
        UNIT["Degree",0.0174532925199433]]
    scalerank: Integer (4.0)
    featurecla: String (30.0)
    labelrank: Real (16.6)
    sovereignt: String (254.0)
    sov_a3: String (254.0)
    adm0_dif: Real (16.6)
    level: Real (16.6)
    type: String (254.0)
    admin: String (254.0)
    adm0_a3: String (254.0)
    geou_dif: Real (16.6)
    geounit: String (254.0)
    gu_a3: String (254.0)
    su_dif: Real (16.6)
    subunit: String (254.0)
    su_a3: String (254.0)
    brk_diff: Real (16.6)
    name: String (254.0)
    name_long: String (254.0)
    brk_a3: String (254.0)
    brk_name: String (254.0)
    brk_group: String (254.0)
    abbrev: String (254.0)
    postal: String (254.0)
    formal_en: String (254.0)
    formal_fr: String (254.0)
    note_adm0: String (254.0)
    note_brk: String (254.0)
    name_sort: String (254.0)
    name_alt: String (254.0)
    mapcolor7: Real (16.6)
    mapcolor8: Real (16.6)
    mapcolor9: Real (16.6)
    mapcolor13: Real (16.6)
    pop_est: Real (16.6)
    gdp_md_est: Real (16.6)
    pop_year: Real (16.6)
    lastcensus: Real (16.6)
    gdp_year: Real (16.6)
    economy: String (254.0)
    income_grp: String (254.0)
    wikipedia: Real (16.6)
    fips_10: String (254.0)
    iso_a2: String (254.0)
    iso_a3: String (254.0)
    iso_n3: String (254.0)
    un_a3: String (254.0)
    wb_a2: String (254.0)
    wb_a3: String (254.0)
    woe_id: Real (16.6)
    adm0_a3_is: String (254.0)
    adm0_a3_us: String (254.0)
    adm0_a3_un: Real (16.6)
    adm0_a3_wb: Real (16.6)
    continent: String (254.0)
    region_un: String (254.0)
    subregion: String (254.0)
    region_wb: String (254.0)
    name_len: Real (16.6)
    long_len: Real (16.6)
    abbrev_len: Real (16.6)
    tiny: Real (16.6)
    homepart: Real (16.6)


If you run ogrinfo without a parameter you will get a summary about your data and afterwards a section for every dataset. You can forward the result from ogrinfo to grep to filter and get only the attribute COUNTRY.


    !ogrinfo -ro /home/user/gdal_natural_earth/ne_10m_admin_0_countries.shp ne_10m_admin_0_countries | grep 'admin '

      admin (String) = Aruba
      admin (String) = Afghanistan
      admin (String) = Angola
      admin (String) = Anguilla
      admin (String) = Albania
      admin (String) = Aland
      admin (String) = Andorra
      admin (String) = United Arab Emirates
      admin (String) = Argentina
      admin (String) = Armenia
      admin (String) = American Samoa
      admin (String) = Antarctica
      admin (String) = French Southern and Antarctic Lands
      admin (String) = Antigua and Barbuda
      admin (String) = Australia
      admin (String) = Austria
      admin (String) = Azerbaijan
      admin (String) = Burundi
      admin (String) = Belgium
      admin (String) = Benin
      admin (String) = Burkina Faso
      admin (String) = Bangladesh
      admin (String) = Bulgaria
      admin (String) = Bahrain
      admin (String) = The Bahamas
      admin (String) = Bosnia and Herzegovina
      admin (String) = Bajo Nuevo Bank (Petrel Is.)
      admin (String) = Saint Barthelemy
      admin (String) = Belarus
      admin (String) = Belize
      admin (String) = Bermuda
      admin (String) = Bolivia
      admin (String) = Brazil
      admin (String) = Barbados
      admin (String) = Brunei
      admin (String) = Bhutan
      admin (String) = Botswana
      admin (String) = Central African Republic
      admin (String) = Canada
      admin (String) = Switzerland
      admin (String) = Chile
      admin (String) = China
      admin (String) = Ivory Coast
      admin (String) = Clipperton Island
      admin (String) = Cameroon
      admin (String) = Cyprus No Mans Area
      admin (String) = Democratic Republic of the Congo
      admin (String) = Republic of Congo
      admin (String) = Cook Islands
      admin (String) = Colombia
      admin (String) = Comoros
      admin (String) = Cape Verde
      admin (String) = Costa Rica
      admin (String) = Coral Sea Islands
      admin (String) = Cuba
      admin (String) = Curaçao
      admin (String) = Cayman Islands
      admin (String) = Northern Cyprus
      admin (String) = Cyprus
      admin (String) = Czech Republic
      admin (String) = Germany
      admin (String) = Djibouti
      admin (String) = Dominica
      admin (String) = Denmark
      admin (String) = Dominican Republic
      admin (String) = Algeria
      admin (String) = Ecuador
      admin (String) = Egypt
      admin (String) = Eritrea
      admin (String) = Dhekelia Sovereign Base Area
      admin (String) = Spain
      admin (String) = Estonia
      admin (String) = Ethiopia
      admin (String) = Finland
      admin (String) = Fiji
      admin (String) = Falkland Islands
      admin (String) = France
      admin (String) = Faroe Islands
      admin (String) = Federated States of Micronesia
      admin (String) = Gabon
      admin (String) = United Kingdom
      admin (String) = Georgia
      admin (String) = Guernsey
      admin (String) = Ghana
      admin (String) = Gibraltar
      admin (String) = Guinea
      admin (String) = Gambia
      admin (String) = Guinea Bissau
      admin (String) = Equatorial Guinea
      admin (String) = Greece
      admin (String) = Grenada
      admin (String) = Greenland
      admin (String) = Guatemala
      admin (String) = Guam
      admin (String) = Guyana
      admin (String) = Hong Kong S.A.R.
      admin (String) = Heard Island and McDonald Islands
      admin (String) = Honduras
      admin (String) = Croatia
      admin (String) = Haiti
      admin (String) = Hungary
      admin (String) = Indonesia
      admin (String) = Isle of Man
      admin (String) = India
      admin (String) = Indian Ocean Territories
      admin (String) = British Indian Ocean Territory
      admin (String) = Ireland
      admin (String) = Iran
      admin (String) = Iraq
      admin (String) = Iceland
      admin (String) = Israel
      admin (String) = Italy
      admin (String) = Jamaica
      admin (String) = Jersey
      admin (String) = Jordan
      admin (String) = Japan
      admin (String) = Baykonur Cosmodrome
      admin (String) = Siachen Glacier
      admin (String) = Kazakhstan
      admin (String) = Kenya
      admin (String) = Kyrgyzstan
      admin (String) = Cambodia
      admin (String) = Kiribati
      admin (String) = Saint Kitts and Nevis
      admin (String) = South Korea
      admin (String) = Kosovo
      admin (String) = Kuwait
      admin (String) = Laos
      admin (String) = Lebanon
      admin (String) = Liberia
      admin (String) = Libya
      admin (String) = Saint Lucia
      admin (String) = Liechtenstein
      admin (String) = Sri Lanka
      admin (String) = Lesotho
      admin (String) = Lithuania
      admin (String) = Luxembourg
      admin (String) = Latvia
      admin (String) = Macao S.A.R
      admin (String) = Saint Martin
      admin (String) = Morocco
      admin (String) = Monaco
      admin (String) = Moldova
      admin (String) = Madagascar
      admin (String) = Maldives
      admin (String) = Mexico
      admin (String) = Marshall Islands
      admin (String) = Macedonia
      admin (String) = Mali
      admin (String) = Malta
      admin (String) = Myanmar
      admin (String) = Montenegro
      admin (String) = Mongolia
      admin (String) = Northern Mariana Islands
      admin (String) = Mozambique
      admin (String) = Mauritania
      admin (String) = Montserrat
      admin (String) = Mauritius
      admin (String) = Malawi
      admin (String) = Malaysia
      admin (String) = Namibia
      admin (String) = New Caledonia
      admin (String) = Niger
      admin (String) = Norfolk Island
      admin (String) = Nigeria
      admin (String) = Nicaragua
      admin (String) = Niue
      admin (String) = Netherlands
      admin (String) = Norway
      admin (String) = Nepal
      admin (String) = Nauru
      admin (String) = New Zealand
      admin (String) = Oman
      admin (String) = Pakistan
      admin (String) = Panama
      admin (String) = Pitcairn Islands
      admin (String) = Peru
      admin (String) = Spratly Islands
      admin (String) = Philippines
      admin (String) = Palau
      admin (String) = Papua New Guinea
      admin (String) = Poland
      admin (String) = Puerto Rico
      admin (String) = North Korea
      admin (String) = Portugal
      admin (String) = Paraguay
      admin (String) = Palestine
      admin (String) = French Polynesia
      admin (String) = Qatar
      admin (String) = Romania
      admin (String) = Russia
      admin (String) = Rwanda
      admin (String) = Western Sahara
      admin (String) = Saudi Arabia
      admin (String) = Scarborough Reef
      admin (String) = Sudan
      admin (String) = South Sudan
      admin (String) = Senegal
      admin (String) = Serranilla Bank
      admin (String) = Singapore
      admin (String) = South Georgia and South Sandwich Islands
      admin (String) = Saint Helena
      admin (String) = Solomon Islands
      admin (String) = Sierra Leone
      admin (String) = El Salvador
      admin (String) = San Marino
      admin (String) = Somaliland
      admin (String) = Somalia
      admin (String) = Saint Pierre and Miquelon
      admin (String) = Republic of Serbia
      admin (String) = Sao Tome and Principe
      admin (String) = Suriname
      admin (String) = Slovakia
      admin (String) = Slovenia
      admin (String) = Sweden
      admin (String) = Swaziland
      admin (String) = Sint Maarten
      admin (String) = Seychelles
      admin (String) = Syria
      admin (String) = Turks and Caicos Islands
      admin (String) = Chad
      admin (String) = Togo
      admin (String) = Thailand
      admin (String) = Tajikistan
      admin (String) = Turkmenistan
      admin (String) = East Timor
      admin (String) = Tonga
      admin (String) = Trinidad and Tobago
      admin (String) = Tunisia
      admin (String) = Turkey
      admin (String) = Tuvalu
      admin (String) = Taiwan
      admin (String) = United Republic of Tanzania
      admin (String) = Uganda
      admin (String) = Ukraine
      admin (String) = United States Minor Outlying Islands
      admin (String) = Uruguay
      admin (String) = United States of America
      admin (String) = US Naval Base Guantanamo Bay
      admin (String) = Uzbekistan
      admin (String) = Vatican
      admin (String) = Saint Vincent and the Grenadines
      admin (String) = Venezuela
      admin (String) = British Virgin Islands
      admin (String) = United States Virgin Islands
      admin (String) = Vietnam
      admin (String) = Vanuatu
      admin (String) = Wallis and Futuna
      admin (String) = Akrotiri Sovereign Base Area
      admin (String) = Samoa
      admin (String) = Yemen
      admin (String) = South Africa
      admin (String) = Zambia
      admin (String) = Zimbabwe


The shape file we just created can not be rendered directly in the notebook. Later in the python tutorial we'll learn how to use libraries like *shapely* to render directly vector data. 
For now to display the results of our processing in the notebook we'll use the ```shp2img``` command line tool (provided by *[mapserver](../doc/en/overview/mapserver_overview.html)* ).
```shp2img``` require a *mapserver mapfile* as input to generate a rendered image.
Below we'll write a mapfile with 3 layers :
* west.tif
* east.tif
* index_natural_earth.shp
Note: the shapefile color has been classified based on the shapefile attribute ```location``` with a translarency to show the 2 raster images underneat.


    %%file index_natural_earth.map
    MAP
      EXTENT -180 -89.999999999982 179.999999999964 90
      IMAGETYPE "png"
      NAME "simplepolygon"
      SIZE 600 600
      STATUS ON
      UNITS DD
    
      OUTPUTFORMAT
        NAME "png"
        MIMETYPE "image/png"
        DRIVER "AGG/PNG"
        EXTENSION "png"
        IMAGEMODE RGB
        TRANSPARENT TRUE
      END # OUTPUTFORMAT
    
      PROJECTION
        "proj=longlat"
        "datum=WGS84"
        "no_defs"
      END # PROJECTION
    
        LAYER
        DATA "/home/user/gdal_natural_earth/west.tif"
        EXTENT -180 -89.999999999982 -1.79596892913025e-11 90
        METADATA
          "ows_title"	"west"
        END # METADATA
        NAME "west"
        PROJECTION
          "proj=longlat"
          "datum=WGS84"
          "no_defs"
        END # PROJECTION
        STATUS ON
        TILEITEM "location"
        TYPE RASTER
        UNITS METERS
      END # LAYER
    
      LAYER
        DATA "/home/user/gdal_natural_earth/east.tif"
        EXTENT -1.79596892913025e-11 -89.999999999982 179.999999999964 90
        METADATA
          "ows_title"	"east"
        END # METADATA
        NAME "east"
        PROJECTION
          "proj=longlat"
          "datum=WGS84"
          "no_defs"
        END # PROJECTION
        STATUS ON
        TILEITEM "location"
        TYPE RASTER
        UNITS METERS
      END # LAYER
      
      LAYER
        DATA "/home/user/gdal_natural_earth/index_natural_earth.shp"
        EXTENT -180 -89.999999999982 179.999999999964 90
        NAME "index_natural_earth"
        PROJECTION
          "proj=longlat"
          "datum=WGS84"
          "no_defs"
        END # PROJECTION
        STATUS ON
        TILEITEM "location"
        TYPE POLYGON
        UNITS METERS
        CLASS
          NAME "/home/user/gdal_natural_earth/east.tif"
          EXPRESSION ("[location]" ="/home/user/gdal_natural_earth/east.tif")
          STYLE
            OPACITY 50
            COLOR 218 57 57
          END # STYLE
          STYLE
            OUTLINECOLOR 0 0 0
            WIDTH 0.26
          END # STYLE
        END # CLASS
        CLASS
          NAME "/home/user/gdal_natural_earth/west.tif"
          EXPRESSION ("[location]" ="/home/user/gdal_natural_earth/west.tif")
          STYLE
            OPACITY 50
            COLOR 18 211 14
          END # STYLE
          STYLE
            OUTLINECOLOR 0 0 0
            WIDTH 0.26
          END # STYLE
        END # CLASS
      END # LAYER    
    END # MAP

    Overwriting index_natural_earth.map



    !shp2img -m index_natural_earth.map -i PNG -o index_natural_earth.png


    Image('index_natural_earth.png')




![png](output_77_0.png)



<b><h1 style="margin: 0.0px 0.0px 0.0px 0.0px; line-height: 15.4px; font: 18.0px 'Lucida Sans'; color: #004d87; -webkit-text-stroke: #004d87; background-color: #ffffff"><span class="s1">Use ogr2ogr to convert data between file formats</span></h1></b>  


Like with ```gdalinfo``` You can use ogr2ogr to converts simple features data between file formats. You can use –formats to get the list of the supported formats with read/write information.


    !ogrinfo --formats

    Supported Formats:
      -> "ESRI Shapefile" (read/write)
      -> "MapInfo File" (read/write)
      -> "UK .NTF" (readonly)
      -> "SDTS" (readonly)
      -> "TIGER" (read/write)
      -> "S57" (read/write)
      -> "DGN" (read/write)
      -> "VRT" (readonly)
      -> "REC" (readonly)
      -> "Memory" (read/write)
      -> "BNA" (read/write)
      -> "CSV" (read/write)
      -> "NAS" (readonly)
      -> "GML" (read/write)
      -> "GPX" (read/write)
      -> "LIBKML" (read/write)
      -> "KML" (read/write)
      -> "GeoJSON" (read/write)
      -> "Interlis 1" (read/write)
      -> "Interlis 2" (read/write)
      -> "GMT" (read/write)
      -> "GPKG" (read/write)
      -> "SQLite" (read/write)
      -> "DODS" (readonly)
      -> "ODBC" (read/write)
      -> "WAsP" (read/write)
      -> "PGeo" (readonly)
      -> "MSSQLSpatial" (read/write)
      -> "OGDI" (readonly)
      -> "PostgreSQL" (read/write)
      -> "MySQL" (read/write)
      -> "PCIDSK" (read/write)
      -> "OpenFileGDB" (readonly)
      -> "XPlane" (readonly)
      -> "AVCBin" (readonly)
      -> "AVCE00" (readonly)
      -> "DXF" (read/write)
      -> "Geoconcept" (read/write)
      -> "GeoRSS" (read/write)
      -> "GPSTrackMaker" (read/write)
      -> "VFK" (readonly)
      -> "PGDump" (read/write)
      -> "OSM" (readonly)
      -> "GPSBabel" (read/write)
      -> "SUA" (readonly)
      -> "OpenAir" (readonly)
      -> "PDS" (readonly)
      -> "WFS" (readonly)
      -> "HTF" (readonly)
      -> "AeronavFAA" (readonly)
      -> "Geomedia" (readonly)
      -> "EDIGEO" (readonly)
      -> "GFT" (read/write)
      -> "GME" (read/write)
      -> "SVG" (readonly)
      -> "CouchDB" (read/write)
      -> "Idrisi" (readonly)
      -> "ARCGEN" (readonly)
      -> "SEGUKOOA" (readonly)
      -> "SEGY" (readonly)
      -> "XLS" (readonly)
      -> "ODS" (read/write)
      -> "XLSX" (read/write)
      -> "ElasticSearch" (read/write)
      -> "PDF" (read/write)
      -> "Walk" (readonly)
      -> "CartoDB" (readonly)
      -> "SXF" (readonly)


Convert the countries to GeoJson.

<b><h1 style="margin: 0.0px 0.0px 0.0px 0.0px; line-height: 15.4px; font: 16.0px 'Lucida Sans'; color: #004d87; -webkit-text-stroke: #004d87; background-color: #ffffff"><span class="s1">ogr2ogr</span></h1></b>


    !ogr2ogr -f GeoJSON /home/user/gdal_natural_earth/countries.json /home/user/gdal_natural_earth/ne_10m_admin_0_countries.shp


    #unfinished - need to add ogr2ogr features yet, I'm considering to split this notebook in 2 parts (one for gdal and one for ogr2ogr) i'll study the gdal tutorial released recently

[top](#Notebooks---Access-to-Geospatial-data)


    
