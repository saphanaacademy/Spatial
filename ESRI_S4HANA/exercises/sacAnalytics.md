<table width=100% border=>
<tr><td colspan=2><h1>How to Extend S/4HANA with HANA Spatial and SAC</h1></td></tr>
<tr><td><h3>Creation of Direct Connection to HANA and Analytics in SAP Analytics Cloud</h3></td><td width=60%></br>&nbsp;Task #7, SAP Analytics Cloud</p></td></tr>
</table>

## Description

In the next steps you will set up a connection between your SAP HANA database and the SAP Analytics Cloud. Afterwards you will work in SAC to create analytics based on live data from that connection.

<img src="../images/XXXXXX.jpg">

## Prerequisites

You should have completed all of the exercise [Prerequisites](../exercises/preReqs.md). You should have also completed [Task 6: Setup of the SAP HANA System for Resource Sharing](hdbCORS.md) using WinSCP and the Eclipse IDE.

## <a name="steps"></a> Steps

Now that the HANA resources (Calculation Views etc.) have been made available by setting up Cross Origin Resource Sharing (CORS) you can make a Connection in SAC to the HANA database on your trial system. This will be a "Direct" connection using the HACKT28 technical user and will be on live data. 

Afterwards you will create a model based on the combined S/4HANA and census data. A Location Dimension will also be added to the model so that a map can be added to your analytic story. 

1. [Creating a Live Direct Data Connection to SAP HANA](#saccon)
1. [Troubleshooting a Connection Error from SAC to HANA](#sacconts)
1. [Creating a SAC Data Model with a Location Dimension](#sacmod)

### <a name="saccon"></a> Creating a Live Direct Data Connection to SAP HANA

In this exercise, you will create a Direct Connection between your HANA database and SAC. This is possible as in the last task you enabled Cross Origin Resource Sharing (CORS) in your HANA system.

* Log into your SAP Analytics Cloud (SAC) tenant (using Chrome as currently it's the only fully supported browser for SAC) and press the "Main Menu" button and choose the "Connection" option.

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

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="../images/sac03a.jpg">

* Press the OK button. Hopefully all is ok with your connection and you will see a new SAC Connection in your list.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="../images/sacmod01.jpg">

If you do not see an error and do have a new successful connection, then please skip the next step and go to [Creating a SAC Data Model with a Location Dimension.](#sacmod)  

If you do get an error message it most likely asking you to check your CORS settings or an error mentioning SSL and your credentials. In this case you will want to follow the troubleshooting steps below.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="../images/sac04.jpg">

### <a name="sacconts"></a> Troubleshooting a Connection Error from SAC to HANA

This step is only necessary if you get an error when trying to connect to your HANA system from SAC. Please note that after testing, the later releases of the S/4HANA trial (e.g. >= 1809 U32) seem to have less connection issues than previous versions such as the 1709 versions. Later versions of Chrome seem to work better as well.

* In the error that you got, there is a link to open up a "Troubleshoot" page.

* The help page mentions a certificate issue. If you are using an S/4HANA trial then it will have self-signed certificates and you've probably already seen some warnings whilst using some of the SAP HANA tools in Chrome.

* One additional point (at the time that this exercise was written, January 4, 2019 at 1:56 PM, PST) is that you don't get an option to ignore the certificate warnings in the SAC connection like you do in the HANA web based tools you've been using.

* Here are some things that you can do to try to resolve the issue:
  - Update your Chrome browser by going to the "Customize and Control Chrome" menu (the 3 vertical dots in the top right) and choose Help > About Google Chrome. Try creating the Connection in SAC again.
  - Press the Windows button in the lower left of your Windows Desktop client and type in "Internet Options". Go to the Security tab > Trusted Sites > Sites and make sure your host name is added: "https://vhcalhdbdb.dummy.nodomain". Try creating the Connection in SAC again.
  - Close Chrome and then go to the Windows button and type Run and then enter "chrome -–ignore-certificate-errors". Try creating the Connection in SAC again.
  - As a last resort (and, please, this is only for those using a trial appliance) use a brute force method and reboot your entire S/4HANA trial system in CAL. Try creating the Connection in SAC again. This has worked as a last resort on 1709 & 1809 S/4HANA trial systems.

[Go Back Up to the List of Steps](#steps)

### <a name="sacmod"></a> Creating a SAC Data Model with a Location Dimension

In this step we will create a Model using the Calculation View that has the combined data in your HANA system. You will also add a Location Dimension off of the second view you created on the geo-coded data. You should now have a Live, Direct connection to your HANA system to make this possible.

* Press the Main Menu / hamburger button and choose Create and then Model.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="../images/mod02.jpg">



### <a name="######"></a> ######



You have now completed the step "######" and are done with the whole task of "Creation of Direct Connection to HANA and Analytics in SAP Analytics Cloud". 

You have also completed the entire exercise...congratulations!

[Go Back to the Main Page](../demoHowTo.md)

[Go Back Up to the List of Steps](#steps)
