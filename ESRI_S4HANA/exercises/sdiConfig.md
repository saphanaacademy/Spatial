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

You will need first install and configure the Data Provisioning Agent on the trial appliance's Windows client and then work in the Eclipse HANA Development Perspective to activate and configure the Smart Data Access components.

1. [Installing the Data Provisioning Agent](#sdidpa)

1. [Activating the Data Provisioning Server in HANA](#sdihdps)

1. [Creating a Remote Source and Virtual Tables](#sdarsvt)


### <a name="sdidpa"></a> Installing the Data Provisioning Agent

In order to connect your SAP HANA system to your S/4HANA system you need to first set up the Data Provisioning Agent.  

* Go to [tools.hana.ondemand](https://tools.hana.ondemand.com) where you can find a lot of the tools you'll need for SAP development > then click on the "Cloud Integration" tab > and scroll down to the "Data Integration Downloads" section.

* If you are using the S/4HANA trial then you will want to download the SDI Data Provisioning Agent for Windows. The download will take several minutes to complete.

* Note that this download is only for dev/testing purposes. Please contact your SAP representative should you need to license this product on a production system.

<img src="../images/XXXXXX.jpg">

* The Data Provisioning Agent is a .SAR file so you will need to download sapcar.exe. Go to the SAP 

1)	Copy sapcar.exe to your system directory
2)	Create a file SAPCAR_e.BAT with the following contents

SAPCAR.EXE -xvf %1, -R ".\sapcar_out"
Pause

3)	Save the batch file to the same directory as sapcar.exe
4)	Right click on any sar file and change the file Properties so that it and other sars (not affiliated with the respiratory syndrome) point to the .bat file

https://blogs.sap.com/2012/04/12/easier-way-to-extract-sar-and-car-files-with-sapcar-under-windows/


https://help.sap.com/viewer/p/HANA_SMART_DATA_INTEGRATION > in the Intallation and Upgrade section > click on the Installation and Configuration Guide

SDI ABAP Adapter https://www.youtube.com/watch?v=ZNr7xc3FHm0&list=PLkzo92owKnVwQ_preA3cxlQjn_v3W0Eh5&index=52&t=0s


### <a name="sdihdps"></a> Activating the Data Provisioning Server in HANA


### <a name="sdarsvt"></a> Creating a Remote Source and Virtual Tables





[Go to Task 4: Setup of Sample Database for the SAP HANA System](hdbData.md)

[Go Back to the Main Page](../demoHowTo.md)

[Back to Steps](#steps)
