<table width=100% border=>
<tr><td colspan=2><h1>How to Extend S/4HANA with HANA Spatial and SAC</h1></td></tr>
<tr><td><h3>Setup of Remote Connection and Virtual Tables for S/4HANA</h3></td><td width=60%></br>&nbsp;Task #3, Using Data Provisioning &  Eclipse HANA Development</p></td></tr>
</table>

## Description

This includes installing the Data Provisioning Agent, activating HANA's Data Provisioning server, creating Virtual Tables for the ABAP CDS views we created earlier.

<img src="../images/XXXXXX.jpg">

## Prerequisites

## Steps

You will need first install the Data Provisioning Agent from tools.hana.ondemand.com and then register your HANA system. In the HANA Development Perspective in Eclipse you will create the Remote Source and add the Virtual Tables.

1. [Logging into HANA as an Admin User](#hdbadmin)

1. [Creating the Development User with a Script](#hdbdev)

1. [Granting Rights to the Development User's Project](#hdbrepo)


### <a name="hdbadmin"></a> Logging into HANA as an Admin User

In order to connect your SAP HANA system to your S/4HANA system you need to first set up the Data Provisioning Agent.  
https://tools.hana.ondemand.com/ > click on the Cloud Integration tab > scroll down to the Data Integration Downloads section.

* Note that this download is only for dev/testing purposes. Please contact your SAP representative for licensing of this product on a production system.

https://help.sap.com/viewer/p/HANA_SMART_DATA_INTEGRATION > in the Intallation and Upgrade section > click on the Installation and Configuration Guide

SDI ABAP Adapter https://www.youtube.com/watch?v=ZNr7xc3FHm0&list=PLkzo92owKnVwQ_preA3cxlQjn_v3W0Eh5&index=52&t=0s

[Go to Task 4: Setup of Sample Database for the SAP HANA System](hdbData.md)

[Go Back to the Main Page](../demoHowTo.md)

[Back to Steps](#steps)
