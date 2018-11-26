<table width=100% border=>
<tr><td colspan=2><h1>How to Extend S/4HANA with HANA Spatial and SAC&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</h1></td></tr>
<tr><td><h3>More Info on the S/4HANA Trial</h3></td><td width=60%></br>&nbsp;Development Environment</p></td></tr>
</table>

## Helpful hints to get you started

Amazon Web Services and the 30-Day trial:

When should I start the 30-day trial for S/4 HANA?

Since the 30-day clock is based on the calendar and not the usage, you should not start your instance until you are ready to start the course. Please note that the AWS instance make take some time to create, so you might want to allow for that in your planning.
How long does it take to create the Amazon instance?

It can take up to 2 hours for AWS to create, validate and instantiate your instance for the first time. After that, it is only a few minutes to Activate your instance if you have suspended it.
How much does it cost to use AWS for this course?

The AWS infrastructure will run about $3.40 per hour in the US. If you kept this instance active for an entire month, it would be under $200. Please remember that the S/4 HANA license is only available for 30 days in the trial version, so if you are setting up the account just for this course, you will want to delete the AWS instance at the end of the course to stop any future billing.
What instance do I choose from the AWS console?

You actually only need to set up an account with the credit card for billing. Then, you will go to your Account settings and use the Security Credentials option to create the necessary keys to connect to AWS from within the SAP Cloud Appliance Library.  The S/4 HANA instance in CAL is pre-configured to select and create the appropriate back end servers.
Is the AWS billing for every hour or just those used?

If you suspend your instance through the SAP Cloud Appliance Library (CAL) console, you will reduce your billing costs to only those associated with storage (which is minimal). The main portion of the billing is for server “up time” and thus is deterred by managing the instance active times.
The Status of my instance shows “Undefined.”  What does that mean?

On occasion one of the servers included in the instance may not be properly initialized in AWS. This will show in a variety of errors, but is most easily spotted by having a status that does not turn to Active.  You can terminate this instance and request another instance to be created.  Note that it might take a few minutes for the terminated instance to disappear from the console and allow you to create another Trial instance in its place.
Working with the SAP Cloud Appliance Library (CAL) Console:

My CAL console logged off while I was waiting for the AWS instance to be created. What should I do?

You simply need to log on again. The server creation process is happening at Amazon.  The CAL console is just opening a window to the admin console for user interaction.
I want to get back into my instance after I suspended it. How do I connect?

First step is to Activate your instance from the Cloud Appliance Library (CAL) console.
Click on the instance to see the INFO details of that instance.
Copy the Windows External IP Address from the list of IP Addresses, and copy that into a Remote Desktop Connection.
Once the instance has fully activated in CAL, you will be able to use this Remote Desktop Connection to access the Windows server in your S/4 HANA landscape. All the work in this video set happens on this server.
If you disconnect and suspend in CAL, you will get a new IP address the next time you Activate the instance.
Working through the exercises, here are some helpful tips:

I am connecting to CAL with a Mac, is there anything different I need to do?

Please make sure you are using the Microsoft Remote Desktop utility available from the AppStore. 
When I open Eclipse on the image, it already has a connection to S4HANA using the BPINST user. Do I still need to create a new connection?

For the steps covered in our videos, we will be using a new connection for a new user we will create. Following along with the videos ensures that later steps will work as described.
I cannot log into SAP Logon or Fiori Launchpad with the BPINST user.

Please make sure you are using the proper case for the password: Welcome1
When I try to Add Selected Service to my local package, I do not see the new service I created in my view using the Odata Publish annotation. Why?

When copying the service name from the popup message, make sure you do not have any extra spaces after the name.
I do not see the Purchasing Analytics group in my Fiori Launchpad. Why?

Fiori Launchpad access is driven by user roles and profiles. It is possible that you did not add the relevant role to be able to see this group.  Make sure you have assigned SAP_BR_BUYER to your user you created to view the Fiori tiles.
In the video you show using Eclipse to “Create Connection with Different User” but I don’t see that option when I do a right click on the system.  Why?

Make sure that you log in to the HDB system with your Windows password for this image first, then you should get the full context menu available.
General Notes for Troubleshooting:  

Please be careful with your case. Many of the scripts and services are case-sensitive.
Please take note of any on-screen annotations added to the videos as we have noted a few changes in syntax or menu options released with the latest 1610 image build since the videos were created.
Please make sure to read the notes in GitHub as this will contain any new caveats, updates or resolutions that may arise.
Links and URLs that are helpful:

Can you provide the links you used in the videos?

GitHub Repository: https://github.com/saphanaacademy/s4hana
Week One: S4HANA_Hive_VIRTUAL_LAB.txt
Week Two and Three: s4ExtendingWithExternalData.txt
Previous CDS Lab: s4hana_CDS_creating_a_sample_virtual_data_model
Sample CSV file: AirportWebservices.csv
Launchpad: /sap/bc/ui5_ui5/ui2/ushell/shells/abap/FioriLaunchpad.html
Launchpad Designer: /sap/bc/ui5_ui5/sap/arsrvc_upb_admn/main.html?sap-client=100
Are there other sources of documentation that might be helpful to me?

SAP S/4HANA 1610 trial landing page
Link to CAL documentation
Link to CAL FAQ documents
Link to Getting Started Guide for the S/4 HANA 1610 image in CAL
Link to Odata documentation
Reference Blog for S/4 HANA 1610 
Previous SAP HANA Academy Lab: Introduction to CDS Views
Link to ABAP – CDS Help > click on ABAP - CDS Syntax at the bottom for more info > click on ABAP - CDS Annotations > Context for Annotations, choose subject of interest in the context...note these pages are not that fast
