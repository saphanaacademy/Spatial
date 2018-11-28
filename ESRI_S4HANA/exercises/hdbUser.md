<table width=100% border=>
<tr><td colspan=2><h1>How to Extend S/4HANA with HANA Spatial and SAC</h1></td></tr>
<tr><td><h3>Creation of Development User for the SAP HANA System</h3></td><td width=60%></br>&nbsp;Task #2, Using Eclipse IDE, HANA Development Perspective</p></td></tr>
</table>



## Description

In the next steps you will create a technical HANA database user that has the rights to create remote connections and tables, import objects, create Calculation Views, etc.


## Prerequisites

You should have completed all of the exercise [Prerequisites](../exercises/preReqs.md). You should have also completed [Task 1: Creation of CDS Views in S/4HANA](../exercises/s4hViews.md) using the Eclipse IDE.

## Steps

You will need to use the HANA Development Perspective in Eclipse as an admin user. This admin user will have the rights to create the new development user that will complete a lot of the upcoming tasks in the HANA environment. 

1. [Logging into HANA as an Admin User](#hdbadmin)

1. [Creating the Development User with a Script](#hdbdev)

1. [Granting Rights to the Developmnent User's Project](#hdbrepo)


### <a name="hdbadmin"></a> Logging into HANA as an Admin User

* In Eclipse click on the Open Perspective shortcut to get the full list of Perspectives. (Perspectives are also accessible through the Window menu > Perspective > Open Perspective > Other.)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="../images/eclpers04.jpg">

* Select the SAP HANA Development Perspective. Note that there are a couple other Perspectives that you could use for the next tasks such as the SAP HANA Administration Console. However you are also going to be creating some HANA Calculation Views so this Perspective is a good catch-all for our HANA related tasks.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="../images/eclpershana2.jpg">

* Now go to the Systems tab.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="../images/eclhdbsystab.jpg">

* You should see an entry for the System user connection to the local HANA system. If not don't worry as a bit further down we'll show you how to create a new connection when the Systems panel is empty.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="../images/eclhdbsystab2.jpg">

* You can close all of the open console windows in Eclipse as well by right-clicking on one and choosing Close All.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="../images/eclhdbsystab3.jpg">

*

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="../images/eclhdbsystab4.jpg">

*

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="../images/eclhdbsystab5.jpg">

*

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="../images/eclhdbsystab6.jpg">

*

```
------------
--
-- hdb user
--
------------

CREATE USER HACKT28 PASSWORD Initial1;
ALTER USER HACKT28 DISABLE PASSWORD LIFETIME;

GRANT CREATE REMOTE SOURCE TO HACKT28;
GRANT ADAPTER ADMIN TO HACKT28;
GRANT AGENT ADMIN TO HACKT28;
GRANT IMPORT TO HACKT28;
GRANT CONTENT_ADMIN TO HACKT28;
GRANT MODELING TO HACKT28;


INSERT INTO _SYS_REPO.PACKAGE_CATALOG(PACKAGE_ID, SRC_SYSTEM, SRC_TENANT, DESCRIPTION, RESPONSIBLE, IS_STRUCTURAL) 
	VALUES ('HACKT28','HDB','','HACKT28','HACKT28',0);
GRANT EXECUTE ON REPOSITORY_REST TO HACKT28;
GRANT EXECUTE ON GRANT_ACTIVATED_ROLE TO HACKT28;
GRANT EXECUTE ON REVOKE_ACTIVATED_ROLE TO HACKT28;
GRANT REPO.READ, REPO.EDIT_NATIVE_OBJECTS, REPO.ACTIVATE_NATIVE_OBJECTS, REPO.MAINTAIN_NATIVE_PACKAGES 
	ON "HACKT28" TO HACKT28;
GRANT REPO.EDIT_IMPORTED_OBJECTS, REPO.ACTIVATE_IMPORTED_OBJECTS, REPO.MAINTAIN_IMPORTED_PACKAGES 
	ON "HACKT28" TO HACKT28;

-- To delete user --
-- DELETE FROM _SYS_REPO.PACKAGE_CATALOG WHERE RESPONSIBLE = 'HACKT28';
-- SELECT TOP 1000 * FROM "_SYS_REPO"."PACKAGE_CATALOG" WHERE PACKAGE_ID = 'HACKT28';
-- DROP USER HACKT28 CASCADE;

```

```

-- run this as HACKT28
GRANT SELECT, INSERT, UPDATE, DELETE, EXECUTE ON SCHEMA HACKT28 to _SYS_REPO WITH GRANT OPTION;

```

[Go Back to the Main Page](../demoHowTo.md)

[Go Back Up to the List of Steps](#steps)
