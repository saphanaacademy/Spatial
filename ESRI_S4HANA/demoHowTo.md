<table width=100% border=>
<tr><td colspan=2><h1>How to Extend S/4HANA with HANA Spatial and SAC</h1></td></tr>
<tr><td><h3>Exercise Overview</h3></td><td width=60%></br>&nbsp;Difficulty Level: Intermediate</p></td></tr>
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


## Target group

* People interested in learning about extending S/4HANA with ESRI spatial data 
* People interested in extending S/4HANA with a HANA sidecar
* Data analysts and developers


## Prerequisites
  
Here is a list of the equipment prerequisites for this exercise. A link to the prerequisites page is further below.

* A fully activated S/4HANA on premise trial system (or a non-production / development S/4HANA system)
* An SAP HANA system (for this exercise we can use the HANA database on (a) S/4HANA or (b) in SAP Cloud Platform)
* An SAP Analytics Cloud (SAC) account
* A configured connection from the SAC tenant to the HANA system (we will use SDI's Data Provisioning and Remote Sources)

Here are the knowledge prerequisites for this exercise.

* Familiarity with ABAP CDS views in S/4HANA
* Familiarity with Calculation views in SAP HANA
* Familiarity with Story design in SAP Analytics Cloud

[Go to the Prerequisites](exercises/preReqs.md)


## <a name="tasks"></a> Tasks

After you've completed the prerequisites there are a number of main tasks to complete. Some of these tasks will consist of running code in the Eclipse IDE with SAP tools. The Eclipse IDE is installed on the Windows client of the S/4HANA trial appliance. You will also need to import several HANA pieces like a sample database and some SQL and Calculation Vews.

1. We need to create two ABAP CDS views in our S/4HANA system. The first CDS view that needs to be created will include sales amounts by customer > location > product. The second CDS view that needs to be created will be a customer location hierarchy. This hierarchical data will be used later on in the SAP Analytics Cloud for the mapping component.

* [Creation of CDS Views in S/4HANA](exercises/s4hViews.md)

2. We need to create a HANA database user that has the rights to create remote connections and tables, import objects, create Calculation Views, etc.

&nbsp;&nbsp;&nbsp;&nbsp;[Creation of Developer User for the SAP HANA System](hdbUser)

3. The next task includes installing the Data Provisioning Agent, activating HANA's Data Provisioning server, creating Virtual Tables for the ABAP CDS views we created earlier.

&nbsp;&nbsp;&nbsp;&nbsp;[Setup of Smart Data Access to the S/4HANA System](exercises/sdiConfig.md)

4. A sample database is used for this exercise and consists of US Census data as well as a table used to approimate the Longitude and Latitude of customer addresses in the S/4HANA sales data. This task will be undertaken by the technical HANA user we created earlier.

&nbsp;&nbsp;&nbsp;&nbsp;[Setup of Sample Database for the SAP HANA System](exercises/hdbData.md)

5.

&nbsp;&nbsp;&nbsp;&nbsp;[Creation of EPSG (SRID 3857) Spatial System and Data Transform](exercises/hdbSpatial.md)

6.

&nbsp;&nbsp;&nbsp;&nbsp;[Creation of SQL and Calculation Views on Integrated Data](exercises/hdbViews.md)

7.

&nbsp;&nbsp;&nbsp;&nbsp;[Creation of Connection and Models and Story in SAP Analytics Cloud](exercises/sacAnalytics.md)

