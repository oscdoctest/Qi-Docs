Namespace
=======================================================

A Namespace is a collection of Data Streams.

	The following code shows the JSON-serialized Namespace object for HTTP requests and responses:

.. _NamespaceObj: 

.. highlight:: C#

::

 {
    "Id": "id",                            //Name of this Namespace. Unique within a Tenant's Namespaces.
    "TenantId": "tenantid",                //GUID of the Tenant that this Namespace corresponds to
    "Description": "description",          //Description of this Namespace.
    "TierId": "tierid",                    //GUID of the Tier that this Namespace is associated with.
    "ThroughputUnits": 0,                  //Number of Throughput units for this Namespace.
    "StorageUnits": 0,                     //Number of Storage units for this Namespace.
    "CalculationUnits": 0,                 //Number of Calculation units for this Namespace.
    "State": 0                             //Current state of this Namespace.
 }

``GetAll()``
--------------------------------------------------------------------

Returns all Namespaces owned by the specified tenant.

**Http**

::

	GET api/Tenants/{tenantId}/Namespaces

**Parameters**

``String tenantId``
	The :ref:`Tenant <TenantObj>` identifier for the request

**Security**
	Allowed by Account Member and Cluster Operator :ref:`Roles <RoleObj>`

**Returns**
	An array of all :ref:`Namespace <NamespaceObj>` objects for the specified tenantId



|

**********************

``GetNamespaceById()``
--------------------------------------------------------------------

Returns the Namespace with the specified Id.

**Http**

::

	GET api/Tenants/{tenantId}/Namespaces/{namespaceId}

**Parameters**

``String namespaceId``
	The Namespace identifier for this request
``String tenantId``
	The account identifier for the request

**Security**
	Allowed by Account Member and Cluster Operator :ref:`Roles <RoleObj>`

**Returns**
	A :ref:`Namespace <NamespaceObj>` object with the specified namespaceId



|

**********************

``Create()``
--------------------------------------------------------------------

Creates a namespace.

**Http**

::

	POST api/Tenants/{tenantId}/Namespaces

**Parameters**

``Namespace namespaceObj``
	The :ref:`Namespace <NamespaceObj>` to be created
``String tenantId``
	The idenfifier for the account the namespace is to be created for

**Security**
	Allowed by Account Administrator and Cluster Operator :ref:`Roles <RoleObj>`

**Returns**
	The created :ref:`Namespace <NamespaceObj>` object



|

**********************

``Delete()``
--------------------------------------------------------------------

Deletes a namespace.

**Http**

::

	DELETE api/Tenants/{tenantId}/Namespaces/{namespaceId}

**Parameters**

``String namespaceId``
	The identifier of the namespace to be deleted
``String tenantId``
	The identifier of namespace's account

**Security**
	Allowed by Account Administrator and Cluster Operator :ref:`Roles <RoleObj>`

**Returns**
	Nothing is returned



|

**********************

``Update()``
--------------------------------------------------------------------

Updates namespace information - description and tier Id.

**Http**

::

	PUT api/Tenants/{tenantId}/Namespaces/{namespaceId}

**Parameters**

``String namespaceId``
	The identifier for the namespace to update
``String tenantId``
	The identifier of namespace's account
``Namespace namespaceObj``
	The namespace to be updated

**Security**
	Allowed by Account Administrator and Cluster Operator :ref:`Roles <RoleObj>`

**Returns**
	The updated :ref:`Namespace <NamespaceObj>`



|

**********************


