Feature
==========

``GetTenantFeatureState()``
----------------------

Returns the current state of the tenant.

**Syntax**

.. highlight:: none

**Http**

::

	GET PICS/Tenants/{tenantId}/Features/{featureId}


**Parameters**

``String tenantId``
  The tenant identifier for the request
``String featureId``
  The identifier of the feature
  
**Security**

Any OSIsoft Cloud Services user

*******************

GlobalGroup
==========

Group
==========

``GetGroup()``
----------------------

Returns the current group.

**Syntax**

.. highlight:: none

**Http**

::

	GET PICS/Tenants/{tenantId}/Groups/{groupId}

**Parameters**

``String tenantId``
  The tenant identifier for the request
``String groupId``
  The group identifier for the request


**Security**

OSIsoft Cloud Services tenant administrator


*********************


``GetGroups()``
----------------------

**Syntax**

.. highlight:: none

**Http**

::

	GET PICS/Tenants/{tenantId}/Groups

**Parameters**
``String tenantId``


**Security**

OSIsoft Cloud Services tenant administrator

**********************


``GetGroupMembers()``
----------------------

**Syntax**

.. highlight:: none

**Http**

::

	GET PICS/Tenants/{tenantId}/Groups/{groupId}/Users

**Parameters**
``String tenantId``
``String groupId``

**Security**

OSIsoft Cloud Services tenant administrator

**********************


``Create()``
----------------------

**Syntax**

.. highlight:: none

**Http**

::

	POST PICS/Tenants/{tenantId}/Groups

**Parameters**
``String tenantId``
``Group group``
**Body**
{
  "Id": "id",
  "Name": "name",
  "AzureActiveDirectoryGroupName": "azureactivedirectorygroupname",
  "Description": "description"
}


**Security**

OSIsoft Cloud Services tenant administrator

**********************


``Delete()``
----------------------

**Syntax**

.. highlight:: none

**Http**

::

	DELETE PICS/Tenants/{tenantId}/Groups/{groupId}

**Parameters**
``String tenantId``
``String groupId``


**Security**

OSIsoft Cloud Services tenant administrator


**********************


``AddUserToGroup()``
----------------------

**Syntax**

.. highlight:: none

**Http**

::

	POST PICS/Tenants/{tenantId}/Groups/{groupId}/Users

**Parameters**
``String tenantId``
``String groupId``
``CreateUser user``
**Body**
{
  "SendNotification": false,
  "IsAdministrator": false,
  "Id": "id",
  "FirstName": "firstname",
  "LastName": "lastname",
  "LoginName": "loginname",
  "ContactEmail": "contactemail",
  "ContactPhone": "contactphone",
  "UPN": "upn",
  "Password": "password"
}


**Security**

OSIsoft Cloud Services tenant administrator

**********************


``RemoveUserFromGroup()``
----------------------

**Syntax**

.. highlight:: none

**Http**

::

	DELETE PICS/Tenants/{tenantId}/Groups/{groupId}/Users/{userId}

**Parameters**
``String tenantId``
``String groupId``
``String userId``

**Security**

OSIsoft Cloud Services tenant administrator

**********************


Namespace
==========

``GetAll()``
----------------------

**Syntax**

.. highlight:: none

**Http**

::

	GET PICS/Tenants/{tenantId}/Namespaces

**Parameters**
``String tenantId``


**Security**

Any OSIsoft Cloud Services user


**********************


``GetNamespaceById()``
----------------------

**Syntax**

.. highlight:: none

**Http**

::

	GET PICS/Tenants/{tenantId}/Namespaces/{Id}

**Parameters**
``String id``
``String tenantId``

**Security**

Any OSIsoft Cloud Services user


**********************



``Create()``
----------------------

**Syntax**

.. highlight:: none

**Http**

::

	POST PICS/Tenants/{tenantId}/Namespaces/

**Parameters**
``Namespace namespaceObj``
**Body**
{
  "Id": "id",
  "TenantId": "tenantid",
  "Description": "description",
  "TierId": "tierid",
  "ThroughputUnits": 0,
  "StorageUnits": 0,
  "CalculationUnits": 0
}

**Security**

OSIsoft Cloud Services tenant administrator

**********************


``Delete()``
----------------------

**Syntax**

.. highlight:: none

**Http**

::

	DELETE PICS/Tenants/{tenantId}/Namespaces/{Id}

**Parameters**
``String id``
``String tenantId``


**Security**

OSIsoft Cloud Services tenant administrator

**********************


``DeleteNamespaces()``
----------------------

**Syntax**

.. highlight:: none

**Http**

::

	DELETE PICS/Tenants/{tenantId}/Namespaces/

**Parameters**
``String tenantId``


**Security**

OSIsoft Cloud Services tenant administrator

**********************


``UpdateNamespace()``
----------------------

**Syntax**

.. highlight:: none

**Http**

::

	PUT PICS/Tenants/{tenantId}/Namespaces/{Id}

**Parameters**
``String id``
``String tenantId``
``Namespace namespaceObj``
**Body**
{
  "Id": "id",
  "TenantId": "tenantid",
  "Description": "description",
  "TierId": "tierid",
  "ThroughputUnits": 0,
  "StorageUnits": 0,
  "CalculationUnits": 0
}


**Security**

OSIsoft Cloud Services tenant administrator


**********************

ServiceBlog
==========

``GetByPage()``
----------------------

