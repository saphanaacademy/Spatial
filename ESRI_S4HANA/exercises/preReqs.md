<table width=100% border=>
<tr><td colspan=2><h1>How to Extend S/4HANA with HANA Spatial and SAC</h1></td></tr>
<tr><td><h3>Prerequisites</h3></td><td width=60%></br>&nbsp;Getting Your Environment Ready</p></td></tr>
</table>

## Description

In the next steps we will set up our development / trial environment for the exercise. 

We will need an S/4HANA system, a HANA datbase, and access to the SAP Analytics Cloud.

For the HANA 'sidecar' there are two options depending on what you want to accomplish. The first option will be to emulate having a sidecar and just use the HANA database that is on the S/4HANA trial appliance. The second option will be to use a HANA database on SAP Cloud Platform. The latter option is of course more work and potentially more expensive.

## <a name="steps"></a> Steps

Here are the steps for completing the exercise prerequisites.

1. It is highly recommenced that this exercise be done on a trial S/4HANA system as this is a technical / 'how to' demo. This demo also uses customer sales CDS views. On a trial system these views would only return several hundred records vs. what is on a production system. If you do insist on using your production system, then you will need to filter your final custom CDS views so that a much smaller / sample record set is returned. Creating the custom views will be covered later on.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Starting up an S/4HANA Trial System](#s4htrial)

2. (Option A) Accessing the SAP HANA System Using the S/4HANA Trial Appliance

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Accessing the SAP HANA System Using the S/4HANA Trial Appliance](#hdbons4h)

2. (Option B) Starting an SAP Cloud Platform HANA System to Use as a Sidecar

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Starting an SAP Cloud Platform HANA System to Use as a Sidecar](#hdbonscp)

3. Getting an SAP Analytics Cloud (SAC) System

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Getting an SAP Analytics Cloud (SAC) System](#sac)

4. Configuring the SAC Connection to the SAP HANA Database

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Configuring the SAC Connection to the SAP HANA Database](#sactohdb)


## <a name="s4htrial"></a> Starting up an S/4HANA Trial System

The S/4HANA trial system can be found at the [SAP Cloud Appliance Library.](https://cal.sap.com/console/tenant_5XPSH094G71U#/solutions/614183a7-11c6-4030-9908-81b6eab86d54) If you are using the trial appliance then the appropriate user for this exercise is S4H_SD_DEM. Please see the Welcome page on the Windows Remote Desktop included with the appliance. 

Business Roles for the S/4HANA technical user (S4H_SD_DEM) include:
* SAP_BR_SALES_MANAGER

Note that the appliance Windows machine includes a configured Eclipse IDE with the needed tools for ABAP CDS development installed. If you are interested in learning more about how to set up your own Eclipse environment, please see the downloads and instructions for ABAP and HANA tools for Eclipse at https://tools.hana.ondemand.com/

For more information on getting started with the S/4HANA fully activated trial appliance please see [these videos on the SAP HANA Academy.](https://www.youtube.com/playlist?list=PLkzo92owKnVwCbYmnsFkPQ8hCyzGmXO8_)

[Go Back to the List of Steps](#steps)

## <a name="hdbons4h"></a> Accessing the SAP HANA System Using the S/4HANA Trial Appliance

[Go Back to the List of Steps](#steps)

## <a name="hdbonscp"></a> Starting an SAP Cloud Platform HANA System to Use as a Sidecar

[Go Back to the List of Steps](#steps)

## <a name="sac"></a> Getting an SAP Analytics Cloud (SAC) System

[Go Back to the List of Steps](#steps)

## <a name="sactohdb"></a> Configuring the SAC Connection to the SAP HANA Database

[Go Back to the List of Steps](#steps)

[Go Back to the Main Page](../demoHowTo.md)
