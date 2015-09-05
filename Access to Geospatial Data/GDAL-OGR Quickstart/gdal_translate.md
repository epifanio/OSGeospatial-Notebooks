##/[Notebooks](../../)/[Access to Geospatial data](../GDAL-OGR Quickstart/)/[GDAL-OGR Quickstart](GDAL-OGR Quickstart/GDAL-OGR Quickstart.md)/

#gdal_translate

##Format translation

Translations are accomplished with the gdal_translate command. The default output format is GeoTIFF. The ```-of``` flag is used to select an output format and the ```-co``` flag is used to specify a creation option:

The web browser is not happy with tif files so to have a quick look at the image we convert it to a web friendly format (JPG) using ```gdal_translate``` (this requires few seconds)


    !gdal_translate -of JPEG -co QUALITY=10 /home/user/gdal_natural_earth/HYP_50M_SR_W.tif /home/user/gdal_natural_earth/HYP_50M_SR_W.jpg

    Input file size is 10800, 5400
    0...10...20...30...40...50...60...70...80...90...100 - done.


##Image Display


    Image('/home/user/gdal_natural_earth/HYP_50M_SR_W.jpg')




![jpeg](output_23_0.jpeg)



The -ot switch can be used to alter the output data type.


    !gdal_translate -ot Int16 /home/user/gdal_natural_earth/HYP_50M_SR_W.tif /home/user/gdal_natural_earth/HYP_50M_SR_W_Int16.tif

    Input file size is 10800, 5400
    0...10...20...30...40...50...60...70...80...90...100 - done.


Use gdalinfo to verify data type.


    !gdalinfo /home/user/gdal_natural_earth/HYP_50M_SR_W.tif | grep Band

    Band 1 Block=256x256 Type=Byte, ColorInterp=Red
    Band 2 Block=256x256 Type=Byte, ColorInterp=Green
    Band 3 Block=256x256 Type=Byte, ColorInterp=Blue



    !gdalinfo /home/user/gdal_natural_earth/HYP_50M_SR_W_Int16.tif | grep Band

    Band 1 Block=10800x1 Type=Int16, ColorInterp=Red
    Band 2 Block=10800x1 Type=Int16, ColorInterp=Green
    Band 3 Block=10800x1 Type=Int16, ColorInterp=Blue


##Resizing

The -outsize switch can be used to set the size of the output file.


    !gdal_translate -outsize 50% 50% /home/user/gdal_natural_earth/HYP_50M_SR_W.tif  /home/user/gdal_natural_earth/HYP_50M_SR_W_small.tif

    Input file size is 10800, 5400
    0...10...20...30...40...50...60...70...80...90...100 - done.


Use gdalinfo to verify the size.


    !gdalinfo /home/user/gdal_natural_earth/HYP_50M_SR_W.tif | grep Size

    Size is 10800, 5400
    Pixel Size = (0.033333333333330,-0.033333333333330)



    !gdalinfo /home/user/gdal_natural_earth/HYP_50M_SR_W_small.tif | grep Size

    Size is 5400, 2700
    Pixel Size = (0.066666666666660,-0.066666666666660)


##Rescaling

The -scale switch can be used to rescale the data range of a given image. Explicit control of the input and output ranges is also available. The gdalinfo ```-mm``` switch can be used to see pixel min/max values.

The output will display a computed Min/Max value for each band in the raster imput (3 band in our case)


    !gdalinfo -mm /home/user/gdal_natural_earth/HYP_50M_SR_W_small.tif | grep Min/Max

        Computed Min/Max=62.000,255.000
        Computed Min/Max=85.000,255.000
        Computed Min/Max=79.000,255.000


To rescale a specific band we can use the "-scale_bn" syntax where bn is a band number (e.g. "-scale_2" for the 2nd band of the output dataset), in the example below we will rescale the 3 bands of the HYP_50M_SR_W GeoTiff to be in the range 0-255 :


    !gdal_translate -scale_1 62.000 255.000 0 255.000 \
                   -scale_2 85.000 255.000 0 255.000 \
                   -scale_3 79.000 255.000 0 255.000 \
                   /home/user/gdal_natural_earth/HYP_50M_SR_W.tif /home/user/gdal_natural_earth/HYP_50M_SR_W_scaled.tif

    Input file size is 10800, 5400
    0...10...20...30...40...50...60...70...80...90...100 - done.


Check the results with ```gdalinfo``` :


    !gdalinfo -mm /home/user/gdal_natural_earth/HYP_50M_SR_W_scaled.tif | grep Min/Max

        Computed Min/Max=0.000,255.000
        Computed Min/Max=0.000,255.000
        Computed Min/Max=0.000,255.000


Let's convert the scaled output to JPG for a quick display, notice the color rearrangement.


    !gdal_translate -of JPEG -co QUALITY=40 /home/user/gdal_natural_earth/HYP_50M_SR_W_scaled.tif /home/user/gdal_natural_earth/HYP_50M_SR_W_scaled.jpg

    Input file size is 10800, 5400
    0...10...20...30...40...50...60...70...80...90...100 - done.



    Image('/home/user/gdal_natural_earth/HYP_50M_SR_W_scaled.jpg')




![jpeg](output_43_0.jpeg)


compare with [original image](#Image-Display)

##Splitting

Let’s split our image into two with ```-srcwin``` which makes a copy based on pixel/line location (xoff yoff xsize ysize). You also could use ```-projwin``` and define the corners in georeferenced coordinates (ulx uly lrx lry).


    !gdal_translate -srcwin 0 0 5400 5400 /home/user/gdal_natural_earth/HYP_50M_SR_W.tif  /home/user/gdal_natural_earth/west.tif
    !gdal_translate -srcwin 5400 0 5400 5400 /home/user/gdal_natural_earth/HYP_50M_SR_W.tif  /home/user/gdal_natural_earth/east.tif

    Input file size is 10800, 5400
    0...10...20...30...40...50...60...70...80...90...100 - done.
    Input file size is 10800, 5400
    0...10...20...30...40...50...60...70...80...90...100 - done.



    !gdal_translate -of JPEG -co QUALITY=40 /home/user/gdal_natural_earth/east.tif /home/user/gdal_natural_earth/east.jpg
    !gdal_translate -of JPEG -co QUALITY=40 /home/user/gdal_natural_earth/west.tif /home/user/gdal_natural_earth/west.jpg

    Input file size is 5400, 5400
    0...10...20...30...40...50...60...70...80...90...100 - done.
    Input file size is 5400, 5400
    0...10...20...30...40...50...60...70...80...90...100 - done.
