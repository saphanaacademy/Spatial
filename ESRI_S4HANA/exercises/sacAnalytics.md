<table width=100% border=>
<tr><td colspan=2><h1>How to Extend S/4HANA with HANA Spatial and SAC</h1></td></tr>
<tr><td><h3>Creation of Connection and Models and Story in SAP Analytics Cloud</h3></td><td width=60%></br>&nbsp;Task #6, Apache HTTP Server & SAP Analytics Cloud</p></td></tr>
</table>

## Description

In the next steps you will set up a connection between your SAP HANA database and the SAP Analytics Cloud.  

<img src="../images/######.jpg">

## Prerequisites

You should have completed all of the exercise [Prerequisites](../exercises/preReqs.md). You should have also completed [Task 5: Creation of HANA Calculation Views on Integrated Data](hdbViews.md) using the Eclipse IDE.

## <a name="steps"></a> Steps

A connection must be made between your SAP HANA database and the SAP Analytics Cloud. In order to establish the sharing of objects from HANA with SAC, you must do so with either [CORS (Cross-Origin Resource Sharing) or via a reverse proxy.](https://blogs.sap.com/2017/12/29/creating-sap-analytics-cloud-live-connection-to-sap-hana-database-on-sap-cloud-platform/) In this exercise a reverse proxy will be set up and then later a "Path" connection will be used in SAC. The reverse proxy is used for several reasons including ease of setup and avoiding any self-signed certificate issues (as you're using the S/4HANA trial image) and the proxy will allow for a quick additional connection to S/4HANA resources (CDS views) in SAC.

Once the connection between SAC & HANA is established a Model (including a Location Dimension) will be created in SAC as well as a Story which will feature a map.

1. [Setup of Reverse Proxy Server on the Windows Client](#revproxy)
1. [######](#   )


### <a name="revproxy"></a> Setup of Reverse Proxy Server on the Windows Client

```
code block
```

You have now completed the step "Setup of Reverse Proxy Server on the Windows Client".

[Go Back Up to the List of Steps](#steps)




You have now completed the step "######" and are done with the whole task of "Creation of Connection and Models and Story in SAP Analytics Cloud". You have also completed the entire exercise...congratulations!

[Go Back to the Main Page](../demoHowTo.md)

[Go Back Up to the List of Steps](#steps)
