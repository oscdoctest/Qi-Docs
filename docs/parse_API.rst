Parse API calls
==================


The API calls in this section are all used to ...
See `Parse introduction <https://qi-docs-rst.readthedocs.org/en/latest/parse_intro.html>`__ for an introduction to Parse.

QiStream management via the Qi Client Libraries is performed through the ``IQiMetadataService`` 
interface, which you access using the ``QiService.GetMetadataService( )`` helper.

***********************

``GET api/tenants/{tenantId}/devices/count``
--------------------------------------------

Gets the number of devices for a tenant.  


**Parameters**

``tenantId``
  A unique Id for the Tenant


**Returns**
  Integer count of the number of devices found. 
 

***********************
