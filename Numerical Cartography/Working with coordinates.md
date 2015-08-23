
<h1><center>[Notebooks](../) - [Numerical Cartography](../numerical cartography)</center></h1>

# Working with Coordinates

* [Coordinate notation](#Coordinate-notation)
* [Coordinate conversion](#Coordinate-conversion)
* [Datum transformation](#Datum-transformation)

## Coordinate notation
To express the values for the geographic longitude and latitude there are different notations, the most used are:
   * **degimal degrees** (eg: $30.263888889^{\circ}$)
   * **sessagesimal degrees** (eg: $ 30^{\circ} 15^{'} 50^{"}$)

A simple example to convert back and forward those 2 different notations is shown below:

---

Let's use the IPython magic funcion ```%%file``` to make a simple comma separated value (CSV) file'


    %%file test.csv
    30.263888889,45.563456
    23.457654,34.433425

    Overwriting test.csv


now read the CSV using [pandas](), we'll create a [pandas.dataframe]() using the [pandas.read_csv]() method:


    import pandas as pd


    input = pd.read_csv('test.csv', names=['Latitude', 'Longitude'])
    input




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Latitude</th>
      <th>Longitude</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>30.263889</td>
      <td>45.563456</td>
    </tr>
    <tr>
      <th>1</th>
      <td>23.457654</td>
      <td>34.433425</td>
    </tr>
  </tbody>
</table>
</div>



Simple code to convert between the two notations:

* d2s: convert from decimal degrees to sessagesimal degrees
* s2d: convert from sessagesimal degrees to decimal degrees


    import numpy as np
    
    def d2s(df,key='Latitude'):
        '''convert from decimal degrees to sessagesimal degrees
        take as input a pandas dataframe and a column name'''
        g = df[key].values.astype(int)
        p = ((( df[key].values) - df[key].values.astype(int))*60).astype(int)
        s = (((df[key].values - df[key].values.astype(int)) * 60. ) - p ) * 60.
        param = key
        ses = pd.DataFrame(np.array([g,p,s]).T, columns=['Degree','Minute','Second'] , dtype=float)
        return ses
    
    def s2d(df,key=['Degree','Minute','Second']):
        '''convert from sessagesimal degrees to decimal degrees
        take as input a pandas dataframe and a list of column names'''
        deg=df[key[0]].values+(df[key[1]].values/60.+df[key[2]].values/3600.)
        return deg


    # convert from decimal degrees to sessagesimal degree


    Lat = d2s(df=input,key='Latitude')
    Lon = d2s(df=input,key='Longitude')


    Lat




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Degree</th>
      <th>Minute</th>
      <th>Second</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>30</td>
      <td>15</td>
      <td>50.0000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>23</td>
      <td>27</td>
      <td>27.5544</td>
    </tr>
  </tbody>
</table>
</div>




    Lon




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Degree</th>
      <th>Minute</th>
      <th>Second</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>45</td>
      <td>33</td>
      <td>48.4416</td>
    </tr>
    <tr>
      <th>1</th>
      <td>34</td>
      <td>26</td>
      <td>0.3300</td>
    </tr>
  </tbody>
</table>
</div>




    # convert from sessagesimal degree to decimal degree


    s2d(Lat)




    array([ 30.26388889,  23.457654  ])




    s2d(Lon)




    array([ 45.563456,  34.433425])



---

## Coordinate conversion

Common task when working with points is to convert their coordinates from Latitude and Longitude  to UTM and viceversa.  
Common example is the position reported by a GPS receiver which usually report the position latitude and longitude expressed in decimal degrees and referred to the WGS84 ellipsoid. In this case we have a two way conversion:
   * from Geographic to UTM
   * from UTM to Geographic
Note: this is an exact conversion, it is not a transformation of coordinates. The point is located on the same ellipsoid *WGS84* and the conversion between the two different notation does not involve any approssimation.

**Example:**

We want find the UTM coordinates for the point. For the purpose of this excercize we will use the [pyproj](http://jswhit.github.io/pyproj/) module (python wrapper of the widely used Cartographic Projections Library: [PROJ](https://github.com/OSGeo/proj.4/wiki).


$$P(longitude,latitude) :\quad  -70.9393^{\circ}, 43.1356^{\circ}$$

The UTM coordinate system is divided in 60 different zones, each zone has its own definition and can be easly identified by an unic ID using its [EPSG code](). 
Our point P falls in the state of New Hampshire (US) which is included in the 19th fuse of the UTM system.
To find out which EPSG code is assigned to the UTM zone 19th on the WGS84 ellipsoid, we can use services like [EPSG.io](http://epsg.io/) which are based on the [EPSG API](http://www.ogp.org.uk/pubs/373-07-3.pdf) and look for: 

```WGS 84 / UTM zone 19N```


Which will return : 

[```EPSG:32619```](http://epsg.io/32619)

* Longitude Latitude WGS84 -> UTM 19N / WGS 84


    #import the pyproj library
    import pyproj
    
    # set point P coordinates: 
    P = (-70.93931369842528, 43.13567095719326)
    
    # define projection UTM 19 N: 
    #    UTM zone 19, WGS84 ellipse, WGS84 datum, defined by epsg code 32619
    p1 = pyproj.Proj(init='epsg:32619')
    
    #Find UTM coordinates for the point P(-70.93931369842528,43.13567095719326)
    x1, y1 = p1(P[0],P[1])


    x1, y1




    (342275.954354025, 4777706.425362386)



---
You can easly verify the results of the conversion using the [epsg.io map widget](http://epsg.io/32619/map) on  and look for:

```Jere A. Chase Ocean Engineering Laboratory
24 Colovos Road, Durham, NH 03824, United States```

which will show the coordinated of the point $P$ in longitude and lattude on the upper right and in UTM on the center bottom.

---

## Datum transformation 
(Change in reference system)


A reference system is a set of rules and measurments to establish the spatio-temporal position of a point location, regardless off the coordinate system. This system of rules and measurments must lock the degrees of freedom left free from the relative measurments. A coordinate system can be referenced to celestial bodies (quasi-inertial-reference-frame) or the more practical systems referenced to the earth. In the case of earth referenced system a SRS is defined by:

* A Reference Surface (Ellipsoid)
* Its Localization, where the ellipsoid can be earth-centered (WGS84) or oriented locally (eg. Gauss Boaga Roma 1940)

A change in reference system can not be confused with coordinate transformation, which  are pure mathematical transformations. Those problems can be separted in :

* Coordinate Transformation
* Change in Reference System (or DATUM change)



A Change in reference System is a tranformation which involve the estimation of a set of transformation parameteres. there are different methods which can be used to estimate those parameters besed on a set of reference points which coodinates are know in different reference systems. The proj library can be used to perform DATUM changes, see examples below: 

**Example** 

*  UTM 19N / WGS 84 -> UTM 19N NAD 83 


    # define projection 1: 
    #    UTM zone 19, WGS84 ellipse, WGS84 datum, defined by epsg code 32619
    p1 = pyproj.Proj(init='epsg:32619')
    
    # define projection 2: UTM zone 19, GRS 1980 ellipse, NAD83 datum
    p2 = pyproj.Proj(init='epsg:26919')
    
    # transform the UTM coordinates for the point P to projection 2 coordinates.
    x2, y2 = pyproj.transform(p1,p2,x1,y1)
    
    x2, y2




    (342275.954352494, 4777706.425244128)



*  UTM 19N / WGS 84 -> UTM 19N NAD 27 


    # define projection: UTM zone 19, Clarke 1866, NAD27 datum
    p3 = pyproj.Proj(init='epsg:26719')


    # transform the UTM coordinates for the point P to projection 3 coordinates.
    x3, y3 = pyproj.transform(p1,p3,x1,y1)


    x3, y3




    (342238.6977803253, 4777482.383716499)



Note: 

The earth is in constant movment (Plate tectonics theory). Geodesist costantly redefine the specification of ellipsoid used as reference for the various CRS. The initial definition of NAD83(1986) was intended to match GRS80 and WGS84. In this example we are considering the *original* CRS means the WGS84 with ellipsoid epoc:1984 and the NAD 83 as defined in the 1986.

This explain how close are the coordinates for the two CRS *UTM 19 N / WGS 84* and *UTM 19 N / NAD 83* which for the epoc of their definition are almost identical.
To perform a more accurate transformation it is possible to specify the projection parameters esplicitly using the proj format string.
read more: [WGS84 and NAD83](http://www.ngs.noaa.gov/CORS/Articles/WGS84NAD83.pdf), [North American Datum](https://en.wikipedia.org/wiki/North_American_Datum)

---

The problem of parameter estimation is developed on a dedicated in the [geometric transformations notebook](geometric-transformation.ipynb)

---

[top](#Notebooks---Numerical-Cartography)


    
