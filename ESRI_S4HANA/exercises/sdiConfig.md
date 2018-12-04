<table width=100% border=>
<tr><td colspan=2><h1>How to Extend S/4HANA with HANA Spatial and SAC</h1></td></tr>
<tr><td><h3>Setup of Remote Connection and Virtual Tables for S/4HANA</h3></td><td width=60%></br>&nbsp;Task #3, Using Data Provisioning &  Eclipse HANA Development</p></td></tr>
</table>

## Description

A connection needs to be made between the HANA database and the S/4HANA system. Afterwards, data from the ABAP CDS views will be virtualized in the target HANA database.

<img src="../images/XXXXXX.jpg">

## Prerequisites

You should have completed all of the exercise [Prerequisites](../exercises/preReqs.md). You should have also completed [Task 2: Creation of Development User for the SAP HANA System](../exercises/hdbUser.md) using the Eclipse IDE.

## Steps

First you will need to install and configure the Data Provisioning Agent on the trial appliance's Windows client and then work in the Eclipse HANA Development Perspective to activate and configure the Smart Data Access components.

1. [Installing the Data Provisioning Agent](#sdidpa)

1. [Activating the Data Provisioning Server in HANA](#sdihdps)

1. [Creating a Remote Source and Virtual Tables](#sdarsvt)


### <a name="sdidpa"></a> Installing the Data Provisioning Agent

In order to connect your SAP HANA system to your S/4HANA system you need to first set up the Data Provisioning Agent.  

* Go to [tools.hana.ondemand](https://tools.hana.ondemand.com) where you can find a lot of the tools you'll need for SAP development > then click on the "Cloud Integration" tab > and scroll down to the "Data Integration Downloads" section.

* If you are using the S/4HANA trial then you will want to download the SDI Data Provisioning Agent for Windows. The download will take several minutes to complete.

* Note that this download is only for dev/testing purposes. Please contact your SAP representative should you need to license this product on a production system.

* The Data Provisioning Agent is a .SAR archive file so you will need to download sapcar.exe to extract it. Go to [help.sap.com](http://help.sap.com) and search on "sapcar" and you should see a link to "Installing the SAPCAR Utility".

* For an easy way to use sapcar follow the steps below from the blog post [here](https://blogs.sap.com/2012/04/12/easier-way-to-extract-sar-and-car-files-with-sapcar-under-windows/):

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;i)	Save sapcar.exe to your Downloads directory.\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ii)	In Notepad create a file named SAPCAR_e.BAT in the Downloads directory with the following contents.

```
SAPCAR.EXE -xvf %1, -R ".\sapcar_out"
Pause
```

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;iii)	Right click on the sar file and change the Open With dialogue so that all "sar" files point to the .bat file.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="../images/sapcar1.jpg">

* Now double-click on your sapcar.sar file. You should see a new sapcar_out folder and the extracted contents inside. You may have to double-click on the file once more for this to happen.

* In the "HANA_DP_AGENT" folder the .exe that you need to run is the hdbsetup file.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="../images/sapcar2.jpg">

* Click Next to accept the first dialogue options and in the second dialogue use the following information.

```
Agent Unique Name:  DPAgent
Domain\Username:   <your host name>\administrator  
  - where your host name is found via the Command Prompt > hostname
Password:           your Windows administrator logon password 
  - the password you used when you created the S/4HANA trial)
```

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="../images/sdidpa1.jpg">

https://help.sap.com/viewer/p/HANA_SMART_DATA_INTEGRATION > in the Intallation and Upgrade section > click on the Installation and Configuration Guide

SDI ABAP Adapter https://www.youtube.com/watch?v=ZNr7xc3FHm0&list=PLkzo92owKnVwQ_preA3cxlQjn_v3W0Eh5&index=52&t=0s

[Go Back Up to the List of Steps](#steps)

### <a name="sdihdps"></a> Activating the Data Provisioning Server in HANA

[Go Back Up to the List of Steps](#steps)

### <a name="sdarsvt"></a> Creating a Remote Source and Virtual Tables


[Go to Task 4: Setup of Sample Database for the SAP HANA System](hdbData.md)

[Go Back to the Main Page](../demoHowTo.md)

[Go Back Up to the List of Steps](#steps)
