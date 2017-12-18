QiStream Metadata and Tags
==========================

QiStream metadata is represented as a dictionary of string keys and associated string values. 
It can be used to associate additional information with a stream. QiStream tags are represented 
as a list of strings. Tags can be used to categorize or denote special attributes of streams. 

QiStream Metadata API 
---------------------

``Get stream metadata``
--------------

Returns the metadata dictionary for the specified stream. 


**Request**

::

    GET api/Tenants/{tenantId}/Namespaces/{namespaceId}/Streams/{streamId}/Metadata 


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

  The metadata for the specified QiStream. 

**Sample response body**

::
  
  HTTP/1.1 200 
  Content-Type: application/json 
  { 
      "a metadata key":"a metadata value", 
      "another key":"another value" 
  } 


**.NET Library**

::

  Task<IDictionary<string, string>> GetStreamMetadataAsync(string streamId); 


**Security**

  Allowed for administrator and user accounts


***********************
