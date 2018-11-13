<table width=100% border=>
<tr><td colspan=2><h1>Exercise - Extending S/4HANA with ESRI Spatial Data</h1></td></tr>
<tr><td width=40%><h3>SAP Spatial</h3></td><td width=60%><h3>&nbsp;Difficulty Level: Intermediate</h3></td></tr>
</table>


## Description
In this exercise, you’ll learn how to integrate S/4HANA and ESRI GIS data at the data level. This integrated data will be consumed in SAP Analytics Cloud.

<img src="images/s4HpEsriDemoArch02.jpg">    

* In S/4HANA CDS views are created to combine customer sales, product, and location information
* 
* The ABAP connector is activated in the Data Provisioning Agent is used enabling the ABAP Connector to S4
* In HANA virtual tables of the S/4HANA data are created
* In HANA the virtual tables from the S/4HANA data are combined with spatial tables in calculation views for consumption






For further reading on HANA Spatial and ESRI, click link below.

<http://www.sap.com>

## Target group

* Developers
* People interested in learning about S/4HANA extension and ESRI data  


## Goal

XXXXXX


## Prerequisites
  
Here below are prerequisites for this exercise.

* dddddddd


## Steps

1. [Creation of CDS Views in S/4HANA](#cdsview1)

An S/4HANA user must be available that has the appropriate roles to access sales data and create CDS views. A technical user is also required to create a connection from HANA to the S/4HANA system via Smart Data Access.

Downloads and instructions for ABAP and HANA tools for Eclipse
	https://tools.hana.ondemand.com/

Business Roles for S/4HANA User Include 
* SAP_BC_SEFS_ADMIN
* SAP_BC_SES_ADMIN
* SAP_BR_BILLING_CLERK
* SAP_BR_BUPA_MASTER_SPECIALIST
* SAP_BR_CREDIT_CONTROLLER
* SAP_BR_EMPLOYEE
* SAP_BR_INTERNAL_SALES_REP
* SAP_BR_INTRASTAT_SPECIALIST
* SAP_BR_ORDER_FULFILLMNT_MNGR
* SAP_BR_ORDER_FULFILLMNT_SPCLST
* SAP_BR_PRICING_SPECIALIST
* SAP_BR_PRODMASTER_SPECIALIST
* SAP_BR_PRODN_SUPERVISOR_RPTV
* SAP_BR_RECEIVING_SPECIALIST
* SAP_BR_RETURNS_REFUND_CLERK
* SAP_BR_SALES_MANAGER
* SAP_BR_SALES_PROCESS_MANAGER
* SAP_BR_SET_CLERK
* SAP_BR_SHIPPING_SPECIALIST
* SAP_BR_WAREHOUSE_CLERK


### <a name="cdsview1"></a> Creation of CDS Views in S/4HANA
	
```
@AbapCatalog.sqlViewName: 'ZXSHCSLSORDITFSZ'
@AbapCatalog.compiler.compareFilter: true
@AccessControl.authorizationCheck: #NOT_REQUIRED
@ClientHandling.algorithm: #SESSION_VARIABLE
@EndUserText.label: 'Z Copy Sales Order Item'
@VDM.viewType: #CONSUMPTION

define view ZXSH_C_SALESORDERITEMFSZ as select from C_Salesorderitemfs
left outer join I_Customer
    on C_Salesorderitemfs.ShipToParty = I_Customer.Customer
left outer join I_Address
    on I_Customer.AddressID = I_Address.AddressID
{
    Customer,
    CustomerName,
    SalesOrder,
    RequestedDeliveryDate,
    SalesOrderItem,
    SalesOrderItemText,
    NetAmount,
    TransactionCurrency,
    RequestedQuantity,
    I_Address.AddressID,
    I_Address.AddressTimeZone,
    I_Address.CityName,
    I_Address.District,
    I_Address.Region,
    I_Address.County,
    I_Address.PostalCode
}
```

```
@AbapCatalog.sqlViewName: 'ZXSHCCUSTOMERGEO'
@ClientHandling.algorithm: #SESSION_VARIABLE
@AbapCatalog.compiler.compareFilter: true
@AccessControl.authorizationCheck: #NOT_REQUIRED
@EndUserText.label: 'customer geo data for location hierarchy'
@VDM.viewType: #CONSUMPTION

define view ZXSH_C_CUSTOMERGEO as select from I_Customer 
inner join I_Address
    on I_Customer.AddressID = I_Address.AddressID
{
   I_Customer.Customer as LHCustomer,
   I_Address.AddressID as LHAddressID, 
   I_Address.AddressTimeZone as LHAddressTimeZone, 
   I_Address.CityName as LHCityName,
   I_Address.District as LHDistrict,
   I_Address.Region as LHRegion,
   I_Address.County as LHCounty,
   I_Address.Country as LHCountry,
   I_Address.PostalCode as LHPostalCode
}
```

	
	

