###/[Notebooks](../../)/[Access to Geospatial data](../GDAL-OGR Quickstart/)/[GDAL-OGR Quickstart](GDAL-OGR Quickstart/GDAL-OGR Quickstart.md)/

<center><b><h1 style="margin: 0.0px 0.0px 0.0px 0.0px; line-height: 15.4px; font: 18.0px 'Lucida Sans'; color: #004d87; -webkit-text-stroke: #004d87; background-color: #ffffff"><span class="s1">gdaltindex</span></h1></b></center>  


<b><h1 style="margin: 0.0px 0.0px 0.0px 0.0px; line-height: 15.4px; font: 16.0px 'Lucida Sans'; color: #004d87; -webkit-text-stroke: #004d87; background-color: #ffffff"><span class="s1">Raster tileindex with gdaltindex</span></h1></b> 
You can build a shapefile as a raster tileindex. For every image a polygon is generated with the bounds of the extent of the polygon and the path to the file.

``` bash
!gdaltindex /home/user/gdal_natural_earth/index_natural_earth.shp /home/user/gdal_natural_earth/*st.tif

Creating new index file...
```

The command above just created a new ESRI Shape File (default vector format), we will see how to work on vector files later on in the **OGR** section.
