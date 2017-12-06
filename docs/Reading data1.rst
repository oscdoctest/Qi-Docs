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


**where:**

``string tenantId``
  The tenant identifier
``string namespaceId``
  The namespace identifier
``string streamId``
  The stream identifier


Response Format
---------------

Supported response formats include json, verbose json, and Qi. 

The default response format for is json, which is used in all examples in this document.  Default json 
responses do not include any values that are equal to the default value for their type.

Verbose json responses include all values, including defaults, in the returned json payload. To specify 
verbose json return, add the header ``Accept-Verbosity`` with a value of ``verbose`` to the request.  

To specify Qi format, set the ``Accept`` header in the request to ``application/qi``.

Indexes and reading data
------------------------

Most read operations take at least one index as a parameter. Indexes may be specified as strings, or, 
when using the Qi Client libraries, the index may be passed as-is to read methods that take the index 
type as a generic argument. Additional details about working with indexes can be found on the :ref:`Qi_Indexes_topic` page. 

QiView and QiStreamBehavior
---------------------------

All reads support specifying a QiView identifier in the query string to shape the results of the read:

``viewId={viewId}``

Working with views is covered in detail in the :ref:`Qi_View_topic` section.

When data is requested at an index for which no stored event exists, the type of the index and 
the QiStreamBehavior for the stream determine whether the result is an error, null event, interpolated event, 
or extrapolated event. QiStreamBehavior is discussed in the Get Value, GetValues and GetWindowValues samples.

QiBoundaryType
--------------

QiBoundaryType defines how data on the boundary of queries is handled: around the start index for range value queries, 
and around the start and end index for window values. The following are valid values for QiBoundaryType:

+-------------------+-----------------------------------+---------------------------------------------------------------+
| Boundary          | Enumeration value                 | Operation                                                     |
+===================+===================================+===============================================================+
| Exact             | 0                                 | Results include the event at the specified index boundary     |
|                   |                                   | if a stored event exists at that index.                       |
+-------------------+-----------------------------------+---------------------------------------------------------------+
| Inside            | 1                                 | Results include only events within the index boundaries       |
+-------------------+-----------------------------------+---------------------------------------------------------------+
| Outside           | 2                                 | Results include up to one event that falls immediately        |
|                   |                                   | outside of the specified index boundary.                      |
+-------------------+-----------------------------------+---------------------------------------------------------------+
| ExactOrCalculated | 3                                 | Results include the event at the specified index boundary. If |
|                   |                                   | no stored event exists at that index, one is calculated based |
|                   |                                   | on the index type and QiStreamBehavior settings.              |
+-------------------+-----------------------------------+---------------------------------------------------------------+

QiSearchMode
------------

The QiSearchMode enum defines search behavior when seeking a stored event near a specified index. The following are 
available QiSearchModes:

+-------------------+-----------------------------------+---------------------------------------------------------------+
| Mode              | Enumeration value                 | Operation                                                     |
+===================+===================================+===============================================================+
| Exact             | 0                                 | If a stored event exists at the specified index, that event   |
|                   |                                   | is returned. Otherwise no event is returned.                  |
+-------------------+-----------------------------------+---------------------------------------------------------------+
| ExactOrNext       | 1                                 | If a stored event exists at the specified index, that event   |
|                   |                                   | is returned. Otherwise the next event in the stream is        |
|                   |                                   | returned.                                                     |
+-------------------+-----------------------------------+---------------------------------------------------------------+
| Next              | 2                                 | Returns the stored event after the specified index.           |
+-------------------+-----------------------------------+---------------------------------------------------------------+
| ExactOrPrevious   | 3                                 | If a stored event exists at the specified index, that event   |
|                   |                                   | is returned. Otherwise the previous event in the stream is    |
|                   |                                   | returned.                                                     |
+-------------------+-----------------------------------+---------------------------------------------------------------+
| Previous          | 4                                 | Returns the stored event before the specified index.          |
+-------------------+-----------------------------------+---------------------------------------------------------------+






