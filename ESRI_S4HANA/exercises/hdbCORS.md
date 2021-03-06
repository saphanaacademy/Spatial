<table width=100% border=>
<tr><td colspan=2><h1>How to Extend S/4HANA with HANA Spatial and SAC</h1></td></tr>
<tr><td><h3>Setup of the SAP HANA System for Resource Sharing</h3></td><td width=60%></br>&nbsp;Task #6, WinSCP and Eclipse IDE
</table>

## Description

In the next steps you will configure the SAP HANA system so that resources like Calculation Views can be consumed on the SAP Analytics Cloud. 

<img src="../images/cors3a.jpg">

## Prerequisites

You should have completed all of the exercise [Prerequisites](../exercises/preReqs.md). You should have also completed [Task 5: Creation of HANA Calculation Views on Integrated Data](hdbViews.md) using the Eclipse IDE.

## Warnings

During the installation process for the SAP HANA EPM-MDS plugin your HANA system will be stopped and started automatically. 

This exercise is aimed at users who will connect their SAP Analytics Cloud tenant to an S/4HANA trial appliance. If you are a HANA administrator setting up a connection to a production system then please consult [help.sap.com](https://help.sap.com/viewer/search?q=SAP%20Analytics%20Cloud%20Live%20Data%20Connections%20to%20SAP%20HANA) with a search on "SAP Analytics Cloud Live Data Connections to SAP HANA".

## <a name="steps"></a> Steps

A connection must be made between your SAP HANA database and the SAP Analytics Cloud. In order to establish the sharing of objects from HANA with SAC, you must do so with either [CORS (Cross-Origin Resource Sharing) or via a reverse proxy.](https://blogs.sap.com/2017/12/29/creating-sap-analytics-cloud-live-connection-to-sap-hana-database-on-sap-cloud-platform/) In this exercise you will set up CORS and then later a "Direct" connection will be used in SAC.

An additional component will be installed on HANA and then Cross Origin Resource Sharing will be configured.

1. [Checking to see if the SAP HANA EPM-MDS Plugin is Already Installed](#epmmdstest)
1. [Downloading the SAP HANA EPM-MDS Plugin](#epmmds)
1. [Connecting WinSCP to the S/4HANA Appliance's Linux File System](#winscp)
1. [Installing the SAP HANA EPM-MDS Plugin](#epmmdsinst)
1. [Configuring Cross Origin Resource Sharing, CORS](#cors)

### <a name="epmmdstest"></a> Checking to see if the SAP HANA EPM-MDS Plugin is Already Installed

In this exercise, you will most likely need to download the EPM-MDS plugin which will facilitate a connection between the SAP Analytics Cloud and SAP HANA Calculation Views. At this time (January 3rd 2019 at 06:56 AM PST) and as per [this SAP KBA](https://apps.support.sap.com/sap/support/knowledge/public/en/2536153) this plugin is not installed by default on HANA 2.0.

To first check to verify thta the EPM-MDS plugin is not installed, go to your Windows desktop client, open the url below in Chrome, and log in as your HACKT28 user. You assigned HACKT28 the appropriate rights for this in an earlier lesson.

```
URL: https://vhcalhdbdb.dummy.nodomain:4302/sap/bc/ina/service/v2/GetServerInfo

Returned: {"Messages":[{"Number":42001,"Type":2,"Text":"InformationAccess Service GetServerInfo is not available. Install the SAP HANA EPM-MDS plugin."}]}
```

If you get the above message returned then please proceed to the next step as you need to download and install the HANA EPM-MDS plugin.

If the above message is not returned, and you do in fact get a whole bunch of server info back, then please proceed to the later step [Configuring Cross Origin Resource Sharing, CORS](#cors).

You have now completed the step "Checking to see if the SAP HANA EPM-MDS Plugin is Already Installed". 

[Go Back Up to the List of Steps](#steps)

### <a name="winscp"></a> Connecting WinSCP to the S/4HANA Appliance's Linux File System

This step will involve using WinSCP which was downloaded and installed in the [Prerequisites](../exercises/preReqs.md). It will be used to transfer the EPM-MDS plugin from the Windows desktop client to the S/4HANA machine's file system.

* Open up WinSCP and enter the following information into the main dialogue.

```
Host Name: vhcalhdbdb.dummy.nodomain
User Name: root
```

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="../images/winscp1.jpg">

* Press the "Advanced" button.
* Click on "Authentication".

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="../images/winscp2.jpg">

* Press the browse button for the "Private key file" and navigate to where you stored your pem file in the Prerequisites.
* In the file type select "All Private Key Files".

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="../images/winscp3.jpg">

* Select your pem file and press Open.
* Press OK to convert the Open SSH Private Key to a Putty (ppk) format.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="../images/winscp4.jpg">

* If you created a password for your .pem file when you created your appliance in CAL.SAP.com then enter that password and press OK.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="../images/winscp5.jpg"> 

* Press the Save button to save the ppk file to the same directory as your original pem file.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="../images/winscp6.jpg">

* You should get a successful message. Press the OK button to close this message and then press the OK button to close the Advanced Site settings dialogue.
* In the main WinSCP dialogue press the Save button and then the OK button to accept the default name.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="../images/winscp7.jpg">

* Press the "Login" button and then press "Yes" to ignore any warning about connecting to an unknown server.
* If applicable, enter the password you used earlier for your pem file, and then press OK. You should now be connected to the file system of the Linux machine hosting your S/4HANA system.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="../images/winscp8.jpg">

You have now completed the step "Connecting WinSCP to the S/4HANA Appliance's Linux File System".

[Go Back Up to the List of Steps](#steps)

### <a name="epmmds"></a> Downloading the SAP HANA EPM-MDS Plugin

The next step will be to download the EPM-MDS plugin which, as mentioned earlier, will facilitate a connection between the SAP Analytics Cloud and SAP HANA Calculation Views. 

* To download the plugin go to [Support.SAP.com](https://launchpad.support.sap.com/#/softwarecenter/search/SAP%2520HANA%2520EPM-MDS) and then you should see results for SAP HANA EPM-MDS.
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="../images/epmmds1.jpg">

* Select SAP HANA EPM-MDS 1.0 and you should see a cornucopia of download options. In this case you do not want to download the latest release as they are geared to a specific release of HANA.

* To get your HANA version, one way is to go to your Eclipse IDE and in the SAP HANA Development Perspective open up a SQL Console as your HACKT28 user. Run the following SQL code.

```
SELECT version FROM m_database;
```

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="../images/epmmds2.jpg">

* Using the example above the plugin should be for HANA 2.0 Rev 32.0. Note that there may be several downloads (different releases) for your HANA Revision. You should be able to use the latest one as long as you match the version and revision of your HANA system.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="../images/epmmds3.jpg">

* Download the appropriate plugin version and ensure that the file (.sar) is in the same directory where you created your "SAPCAR_e.BAT" file. This batch file was used when you worked on the Smart Data Access workflows.
* Double click on the .sar file and you should have an extracted folder in your "sapcar_out" folder.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="../images/epmmds4.jpg">

* Go back to your WinSCP tool and then navigate in the left panel to where you extracted your .sar file. Navigate in the right panel to the "root > usr > tmp" folder (you may need to go up one folder first) where you might see some other HANA addons or updates.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="../images/epmmds5.jpg">

* Drag the entire SAP_HANA_EPM-MDS folder over to the "tmp" folder. 
* Right click on the folder in the "usr > tmp" directory and choose properties.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="../images/winscp9.jpg">

* Ensure that you change the properties similar to the following.
```
Group: sapsys [####]
Owner: hdbadm [####]

Check "Set group, owner and permissions recursively". 
```

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="../images/winscp9b.jpg">

* Press OK to close the Properties dialogue.

Note that there are of course other ways to get components and updates over to your HANA system and extract them. This was hopefully the easiest way given that you are using an S/4HANA trial appliance environment.

You have now completed the step "Downloading the SAP HANA EPM-MDS Plugin".

[Go Back Up to the List of Steps](#steps)

### <a name="epmmdsinst"></a> Installing the SAP HANA EPM-MDS Plugin

In this step you will use the HANA Lifecycle Manager (LCM) to install the EPM-MDS plugin you copied to your Linux file system earlier.

* On your Windows desktop copy the following URL into a Chrome browser window.

```
URL: https://vhcalhdbdb.dummy.nodomain:1129/lmsl/HDBLCM/HDB/index.html#

User: hdbadm (a user with the necessary rights for HANA updates, installations, service restarts, etc.)
Password: the main password you used when the S/4HANA trial appliance was created
```

* You should get a "Your connection is not private" warning. Click on the "Advanced" button and then on "Proceed to vhcalhdbdb.dummy.nodomain (unsafe)". 

* Enter the user and password combo from the code block above.

* Click on the tile named "Install or Update Additional Components.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="../images/epmmdsinst1.jpg">

* Click on the "Add Software Components" button.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="../images/epmmdsinst2.jpg">

* Navigate to the "/usr/tmp/SAP_HANA_EPM-MDS" or the directory where you copied the EPM-MDS folder and contents.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="../images/epmmdsinst3.jpg">

* Press OK to close this dialogue and then press the "Add" button.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="../images/epmmdsinst4.jpg">

* You should see that the EPM-MDS component is recognized.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="../images/epmmdsinst5.jpg">

* Press Next and then check "Install SAP HANA EPM-MDS" and press Next.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="../images/epmmdsinst6.jpg">

* Enter the HDBADM user password (same one as before) and press Next again.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="../images/epmmdsinst7.jpg">

* Note the warning "During update the SAP HANA Database System will be restarted" and then press the "Update" button.
* You should see a progress screen similar to below. If not, please go back to the WinSCP steps and ensure that you set the permissions for the folder as required.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="../images/epmmdsinst8.jpg">

* After several minutes you should see a screen like the one below. This installation was successful and all of the HANA services have been restarted.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="../images/epmmdsinst9.jpg">

* If you now go back to the following URL, logging in as the HACKT28 user, you should see a full server info page.

```
https://vhcalhdbdb.dummy.nodomain:4302/sap/bc/ina/service/v2/GetServerInfo
```

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="../images/epmmdsinst9b.jpg">

You have now completed the step "Installing the SAP HANA EPM-MDS Plugin".

[Go Back Up to the List of Steps](#steps)


### <a name="cors"></a> Configuring Cross Origin Resource Sharing, CORS

When the HACKT28 user was created certain rights were granted so that user can connect to an admin tool and make changes to the HANA Info Access (InA) service. Cross Origin Resource Sharing (CORS) changes need to be done so that the SAP Analytics Cloud has access to HANA resources such as Calculation Views.

* Open the following URL in the Windows client browser and log in as the HACKT28 user. 

```
URL: http://vhcalhdbdb.dummy.nodomain:8002/sap/hana/xs/admin/#/package/sap.bc.ina.service.v2
User: hackt28
```

* Click on CORS. Note that this has not been configured. 

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="../images/cors1a.jpg">

* You will not be using this tool for this exercise but will be using a script in a SQL Console for convenience. 

* Before moving on to the next step, press the Reset button in the lower right of this admin page and then press the OK button. Please don't close this tool yet as you'll want to check it again in a bit. 

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="../images/cors1b_reset.jpg">

* Go to your Eclipse IDE and in the SAP HANA Development perspective open up a SQL Console for the HACKT28 user. Copy in the code from the block below.

* NOTE: You will need to change the "XXX.XXX" in "XXX.XXX.sapanalytics.cloud" to your SAC account and tenant location. After making the change Execute (F8) the code.

```
UPDATE "_SYS_XS"."RUNTIME_CONFIGURATION" 
SET "CONFIGURATION" = ' {"cors":{
	"enabled":true,
	"allowOrigin":["https://XXX.XXX.sapanalytics.cloud"],
	"exposeHeaders":["x-csrf-token"],
	"allowHeaders":["accept-language","x-sap-cid","x-request-with","x-csrf-token","content-type","authorization","accept"],
	"allowMethods":["GET","HEAD","POST","OPTIONS"],
	"maxAge":3600}
}' 
WHERE "PACKAGE_ID" = 'sap.bc.ina.service.v2';
```

* You should get a Statement that the CORS configuration was updated.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="../images/cors2a.jpg">

* Go back to the web based admin tool you had opened earlier and reload the page and click on CORS again. You should see that CORS is enabled and that the required headers and methods have been allowed.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="../images/cors3a.jpg">

* If you want to find out more about setting up CORS and using the web based tool please go to [help.SAP.com](https://help.sap.com/viewer/search?q=Live%20Data%20Connection%20to%20SAP%20HANA%20Using%20a%20Direct%20Connection%20and%20SSO) with a search on "Live Data Connection to SAP HANA Using a Direct Connection and SSO". 

You have now completed the step "Configuring Cross Origin Resource Sharing, CORS" and are done with the whole task of "Setup of the SAP HANA System for Resource Sharing". 

Your next task is to configure the SAP HANA system so that resources like Calculation Views can be consumed on the SAP Analytics Cloud. 

[Go to Task 7: Creation of Direct Connection to HANA and Analytics in SAP Analytics Cloud](sacAnalytics.md)

[Go Back to the Main Page](../demoHowTo.md)

[Go Back Up to the List of Steps](#steps)
