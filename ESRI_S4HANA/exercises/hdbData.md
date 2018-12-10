<table width=100% border=>
<tr><td colspan=2><h1>How to Extend S/4HANA with HANA Spatial and SAC</h1></td></tr>
<tr><td><h3>Setup of Sample Spatial Data for the SAP HANA System</h3></td><td width=60%></br>&nbsp;Task #4, Using Eclipse IDE, HANA Development Perspective</p></td></tr>
</table>

## Description

In the next steps we will import and configure a sample database for the HANA database. Existing data will be transformed into spatial-type data that can be consumed later in the SAP Analytics Cloud. 

<img src="../images/XXXXXX.jpg">

## Prerequisites

You should have completed all of the exercise [Prerequisites](../exercises/preReqs.md). You should have also completed [Task 3: Setup of Smart Data Access to the S/4HANA System](sdiConfig.md) using Data Provisioning and the Eclipse IDE.

## Steps

You will need to use the HANA Development Perspective in Eclipse as the HACKT28 user. Data in the form of a .csv Export from HANA will be imported into your HANA system.  In several steps the data will be readied so that Calculation Views with HANA Spatial features can be built against the new tables and the virtualized S/4HANA data.

1. [Import of Sample Data into HANA](#hdbdimp)

2. [Creation of HANA Spatial-Type Columns](#hdbdstc)

3. [Creation of EPSG (SRID 3857) Spatial System](#hdbdess) 
 
4. [Transform of HANA Spatial Data into EPSG Type](#hdbdetss)
 
### <a name="hdbdimp"></a> Import of Sample Data into HANA

There are two tables of sample data that will be imported into your HANA system. One table is a US Census table and the other table will be used to perform a simple geocoding of the customer addresses from the S/4HANA system. The geocoding in this case is approximating the location using the centroid of its zipcode approximation.

* Copy the [link address for the sample data download from here.](https://goo.gl/k9ydJV) and download the .zip file and extract the contents.

* Go to Eclipse using the SAP HANA Development perspective and right click on the HACKT28 schema in your HACKT28 user's connection. Choose "Import".

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="../images/dataimp1.jpg">

* Browse to the Windows folder where you extracted the data and select the folder one level up from the "index" folder. Press the "Next" button.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="../images/dataimp2.jpg">

* Add both of the Catalog Objects. These are both tables that were exported from a HANA database. Press the "Next" button.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="../images/dataimp3.jpg">

* In this case the only required option is to choose to import the data and you can increase the number of threads used for the import if you wish. This particular data import is not that large. Note that if you are using a production based system and want to find out more about data imports / loads then please see [the blog post here.](https://blogs.saphana.com/2013/04/07/best-practices-for-sap-hana-data-loads/)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="../images/dataimp4a.jpg">

* After you press "Finish" you will most likely need to right click on your Tables folder and choose Refresh. Now if you choose "Open Data Preview" for the Geocode table then you should see that there are two columns (they are decimal type) for longitude and latitude. In the next steps you will be creating spatial-type columns, in your new tables, based on these columns.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="../images/dataimp5.jpg">

[Go Back Up to the List of Steps](#steps)

### <a name="hdbdstc"></a> Creation of HANA Spatial-Type Columns

Using the Geocode table as an example, you will add a new spatial-type column and then populate that column by converting the longitude and latitude decimal type columns. Note that this new column will be a planar type spatial column with a system type ID Of 1000004326. The system that you will use in SAP Analytics Cloud exercise is EPSG 3857 and this system needs to be added to HANA. 

The existing decimal data could of course be converted directly into EPSG after adding that system, so the next minor steps are just to give a quick overview of converting longitude latitude data into an existing spatial system (planar 1000004326) in HANA. 

*

```
SELECT  
	"ZIPCODE", 
	"COORDINATES_LON",
	"COORDINATES_LAT",
	ST_GeomFromText( 'Point(' || "COORDINATES_LON" || ' ' || "COORDINATES_LAT" || ')', 1000004326 ) 
		as "POINT_BINARY",
	ST_GeomFromText( 'Point(' || "COORDINATES_LON" || ' ' || "COORDINATES_LAT" || ')', 1000004326 ).ST_AsWKT() 
		as "POINT_TEXT"
FROM "HACKT28"."GEOCODE"; 
```

*

```
ALTER TABLE "HACKT28"."GEOCODE"
ADD ("ZIPCODE_WGSP4326" ST_POINT(1000004326));
```

*

```
UPDATE "HACKT28"."GEOCODE"
SET "ZIPCODE_WGSP4326" = 
 	ST_GeomFromText( 'Point(' || "COORDINATES_LON" || ' ' || "COORDINATES_LAT" || ')', 1000004326 );
```

*

```
SELECT * FROM  "HACKT28"."GEOCODE";
```


data changes "HACKT28"."CENSUS" table

```
ALTER TABLE "HACKT28"."CENSUS"
ADD ("CENSUS_GEO_WGSP4326" ST_POINT(1000004326));

UPDATE "HACKT28"."CENSUS"
SET "CENSUS_GEO_WGSP4326" = 
 	ST_GeomFromText( 'Point(' || "COORDINATES_LON" || ' ' || "COORDINATES_LAT" || ')', 1000004326 );
 	
SELECT * FROM "HACKT28"."CENSUS"; 
```

[Go Back Up to the List of Steps](#steps)


### <a name="hdbdess"></a> Creation of EPSG (SRID 3857) Spatial System

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

[Go Back Up to the List of Steps](#steps)

### <a name="hdbdetss"></a> Transform of HANA Spatial Data into EPSG Type

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
