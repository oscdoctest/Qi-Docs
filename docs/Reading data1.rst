.. _Qi_Reading_data_topic:

Reading Qi data
===============

The REST APIs provide programmatic access to read and write Qi data. This section identifies and describes 
the APIs used to read :ref:`Qi_Stream_topic` data. Results are influenced by :ref:`Qi_Stream_behavior_topic` 
and :ref:`Qi_View_topic`.

If you are working in a .NET environment, convenient Qi Client libraries are available. 
The ``IQiDataServiceinterface``, which is accessed using the ``QiService.GetDataService()`` helper, 
defines the functions that are available.

The following methods for reading a single value are available:

* ``Get Value`` returns a value at a specified index, calculated if no stored value exists at that index. 
* ``Get First Value`` returns the first value in the stream.
* ``Get Last Value`` returns the last value in the stream.
* ``Get Distinct Value`` returns a value at the specified index, only if a stored value exists at that index.
* ``Find Distinct Value`` searches for a value based on a starting index and search criteria.

In addition, the following methods support reading multiple values:

* ``Get Values`` retrieves a collection of values at specified indexes, calculated if no stored 
  value exists at the index(es). ``Get values`` supports specifying the desired indexes as a list of indexes, 
  a filter expression and count, or a starting index, ending index, and count.
* ``Get Range Values`` retrieves a collection of stored values based on the specified start index and count.
* ``Get Window Values`` retrieves a collection of stored values based on specified start and end indexes.
* ``Get Intervals (preview*)`` retrieves a collection of evenly spaced summary intervals based on a count 
  and specified start and end indexes.

All reads are HTTP GET actions. Reading data involves getting events from streams. The base reading URI is as follows:

``api/Tenants/{tenantId}/Namespaces/{namespaceId}/Streams/{streamId}/Data``



