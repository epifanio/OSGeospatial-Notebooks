

---

# Open Source Geospatial Notebooks

##Abstract:

   This GSoC 2015 Idea will focus on the development of a cross-projects python library with the aim of bridging together the several software libraries already installed on the live through the use of the  [Jupyter notebook](http://jupyter.org) server in a series of geospatial notebooks. 

##Introduction
  
  OSGeo-Live is a self-contained bootable DVD, USB thumb drive or Virtual Machine based on Lubuntu, that allows you to try a wide variety of open source geospatial software without installing anything. It is composed entirely of free software, allowing it to be freely distributed, duplicated and passed around. It provides pre-configured applications for a range of geospatial use cases, including storage, publishing, viewing, analysis and manipulation of data. It also contains sample datasets and documentation.
  

##Background
 
   The OSGeo-Live user has access to a wide set of desktop and web GIS application, which are easily accessible from the OS application-menu and for each software a quick-starts introduction is available to help new users to get started. 
   The documentation is automatically built during the live-disc generation process from a set of RST files, one for each project, and is accessible via web browser. 
   On the OSGeo-Live also a large number of software libraries is installed and ready for use, most of them are accessible from command line or via python bindings other are accessible via specific software like R, commonly used for statistical analysis. All this software libraries, at the  moment, are hidden under the hood of the OSGeo-Live with missed or poor documentation. Moreover they can complete specific tasks like I/O, Statistic analysis, geoprocessing, Chart display and more.
 
##The idea
  
  This GSoC 2015 Idea will focus on the development of a cross-projects python library with the aim of bridging together the several software libraries already installed on the live through the use of the Jupyter notebook server [1] in a series of "topic-oriented" geospatial notebooks.
 
  This work will not only include python libraries, but thanks to recently added support for different type of kernels, will support R, Octave Bash and more. Because it supports Bash, it is now possible to include in a notebook any command line tool installed on OSGeo-Live. Since one of the main goals of OSGeo-Live is for education, this will substantially improve the user experience in having access to many tools under the OSGeo umbrella. The OSGeo-Live user will learn how to bring all this software together as well as learn how to process geospatial data using other standard scientific tools for data exploration.
 

###Topic list
* Access to Geospatial data:
    * GDAL-OGR Quickstart
    * GDAL-OGR Python Cook Book
    * OSSIM Quickstart
* Numerical cartography
    * Spatial and Coordinate Reference System
    * Working with coordinates
    * The Geodesic Problem
    * Map Projections
    * Geometric transformation
* Raster algebra :
    * gdal grass array multi layer
    * Map algebra: filtering, masking, general statistics: (this part will be dedicated to GRASS GIS, perhaps exploring the landsat 8 dataset)
* Access to web based resources :
    * OWSlib to access OGC web standards
    * Processing of NETCDF dataset
* Web-Gis :
    * publish result of processing in HTML+JS  js widgets (openlayers, leaflet, Cesium)
* Intro to geostatistic:
    * Combined use of R, GRASS and Python 
 

  Part of this idea is to develop a software library written in python, to simplify the usage of geospatial data inside the notebook. Providing wrapper function to solve general tasks like I/O, Database connections, map display using gui widgets and rich text for data documentation and report building.
 
This idea integrates several projects such as GDAL, GRASS, OSSIM, R, OTB, Numpy, Scipy, Pandas, R, owslib, netcdf4-python, pycsw, openlayers/leaflet/cesium, qgis-browser, gmt, postgis, in addition to the python specific projects (e.g. fiona, shapely, geopandas, scikit-image, pysal, cartopy, iris, and more). Generally each library that has python bindings and or is accessible from the command line.


*Note this Project plan can be subject to changes based on the feedback received by mentors and from the project's mailing list.
