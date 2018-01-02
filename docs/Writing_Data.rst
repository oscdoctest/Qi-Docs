Writing Qi data
===============

The Qi REST APIs provide programmatic access to read and write Qi data. This section describes 
the APIs used to write QiStream data.

When working in .NET, convenient Qi Client libraries are available. The ``IQiDataServiceinterface``, accessed using the
``QiService.GetDataService( )`` helper, defines the available functions.

All writes rely on stream’s key or primary index. Preexisting values and positioning within the stream 
is determined exclusively by the primary index. Secondary indexes are updated, but they do not contribute 
to the request. All references to indexes are to the primary index.

The following single value write methods are available:

* **Insert Value** inserts a value at the specified primary index. 
* **Patch Value** updates specific fields in an existing value identified by the primary index.
* **Replace Value** replaces the value at the specified primary index.
* **Update Value** replaces the value with matching primary index. If no value exists the value is added.
* **Remove Value** deletes the value at the specified primary index.


The following support writing multiple values:

* **Insert Values** inserts a collection of values.
* **Patch Values** updates specific fields for a collection of values.
* **Replace Values** replaces a collection of values.
* **Update Values** replaces or adds a collection of values.
* **Remove Values** deletes the values at the specified primary indexes.
* **Remove Window Values** removes values that fall within the window defined by the start and end primary indexes.


The base URI for writing Qi data is:

::

  api/Tenants/{tenantId}/Namespaces/{namespaceId}/Streams/{streamId}/Data

where

string tenantId
  The tenant identifier
string namespaceId
The namespace identifier
string streamId
The stream identifier






