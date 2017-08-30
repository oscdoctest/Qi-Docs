QiStreamBehavior API
====================

The REST APIs provide programmatic access to create and manipulate QiStreamBehaviors. 
The APIs in this section interact with QiStreamBehavior. When working in .NET convenient 
Qi Client libraries are available. The IQiMetadataService interface, accessed using the 
``QiService.GetMetadataService()`` helper defines the available functions. 

See `QiStreamBehavior <https://qi-docs-rst.readthedocs.org/en/latest/Qi_Stream_Behavior.html>`__ for 
general QiStreamBehavior information.


***********************


``Get Behavior``
----------------

Returns a QiStreamBehavior corresponding to the specified behaviorId

**Request**

::

    GET api/Tenants/{tenantId}/Namespaces/{namespaceId}/Behaviors/{behaviorId}

**Parameters**

``string tenantId``
  The tenant identifier
``string namespaceId``
  The namespace identifier
``string behaviorId``
  The stream behavior identifier


**Response**

The response includes a status code and a response body.

  Response body:
    The requested QiStreamBehavior
    
::

  Sample response body
  HTTP/1.1 200
  Content-Type: application/json

  {  
     "Id":"Behavior",
     "Name":"Behavior",
     "Mode":1,
     "ExtrapolationMode":1
  }

**.NET Library**

::

  Task<QiStreamBehavior> GetBehaviorAsync(string behaviorId);

**Security**

  Allowed for administrator and user accounts


**********************


``GetBehaviorAsync()``
----------------

Retrieves a QiStreamBehavior from the specified namespace that matches the specified behaviorId

**Syntax**

::

    Task<QiStreamBehavior> GetBehaviorAsync( );

**Http**

::

    GET Qi/{tenantId}/{namespaceId}/Behaviors/{behaviorId}

**Parameters**

``string tenantId``
  The tenant identifier for the request
``string namespaceId``
  The namespace identifier for the request


**Returns**
  A QiStream object

Security
  Allowed by administrator and user accounts

**********************


``GetBehaviorsAsync()``
----------------

Retrieves all QiStream behaviors from a namespace.


**Syntax**

::

    Task<IEnumerable<QiStreamBehavior>> GetBehaviorsAsync( ;

**Http**

::

    GET Qi/{tenantId}/{namespaceId}/Behaviors

**Parameters**

``string tenantId``
  The tenant identifier for the request
``string namespaceId``
  The namespace identifier for the request
``behaviorId``
  The Id of the behavior to retrieve.


**Returns**
  An IEnumerable of all behavior objects

Security
  Allowed by administrator and user accounts

  
**********************


``GetOrCreateBehaviorAsync()``
----------------

Retrieves the QiStream behavior from a namespace, or creates the behavior if the behavior does not already exist. If the behavior exists, it is returned to the caller unchanged.

**Syntax**

::

    Task<QiStreamBehavior> GetOrCreateBehaviorAsync(QiStreamBehavior qibehavior);

**Http**

::

    POST  Qi/{tenantId}/{namespaceId}/Behaviors
	
**Parameters**

``string tenantId``
  The tenant identifier for the request
``string namespaceId``
  The namespace identifier for the request
``qibehavior``
  A QiStreamBehavior object to add to Qi.


**Returns**
  An IEnumerable of all behavior objects.

Security
  Allowed by administrator accounts
  
**Notes**
  For HTTP requests, the message body content is a QiStreamBehavior object that is serialized in JSON format. For example:

::

	{
		"Id":"WaveData_SampleBehavior",
		"Name":null,
		"Mode":1,
		"ExtrapolationMode":0,
		"Overrides":null
	}


**********************


``UpdateBehaviorAsync()``
----------------

Replaces the stream’s existing behavior with those defined in the ‘qibehavior’. If certain aspects of the existing behavior are meant to remain, they must be included in qibehavior.

An override list can be included in the ‘qibehavior’ to cause
the addition, removal, or change to this list.

**Syntax**

::

    Task UpdateBehaviorAsync(string behaviorId, QiStreamBehavior qibehavior);

**Http**

::

    PUT Qi/{tenantId}/{namespaceId}/Behaviors/{behaviorId}
    

Content is a serialized QiStreamBehavior object.


**Parameters**

``string tenantId``
  The tenant identifier for the request
``string namespaceId``
  The namespace identifier for the request
``qibehavior``
  The updated stream behavior


**Returns**
  An IEnumerable of all behavior objects

Security
  Allowed by administrator accounts

