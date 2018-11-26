<table width=100% border=>
<tr><td colspan=2><h1>Creating Demo ABAP CDS Views in S/4HANA</h1></td></tr>
<tr><td><h3>Creation of EPSG (SRID 3857) Spatial System and Transform of Spatial Data</h3></td><td width=60%></br>&nbsp;Task #1</p></td></tr>
</table>

XXXXXX need steps and video links etc.	

## Description

In the next steps we will first create a Spatial Reference System in our HANA database. This system will be EPSG / 3857 and is a requirement to use the data later ESRI Arc GIS. We will also alter an existing table in our sample HANA data so that it has a column with spatial data transformed to SRID 3857.


## Prerequisites

You should have an S/4HANA fully activated trial appliance set up. This appliance will have a Windows client, accessible by Remote Desktop, with the Eclipse IDE with SAP HANA tools installed. 

You might want to have some familiarity with ABAP CDS views in S/4HANA but that is not a big requirement. You don't necessarily have to create your own CDS views from the ground up as you might just wish to slightly modify / extend existing CDS views.

If you want to find out more about creating your own virtual models in CDS please see [the HANA Academy playlist on ABAP CDS here](https://www.youtube.com/playlist?list=PLkzo92owKnVxO-jWmOWugBv_9WQiq8wLc). Please note that these videos were created using an earlier S/4HANA trial system on version 1510 so some workflows might be slightly different looking, but the concepts should be the same.




## Steps

## <a name="steps"></a> Steps

1. [Creation of CDS View with Customer Sales, Products, and Location in S/4HANA](#cdsview1)
1. [Creation of CDS View with Customer Location Data in S/4HANA](#cdsview2)

### <a name="cdsview1"></a> Creation of CDS View with Customer Sales, Products, and Location

The first CDS view that needs to be created will include sales amounts by customer > location > product. In your Eclipse ABAP project create a new CDS view with the following information.

```
Name = ZXSH_C_SALESORDERITEMFSZ
Description = Public Consumption View, Z Copy Sales Order Item
```

<img src="images/s4HpEsriDemoPics01.jpg">

Copy the following code into the view editor. You can substitute the "SH" in ZXSH to match your namespace.
	
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

[Back to Steps](#steps)


### <a name="cdsview2"></a> Creation of CDS View with Customer Location

The second CDS view that needs to be created will be a customer location hierarchy. This hierarchical data will be used later on in the SAP Analytics Cloud for the mapping component. In your Eclipse ABAP project create a new CDS view with the following information.

```
Name = ZXSH_C_CUSTOMERGEO
Description = Public Consumption View, Customer Location Hierarchy
```

<img src="images/s4HpEsriDemoPics02.jpg">

Copy the following code into the view editor. You can substitute the "SH" in ZXSH to match your namespace.

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
