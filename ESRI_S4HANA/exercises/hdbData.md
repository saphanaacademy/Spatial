<table width=100% border=>
<tr><td colspan=2><h1>How to Extend S/4HANA with HANA Spatial and SAC</h1></td></tr>
<tr><td><h3>Setup of Sample Data for the SAP HANA System</h3></td><td width=60%></br>&nbsp;Task #4, Using Eclipse IDE, HANA Development Perspective</p></td></tr>
</table>

## Description

In the next steps we will import a sample database for the HANA database. This task will be undertaken by the technical HANA user we created earlier.

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

### <a name="hdbadmin"></a> Logging into HANA as an Admin User

* In Eclipse click on the Open Perspective shortcut to get the full list of Perspectives. Perspectives are also accessible through the Window menu > Perspective > Open Perspective > Other.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="../images/eclpers04.jpg">

[Go to Task 5: Creation of EPSG (SRID 3857) Spatial System and Data Transform](hdbSpatial.md)

[Go Back to the Main Page](../demoHowTo.md)

[Go Back Up to the List of Steps](#steps)
