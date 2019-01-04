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

* Log into your SAP Analytics Cloud (SAC) tenant and press the "Main Menu" button and choose the "Connection" option.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="../images/sac01.jpg">

* Add a new Connection choosing Live Data Connection > SAP HANA.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="../images/sac02.jpg">

* In the New Live Connection dialogue use the following info.

```
Connection Type: Direct
Host: vhcalhdbdb.dummy.nodomain
HTTPS Port: 4302
Authentication Method: User Name and Password
User Name: hackt28
Password: the one that you gave to your HACKT28 user
```

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="../images/sac03.jpg">

* Press the OK button. You should get an error message to check your CORS settings or your credentials. Although these 

You have now completed the step "Creating a Live Direct Data Connection to SAP HANA". 

[Go Back Up to the List of Steps](#steps)




######

* port 443 (& optional 44301) must be opened in firewall

To open a port in the Windows firewall for TCP access
On the Start menu, click Run, type WF.msc, and then click OK.
In the Windows Firewall with Advanced Security, in the left pane, right-click Inbound Rules, and then click New Rulein the action pane (upper right corner).


You have now completed the step "######" and are done with the whole task of "Creation of Direct Connection to HANA and Analytics in SAP Analytics Cloud". 

You have also completed the entire exercise...congratulations!

[Go Back to the Main Page](../demoHowTo.md)

[Go Back Up to the List of Steps](#steps)
