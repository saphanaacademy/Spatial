<table width=100% border=>
<tr><td colspan=2><h1>How to Extend S/4HANA with HANA Spatial and SAC&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</h1></td></tr>
<tr><td><h3>Prerequisites</h3></td><td width=60%></br>&nbsp;Development Environment</p></td></tr>
</table>

## Description

In the next steps you will set up your development environment for the exercise. 

You will need an S/4HANA system, a HANA database, and access to the SAP Analytics Cloud.

For the HANA 'sidecar' there are two options depending on what you want to accomplish. The first option will be to emulate having a sidecar and just use the HANA database that is on the S/4HANA trial appliance. The second option will be to use a HANA database on SAP Cloud Platform. The latter option is of course more work and potentially more expensive.

<img src="../images/s4HpEsriDemoArch.jpg">  

## More Help & FAQ

For more info on using the S/4HANA trial and the SAP Cloud Appliance Library and completing this exercise, please see [this help page.](genHelp.md)

## <a name="steps"></a> Steps

Here are the steps for completing the exercise prerequisites.

1. You will need to activate a trial S/4HANA System in CAL.SAP.com. This exercise should not be done on a production system.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Starting up an S/4HANA Trial System](#s4htrial)

2. There are some additional setup steps for the S/4HANA trial appliance which include installation third party software installations.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Additional Setup for the S/4HANA Trial Appliance](#s4hsetup)

3. Getting an SAP Analytics Cloud (SAC) System

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Getting an SAP Analytics Cloud (SAC) System](#sac)

## <a name="s4htrial"></a> Starting up an S/4HANA Trial System

It is highly recommenced that this exercise be done on a trial S/4HANA system as this is a technical / 'how to' demo. This demo also uses customer sales CDS views. On a trial system these views would only return several hundred records vs. what is on a production system. If you do insist on using your shop's development system, then you will need to filter your final custom CDS views so that a much smaller / sample record set is returned. Creating the custom views will be covered later on.

For information on getting started with the S/4HANA fully activated trial in the SAP Cloud Appliance Library please see [these videos on the SAP HANA Academy.](https://www.youtube.com/playlist?list=PLkzo92owKnVwCbYmnsFkPQ8hCyzGmXO8_)  Note that these videos are for the 1610 version of S/4HANA on premise but the setup steps in the videos should be applicable to a later version such as 1809.

The S/4HANA trial system can be found at the [SAP Cloud Appliance Library.](https://cal.sap.com/console/tenant_5XPSH094G71U#/solutions) and entering a search of "https://cal.sap.com/console/tenant_5XPSH094G71U#/solutions". You should see an entries such as "SAP S/4HANA 1809, Fully-Activated Appliance" where the "fully activated appliance" is already configured with users, content, etc.

NOTE: when you go through the steps of activating the appliance please ensure that you Store and Save / download the PEM file for the appliance. You will need this later on.

[Go Back Up to the List of Steps](#steps)

## <a name="s4hsetup"></a> Additional Setup for the S/4HANA Trial Appliance

After your appliance has fully started (usually takes about 90 minutes) please see the Welcome page on the Windows Remote client included with the appliance. Note that the appropriate user for this exercise in later S/4HANA tasks is S4H_SD_DEM. Business Roles for the S/4HANA technical user (S4H_SD_DEM) include the SAP_BR_SALES_MANAGER role.

Note that the appliance Windows machine includes a configured Eclipse IDE with the needed tools for ABAP CDS development installed. If you are interested in learning more about how to set up your own Eclipse environment, please see the downloads and instructions for ABAP and HANA tools for Eclipse at [tools.hana.ondemand](https://tools.hana.ondemand.com) > HANA tab.

* You will need to install the Chrome browser on the Windows Remote client as you will be using the SAP Analytics Cloud amongst other things that work better on Chrome.

* You will need to [download and install WinSCP](https://winscp.net/eng/download.php) on the Windows Remote client. This will be used in the process of adding an additional component to your HANA system.

[Go Back Up to the List of Steps](#steps)

## <a name="sac"></a> Getting an SAP Analytics Cloud (SAC) System

XXXXXX Instructions Coming Soon


You have now completed the Prerequisites for this exercise.

[Go to Task 1: Creation of CDS Views in S/4HANA](../exercises/s4hViews.md)

[Go Back to the Main Page](../demoHowTo.md)

[Go Back Up to the List of Steps](#steps)
