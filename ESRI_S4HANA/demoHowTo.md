<table width=100% border=>
<tr><td colspan=2><h1>Exercise - Extending S/4HANA with ESRI Spatial Data</h1></td></tr>
<tr><td width=40%><h3>SAP HANA Spatial & S/4HANA</h3></td><td width=60%><h3>&nbsp;Difficulty Level: Intermediate</h3></td></tr>
</table>

## Description
In this exercise, you’ll learn how to integrate S/4HANA and ESRI GIS data at the data level. This integrated data can be consumed in SAP Analytics Cloud.

<img src="images/s4HpEsriDemoSAC01.jpg">


## Overview

* In S/4HANA CDS views are created to combine customer sales, product, and location information
* The Data Provisioning Agent is installed and the ABAP adapter is registered with the SAP HANA system
* A Remote Connection is made from the HANA system to the S/4HANA system
* Virtual Tables of the S/4HANA CDS views are created
* In HANA the virtual tables from the S/4HANA data are combined with spatial tables in calculation views for consumption

<img src="images/s4HpEsriDemoArch.jpg">  


For further reading on HANA Spatial and ESRI, click link below.

XXXXXX need appropriate link <http://www.sap.com>


## Target group

* Data analysts and developers
* People interested in learning about extending S/4HANA with ESRI spatial data  


## Prerequisites
  
Here is a list of the equipment prerequisites for this exercise. A link to the prerequisites page is further below.

