<table width=100% border=>
<tr><td colspan=2><h1>How to Extend S/4HANA with HANA Spatial and SAC</h1></td></tr>
<tr><td><h3>Creation of EPSG (SRID 3857) Spatial System and Transform of Spatial Data</h3></td><td width=60%></br>&nbsp;</p></td></tr>
</table>

XXXXXX need steps and video links etc.	

## Description

In the next steps we will first create a Spatial Reference System in our HANA database. This system will be EPSG / 3857 and is a requirement to use the data later ESRI Arc GIS. We will also alter an existing table in our sample HANA data so that it has a column with spatial data transformed to SRID 3857.


## Prerequisites

You will need the Eclipse IDE with SAP HANA tools installed. You will have also had to follow the previous steps setting up our HANA user and sample database.


## Steps

In the HANA Development perspective and as the HACKT28 technical HANA user, open up a new SQL console in your Eclipse IDE. Copy and paste the following code into the SQL console and execute. 

```

------------
--
-- spatial sys
--
------------

-- run this as the HACKT28 technical HANA user

CREATE SPATIAL REFERENCE SYSTEM "WGS 84 / Pseudo-Mercator" IDENTIFIED BY 3857
TYPE PLANAR
SNAP TO GRID 1e-4
TOLERANCE 1e-4
COORDINATE X BETWEEN -20037508.3427892447 AND 20037508.3427892447
COORDINATE Y BETWEEN -19929191.7668547928 AND 19929191.766854766
ORGANIZATION "EPSG" IDENTIFIED BY 3857
LINEAR UNIT OF MEASURE "metre"
ANGULAR UNIT OF MEASURE NULL
POLYGON FORMAT 'EvenOdd'
STORAGE FORMAT 'Internal'
DEFINITION 'PROJCS["Popular Visualisation CRS / Mercator",GEOGCS["Popular Visualisation CRS",DATUM["Popular_Visualisation_Datum",SPHEROID["Popular Visualisation Sphere",6378137,0,AUTHORITY["EPSG","7059"]],TOWGS84[0,0,0,0,0,0,0],AUTHORITY["EPSG","6055"]],PRIMEM["Greenwich",0,AUTHORITY["EPSG","8901"]],UNIT["degree",0.01745329251994328,AUTHORITY["EPSG","9122"]],AUTHORITY["EPSG","4055"]],UNIT["metre",1,AUTHORITY["EPSG","9001"]],PROJECTION["Mercator_1SP"],PARAMETER["central_meridian",0],PARAMETER["scale_factor",1],PARAMETER["false_easting",0],PARAMETER["false_northing",0],AUTHORITY["EPSG","3785"],AXIS["X",EAST],AXIS["Y",NORTH]]'
TRANSFORM DEFINITION '+proj=merc +a=6378137 +b=6378137 +lat_ts=0.0 +lon_0=0.0 +x_0=0.0 +y_0=0 +k=1.0 +units=m +nadgrids=@null +wktext  +no_defs';

```

[Go Back to the Main Page](../demoHowTo.md)
