
#Spatial and Coordinate Reference System

A **spatial reference system** (SRS) or **coordinate reference system** (CRS) is a [coordinate-based](https://en.wikipedia.org/wiki/Coordinate_system) local, regional or global system used to locate geographical entities. A spatial reference system defines a specific [map projection](https://en.wikipedia.org/wiki/Map_projection), as well as transformations between different spatial reference systems. Spatial reference systems are defined by the [OGC](https://en.wikipedia.org/wiki/Open_Geospatial_Consortium)'s [Simple feature access](https://en.wikipedia.org/wiki/Simple_feature_access) using [well-known text](https://en.wikipedia.org/wiki/Well-known_text), and support has been implemented by several [standards-based](https://en.wikipedia.org/wiki/Technical_standard) [geographic information systems](https://en.wikipedia.org/wiki/Geographic_information_system). Spatial reference systems can be referred to using a [SRID](https://en.wikipedia.org/wiki/SRID) integer, including EPSG codes defined by the [International Association of Oil and Gas Producers](https://en.wikipedia.org/wiki/International_Association_of_Oil_and_Gas_Producers).

**source:** 

**[Wikipedia: Spatial reference system](https://en.wikipedia.org/wiki/Spatial_reference_system)**

**[Wikipedia: Geographic coordinate system](https://en.wikipedia.org/wiki/Geographic_coordinate_system)**

##Coordinate Reference System (CRS):
A position refers to the spatial location of an entity and it is determined by its spatial coordinates relative to a spatial reference system (SRS).
The most common choices of coordinates are ** *Geographic coordinates* ** and ** *UTM coordinates* **.


###Geographic latitude and longitude:
    
   A geographic coordinate system is a coordinate system that enables every location on the Earth to be specified by a set of numbers or letters.A common choice of coordinates is latitude, longitude and elevation.
    
   * **Latitude** (angle between the equatorial plane and the straight line that passes through that point and through, or close to, the center of the Earth)
   * **Longitude** (the angle east or west from a reference meridian to another meridian that passes through that position). 

The combination of these two components specifies the position of any location on the surface of the Earth, without consideration of altitude or depth. 

<img src="../images/ECEF.svg">

###Universal Transverse Mercator (UTM) coordinate system:

   The UTM coordinate system use a metric-based cartesian grid laid out on a conformally projected surface. The UTM system is not a single map projection but a series of sixty, each covering 6-degree bands of longitude.
   
   
<img src="../images/utmzone.svg">

##Geodetic Coordinates:
   
   To completely specify a location of a topographical feature on, in, or above the Earth, one has to also specify the vertical distance from the centre of the Earth, or from the surface of the Earth.
    
   In order to be unambiguous about the direction of "vertical" and the "surface" above which they are measuring, map-makers choose a reference ellipsoid with a given origin and orientation that best fits their need for the area they are mapping. They then choose the most appropriate mapping of the spherical coordinate system onto that ellipsoid, called a terrestrial reference systemor geodetic datum. Datums may be global, meaning that they represent the whole earth, or they may be local, meaning that they represent a best-fit ellipsoid to only a portion of the earth.
    
   The choice of which layer to use for defining height is arbitrary. Common height baselines include:
   * The surface of the datum ellipsoid, resulting in an ellipsoidal height
   * The mean sea level as described by the gravity geoid, yielding the orthometric height
   * A vertical datum, yielding a dynamic height relative to a known reference height.
Along with the latitude $\phi$ and longitude $\lambda$, the height $h$ provides the three-dimensional *geodetic coordinates* or *geographic coordinates* for a location.
