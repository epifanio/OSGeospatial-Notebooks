
<b><h1 style="margin: 0.0px 0.0px 0.0px 0.0px; line-height: 15.4px; font: 22.0px 'Lucida Sans'; color: #004d87; -webkit-text-stroke: #004d87; background-color: #ffffff"><span class="s1">GDAL/OGR Quickstart</span></h1></b>

The first Notebook is dedicared to the use of the Geospatial Data Abstraction Library **GDAL** from the bash command line. GDAL is a powerful translator library for raster and vector geospatial data formats it presents a single raster abstract data model and vector abstract data model to the calling application for all supported formats.

This Notebook is derived from the original [GDAL-OGR quickstart](../doc/en/quickstart/gdal_quickstart.html)  adapted to run interactively in a IPython notebook and is composed by two main parts **GDAL** (to handle raster data) and **OGR** (to work with vector data)

<h1 style="margin: 0.0px 0.0px 0.0px 0.0px; line-height: 15.4px; font: 18.0px 'Lucida Sans'; color: #004d87; -webkit-text-stroke: #004d87; background-color: #ffffff"><span class="s1">GDAL</span></h1>

* Explore your image data with [```gdalinfo```](#gdalinfo)
* Format translations, Rescaling, Resizing, Splitting with [```gdal_translate```](#gdal_translate)
    * [```Format translations```](#Format-translation)
    * [```Resizing```](#Resizing)
    * [```Rescaling```](#Rescaling)
    * [```Splitting```](#Splitting)
* Reproject  with [```gdalwarp```](#Reprojecting)
* Raster tileindex with [```gdaltindex```](#gdaltindex)
* Image Mosaic with ```gdal_warp``` or [```gdal_merge.py```](#Mosaicking)

<h1 style="margin: 0.0px 0.0px 0.0px 0.0px; line-height: 15.4px; font: 18.0px 'Lucida Sans'; color: #004d87; -webkit-text-stroke: #004d87; background-color: #ffffff"><span class="s1">OGR </span></h1>
* get information about your data with [```ogrinfo```](#ogrinfo)
* use [```ogr2ogr```](#ogr2ogr) to transform your data to other formats

<b><h1 style="margin: 0.0px 0.0px 0.0px 0.0px; line-height: 15.4px; font: 18.0px 'Lucida Sans'; color: #004d87; -webkit-text-stroke: #004d87; background-color: #ffffff"><span class="s1">Get to know GDAL</span></h1></b> 


You will find the demo data at ```/usr/local/share/data```. We want to have a look at the [naturalearth dataset](../doc/en/overview/naturalearth_overview.html) data in this quickstart. We want to work with a copy of the data. So the first step is to copy the data to your home directory.


    # Import IPython utility to display images
    from IPython.core.display import Image


    cd /home/user

    [Errno 2] No such file or directory: '/home/user'
    /home/epinux/jupyter/GSOC/IPython_notebooks/OSGeo-live/osgeolive-gsoc-2015/notebooks/Access to Geospatial data



    !rm -rf /home/user/gdal_natural_earth


    !cp -R /usr/local/share/data/natural_earth2/ /home/user/gdal_natural_earth

You will then find a series of geotiff file:


    ls /home/user/gdal_natural_earth/HYP_50M_SR_W.*

<b><h1 style="margin: 0.0px 0.0px 0.0px 0.0px; line-height: 15.4px; font: 18.0px 'Lucida Sans'; color: #004d87; -webkit-text-stroke: #004d87; background-color: #ffffff"><span class="s1">gdalinfo</span></h1></b> 

<b><h2 style="margin: 0.0px 0.0px 0.0px 0.0px; line-height: 15.4px; font: 16.0px 'Lucida Sans'; color: #004d87; -webkit-text-stroke: #004d87; background-color: #ffffff"><span class="s1">get information about the raster data</span></h2></b> 


    !gdalinfo /home/user/gdal_natural_earth/HYP_50M_SR_W.tif

---

Note:
* Driver is “GTiff/GeoTIFF”
* Size is 10800x5400
* 3 Bands of type Byte.
* Coordinates
* Coordinate system is World Geodetic System 84

<b><h1 style="margin: 0.0px 0.0px 0.0px 0.0px; line-height: 15.4px; font: 16.0px 'Lucida Sans'; color: #004d87; -webkit-text-stroke: #004d87; background-color: #ffffff"><span class="s1">Listing available Drivers</span></h1></b> 

First get to know your drivers. The ```--formats``` commandline switch of gdalinfo can be used to see a list of available format drivers.

List all the available formats:


    !gdalinfo --formats

Each format reports if it is:
* read only (ro),
* read/write (rw) or
* read/write/update (rw+).

It is also possible to ask for specific formats details:


    !gdalinfo --format GTiff 

<b><h1 style="margin: 0.0px 0.0px 0.0px 0.0px; line-height: 15.4px; font: 18.0px 'Lucida Sans'; color: #004d87; -webkit-text-stroke: #004d87; background-color: #ffffff"><span class="s1">gdal_translate</span></h1></b> 

<b><h1 style="margin: 0.0px 0.0px 0.0px 0.0px; line-height: 15.4px; font: 16.0px 'Lucida Sans'; color: #004d87; -webkit-text-stroke: #004d87; background-color: #ffffff"><span class="s1">Format translation</span></h1></b> 

Translations are accomplished with the gdal_translate command. The default output format is GeoTIFF. The ```-of``` flag is used to select an output format and the ```-co``` flag is used to specify a creation option:

The web browser is not happy with tif files so to have a quick look at the image we convert it to a web friendly format (JPG) using ```gdal_translate``` (this requires few seconds)


    !gdal_translate -of JPEG -co QUALITY=10 /home/user/gdal_natural_earth/HYP_50M_SR_W.tif /home/user/gdal_natural_earth/HYP_50M_SR_W.jpg


    Image('/home/user/gdal_natural_earth/HYP_50M_SR_W.jpg')

The -ot switch can be used to alter the output data type.


    !gdal_translate -ot Int16 /home/user/gdal_natural_earth/HYP_50M_SR_W.tif /home/user/gdal_natural_earth/HYP_50M_SR_W_Int16.tif

Use gdalinfo to verify data type.


    !gdalinfo /home/user/gdal_natural_earth/HYP_50M_SR_W.tif | grep Band


    !gdalinfo /home/user/gdal_natural_earth/HYP_50M_SR_W_Int16.tif | grep Band

<b><h1 style="margin: 0.0px 0.0px 0.0px 0.0px; line-height: 15.4px; font: 16.0px 'Lucida Sans'; color: #004d87; -webkit-text-stroke: #004d87; background-color: #ffffff"><span class="s1">Resizing</span></h1></b>  

The -outsize switch can be used to set the size of the output file.


    !gdal_translate -outsize 50% 50% /home/user/gdal_natural_earth/HYP_50M_SR_W.tif  /home/user/gdal_natural_earth/HYP_50M_SR_W_small.tif

Use gdalinfo to verify the size.


    !gdalinfo /home/user/gdal_natural_earth/HYP_50M_SR_W.tif | grep Size


    !gdalinfo /home/user/gdal_natural_earth/HYP_50M_SR_W_small.tif | grep Size

<b><h1 style="margin: 0.0px 0.0px 0.0px 0.0px; line-height: 15.4px; font: 16.0px 'Lucida Sans'; color: #004d87; -webkit-text-stroke: #004d87; background-color: #ffffff"><span class="s1">Rescaling</span></h1></b>  

The -scale switch can be used to rescale the data range of a given image. Explicit control of the input and output ranges is also available. The gdalinfo ```-mm``` switch can be used to see pixel min/max values.

The output will display a computed Min/Max value for each band in the raster imput (3 band in our case)


    !gdalinfo -mm /home/user/gdal_natural_earth/HYP_50M_SR_W_small.tif | grep Min/Max

To rescale a specific band we can use the "-scale_bn" syntax where bn is a band number (e.g. "-scale_2" for the 2nd band of the output dataset), in the example below we will rescale the 3 bands of the HYP_50M_SR_W GeoTiff to be in the range 0-255 :


    !gdal_translate -scale_1 62.000 255.000 0 255.000 \
                   -scale_2 85.000 255.000 0 255.000 \
                   -scale_3 79.000 255.000 0 255.000 \
                   /home/user/gdal_natural_earth/HYP_50M_SR_W.tif /home/user/gdal_natural_earth/HYP_50M_SR_W_scaled.tif

Check the results with ```gdalinfo``` :


    !gdalinfo -mm /home/user/gdal_natural_earth/HYP_50M_SR_W_scaled.tif | grep Min/Max

Let's convert the scaled output to JPG for a quick display, notice the color rearrangement.


    !gdal_translate -of JPEG -co QUALITY=40 /home/user/gdal_natural_earth/HYP_50M_SR_W_scaled.tif /home/user/gdal_natural_earth/HYP_50M_SR_W_scaled.jpg


    Image('/home/user/gdal_natural_earth/HYP_50M_SR_W_scaled.jpg')

<b><h1 style="margin: 0.0px 0.0px 0.0px 0.0px; line-height: 15.4px; font: 16.0px 'Lucida Sans'; color: #004d87; -webkit-text-stroke: #004d87; background-color: #ffffff"><span class="s1">Splitting</span></h1></b> 

Let’s split our image into two with ```-srcwin``` which makes a copy based on pixel/line location (xoff yoff xsize ysize). You also could use ```-projwin``` and define the corners in georeferenced coordinates (ulx uly lrx lry).


    !gdal_translate -srcwin 0 0 5400 5400 /home/user/gdal_natural_earth/HYP_50M_SR_W.tif  /home/user/gdal_natural_earth/west.tif
    !gdal_translate -srcwin 5400 0 5400 5400 /home/user/gdal_natural_earth/HYP_50M_SR_W.tif  /home/user/gdal_natural_earth/east.tif


    !gdal_translate -of JPEG -co QUALITY=40 /home/user/gdal_natural_earth/east.tif /home/user/gdal_natural_earth/east.jpg
    !gdal_translate -of JPEG -co QUALITY=40 /home/user/gdal_natural_earth/west.tif /home/user/gdal_natural_earth/west.jpg

<b><h1 style="margin: 0.0px 0.0px 0.0px 0.0px; line-height: 15.4px; font: 18.0px 'Lucida Sans'; color: #004d87; -webkit-text-stroke: #004d87; background-color: #ffffff"><span class="s1">gdalwarp</span></h1></b>  


<b><h1 style="margin: 0.0px 0.0px 0.0px 0.0px; line-height: 15.4px; font: 16.0px 'Lucida Sans'; color: #004d87; -webkit-text-stroke: #004d87; background-color: #ffffff"><span class="s1">Reprojecting</span></h1></b>  


For this process we assume that HYP_50M_SR_W.tif has been properly created with bounds. As we saw before with gdalinfo HYP_50M_SR_W has a proper coordinate system set. 

If the tif file we want work on doesn't have proper projection information (wich is the case in most *.tif* files when associated with a world file *.tfw*) it is possible to assign a coordinate system to the image with ```gdal_translate``` and the flag ```-a_srs``` e.g :

    gdal_translate -a_srs WGS84 HYP_50M_SR_W.tif HYP_50M_SR_W_4326.tif
    
    
Given a proper georeferenced raster file the ```gdalwarp``` command can be used to assign a new Spatial Reference System to it. Here we reproject the WGS84 geographic image to the Mercator projection:


    !gdalwarp -t_srs '+proj=merc +datum=WGS84' /home/user/gdal_natural_earth/HYP_50M_SR_W.tif /home/user/gdal_natural_earth/mercator.tif


    !gdal_translate -of JPEG -co QUALITY=40 /home/user/gdal_natural_earth/mercator.tif /home/user/gdal_natural_earth/mercator.png


    Image('/home/user/gdal_natural_earth/mercator.png')

Here we reproject to the Ortho projection.


    !gdalwarp -t_srs '+proj=ortho +datum=WGS84' /home/user/gdal_natural_earth/HYP_50M_SR_W.tif /home/user/gdal_natural_earth/ortho.tif


    !gdal_translate -of JPEG -co QUALITY=40 /home/user/gdal_natural_earth/ortho.tif /home/user/gdal_natural_earth/ortho.png


    Image('/home/user/gdal_natural_earth/ortho.png')

<b><h1 style="margin: 0.0px 0.0px 0.0px 0.0px; line-height: 15.4px; font: 18.0px 'Lucida Sans'; color: #004d87; -webkit-text-stroke: #004d87; background-color: #ffffff"><span class="s1">gdaltindex</span></h1></b>  


<b><h1 style="margin: 0.0px 0.0px 0.0px 0.0px; line-height: 15.4px; font: 16.0px 'Lucida Sans'; color: #004d87; -webkit-text-stroke: #004d87; background-color: #ffffff"><span class="s1">Raster tileindex with gdaltindex</span></h1></b> 
You can build a shapefile as a raster tileindex. For every image a polygon is generated with the bounds of the extent of the polygon and the path to the file.


    !gdaltindex /home/user/gdal_natural_earth/index_natural_earth.shp /home/user/gdal_natural_earth/*st.tif

The command above just created a new ESRI Shape File (default vector format), we will see how to work on vector files later on in the **OGR** section.

<b><h1 style="margin: 0.0px 0.0px 0.0px 0.0px; line-height: 15.4px; font: 18.0px 'Lucida Sans'; color: #004d87; -webkit-text-stroke: #004d87; background-color: #ffffff"><span class="s1">Mosaicking</span></h1></b>   

```gdal_merge.py``` is a python script that can be used for simple mosaicking tasks. Mosaic the east.tif and west.tif into a single file:


    !gdal_merge.py  /home/user/gdal_natural_earth/east.tif /home/user/gdal_natural_earth/west.tif -o /home/user/gdal_natural_earth/merged.tif

Convert to jpg to display in the notebook and you can see the original image recomposed


    !gdal_translate -of JPEG -co QUALITY=40 /home/user/gdal_natural_earth/merged.tif /home/user/gdal_natural_earth/merged.jpg


    Image('/home/user/gdal_natural_earth/merged.jpg')

The same task can be accomplished with gdalwarp. gdalwarp has a variety of advantages over gdal_merge, but can be slow to merge many files:

    gdalwarp east.tif west.tif warpmerged.tif

<b><h1 style="margin: 0.0px 0.0px 0.0px 0.0px; line-height: 15.4px; font: 18.0px 'Lucida Sans'; color: #004d87; -webkit-text-stroke: #004d87; background-color: #ffffff"><span class="s1">Get to know OGR</span></h1></b>  


<b><h1 style="margin: 0.0px 0.0px 0.0px 0.0px; line-height: 15.4px; font: 16.0px 'Lucida Sans'; color: #004d87; -webkit-text-stroke: #004d87; background-color: #ffffff"><span class="s1">ogrinfo</span></h1></b>  

Like we did with raster using ```gdalinfo```, is possible to retrieve descriptive information from a vector datasource using the command line too ```ogrinfo```.
Let's run ```ogrinfo``` on the previously generated shapefile ```index_natural_earth.shp```:


    !ogrinfo /home/user/gdal_natural_earth/index_natural_earth.shp index_natural_earth

Get a summary about your data with ogrinfo together with -so.


    !ogrinfo -ro -so /home/user/gdal_natural_earth/ne_10m_admin_0_countries.shp ne_10m_admin_0_countries

If you run ogrinfo without a parameter you will get a summary about your data and afterwards a section for every dataset. You can forward the result from ogrinfo to grep to filter and get only the attribute COUNTRY.


    !ogrinfo -ro /home/user/gdal_natural_earth/ne_10m_admin_0_countries.shp ne_10m_admin_0_countries | grep 'admin '

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


    !shp2img -m index_natural_earth.map -i PNG -o index_natural_earth.png


    Image('index_natural_earth.png')

<b><h1 style="margin: 0.0px 0.0px 0.0px 0.0px; line-height: 15.4px; font: 18.0px 'Lucida Sans'; color: #004d87; -webkit-text-stroke: #004d87; background-color: #ffffff"><span class="s1">Use ogr2ogr to convert data between file formats</span></h1></b>  


Like with ```gdalinfo``` You can use ogr2ogr to converts simple features data between file formats. You can use –formats to get the list of the supported formats with read/write information.


    !ogrinfo --formats

Convert the countries to GeoJson.

<b><h1 style="margin: 0.0px 0.0px 0.0px 0.0px; line-height: 15.4px; font: 16.0px 'Lucida Sans'; color: #004d87; -webkit-text-stroke: #004d87; background-color: #ffffff"><span class="s1">ogr2ogr</span></h1></b>


    !ogr2ogr -f GeoJSON /home/user/gdal_natural_earth/countries.json /home/user/gdal_natural_earth/ne_10m_admin_0_countries.shp
