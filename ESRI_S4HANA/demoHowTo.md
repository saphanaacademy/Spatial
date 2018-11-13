<table width=100% border=>
<tr><td colspan=2><h1>Demo - Extending S4HANA with ESRI Spatial Data</h1></td></tr>
<tr><td><h3>SAP Spatial</h3></td><td><h1><img src="images/clock.png"> &nbsp;30 min</h1></td></tr>
</table>


## Description
In this exercise, you’ll learn how 

* XXXXXX

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

1. [Create a project with the Neo archetype through the terminal](#cdsview1)


### <a name="cdsview1"></a> Create a cds view
XXXXXX.

	
	
	cd application/target
	


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