**Syntax**

.. highlight:: none

**Http**

::

	GET PICS/ServiceBlog/Entries

**Parameters**
``Int32 skip``
``Int32 take``

**Security**

Any OSIsoft Cloud Services user


**********************


ServiceBlogTemplate
==========

Service
==========

Tenant
==========

``GetTenant()``
----------------------

**Syntax**

.. highlight:: none

**Http**

::

	GET PICS/Tenants/{tenantId}

**Parameters**
``String tenantId``


**Security**

Any OSIsoft Cloud Services user


**********************


TenantFeatureState
==========

TenantServiceState
==========

Applications
==========

``CreateClientApiKeySet()``
----------------------

**Syntax**

.. highlight:: none

**Http**

::

	POST PICS/Tenants/{tenantId}/ClientApiKeySets

**Parameters**
``ClientApiKeySet keySet``
**Body**
{
  "AppUri": "appuri",
  "CreateFirstKey": false,
  "DisplayName": "displayname",
  "Facility": "facility",
  "RequiredResource": null,
  "TenantId": "tenantid"
}


**Security**

OSIsoft Cloud Services tenant administrator


**********************


``GetOrCreateClientApiKeySet()``
----------------------

**Syntax**

.. highlight:: none

**Http**

::

	POST PICS/Tenants/{tenantId}/GetOrCreateClientApiKeySets

**Parameters**
``ClientApiKeySet keySet``
**Body**
{
  "AppUri": "appuri",
  "CreateFirstKey": false,
  "DisplayName": "displayname",
  "Facility": "facility",
  "RequiredResource": null,
  "TenantId": "tenantid"
}


**Security**

OSIsoft Cloud Services tenant administrator

**********************


``DeleteClientApiKeySet()``
----------------------

**Syntax**

.. highlight:: none

**Http**

::

	DELETE PICS/Tenants/{tenantId}/ClientApiKeySets/{applicationId}

**Parameters**
``String tenantId``
``String applicationId``

**Security**

OSIsoft Cloud Services tenant administrator


**********************


NamespaceTier
==========

Utilities
==========

``Ping()``
----------------------

**Syntax**

.. highlight:: none

**Http**

::

	GET PICS/Utilities/ping

**Parameters**


**Security**

Any OSIsoft Cloud Services user

**********************


User
==========

``Get()``
----------------------

**Syntax**

.. highlight:: none

**Http**

::

	GET PICS/Tenants/{tenantId}/Users/{userId}

**Parameters**
``String tenantId``
``String userId``

**Security**

OSIsoft Cloud Services tenant administrator

**********************


``Get()``
----------------------

**Syntax**

.. highlight:: none

**Http**

::

	GET PICS/Tenants/{tenantId}/Users

**Parameters**
``String tenantId``


**Security**

OSIsoft Cloud Services tenant administrator


**********************


``GetUserGroups()``
----------------------

**Syntax**

.. highlight:: none

**Http**

::

	GET PICS/Tenants/{tenantId}/Users/{userId}/Groups

**Parameters**
``String tenantId``
``String userId``


**Security**

OSIsoft Cloud Services tenant administrator
The OSIsoft Cloud Services user which is the object of this call

**********************


``IsUserInGroup()``
----------------------

**Syntax**

.. highlight:: none

**Http**

::

	HEAD PICS/Tenants/{tenantId}/Users/{userId}/Groups/{groupId}

**Parameters**
``String tenantId``
``String userId``
``String groupId``


**Security**

OSIsoft Cloud Services tenant administrator
The OSIsoft Cloud Services user which is the object of this call

**********************


``CreateUser()``
----------------------

**Syntax**

.. highlight:: none

**Http**

::

	POST PICS/Tenants/{tenantId}/Users/

**Parameters**
``String tenantId``
``CreateUser user``
**Body**
{
  "SendNotification": false,
  "IsAdministrator": false,
  "Id": "id",
  "FirstName": "firstname",
  "LastName": "lastname",
  "LoginName": "loginname",
  "ContactEmail": "contactemail",
  "ContactPhone": "contactphone",
  "UPN": "upn",
  "Password": "password"
}


**Security**

OSIsoft Cloud Services tenant administrator

**********************

**Syntax**

.. highlight:: none

``Update()``
----------------------

**Http**

::

	PUT PICS/Tenants/{tenantId}/Users/{userId}

**Parameters**
``String tenantId``
``String userId``
``CreateUser user``
**Body**
{
  "SendNotification": false,
  "IsAdministrator": false,
  "Id": "id",
  "FirstName": "firstname",
  "LastName": "lastname",
  "LoginName": "loginname",
  "ContactEmail": "contactemail",
  "ContactPhone": "contactphone",
  "UPN": "upn",
  "Password": "password"
}


**Security**

OSIsoft Cloud Services tenant administrator


**********************


``Delete()``
----------------------

**Syntax**

.. highlight:: none

**Http**

::

	DELETE PICS/Tenants/{tenantId}/Users/{userId}

**Parameters**
``String tenantId``
``String userId``


**Security**

OSIsoft Cloud Services tenant administrator

**********************


``ResetUserPassword()``
----------------------

**Syntax**

.. highlight:: none

**Http**

::

	POST PICS/Tenants/{tenantId}/Users/{userId}/passwordreset

**Parameters**
``String tenantId``
``String userId``


**Security**

OSIsoft Cloud Services tenant administrator

**********************
