Parse Devices
==================


The API calls in this section are all used to manage devices. See `Introduction to Parse <https://qi-docs-rst.readthedocs.org/en/latest/parse_intro.html>`__ for more information.


***********************

``GET api/tenants/{tenantId}/devices/count``
--------------------------------------------

Returns the number of devices assigned for a specified tenant.  


**Parameters**

``tenantId``
  A unique Id for the Tenant


**Returns**

Integer count of the number of devices found. 
 
***********************

``GET api/tenants/{tenantId}/devices``
--------------------------------------------

Returns all devices for a tenant. 

**Parameters**

``tenantId``
  Unique ID for the tenant. 

**Returns**

  A list of Device objects found. 

************************

``GET api/tenants/{tenantId}/devices/{deviceId}``
--------------------------------------------

Get a specific device. 

**Parameters**

``tenantId``
 Unique ID for the tenant. 
``deviceId``
  Unique ID for the device. 

**Returns**

  The Device object found.  

***************************

``POST api/tenants/{tenantId}/device``
-------------------------------------

Creates or updates a device. The revocation status of a device may be updated. An expiration time may be specified to generate a new token. If not specified, the default time of 50 years will be used. 

Parameters: 

``tenantId``
  Unique ID for the tenant. 

**Body**

A Device object.  

**Returns**

  A Device object. 

******************************

``POST api/tenants/{tenantId}/devices``
---------------------------------------

Creates or updates multiple devices. The revocation status of devices may be updated. An expiration time may be specified to generate new tokens. If not specified, the default time of 50 years will be used. 

**Parameters**

``tenantId``
  Unique ID for the tenant. 

**Body**
  An array of Device objects. 

**Returns**

An array of Device objects. 

************************************

``DELETE api/tenants/{tenantId}/devices/{deviceId}``
---------------------------------------------------

Deletes a device. 

**Parameters**

``tenantId`` 
  Unique ID for the tenant. 
``deviceId``
  Unique ID for the device. 

********************************
