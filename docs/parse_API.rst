QiStream API calls
==================


The API calls in this section are all used to create and manipulate QiStreams. 
See `QiStreams <https://qi-docs-rst.readthedocs.org/en/latest/Qi_Streams.html>`__ for a list of supported QiTypes, a discussion of compound indexes, and general information about QiTypes. 

QiStream management via the Qi Client Libraries is performed through the ``IQiMetadataService`` 
interface, which you access using the ``QiService.GetMetadataService( )`` helper.

***********************

``GetStreamAsync()``
--------------------

Returns a QiStream object from the specified namespace that matches the specified namespace and streamId.

**Syntax**


::

    Task<QiStream> GetStreamAsync (string streamId);

*Http*

::

    GET Qi/{tenantId}/{namespaceId}/Streams/{streamId}

**Parameters**

``string tenantId``
  The tenant identifier for the request
``string namespaceId``
  The namespace identifier for the request
``string streamId``
  The Id of the stream to retrieve


**Returns**
  A QiStream object for the specified streamId and namespace

Security
  Allowed by administrator and user accounts


***********************
