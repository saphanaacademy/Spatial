
## Prerequisites
  
Here are the equipment prerequisites for this exercise.

* A fully activated S/4HANA on premise trial system
* An SAP HANA system 
* An SAP Analytics Cloud (SAC) account
* A configured connection from the SAC tenant to the HANA system

Here are the knowledge prerequisites for this exercise.

* Familiarity with ABAP CDS views in S/4HANA
* Familiarity with Calculation views in SAP HANA
* Familiarity with Story design in SAP Analytics Cloud

It is highly recommenced that this exercise be done on a trial S/4HANA system as this is a technical / 'how to' demo. This demo also uses customer sales CDS views. On a trial systenm these views would only return several hundred records vs. what is on a production system. 

The S/4HANA trial system can be found at the [SAP Cloud Appliance Library.](https://cal.sap.com/console/tenant_5XPSH094G71U#/solutions/614183a7-11c6-4030-9908-81b6eab86d54) If you are using the trial appliance then the appropriate user for this exercise is S4H_SD_DEM. Please see the Welcome page on the Windows Remote Desktop included with the appliance. 

Business Roles for the S/4HANA technical user (S4H_SD_DEM) include:
* SAP_BR_SALES_MANAGER

Note that the appliance Windows machine includes a configured Eclipse IDE with the needed tools for ABAP CDS development installed. If you are interested in learning more about how to set up your own Eclipse environment, please see the downloads and instructions for ABAP and HANA tools for Eclipse at https://tools.hana.ondemand.com/

For more information on getting started with the S/4HANA fully activated trial appliance please see [these videos on the SAP HANA Academy.](https://www.youtube.com/playlist?list=PLkzo92owKnVwCbYmnsFkPQ8hCyzGmXO8_)
