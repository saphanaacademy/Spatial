<table width=100% border=>
<tr><td colspan=2><h1>How to Extend S/4HANA with HANA Spatial and SAC</h1></td></tr>
<tr><td><h3>Creation of Development User for the SAP HANA System</h3></td><td width=60%></br>&nbsp;Task #2, Using Eclipse IDE, HANA Development Perspective</p></td></tr>
</table>

XXXXXX need steps and video links etc.	

## Description

In the next steps we will create a technical HANA database user that has the rights to create remote connections and tables, import objects, create Calculation Views, etc.


## Prerequisites

You will need the Eclipse IDE with SAP HANA tools installed. If you are using the S/4HANA trial appliance then this IDE will be set up already on the Windows client.


## Steps

1. In Eclipse, go to the Window menu > Perspective > Open Perspective >  SAP HANA Development Console (if you don't see it in this options list then choose Other > SAP HANA Development.



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
