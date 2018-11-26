<table width=100% border=>
<tr><td colspan=2><h1>How to Extend S/4HANA with HANA Spatial and SAC</h1></td></tr>
<tr><td><h3>Prerequisites</h3></td><td width=60%></br>&nbsp;</p></td></tr>
</table>

## Description

In the next steps we will set up our demo environment for this exercise. 

## Steps

Here are the  for completing the exercise prerequisites.

1. Starting up an S/4HANA Trial System

It is highly recommenced that this exercise be done on a trial S/4HANA system as this is a technical / 'how to' demo. This demo also uses customer sales CDS views. On a trial system these views would only return several hundred records vs. what is on a production system. If you do insist on using your production system, then you will need to filter your final custom CDS views so that a much smaller / sample record set is returned. Creating the custom views will be covered later on.

2. Option A: Accessing the SAP HANA System Using the S/4HANA Trial Appliance to Emulate a Sidecar

2. Option B: Starting an SAP Cloud Platform HANA System to Use as a Sidecar

3. Getting an SAP Analytics Cloud (SAC) System

4. Configuring the SAC Connection to the SAP HANA Database


The S/4HANA trial system can be found at the [SAP Cloud Appliance Library.](https://cal.sap.com/console/tenant_5XPSH094G71U#/solutions/614183a7-11c6-4030-9908-81b6eab86d54) If you are using the trial appliance then the appropriate user for this exercise is S4H_SD_DEM. Please see the Welcome page on the Windows Remote Desktop included with the appliance. 

Business Roles for the S/4HANA technical user (S4H_SD_DEM) include:
* SAP_BR_SALES_MANAGER

Note that the appliance Windows machine includes a configured Eclipse IDE with the needed tools for ABAP CDS development installed. If you are interested in learning more about how to set up your own Eclipse environment, please see the downloads and instructions for ABAP and HANA tools for Eclipse at https://tools.hana.ondemand.com/

For more information on getting started with the S/4HANA fully activated trial appliance please see [these videos on the SAP HANA Academy.](https://www.youtube.com/playlist?list=PLkzo92owKnVwCbYmnsFkPQ8hCyzGmXO8_)

[Go Back to the Main Page](../demoHowTo.md)
