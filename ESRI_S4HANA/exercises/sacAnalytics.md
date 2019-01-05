<table width=100% border=>
<tr><td colspan=2><h1>How to Extend S/4HANA with HANA Spatial and SAC</h1></td></tr>
<tr><td><h3>Creation of Direct Connection to HANA and Analytics in SAP Analytics Cloud</h3></td><td width=60%></br>&nbsp;Task #7, SAP Analytics Cloud</p></td></tr>
</table>

## Description

In the next steps you will set up a connection between your SAP HANA database and the SAP Analytics Cloud. Afterwards you will work in SAC to create analytics based on live data from that connection.

<img src="../images/######.jpg">

## Prerequisites

You should have completed all of the exercise [Prerequisites](../exercises/preReqs.md). You should have also completed [Task 6: Setup of the SAP HANA System for Resource Sharing](hdbCORS.md) using WinSCP and the Eclipse IDE.

## <a name="steps"></a> Steps

XXXXXX

1. [Creating a Live Direct Data Connection to SAP HANA](#xxxxxx)

### <a name="xxxxxx"></a> XXXXXX

In this exercise, you will create a Direct Connection between your HANA database and SAC. This is possible as in the last task you enabled Cross Origin Resource Sharing (CORS) in your HANA system.

* First you will need to get the external IP address for your SAP S/4HANA & SAP HANA DB in your trial appliance.
* Log into [CAL.SAP.com](https://cal.sap.com) > go to Instances > click on your S/4HANA trial appliance > click on "Info".
* To get the external IP address you'll probably have to click on "More" and find "SAP S/4HANA...External IP Address".

* Log into your SAP Analytics Cloud (SAC) tenant (using Chrome) and press the "Main Menu" button and choose the "Connection" option.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="../images/sac01.jpg">

* Add a new Connection choosing Live Data Connection > SAP HANA.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="../images/sac02.jpg">

* In the New Live Connection dialogue use the following info.

```
Connection Type: Direct
Host: the External IP Address for your SAP S/4HANA 1809 & SAP HANA DB (from CAL.SAP.com > Instances > yours > Info > IP Addresses)
HTTPS Port: 4302
Authentication Method: User Name and Password
User Name: hackt28
Password: the one that you gave to your HACKT28 user
```

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="../images/sac03.jpg">

* Press the OK button. You should get an error message to check your CORS settings or your credentials. There is a link to open up a "Troubleshoot" page.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="../images/sac04.jpg">

* The help page mentions a certificate issue. If you are using an S/4HANA trial then it will have self-signed certificates and you've seen some warnings whilst using some of the SAP HANA tools in Chrome. The issue here (at the time that this exercise was written, January 4, 2019 at 1:56 PM, PST) is that you don't get an option to ignore the certificate warnings in the SAC connection.
* Without closing the New Live HANA Connection dialogue, open up a new tab in Chrome. 
* In the new tab put in the URL for getting the server info that you used before but substitute vhcalhdbdb.dummy.nodomain for the external IP address from your S/4HANA machine.

```
URL: https://###.###.###.###:4302/sap/bc/ina/service/v2/GetServerInfo
Name: hackt28
Password: the one that you gave to your HACKT28 user
```

* You should see a "Your connection is not private" warning. Click the "Advanced" button and then click on the "Proceed to..." link.
* There will be a "Not Secure" warning in the top left of the page. Click on that warning.
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="../images/sac04.jpg">





You have now completed the step "Creating a Live Direct Data Connection to SAP HANA". 

[Go Back Up to the List of Steps](#steps)

######

* port 443 (& optional 44301) must be opened in firewall

To open a port in the Windows firewall for TCP access
On the Start menu, click Run, type WF.msc, and then click OK.
In the Windows Firewall with Advanced Security, in the left pane, right-click Inbound Rules, and then click New Rule in the action pane (upper right corner).


You have now completed the step "######" and are done with the whole task of "Creation of Direct Connection to HANA and Analytics in SAP Analytics Cloud". 

You have also completed the entire exercise...congratulations!

[Go Back to the Main Page](../demoHowTo.md)

[Go Back Up to the List of Steps](#steps)