* A fully activated S/4HANA on premise trial system
* An SAP HANA system (for this exercise we can use the HANA database on the S/4HANA system)
* An SAP Analytics Cloud (SAC) account
* A configured connection from the SAC tenant to the HANA system (we will use SDI's Data Provisioning and Remote Sources)

Here are the knowledge prerequisites for this exercise.

* Familiarity with ABAP CDS views in S/4HANA
* Familiarity with Calculation views in SAP HANA
* Familiarity with Story design in SAP Analytics Cloud

[Go to the Prerequisites](exercises/preReqs.md)


## <a name="steps"></a> Steps

1. [Creation of CDS View with Customer Sales, Products, and Location in S/4HANA](#cdsview1)
1. [Creation of CDS View with Customer Location Data in S/4HANA](#cdsview2)
1. [Setup of Remote Connection and Virtual Tables for the S/4HANA System](#remotecon)
1. [Setup of Sample Database for the SAP HANA System](#remotecon)
1. [Creation of EPSG (SRID 3857) Spatial System](#spatialsys)
1. [Creation of SQL and Calculation Views on Integrated Data](#remotecon)
1. [Creation of Connection and Models and Story in SAP Analytics Cloud](#remotecon)

### <a name="cdsview1"></a> Creation of CDS View with Customer Sales, Products, and Location

The first CDS view that needs to be created will include sales amounts by customer > location > product. In your Eclipse ABAP project create a new CDS view with the following information.

```
Name = ZXSH_C_SALESORDERITEMFSZ
Description = Public Consumption View, Z Copy Sales Order Item
```

<img src="images/s4HpEsriDemoPics01.jpg">

Copy the following code into the view editor. You can substitute the "SH" in ZXSH to match your namespace.
	
```
@AbapCatalog.sqlViewName: 'ZXSHCSLSORDITFSZ'
@AbapCatalog.compiler.compareFilter: true
@AccessControl.authorizationCheck: #NOT_REQUIRED
@ClientHandling.algorithm: #SESSION_VARIABLE
@EndUserText.label: 'Z Copy Sales Order Item'
@VDM.viewType: #CONSUMPTION

define view ZXSH_C_SALESORDERITEMFSZ as select from C_Salesorderitemfs
left outer join I_Customer
    on C_Salesorderitemfs.ShipToParty = I_Customer.Customer
left outer join I_Address
    on I_Customer.AddressID = I_Address.AddressID
{
    Customer,
    CustomerName,
    SalesOrder,
    RequestedDeliveryDate,
    SalesOrderItem,
    SalesOrderItemText,
    NetAmount,
    TransactionCurrency,
    RequestedQuantity,
    I_Address.AddressID,
    I_Address.AddressTimeZone,
    I_Address.CityName,
    I_Address.District,
    I_Address.Region,
    I_Address.County,
    I_Address.PostalCode
}
```

[Back to Steps](#steps)


### <a name="cdsview2"></a> Creation of CDS View with Customer Location

The second CDS view that needs to be created will be a customer location hierarchy. This hierarchical data will be used later on in the SAP Analytics Cloud for the mapping component. In your Eclipse ABAP project create a new CDS view with the following information.

```
Name = ZXSH_C_CUSTOMERGEO
Description = Public Consumption View, Customer Location Hierarchy
```

<img src="images/s4HpEsriDemoPics02.jpg">

Copy the following code into the view editor. You can substitute the "SH" in ZXSH to match your namespace.

```
@AbapCatalog.sqlViewName: 'ZXSHCCUSTOMERGEO'
@ClientHandling.algorithm: #SESSION_VARIABLE
@AbapCatalog.compiler.compareFilter: true
@AccessControl.authorizationCheck: #NOT_REQUIRED
@EndUserText.label: 'customer geo data for location hierarchy'
@VDM.viewType: #CONSUMPTION

define view ZXSH_C_CUSTOMERGEO as select from I_Customer 
inner join I_Address
    on I_Customer.AddressID = I_Address.AddressID
{
   I_Customer.Customer as LHCustomer,
   I_Address.AddressID as LHAddressID, 
   I_Address.AddressTimeZone as LHAddressTimeZone, 
   I_Address.CityName as LHCityName,
   I_Address.District as LHDistrict,
   I_Address.Region as LHRegion,
   I_Address.County as LHCounty,
   I_Address.Country as LHCountry,
   I_Address.PostalCode as LHPostalCode
}
```

[Back to Steps](#steps)


### <a name="remotecon"></a> Setup of Remote Connection and Virtual Tables for the S/4HANA System

In order to connect your SAP HANA system to your S/4HANA system you need to first set up the Data Provisioning Agent.  
https://tools.hana.ondemand.com/ > click on the Cloud Integration tab > scroll down to the Data Integration Downloads section.

* Note that this download is only for dev/testing purposes. Please contact your SAP representative for licensing of this product on a production system.

https://help.sap.com/viewer/p/HANA_SMART_DATA_INTEGRATION > in the Intallation and Upgrade section > click on the Installation and Configuration Guide

SDI ABAP Adapter https://www.youtube.com/watch?v=ZNr7xc3FHm0&list=PLkzo92owKnVwQ_preA3cxlQjn_v3W0Eh5&index=52&t=0s

[Back to Steps](#steps)


### <a name="remotecon"></a> Setup of Sample Database for the SAP HANA System

XXXXXX need steps and video links etc.	

In the next steps we will create a HANA database user that has the rights to create remote connections and tables, import objects, create Calculation Views, etc.

```
------------
--
-- hdb user
--
------------

CREATE USER HACKT28 PASSWORD Initial1;
ALTER USER HACKT28 DISABLE PASSWORD LIFETIME;

GRANT CREATE REMOTE SOURCE TO HACKT28;
GRANT ADAPTER ADMIN TO HACKT28;
GRANT AGENT ADMIN TO HACKT28;
GRANT IMPORT TO HACKT28;
GRANT CONTENT_ADMIN TO HACKT28;
GRANT MODELING TO HACKT28;


INSERT INTO _SYS_REPO.PACKAGE_CATALOG(PACKAGE_ID, SRC_SYSTEM, SRC_TENANT, DESCRIPTION, RESPONSIBLE, IS_STRUCTURAL) 
	VALUES ('HACKT28','HDB','','HACKT28','HACKT28',0);
GRANT EXECUTE ON REPOSITORY_REST TO HACKT28;
GRANT EXECUTE ON GRANT_ACTIVATED_ROLE TO HACKT28;
GRANT EXECUTE ON REVOKE_ACTIVATED_ROLE TO HACKT28;
GRANT REPO.READ, REPO.EDIT_NATIVE_OBJECTS, REPO.ACTIVATE_NATIVE_OBJECTS, REPO.MAINTAIN_NATIVE_PACKAGES 
	ON "HACKT28" TO HACKT28;
GRANT REPO.EDIT_IMPORTED_OBJECTS, REPO.ACTIVATE_IMPORTED_OBJECTS, REPO.MAINTAIN_IMPORTED_PACKAGES 
	ON "HACKT28" TO HACKT28;

-- To delete user --
-- DELETE FROM _SYS_REPO.PACKAGE_CATALOG WHERE RESPONSIBLE = 'HACKT28';
-- SELECT TOP 1000 * FROM "_SYS_REPO"."PACKAGE_CATALOG" WHERE PACKAGE_ID = 'HACKT28';
-- DROP USER HACKT28 CASCADE;

```

```

-- run this as HACKT28
GRANT SELECT, INSERT, UPDATE, DELETE, EXECUTE ON SCHEMA HACKT28 to _SYS_REPO WITH GRANT OPTION;

```

### <a name="spatialsys"></a>Creation of EPSG (SRID 3857) Spatial System

```

------------
--
-- spatial sys
--
------------

-- run this as HACKT28
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

[Back to Steps](#steps)

```

------------
--
-- import csv files for census and centroid tables
--
------------

-- see file that has csv files as opposed to binaries (binaries are causing errors)

```

[Back to Steps](#steps)


### <a name="remotecon"></a> Creation of SQL and Calculation Views on Integrated Data

XXXXXX need steps and video links etc.	

```
-- run as HACKT28 to create 3 sql views

-- these sql views will be accessed later in the calculation views
-- we're using sql views as we need to modify a postal code field from s4hana
-- this postal code is used in joins in the calculation views and therefore is modified beforehand

---------------
--
-- sql view SV_ZXSHCCUSTOMERGEO
--
---------------

CREATE VIEW "HACKT28"."SV_ZXSHCCUSTOMERGEO" AS 
select
	 T0."LHCUSTOMER",
	 T0."LHADDRESSID",
	 T0."LHADDRESSTIMEZONE",
	 T0."LHCITYNAME",
	 T0."LHDISTRICT",
	 T0."LHREGION",
	 T0."LHCOUNTY",
	 T0."LHCOUNTRY",
	 case when instr(T0."LHPOSTALCODE", '-') > 0 
		then left(T0."LHPOSTALCODE", instr(T0."LHPOSTALCODE", '-')-1) 
		else T0."LHPOSTALCODE" 
	 	end as LHPOSTALCODE 
from "HACKT28"."VT_RS_Abap_S4H_ZXSHCCUSTOMERGEO" T0;

select * from "HACKT28"."SV_ZXSHCCUSTOMERGEO";


---------------
--
-- sql view SV_ZXSHCSLSORDITFSZ
--
---------------

CREATE VIEW "HACKT28"."SV_ZXSHCSLSORDITFSZ" AS 
select
	 "T0"."MANDT" ,
	 "T0"."CUSTOMER" ,
	 "T0"."CUSTOMERNAME" ,
	 "T0"."SALESORDER" ,
	 "T0"."REQUESTEDDELIVERYDATE" ,
	 "T0"."SALESORDERITEM" ,
	 "T0"."SALESORDERITEMTEXT" ,
	 "T0"."NETAMOUNT" ,
	 "T0"."TRANSACTIONCURRENCY" ,
	 "T0"."REQUESTEDQUANTITY" ,
	 "T0"."ADDRESSID" ,
	 "T0"."ADDRESSTIMEZONE" ,
	 "T0"."CITYNAME" ,
	 "T0"."DISTRICT" ,
	 "T0"."REGION" ,
	 "T0"."COUNTY" ,
	 "T0"."POSTALCODE" ,
	 case when instr(T0."POSTALCODE", '-') > 0 
		then left(T0."POSTALCODE", instr(T0."POSTALCODE", '-')-1) 
		else T0."POSTALCODE" 
	 	end as POSTALCODELINK 
from "HACKT28"."VT_RS_Abap_S4H_ZXSHCSLSORDITFSZ" T0;

select * from "HACKT28"."SV_ZXSHCSLSORDITFSZ";


---------------
--
-- sql view SV_ZXSHCSLSORDITFSZ_HDBGEOZIPCODECENTROID
--
---------------

CREATE VIEW "HACKT28"."SV_ZXSHCSLSORDITFSZ_HDBGEOZIPCODECENTROID" AS 
select
	 "T0"."MANDT" ,
	 "T0"."CUSTOMER" ,
	 "T0"."CUSTOMERNAME" ,
	 "T0"."SALESORDER" ,
	 "T0"."REQUESTEDDELIVERYDATE" ,
	 "T0"."SALESORDERITEM" ,
	 "T0"."SALESORDERITEMTEXT" ,
	 "T0"."NETAMOUNT" ,
	 "T0"."TRANSACTIONCURRENCY" ,
	 "T0"."REQUESTEDQUANTITY" ,
	 "T0"."ADDRESSID" ,
	 "T0"."ADDRESSTIMEZONE" ,
	 "T0"."CITYNAME" ,
	 "T0"."DISTRICT" ,
	 "T0"."REGION" ,
	 "T0"."COUNTY" ,
	 "T0"."POSTALCODE" ,
	 "T0"."POSTALCODELINK" ,
	 "T1"."ZIPCODE" ,
	 "T1"."ZIPCENTROID" ,
	 "T1"."ZIPCENTROID3857" 
from "HACKT28"."SV_ZXSHCSLSORDITFSZ" T0 
left outer join "HACKT28"."GEOZIPCODECENTROID" T1 
	on T0."POSTALCODELINK" = T1."ZIPCODE";

select * from "HACKT28"."SV_ZXSHCSLSORDITFSZ_HDBGEOZIPCODECENTROID";
```

	

[Back to Steps](#steps)


### <a name="remotecon"></a> Creation of Connection and Models and Story in SAP Analytics Cloud

XXXXXX need steps and video links etc.		

[Back to Steps](#steps)

