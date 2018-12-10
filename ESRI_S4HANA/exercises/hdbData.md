<table width=100% border=>
<tr><td colspan=2><h1>How to Extend S/4HANA with HANA Spatial and SAC</h1></td></tr>
<tr><td><h3>Setup of Sample Spatial Data for the SAP HANA System</h3></td><td width=60%></br>&nbsp;Task #4, Using Eclipse IDE, HANA Development Perspective</p></td></tr>
</table>

## Description

In the next steps we will import and configure a sample database for the HANA database. Existing data will be transformed into spatial-type data that can be consumed later in the SAP Analytics Cloud. This task will be undertaken by the technical HANA user we created earlier.

<img src="../images/XXXXXX.jpg">

## Prerequisites

You should have completed all of the exercise [Prerequisites](../exercises/preReqs.md). You should have also completed [Task 3: Setup of Smart Data Access to the S/4HANA System](sdiConfig.md) using Data Provisioning and the Eclipse IDE.

```
-- import csv files for census and centroid tables
```

see file that has csv files as opposed to binaries (binaries are causing errors)

## Steps

You will need to use the HANA Development Perspective in Eclipse as an admin user. This admin user will have the rights to create the new development user that will complete a lot of the upcoming tasks in the HANA environment. 

1. [Logging into HANA as an Admin User](#hdbadmin)

2. Creation of EPSG (SRID 3857) Spatial System 
 
3. Data Transform
 

### <a name="hdbadmin"></a> Logging into HANA as an Admin User

* In Eclipse click on the Open Perspective shortcut to get the full list of Perspectives. Perspectives are also accessible through the Window menu > Perspective > Open Perspective > Other.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="../images/eclpers04.jpg">


data changes "HACKT28"."GEOCODE" table

```
SELECT * FROM  "HACKT28"."GEOCODE";

SELECT  
	"ZIPCODE", 
	"COORDINATES_LON",
	"COORDINATES_LAT",
	ST_GeomFromText( 'Point(' || "COORDINATES_LON" || ' ' || "COORDINATES_LAT" || ')', 1000004326 ) 
		as "POINT_BINARY",
	ST_GeomFromText( 'Point(' || "COORDINATES_LON" || ' ' || "COORDINATES_LAT" || ')', 1000004326 ).ST_AsWKT() 
		as "POINT_TEXT"
FROM "HACKT28"."GEOCODE"; 

ALTER TABLE "HACKT28"."GEOCODE"
ADD ("ZIPCODE_WGSP4326" ST_POINT(1000004326));

UPDATE "HACKT28"."GEOCODE"
SET "ZIPCODE_WGSP4326" = 
 	ST_GeomFromText( 'Point(' || "COORDINATES_LON" || ' ' || "COORDINATES_LAT" || ')', 1000004326 )
;
 
SELECT * FROM  "HACKT28"."GEOCODE";
```


data changes "HACKT28"."CENSUS" table

```
SELECT * FROM "HACKT28"."CENSUS";

SELECT  
	"CENSUS_GEO_ID",
	"COORDINATES_LON",
	"COORDINATES_LAT",
	ST_GeomFromText( 'Point(' || "COORDINATES_LON" || ' ' || "COORDINATES_LAT" || ')', 1000004326 ) 
		as "POINT_BINARY",
	ST_GeomFromText( 'Point(' || "COORDINATES_LON" || ' ' || "COORDINATES_LAT" || ')', 1000004326 ).ST_AsWKT() 
		as "POINT_TEXT"
FROM "HACKT28"."CENSUS";

ALTER TABLE "HACKT28"."CENSUS"
ADD ("CENSUS_GEO_WGSP4326" ST_POINT(1000004326));

UPDATE "HACKT28"."CENSUS"
SET "CENSUS_GEO_WGSP4326" = 
 	ST_GeomFromText( 'Point(' || "COORDINATES_LON" || ' ' || "COORDINATES_LAT" || ')', 1000004326 );
 	
SELECT * FROM "HACKT28"."CENSUS"; 
```

adding new spatial system to hana

* Some popular web mapping and visualization applications such as Google Earth, Bing Maps, and ArcGIS Online, use a spatial reference system with a Mercator projection that is based on a spherical model of the Earth. This spherical model ignores the flattening at the Earth's poles and can lead to errors of up to 800m in position and up to 0.7 percent in scale, but it also allows applications to perform projections more efficiently.

* In the past, commercial applications assigned SRID 900913 to this spatial reference system. However, EPSG has since released this projection as SRID 3857

as HACKT28 run the following syntax

```
SELECT * FROM "SYS"."ST_SPATIAL_REFERENCE_SYSTEMS";

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

SELECT * FROM "SYS"."ST_SPATIAL_REFERENCE_SYSTEMS";
```

spatial changes "HACKT28"."GEOCODE" table

```
SELECT  
	"ZIPCODE", 
	"COORDINATES_LON",
	"COORDINATES_LAT",
	"ZIPCODE_WGSP4326",
	"ZIPCODE_WGSP4326".ST_Transform(3857),
	"ZIPCODE_WGSP4326".ST_AsWKT(),
	"ZIPCODE_WGSP4326".ST_Transform(3857).ST_AsWKT()
FROM "HACKT28"."GEOCODE"; 

ALTER TABLE "HACKT28"."GEOCODE"
ADD ("ZIPCODE_EPSG3857" ST_POINT(3857));

UPDATE "HACKT28"."GEOCODE"
SET "ZIPCODE_EPSG3857" = 
	"ZIPCODE_WGSP4326".ST_Transform(3857);
	
SELECT * FROM "HACKT28"."GEOCODE";
```


spatial changes "HACKT28"."CENSUS" table

```
SELECT  
	"CENSUS_GEO_ID",
	"COORDINATES_LON",
	"COORDINATES_LAT",
	"CENSUS_GEO_WGSP4326",
	"CENSUS_GEO_WGSP4326".ST_Transform(3857),
	"CENSUS_GEO_WGSP4326".ST_AsWKT(),
	"CENSUS_GEO_WGSP4326".ST_Transform(3857).ST_AsWKT()
FROM "HACKT28"."CENSUS";

ALTER TABLE "HACKT28"."CENSUS"
ADD ("CENSUS_GEO_EPSG3857" ST_POINT(3857));

UPDATE "HACKT28"."CENSUS"
SET "CENSUS_GEO_EPSG3857" = 
	"CENSUS_GEO_WGSP4326".ST_Transform(3857);
	
SELECT * FROM "HACKT28"."CENSUS";
```

 misc SQL syntax


-- drop statements to remove new columns from tables

```
/*
alter table "HACKT28"."GEOCODE"
drop ("ZIPCODE_WGSP4326", "ZIPCODE_EPSG3857");

alter table "HACKT28"."CENSUS"
drop "CENSUS_GEO_WGSP4326", "CENSUS_GEO_EPSG3857");
*/
```

drop statement for 3857 srid

```
--DROP SPATIAL REFERENCE SYSTEM "WGS 84 / Pseudo-Mercator";
```

[Go to Task 5: Creation of EPSG (SRID 3857) Spatial System and Data Transform](hdbSpatial.md)

[Go Back to the Main Page](../demoHowTo.md)

[Go Back Up to the List of Steps](#steps)
