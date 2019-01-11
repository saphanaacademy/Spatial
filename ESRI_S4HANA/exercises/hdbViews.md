<table width=100% border=>
<tr><td colspan=2><h1>How to Extend S/4HANA with HANA Spatial and SAC</h1></td></tr>
<tr><td><h3>Creation of HANA Calculation Views on Integrated Data</h3></td><td width=60%></br>&nbsp;Task #5, Using Eclipse IDE, HANA Development Perspective</p></td></tr>
</table>




## *****************************************

## NOTE > THIS TASK IS A WORK IN PROGRESS

## *****************************************





## Description

In the next steps you will two new Calculation Views. One view will combine the S/4HANA customer sales data with the Census data and will be used to build out a story in the SAP Analytics Cloud. The second view will be used in a location hierarchy for a location map.  

<img src="../images/######.jpg">

## Prerequisites

You should have completed all of the exercise [Prerequisites](../exercises/preReqs.md). You should have also completed [Task 4: Setup of Sample Spatial Data for the SAP HANA System](hdbData.md) using the Eclipse IDE.

## Steps

######

1. [######](#######)


### <a name="######"></a> ######

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

You have now completed the step "######".

[Go Back Up to the List of Steps](#steps)


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

You have now completed the step "######" and are done with the whole task of "Creation of HANA Calculation Views on Integrated Data".

Your next task is to configure the SAP HANA system so that resources like Calculation Views can be consumed on the SAP Analytics Cloud. 

[Go to Task 6: Setup of the SAP HANA System for Resource Sharing](hdbCORS.md)

[Go Back to the Main Page](../demoHowTo.md)

[Go Back Up to the List of Steps](#steps)
