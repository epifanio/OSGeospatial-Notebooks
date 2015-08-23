

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
* **c** - Access to web based resources :
    * use of OWSlib to access web based resourcesusing OGC web standards
    * example access and processing of NETCDF dataset
* **d** - Simple web-gis products:
    * publish result of processing in HTML+JS  js widgets (openlayers, leaflet, Cesium)
* **e** - Intro to geostatistic:
    * Combined use of R, GRASS and Python 
 
*Note: After sharing this proposal on the OSGeo-Edu mailing list [2], instructors from University of Massachusetts ,  University of Denver, and Polytechnic of Milano are willing to collaborate sharing educational material to be adapted to the "notebook approach".
 
  Part of this idea is to develop a software library written in python, to simplify the usage of geospatial data inside the notebook. Providing wrapper function to solve general tasks like I/O, Database connections, map display using gui widgets and rich text for data documentation and report building.
 
This idea integrates several projects such as GDAL, GRASS, OSSIM, R, OTB, Numpy, Scipy, Pandas, R, owslib, netcdf4-python, pycsw, openlayers/leaflet/cesium, qgis-browser, gmt, postgis, in addition to the python specific projects (e.g. fiona, shapely, geopandas, scikit-image, pysal, cartopy, iris, and more). Generally each library that has python bindings and or is accessible from the command line. Part of this idea is to :
 
* Develop topic oriented geospatial notebooks as described above (topics TBD)

* Implement a software library written in python, to simplify the usage of geospatial data inside the notebook. This library will provide helper function to work with geospatial data (e.g. general tasks like I/O, Database connections, map display using gui widgets and rich text for data documentation and report building) taking advantage of the api provided by Jupyter.

* Reorganize the way how python libraries are installed on the live by packaging, as .deb, each python project that is missing a proper debian package. Resulting deb can then be upload on the ubuntu gis repository (before approval to ubuntu/debian gis official repository, the packages can can be hosted on an ad-hoc OSgeo-Live debian repository in incubation state)

* Revisiting and upgrading existent OsGeo-Live Quickstart documentation for each project involved in this idea (the rst file format used by OSGeo-Live documentation can be generated on the fly by running notebooks in batch mode, this will integrate quickstart testing and document building in a single process, keeping the quickstarter (notebook-enabled) up-to-date) 

## Project plan
 
###Week 1 
  Discuss with mentors about the topic oriented notebooks, the idea will be to build the notebooks in sections, subsections, references, appendix, acknowledgment. I'll need to spend the first and perhaps second week to organize a precise outline. The [list above](README.ipynb#Topic-list) is a first attempt of possible main topics (dedicating up to 15 days to each topic) 
  
*note: the list of topics I identified as possible candidate to be included in this GSoC. With the mentor advise, based on the time frame and complexity we want reach for each topic, I will identify the ones to implement (if not all)*
 
Start to develop the skeleton of the library to host the classes and methods used as utility functions (setup.py, sphinx docs, directory structure, dependencies)
 
 
###Week 2  
Continue to work on the outlined topics
Set-up the notebook environment variables (needed by some software like GRASS, GMT, R and others) to have them exported correctly in the notebook environment
Start to include in the python library some wrappers around the notebook display capabilities (html, latex, images (url/files), short-cut to command-line, output parser)
 
###Week 3  
First round in packaging missed dependencies
Implement new utility methods as they come necessary, fix possible bugs in the one already implemented (this step will be repeated for each week i'll avoid to repeat it in the next points )
Start to work on topic (a) 
 
###Week 4  
Finish and testing topic (a)  - Mentor will test and provide feedback on a notebook run
Check the notebook output as RST and have a first look on its integration in the OSGeo-Live documentation build process  
 
###Week 5 
Start to work on topic (b)
Continue to work on packaging if needed
 
###Week 6 
Finish and testing topic (b)  - Mentor will test and provide feedback on a notebook run
continue to work on 'RST build-doc' process (if needed)
 
###Week 7  
Start to work on topic (c)
Prepare script to build a first demo of the OSGeo-Live with a subset of application (only the major apps and the ones used to test the notebook) 
 
###Week 8 
Finish and testing topic (c)  - Mentor will test and provide feedback on a notebook run
checking, cleaning, reorganizing classes and methods developed in the utility library (deep look on HTML and JS templates to be used in topic d)
 
###Week 9  
Start to work on topic (d)
FOSS4G EU (feedback from OSGE-Edu community, code sprint and testing)
 
###Week 10 
Continue working on utility library to include HTML and JS template rendering)
Finish and testing topic (d)  - Mentor will test and provide feedback on a notebook run
 
###Week 11 
Start to work on topic (e)
Second round in packaging of missed dependencies
 
###Week 12 
Finish and testing topic (e)  - Mentor will test and provide feedback on a notebook run
Test the automated build of the full set of notebooks
 
###Week 13
Debug and final packaging
 
*Note this Project plan can be subject to changes based on the feedback received by mentors and from the project's mailing list.
