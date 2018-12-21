<table width=100% border=>
<tr><td colspan=2><h1>How to Extend S/4HANA with HANA Spatial and SAC</h1></td></tr>
<tr><td><h3>Creation of Connection and Models and Story in SAP Analytics Cloud</h3></td><td width=60%></br>&nbsp;Task #6, Apache HTTP Server & SAP Analytics Cloud</p></td></tr>
</table>

## Description

In the next steps you will set up a connection between your SAP HANA database and the SAP Analytics Cloud. Afterwards you will work in SAC to create analytics based on live data from that connection.

<img src="../images/######.jpg">

## Prerequisites

You should have completed all of the exercise [Prerequisites](../exercises/preReqs.md). You should have also completed [Task 5: Creation of HANA Calculation Views on Integrated Data](hdbViews.md) using the Eclipse IDE.

## <a name="steps"></a> Steps

A connection must be made between your SAP HANA database and the SAP Analytics Cloud. In order to establish the sharing of objects from HANA with SAC, you must do so with either [CORS (Cross-Origin Resource Sharing) or via a reverse proxy.](https://blogs.sap.com/2017/12/29/creating-sap-analytics-cloud-live-connection-to-sap-hana-database-on-sap-cloud-platform/) In this exercise a reverse proxy will be set up and then later a "Path" connection will be used in SAC. The reverse proxy is used for several reasons including ease of setup and avoiding any self-signed certificate issues (as you're using the S/4HANA trial image) and the proxy will allow for a quick additional connection to S/4HANA resources (CDS views) in SAC.

Once the connection between SAC & HANA is established a Model, including a Location Dimension, will be created in SAC as well as a Story which will feature a map.

1. [Setup of Reverse Proxy Server on the Windows Client](#revproxy)
1. [######](#   )

### <a name="revproxy"></a> Setup of Reverse Proxy Server on the Windows Client

The first step will involve downloading and configuring Apache HTTP Server to be used as a reverse proxy. Please note that the following steps should not be done on a production environment as these are done knowing that a trial S/4HANA environment is used. If you are looking for info on how to set up the connection for a production environmnet then please consult [help.sap.com with a search on "SAP Analytics Cloud Live Data Connections to SAP HANA".](https://help.sap.com/viewer/search?q=SAP%20Analytics%20Cloud%20Live%20Data%20Connections%20to%20SAP%20HANA)

* On the Windows client of your S/4HANA system do a browser search for "apache http server download" and in the "Download - The Apache HTTP Server Project" result click on the Microsoft Windows link.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="../images/revprox01.jpg">

* Choose the "Apache Lounge" as the distributor option for the binary installer. 

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="../images/revprox02.jpg">

* Choose the latest Win64 option to download.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="../images/revprox03.jpg">

* Go to your downloads folder and extract the "httpd-2..." archive to a folder of "d:\apache" with the "Show extracted files..." option.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="../images/revprox04.jpg">

* In the "D:\apache\Apache24\conf" directory choose to open the "http.conf" file with Notepad.
* Find the ServerRoot variable and change it so that it uses your install path, e.g. d:/apache/Apache24".

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="../images/revprox05.jpg">

* You will need the external IP address of the Windows client machine that you are using for your Remote Desktop.
* Go back to the http.conf file. Find the ServerName variable, and uncomment the line if necessary. Change the value to the external IP address you got from CAL.SAP.com.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="../images/revprox06.jpg">

######

port 443 (& optional 44301) must be opened in firewall

To open a port in the Windows firewall for TCP access
On the Start menu, click Run, type WF.msc, and then click OK.
In the Windows Firewall with Advanced Security, in the left pane, right-click Inbound Rules, and then click New Rulein the action pane (upper right corner).

# test local https://localhost/s4h/sap/bw/ina/GetServerInfo
# test external https://vhcals4hci.dummy.nodomain/s4h/sap/bw/ina/GetServerInfo


ina config...if necessary???

http://vhcalhdbdb.dummy.nodomain:8002/sap/hana/xs/admin/#/package/sap.bc.ina.service



######

```
code block
```

You have now completed the step "Setup of Reverse Proxy Server on the Windows Client".

[Go Back Up to the List of Steps](#steps)

You have now completed the step "######" and are done with the whole task of "Creation of Connection and Models and Story in SAP Analytics Cloud". You have also completed the entire exercise...congratulations!

[Go Back to the Main Page](../demoHowTo.md)

[Go Back Up to the List of Steps](#steps)
