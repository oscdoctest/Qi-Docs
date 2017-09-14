QiStream API
============

The REST APIs provide programmatic access to read and write Qi data. The APIs in this 
section interact with QiStreams. When working in .NET convenient Qi Client libraries are 
available. The ``IQiMetadataService`` interface, accessed using the ``QiService.GetMetadataService( )`` helper, 
defines the available functions. See `QiStreams <https://qi-docs-rst.readthedocs.org/en/latest/Qi_Streams.html>`__ for general 
QiStream information. 


***********************

``Get Stream``
--------------

Returns the specified stream.


**Request**

::

    GET api/Tenants/{tenantId}/Namespaces/{namespaceId}/Streams/{streamId}


**Parameters**

``string tenantId``
  The tenant identifier
``string namespaceId``
  The namespace identifier
``string typeId``
  The type identifier


**Response**

  The response includes a status code and a response body.
  

**Response body**

  The requested QiStream.

  Sample response body:

::
  
  HTTP/1.1 200
  Content-Type: application/json

  {  
     "Id":"Simple"
     "Name":"Simple"
     "TypeId":"Simple",
  }


**.NET Library**

::

  Task<QiStream> GetStreamAsync(string streamId);


**Security**

  Allowed by administrator accounts


***********************

``Get Streams``
--------------

Returns a list of streams.

If the optional search parameter is specified, the list of streams returned are filtered to match 
the search criteria. If the optional search parameter is not specified, the list includes all streams 
in the Namespace. See `Searching for QiStreams <https://qi-docs-rst.readthedocs.org/en/latest/Searching.html>`__ 
for information about specifying the search parameter.

**Request**

::

    GET	api/Tenants/{tenantId}/Namespaces/{namespaceId}/Streams?query={query}
        &skip={skip}&count={count}




**Parameters**

``string tenantId``
  The tenant identifier
``string namespaceId``
  The namespace identifier
``string query``
  An optional parameter representing a string search. 
  See `Searching for QiStreams <https://qi-docs-rst.readthedocs.org/en/latest/Searching.html>`__ 
  for information about specifying the search parameter.
``int skip``
  An optional parameter representing the zero-based offset of the first QiStream to retrieve. 
  If not specified, a default value of 0 is used.
``int count``
  An optional parameter representing the maximum number of QiStreams to retrieve. 
  If not specified, a default value of 100 is used.


**Response**

  The response includes a status code and a response body.
  

**Response body**

  A collection of zero or more QiStreams.
  
  Sample response body:

::
  
  HTTP/1.1 200
  Content-Type: application/json

   [  
     {  
        "Id":"Simple",
        "TypeId":"Simple"
     },
     {  
        "Id":"Simple with Secondary",
        "TypeId":"Simple",
        "Indexes":[  
           {  
              "QiTypePropertyId":"Measurement"
           }
        ]
     },
     {  
        "Id":"Compound",
        "TypeId":"Compound"
     },
     ...
  ]


**.NET Library**

::

  Task<IEnumerable<QiStream>> GetStreamsAsync(string query = "", int skip = 0, 
      int count = 100);



**Security**

  Allowed for administrator and user accounts

***********************

``Get Stream Type``
-------------------

Returns the type definition that is associated with a given stream.


**Request**

::

    GET api/Tenants/{tenantId}/Namespaces/{namespaceId}/Streams/{streamId}/Type

**Parameters**

``string tenantId``
  The tenant identifier
``string namespaceId``
  The namespace identifier
``string streamId``
  The stream identifier


**Response**

  The response includes a status code and a response body.
  

**Response body**

  The requested QiType.


**.NET Library**

::

  Task<QiType> GetStreamTypeAsync(string streamId);


**Security**

  Allowed by administrator and user accounts


***********************

``Create Stream``
-----------------

Creates the specified stream.


**Request**

::

    POST api/Tenants/{tenantId}/Namespaces/{namespaceId}/Streams/{streamId}


**Parameters**

``string tenantId``
  The tenant identifier
``string namespaceId``
  The namespace identifier
``string streamId``
  The stream identifier. The stream identifier must match the identifier in content. 
  The request content is the serialized QiStream.

**Response**

  The response includes a status code and a response body.
  

**Response body**

  The newly created QiStream.
  

**.NET Library**

::

  Task<QiStream> GetOrCreateStreamAsync(QiStream qiStream);


If a stream with a matching identifier already exists and it matches the stream in the request body, 
the client redirects a GET to the Location header. If the existing stream does not match the stream 
in the request body, a Conflict error response is returned and the client library method throws an exception. 


**Security**

  Allowed for administrator accounts


***********************

``Create or Update Stream``
-------------------------

Creates the specified stream. If a stream with the same Id already exists, the definition of the stream is updated. 
The following changes are permitted:

•	Name
•	BehaviorId
•	Description

Unpermitted changes result in an error.



**Request**

::

    PUT api/Tenants/{tenantId}/Namespaces/{namespaceId}/Streams/{streamId}

**Parameters**

``string tenantId``
  The tenant identifier of the tenant where you want to update the stream
``string namespaceId``
  The namespace identifier of the namespace where you want to update the stream
``string streamId``
  The stream identifier to be updated

The request content is the serialized QiStream.


**Response**

  The response includes a status code.
  

**.NET Library**

::

  Task CreateOrUpdateStreamAsync(QiStream qiStream);


**Security**

  Allowed for administrator accounts


***********************

``Update Stream Type``
--------------

Updates a stream’s type. The type is modified to match the specified view. 


**Request**

::

    PUT api/Tenants/{tenantId}/Namespaces/{namespaceId}/Streams/{streamId}/Type?viewId={viewId}


**Parameters**

``string tenantId``
  The tenant identifier
``string namespaceId``
  The namespace identifier
``string streamId``
  The stream identifier
``string viewId``
  The view identifier

The request contains no content.


**Response**

  The response includes a status code.
  

**Response body**

  On failure, the content contains a message describing the issue.


**.NET Library**

::

  Task UpdateStreamAsync(string streamId, QiStream qiStream);


**Security**

  Allowed for administrator accounts


***********************

``Delete Stream``
--------------

Deletes a stream. 


**Request**

::

    DELETE api/Tenants/{tenantId}/Namespaces/{namespaceId}/Streams/{streamId}


**Parameters**

``string tenantId``
  The tenant identifier
``string namespaceId``
  The namespace identifier
``string streamId``
  The stream identifier


**Response**

  The response includes a status code.
  

**.NET Library**

::

  Task DeleteStreamAsync(string streamId);


**Security**

  Allowed for administrator accounts


