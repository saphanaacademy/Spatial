<table width=100% border=>
<tr><td colspan=2><h1>How to Extend S/4HANA with HANA Spatial and SAC</h1></td></tr>
<tr><td><h3>Exercise Overview</h3></td><td width=60%></br>&nbsp;Difficulty Level: Intermediate</p></td></tr>
</table>

## Description
In this exercise / demo, you’ll learn how to integrate S/4HANA (on-premise) and ESRI GIS data at the data level in a HANA database. This integrated data will be consumed in SAP Analytics Cloud.

<img src="images/s4HpEsriDemoSAC01.jpg">


## Overview

* In S/4HANA a CDS view is created to combine customer, sales, and location information
* The Data Provisioning Agent is installed and the ABAP adapter is registered with the SAP HANA system
* A Remote Connection is made from the HANA system to the S/4HANA system
* A Virtual Table of the S/4HANA CDS view is created
* In HANA the Virtual Table is combined in a Calculation View with a HANA table that has Spatial Type data
* A Location Dimension view is created in HANA to provide geo-coding using a simple lookup table
* These Calculation Views are consumed in the SAP Analytics Cloud where a map analytic is created using the Spatial Type data

<img src="images/s4HpEsriDemoArchc.jpg">  


## Target group

* People interested in learning about extending S/4HANA (on-premise) with ESRI spatial data 
* People interested in extending S/4HANA with a HANA sidecar
* Data analysts and developers


## Prerequisites
  
Here is a list of the equipment prerequisites for this exercise. A link to the prerequisites page is farther below.

* A fully activated S/4HANA on-premise trial system
* An SAP HANA system (for this exercise you will use the HANA database on S/4HANA to emulate having a separate system)
* An SAP Analytics Cloud (SAC) account

Here are the knowledge prerequisites for this exercise.

* Familiarity with ABAP CDS views in S/4HANA
* Familiarity with Calculation views in SAP HANA
* Familiarity with Story design in SAP Analytics Cloud

[Go to the Prerequisites](exercises/preReqs.md)


## More Help & FAQ

For more info on this exercise, using the S/4HANA trial and the SAP Cloud Appliance Library please see [this help page.](exercises/genHelp.md)


## <a name="tasks"></a> Tasks

After you've completed the prerequisites there are a number of main tasks to complete. Some of these tasks will consist of running code in the Eclipse IDE with SAP tools. The Eclipse IDE is installed on the Windows client of the S/4HANA trial appliance. You will also need to import several HANA pieces like a sample database and some Calculation Vews.

1. You need to create an ABAP CDS view in your S/4HANA system. This view will include sales amounts by customer and location. This view does not have geo-coded data but will provide a postal code which will later be geo-coded in HANA.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Go to Task 1: Creation of a CDS View in S/4HANA](exercises/s4hViews.md)

2. You need to create a HANA database user that has the rights to create Remote Sources and tables, import objects, create Calculation Views, etc. As mentioned in the Prerequisites section, you will use the HANA database on your S/4HANA trial system to emulate having a separate HANA database / HANA sidecar. This will save you some time and perhaps money associated with readying a development HANA system for this exercise.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Go to Task 2: Creation of Developer User for the SAP HANA System](exercises/hdbUser.md)

3. The next task includes installing the Data Provisioning Agent, activating HANA's Data Provisioning server, creating a Virtual Table for the ABAP CDS view we created earlier.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Go to Task 3: Setup of Smart Data Access to the S/4HANA System](exercises/sdiConfig.md)

4. A sample database is used for this exercise and consists of US Census data as well as a table used to approximate the Longitude and Latitude of customer addresses in the S/4HANA sales data. Existing data will be transformed into HANA spatial type data.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Go to Task 4: Setup of Sample Spatial Data for the SAP HANA System](exercises/hdbData.md)

5. New HANA Calculation Views will be built that combine the remote S/4HANA customer sales data with the local Census data. One view will also feature a HANA Spatial Join. These views will be consumed in the SAP Analytics Cloud where one view is used in a map location hierarchy.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Go to Task 5: Creation of HANA Calculation Views on Integrated Data](exercises/hdbViews.md)

6. The SAP HANA system must be configured so that resources like Calculation Views are available to be consumed on the SAP Analytics Cloud. An additional component will be installed on HANA and then Cross Origin Resource Sharing will be configured.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Task 6: Setup of the SAP HANA System for Resource Sharing](exercises/hdbCORS.md)

7. In the final task you will set up a connection from the SAP Analytics Cloud to your SAP HANA database. Afterwards you will work in SAC to create a map analytic based on live data from that connection.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Task 7: Creation of Direct Connection to HANA, and Analytics in SAP Analytics Cloud](exercises/sacAnalytics.md)

