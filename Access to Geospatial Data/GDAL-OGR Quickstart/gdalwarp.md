##/[Notebooks](../../)/[Access to Geospatial data](../GDAL-OGR Quickstart/)/[GDAL-OGR Quickstart](GDAL-OGR Quickstart/GDAL-OGR Quickstart.md)/

<b><h1 style="margin: 0.0px 0.0px 0.0px 0.0px; line-height: 15.4px; font: 18.0px 'Lucida Sans'; color: #004d87; -webkit-text-stroke: #004d87; background-color: #ffffff"><span class="s1">gdalwarp</span></h1></b>  

<b><h1 style="margin: 0.0px 0.0px 0.0px 0.0px; line-height: 15.4px; font: 16.0px 'Lucida Sans'; color: #004d87; -webkit-text-stroke: #004d87; background-color: #ffffff"><span class="s1">Reprojecting</span></h1></b>  


For this process we assume that HYP_50M_SR_W.tif has been properly created with bounds. As we saw before with gdalinfo HYP_50M_SR_W has a proper coordinate system set. 

If the tif file we want work on doesn't have proper projection information (wich is the case in most *.tif* files when associated with a world file *.tfw*) it is possible to assign a coordinate system to the image with ```gdal_translate``` and the flag ```-a_srs``` e.g :

    gdal_translate -a_srs WGS84 HYP_50M_SR_W.tif HYP_50M_SR_W_4326.tif
    
    
Given a proper georeferenced raster file the ```gdalwarp``` command can be used to assign a new Spatial Reference System to it. Here we reproject the WGS84 geographic image to the Mercator projection:


    !gdalwarp -t_srs '+proj=merc +datum=WGS84' /home/user/gdal_natural_earth/HYP_50M_SR_W.tif /home/user/gdal_natural_earth/mercator.tif

    Creating output file that is 7292P x 9625L.
    Processing input file /home/user/gdal_natural_earth/HYP_50M_SR_W.tif.
    0...10...20...30...40...50...60...70...80...90...100 - done.



    !gdal_translate -of JPEG -co QUALITY=40 /home/user/gdal_natural_earth/mercator.tif /home/user/gdal_natural_earth/mercator.png

    Input file size is 7292, 9625
    0...10...20...30...40...50...60...70...80...90...100 - done.



    Image('/home/user/gdal_natural_earth/mercator.png')




![png](output_53_0.png)



Here we reproject to the Ortho projection.


    !gdalwarp -t_srs '+proj=ortho +datum=WGS84' /home/user/gdal_natural_earth/HYP_50M_SR_W.tif /home/user/gdal_natural_earth/ortho.tif

    ERROR 1: tolerance condition error
    ERROR 1: tolerance condition error
    ...
    ...
    ERROR 1: tolerance condition error
    ERROR 1: tolerance condition error
    ERROR 1: Reprojection failed, err = -20, further errors will be suppressed on the transform object.
    Creating output file that is 8538P x 8538L.
    Processing input file /home/user/gdal_natural_earth/HYP_50M_SR_W.tif.
    0...10...20...30...40...50...60...70...80...90...100 - done.



    !gdal_translate -of JPEG -co QUALITY=40 /home/user/gdal_natural_earth/ortho.tif /home/user/gdal_natural_earth/ortho.png

    Input file size is 8538, 8538
    0...10...20...30...40...50...60...70...80...90...100 - done.



    Image('/home/user/gdal_natural_earth/ortho.png')




![png](output_57_0.png)

