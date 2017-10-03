QiView API
==========

The REST APIs provide programmatic access to read and write Qi data. The APIs in this section interact 
with QiViews. When working in .NET convenient Qi Client libraries are available. The IQiMetadataService 
interface, accessed using the ``QiService.GetMetadataService( )`` helper, defines the available functions. 
See QiTypes for general QiView information.

***********************

``Get View``
--------------

Returns the view corresponding to the specified viewId within a given namespace.


**Request**

::

    GET	api/Tenants/{tenantId}/Namespaces/{namespaceId}/Views/{viewId}


**Parameters**

``string tenantId``
  The tenant identifier
``string namespaceId``
  The namespace identifier
``string viewId``
  The view identifier


**Response**

  The response includes a status code and a response body.
  

**Response body**

  The requested QiView.

  Sample response body:

::
  
  HTTP/1.1 200
  Content-Type: application/json

  {  
     "Id":"View",
     "Name":"View",
     "SourceTypeId":"Simple",
     "TargetTypeId":"Simple3",
     "Properties":[  
        {  
           "SourceId":"Time",
           "TargetId":"Time"
        },
        {  
           "SourceId":"Status",
           "TargetId":"Status"
        },
        {  
           "SourceId":"Measurement",
           "TargetId":"Value"
        }
     ]
  }



**.NET Library**

::

  Task<QiView> GetViewAsync(string viewId);


**Security**

  Allowed by administrator accounts
