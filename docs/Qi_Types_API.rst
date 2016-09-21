QiType API calls
==================

The API calls in this section are all used to create and manipulate QiTypes. 
QiType management via the Qi Client Libraries is performed through the 
``IQiMetadataService`` interface, which is accessed using the 
``QiService.GetMetadataService( )`` helper.  
See `QiTypes <https://qi-docs.readthedocs.org/en/latest/Qi_Types.html>`__ 
for general QiType information, working with compound indexes, and supported QiTypes.


***********************


``GetStreamTypeAsync()``
----------------

Returns the type definition that is associated with a given stream from the specified namespace.

**Syntax**

::

    Task<QiType> GetStreamTypeAsync(string streamId);

*Http*
::

    GET Qi/{tenantId}/{namespaceId}/Streams/{streamId}/Type


**Parameters**

``string tenantId``
  The tenant identifier for the request
``string namespaceId``
  The namespace identifier for the request
``string streamId``
  The ID of the stream to search for the specified type definition


**Returns**

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
  The ID of the type to retrieve


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
  The ID of the type to delete

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
