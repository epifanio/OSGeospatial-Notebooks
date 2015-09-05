##[Notebooks](../../)/[Access to Geospatial data](../GDAL-OGR Quickstart/)/[GDAL-OGR Quickstart](GDAL-OGR Quickstart/GDAL-OGR Quickstart.md)

<b><h1 style="margin: 0.0px 0.0px 0.0px 0.0px; line-height: 15.4px; font: 18.0px 'Lucida Sans'; color: #004d87; -webkit-text-stroke: #004d87; background-color: #ffffff"><span class="s1">gdalinfo</span></h1></b> 

<b><h2 style="margin: 0.0px 0.0px 0.0px 0.0px; line-height: 15.4px; font: 16.0px 'Lucida Sans'; color: #004d87; -webkit-text-stroke: #004d87; background-color: #ffffff"><span class="s1">get information about the raster data</span></h2></b> 


    !gdalinfo /home/user/gdal_natural_earth/HYP_50M_SR_W.tif

    Driver: GTiff/GeoTIFF
    Files: /home/user/gdal_natural_earth/HYP_50M_SR_W.tif
           /home/user/gdal_natural_earth/HYP_50M_SR_W.tfw
    Size is 10800, 5400
    Coordinate System is:
    GEOGCS["WGS 84",
        DATUM["WGS_1984",
            SPHEROID["WGS 84",6378137,298.257223563,
                AUTHORITY["EPSG","7030"]],
            AUTHORITY["EPSG","6326"]],
        PRIMEM["Greenwich",0],
        UNIT["degree",0.0174532925199433],
        AUTHORITY["EPSG","4326"]]
    Origin = (-179.999999999999972,90.000000000000000)
    Pixel Size = (0.033333333333330,-0.033333333333330)
    Metadata:
      AREA_OR_POINT=Area
      TIFFTAG_DATETIME=2012:07:16 09:16:14
      TIFFTAG_RESOLUTIONUNIT=2 (pixels/inch)
      TIFFTAG_SOFTWARE=Adobe Photoshop CS5 Macintosh
      TIFFTAG_XRESOLUTION=342.85699
      TIFFTAG_YRESOLUTION=342.85699
    Image Structure Metadata:
      COMPRESSION=YCbCr JPEG
      INTERLEAVE=PIXEL
      SOURCE_COLOR_SPACE=YCbCr
    Corner Coordinates:
    Upper Left  (-180.0000000,  90.0000000) (180d 0' 0.00"W, 90d 0' 0.00"N)
    Lower Left  (-180.0000000, -90.0000000) (180d 0' 0.00"W, 90d 0' 0.00"S)
    Upper Right ( 180.0000000,  90.0000000) (180d 0' 0.00"E, 90d 0' 0.00"N)
    Lower Right ( 180.0000000, -90.0000000) (180d 0' 0.00"E, 90d 0' 0.00"S)
    Center      (  -0.0000000,   0.0000000) (  0d 0' 0.00"W,  0d 0' 0.00"N)
    Band 1 Block=256x256 Type=Byte, ColorInterp=Red
    Band 2 Block=256x256 Type=Byte, ColorInterp=Green
    Band 3 Block=256x256 Type=Byte, ColorInterp=Blue


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

    Supported Formats:
      VRT (rw+v): Virtual Raster
      GTiff (rw+vs): GeoTIFF
      NITF (rw+vs): National Imagery Transmission Format
      RPFTOC (rovs): Raster Product Format TOC format
      ECRGTOC (rovs): ECRG TOC format
      HFA (rw+v): Erdas Imagine Images (.img)
      SAR_CEOS (rov): CEOS SAR Image
      CEOS (rov): CEOS Image
      JAXAPALSAR (rov): JAXA PALSAR Product Reader (Level 1.1/1.5)
      GFF (rov): Ground-based SAR Applications Testbed File Format (.gff)
      ELAS (rw+v): ELAS
      AIG (rov): Arc/Info Binary Grid
      AAIGrid (rwv): Arc/Info ASCII Grid
      GRASSASCIIGrid (rov): GRASS ASCII Grid
      SDTS (rov): SDTS Raster
      OGDI (ros): OGDI Bridge
      DTED (rwv): DTED Elevation Raster
      PNG (rwv): Portable Network Graphics
      JPEG (rwv): JPEG JFIF
      MEM (rw+): In Memory Raster
      JDEM (rov): Japanese DEM (.mem)
      GIF (rwv): Graphics Interchange Format (.gif)
      BIGGIF (rov): Graphics Interchange Format (.gif)
      ESAT (rov): Envisat Image Format
      BSB (rov): Maptech BSB Nautical Charts
      XPM (rwv): X11 PixMap Format
      BMP (rw+v): MS Windows Device Independent Bitmap
      DIMAP (rov): SPOT DIMAP
      AirSAR (ro): AirSAR Polarimetric Image
      RS2 (ros): RadarSat 2 XML Product
      PCIDSK (rw+v): PCIDSK Database File
      PCRaster (rw): PCRaster Raster File
      ILWIS (rw+v): ILWIS Raster Map
      SGI (rw+): SGI Image File Format 1.0
      SRTMHGT (rwv): SRTMHGT File Format
      Leveller (rw+): Leveller heightfield
      Terragen (rw+): Terragen heightfield
      GMT (rw): GMT NetCDF Grid Format
      netCDF (rw+s): Network Common Data Format
      HDF4 (ros): Hierarchical Data Format Release 4
      HDF4Image (rw+): HDF4 Dataset
      ISIS3 (rov): USGS Astrogeology ISIS cube (Version 3)
      ISIS2 (rw+v): USGS Astrogeology ISIS cube (Version 2)
      PDS (rov): NASA Planetary Data System
      TIL (rov): EarthWatch .TIL
      ERS (rw+v): ERMapper .ers Labelled
      L1B (rovs): NOAA Polar Orbiter Level 1b Data Set
      FIT (rwv): FIT Image
      GRIB (rov): GRIdded Binary (.grb)
      JPEG2000 (rwv): JPEG-2000 part 1 (ISO/IEC 15444-1)
      RMF (rw+v): Raster Matrix Format
      WCS (rovs): OGC Web Coverage Service
      WMS (rwvs): OGC Web Map Service
      MSGN (ro): EUMETSAT Archive native (.nat)
      RST (rw+v): Idrisi Raster A.1
      INGR (rw+v): Intergraph Raster
      GSAG (rwv): Golden Software ASCII Grid (.grd)
      GSBG (rw+v): Golden Software Binary Grid (.grd)
      GS7BG (rw+v): Golden Software 7 Binary Grid (.grd)
      COSAR (ro): COSAR Annotated Binary Matrix (TerraSAR-X)
      TSX (rov): TerraSAR-X Product
      COASP (ro): DRDC COASP SAR Processor Raster
      R (rwv): R Object Data Store
      MAP (rov): OziExplorer .MAP
      PNM (rw+v): Portable Pixmap Format (netpbm)
      DOQ1 (rov): USGS DOQ (Old Style)
      DOQ2 (rov): USGS DOQ (New Style)
      ENVI (rw+v): ENVI .hdr Labelled
      EHdr (rw+v): ESRI .hdr Labelled
      GenBin (rov): Generic Binary (.hdr Labelled)
      PAux (rw+): PCI .aux Labelled
      MFF (rw+): Vexcel MFF Raster
      MFF2 (rw+): Vexcel MFF2 (HKV) Raster
      FujiBAS (ro): Fuji BAS Scanner Image
      GSC (rov): GSC Geogrid
      FAST (rov): EOSAT FAST Format
      BT (rw+v): VTP .bt (Binary Terrain) 1.3 Format
      LAN (rw+v): Erdas .LAN/.GIS
      CPG (ro): Convair PolGASP
      IDA (rw+): Image Data and Analysis
      NDF (rov): NLAPS Data Format
      EIR (rov): Erdas Imagine Raw
      DIPEx (rov): DIPEx
      LCP (rwv): FARSITE v.4 Landscape File (.lcp)
      GTX (rw+v): NOAA Vertical Datum .GTX
      LOSLAS (rov): NADCON .los/.las Datum Grid Shift
      NTv2 (rw+vs): NTv2 Datum Grid Shift
      CTable2 (rw+v): CTable2 Datum Grid Shift
      ACE2 (rov): ACE2
      SNODAS (rov): Snow Data Assimilation System
      KRO (rw+v): KOLOR Raw
      ARG (rwv): Azavea Raster Grid format
      RIK (ro): Swedish Grid RIK (.rik)
      USGSDEM (rwv): USGS Optional ASCII DEM (and CDED)
      GXF (ro): GeoSoft Grid Exchange Format
      DODS (ro): DAP 3.x servers
      HTTP (ro): HTTP Fetching Wrapper
      BAG (ro): Bathymetry Attributed Grid
      HDF5 (ros): Hierarchical Data Format Release 5
      HDF5Image (ro): HDF5 Dataset
      NWT_GRD (rov): Northwood Numeric Grid Format .grd/.tab
      NWT_GRC (rov): Northwood Classified Grid Format .grc/.tab
      ADRG (rw+vs): ARC Digitized Raster Graphics
      SRP (rovs): Standard Raster Product (ASRP/USRP)
      BLX (rw): Magellan topo (.blx)
      Rasterlite (rws): Rasterlite
      EPSILON (rwv): Epsilon wavelets
      PostGISRaster (rws): PostGIS Raster driver
      SAGA (rw+v): SAGA GIS Binary Grid (.sdat)
      KMLSUPEROVERLAY (rwv): Kml Super Overlay
      XYZ (rwv): ASCII Gridded XYZ
      HF2 (rwv): HF2/HFZ heightfield raster
      PDF (rwvs): Geospatial PDF
      OZI (rov): OziExplorer Image File
      CTG (rov): USGS LULC Composite Theme Grid
      E00GRID (rov): Arc/Info Export E00 GRID
      WEBP (rwv): WEBP
      ZMap (rwv): ZMap Plus Grid
      NGSGEOID (rov): NOAA NGS Geoid Height Grids
      MBTiles (rov): MBTiles
      IRIS (rov): IRIS data (.PPI, .CAPPi etc)


Each format reports if it is:
* read only (ro),
* read/write (rw) or
* read/write/update (rw+).

It is also possible to ask for specific formats details:


    !gdalinfo --format GTiff 

    Format Details:
      Short Name: GTiff
      Long Name: GeoTIFF
      Extension: tif
      Mime Type: image/tiff
      Help Topic: frmt_gtiff.html
      Supports: Subdatasets
      Supports: Create() - Create writeable dataset.
      Supports: CreateCopy() - Create dataset by copying another.
      Supports: Virtual IO - eg. /vsimem/
      Creation Datatypes: Byte UInt16 Int16 UInt32 Int32 Float32 Float64 CInt16 CInt32 CFloat32 CFloat64
    
    <CreationOptionList>
      <Option name="COMPRESS" type="string-select">
        <Value>NONE</Value>
        <Value>LZW</Value>
        <Value>PACKBITS</Value>
        <Value>JPEG</Value>
        <Value>CCITTRLE</Value>
        <Value>CCITTFAX3</Value>
        <Value>CCITTFAX4</Value>
        <Value>DEFLATE</Value>
        <Value>LZMA</Value>
      </Option>
      <Option name="PREDICTOR" type="int" description="Predictor Type" />
      <Option name="JPEG_QUALITY" type="int" description="JPEG quality 1-100" default="75" />
      <Option name="ZLEVEL" type="int" description="DEFLATE compression level 1-9" default="6" />
      <Option name="LZMA_PRESET" type="int" description="LZMA compression level 0(fast)-9(slow)" default="6" />
      <Option name="NBITS" type="int" description="BITS for sub-byte files (1-7), sub-uint16 (9-15), sub-uint32 (17-31)" />
      <Option name="INTERLEAVE" type="string-select" default="PIXEL">
        <Value>BAND</Value>
        <Value>PIXEL</Value>
      </Option>
      <Option name="TILED" type="boolean" description="Switch to tiled format" />
      <Option name="TFW" type="boolean" description="Write out world file" />
      <Option name="RPB" type="boolean" description="Write out .RPB (RPC) file" />
      <Option name="BLOCKXSIZE" type="int" description="Tile Width" />
      <Option name="BLOCKYSIZE" type="int" description="Tile/Strip Height" />
      <Option name="PHOTOMETRIC" type="string-select">
        <Value>MINISBLACK</Value>
        <Value>MINISWHITE</Value>
        <Value>PALETTE</Value>
        <Value>RGB</Value>
        <Value>CMYK</Value>
        <Value>YCBCR</Value>
        <Value>CIELAB</Value>
        <Value>ICCLAB</Value>
        <Value>ITULAB</Value>
      </Option>
      <Option name="SPARSE_OK" type="boolean" description="Can newly created files have missing blocks?" default="FALSE" />
      <Option name="ALPHA" type="string-select" description="Mark first extrasample as being alpha">
        <Value>NON-PREMULTIPLIED</Value>
        <Value>PREMULTIPLIED</Value>
        <Value>UNSPECIFIED</Value>
        <Value aliasOf="NON-PREMULTIPLIED">YES</Value>
        <Value aliasOf="UNSPECIFIED">NO</Value>
      </Option>
      <Option name="PROFILE" type="string-select" default="GDALGeoTIFF">
        <Value>GDALGeoTIFF</Value>
        <Value>GeoTIFF</Value>
        <Value>BASELINE</Value>
      </Option>
      <Option name="PIXELTYPE" type="string-select">
        <Value>DEFAULT</Value>
        <Value>SIGNEDBYTE</Value>
      </Option>
      <Option name="BIGTIFF" type="string-select" description="Force creation of BigTIFF file">
        <Value>YES</Value>
        <Value>NO</Value>
        <Value>IF_NEEDED</Value>
        <Value>IF_SAFER</Value>
      </Option>
      <Option name="ENDIANNESS" type="string-select" default="NATIVE" description="Force endianness of created file. For DEBUG purpose mostly">
        <Value>NATIVE</Value>
        <Value>INVERTED</Value>
        <Value>LITTLE</Value>
        <Value>BIG</Value>
      </Option>
      <Option name="COPY_SRC_OVERVIEWS" type="boolean" default="NO" description="Force copy of overviews of source dataset (CreateCopy())" />
      <Option name="SOURCE_ICC_PROFILE" type="string" description="ICC profile" />
      <Option name="SOURCE_PRIMARIES_RED" type="string" description="x,y,1.0 (xyY) red chromaticity" />
      <Option name="SOURCE_PRIMARIES_GREEN" type="string" description="x,y,1.0 (xyY) green chromaticity" />
      <Option name="SOURCE_PRIMARIES_BLUE" type="string" description="x,y,1.0 (xyY) blue chromaticity" />
      <Option name="SOURCE_WHITEPOINT" type="string" description="x,y,1.0 (xyY) whitepoint" />
      <Option name="TIFFTAG_TRANSFERFUNCTION_RED" type="string" description="Transfer function for red" />
      <Option name="TIFFTAG_TRANSFERFUNCTION_GREEN" type="string" description="Transfer function for green" />
      <Option name="TIFFTAG_TRANSFERFUNCTION_BLUE" type="string" description="Transfer function for blue" />
      <Option name="TIFFTAG_TRANSFERRANGE_BLACK" type="string" description="Transfer range for black" />
      <Option name="TIFFTAG_TRANSFERRANGE_WHITE" type="string" description="Transfer range for white" />
    </CreationOptionList>