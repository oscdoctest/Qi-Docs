QiType API
==========

The REST APIs provide programmatic access to read and write Qi data. The APIs in this section 
interact with QiTypes. When working in .NET convenient Qi Client libraries are available. 
The IQiMetadataService interface, accessed using theQiService.GetMetadataService( ) helper, 
defines the available functions. See `QiTypes <https://qi-docs.readthedocs.org/en/latest/Qi_Types.html>`__ 
for general QiType information.


***********************


``Get Type``
------------

Returns the type corresponding to the specified typeId within a given namespace.

**Request**

::

    GET api/Tenants/{tenantId}/Namespaces/{namespaceId}/Types/{typeId}


**Parameters**

``string tenantId``
  The tenant identifier
``string namespaceId``
  The namespace identifier
``string typeId``
  The type identifier


**Response**

The response includes a status code and a response body.

  Qitype type definition


Security
  Allowed by administrator and user accounts


***********************


``GetTypeAsync()``
----------------

Returns the type of the specified ``typeId`` from the specified namespace. 

**Syntax**

::

    Task<QiType> GetTypeAsync(string typeId);

*Http*

::

    GET Qi/{tenantId}/{namespaceId}/Types/{typeId}

**Parameters**

``string tenantId``
  The tenant identifier for the request
``string namespaceId``
  The namespace identifier for the request
``string typeId``
  The Id of the type to retrieve


**Returns**
  A QiType specified by the typeId

Security
  Allowed by administrator and user accounts


***********************


``GetTypesAsync()``
----------------

Returns a list of all types within a given namespace. 

**Syntax**

::

    Task<IEnumerable<QiType>> GetTypesAsync( );


*Http*

::

    GET Qi/Types


**Parameters**

``string tenantId``
  The tenant identifier for the request
``string namespaceId``
  The namespace identifier for the request

**Returns**

  IEnumerable QiType of all types in the namespace


Security
  Allowed by administrator and user accounts


***********************


``GetOrCreateTypeAsync()``
----------------

Returns the type of the specified ``typeId`` within a namespace, or creates the type if the ``typeId`` does not already exist. If the ``typeId`` exists, it is returned to the caller unchanged. 


**Syntax**

::

    Task<QiType> GetOrCreateTypeAsync(QiType qitype);

*Http*

::

    POST Qi/{tenantId}/{namespaceId}/Types



**Parameters**

``string tenantId``
  The tenant identifier for the request
``string namespaceId``
  The namespace identifier for the request
``QiType qitype``
  The type of the stream for which the type request is made


**Returns**

  Qitype


Security
  Allowed by administrator account

**Notes**

.. _Introducing JSON: http://json.org/index.html

 For HTTP requests, the message content (the event) must be serialized in JSON format. JSON objects consist of a 
 series of name-value property pairs enclosed within brackets. Because QiType objects can become complex (particularly 
 when properties themselves are QiTypes), OSIsoft recommends using a JSON serializer (available at `Introducing JSON`_). 
 The following example shows the serialization of the QiType object from the WaveData example. See the Qi code 
 samples for the complete WaveData example.


::

	{
		"Id":"WaveData_SampleType",
		"Name":"Wave Data Type",
		"Description":"This is a type for WaveData events",
		"QiTypeCode":0,
		"Properties":[
			{
				"Id":"Order",
				"Name":null,
				"Description":null,
				"QiType":
					{
						"Id":"intType",
						"Name":null,
						"Description":null,
						"QiTypeCode":9,
						"Properties":null
					},
				"IsKey":true
			},
			{
				"Id":"Tau",
				"Name":null,
				"Description":null,
				"QiType":
					{
						"Id":"doubleType",
						"Name":null,
						"Description":null,
						"QiTypeCode":14,
						"Properties":null
					},
				"IsKey":false
			},
			{
				"Id":"Radians",
				"Name":null,
				"Description":null,
				"QiType":
					{
						"Id":"doubleType",
						"Name":null,
						"Description":null,
						"QiTypeCode":14,
						"Properties":null
					},
				"IsKey":false
			},
			{
				"Id":"Sin",
				"Name":null,
				"Description":null,
				"QiType":
					{
						"Id":"doubleType",
						"Name":null,
						"Description":null,
						"QiTypeCode":14,
						"Properties":null
					},
					"IsKey":false
			},
			{
				"Id":"Cos",
				"Name":null,
				"Description":null,
				"QiType":
					{
						"Id":"doubleType",
						"Name":null,
						"Description":null,
						"QiTypeCode":14,
						"Properties":null
					},
				"IsKey":false
			},
			{
				"Id":"Tan",
				"Name":null,
				"Description":null,
				"QiType":
					{
						"Id":"doubleType",
						"Name":null,
						"Description":null,
						"QiTypeCode":14,
						"Properties":null
					},
				"IsKey":false
			},
			{
				"Id":"Sinh",
				"Name":null,
				"Description":null,
				"QiType":
					{
						"Id":"doubleType",
						"Name":null,
						"Description":null,
						"QiTypeCode":14,
						"Properties":null
					},
				"IsKey":false
			},
			{
				"Id":"cosh",
				"Name":null,
				"Description":null,
				"QiType":
					{	
						"Id":"doubleType",
						"Name":null,
						"Description":null,
						"QiTypeCode":14,
						"Properties":null
					},
				"IsKey":false
			},
			{
				"Id":"Tanh",
				"Name":null,
				"Description":null,
				"QiType":
					{
						"Id":"doubleType",
						"Name":null,
						"Description":null,
						"QiTypeCode":14,
						"Properties":null
					},
				"IsKey":false
			}
		]
	}

***********************


``DeleteTypeAsync()``
----------------

Deletes a type from the specified namespace. Note that a type cannot be deleted if any 
streams are associated with it.

**Syntax**

::

    Task DeleteTypeAsync(string typeId);

*Http*

::

    DELETE Qi/{tenantId}/{namespaceId}/Types/{typeId}



**Parameters**

``string tenantId``
  The tenant identifier for the request
``string namespaceId``
  The namespace identifier for the request
``string typeId``
  The Id of the type to delete

**Returns**

  Qitype


Security
  Allowed by administrator account


***********************


``UpdateTypeAsync()``
----------------

Updates the definition of a type. Note that a type cannot be updated if any streams are 
associated with it. Also, certain parameters cannot be changed after they are defined.

**Syntax**

::

    Task UpdateTypeAsync(string typeId, QiType qitype);

*Http*

::

    PUT Qi/{tenantId}/{namespaceId}/Types/{typeId}


Content is a serialized QiType object.

**Parameters**

``string tenantId``
  The tenant identifier for the request
``string namespaceId``
  The namespace identifier for the request
``string qitype``
  The qitype of the type to update


**Returns**

  Qitype

Security
  Allowed by Administrator account
