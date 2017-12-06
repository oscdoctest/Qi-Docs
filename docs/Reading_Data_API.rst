API calls for reading data
===========================

Reading and writing data with the Qi Client Libraries is performed through the ``IQiDataService`` interface, which can be accessed with the ``QiService.GetDataService( )`` helper.



``Get Value``
--------------

Returns the value at the specified index. If no stored event exists at the specified index, the stream’s 
:ref:`Qi_Stream_behavior_topic` determines how the returned event is calculated.


**Request**

::

    GET	api/Tenants/{tenantId}/Namespaces/{namespaceId}/Streams/{streamId}/Data/GetValue
        ?index={index}&viewId={viewId}



**Parameters**

``string tenantId``
  The tenant identifier
``string namespaceId``
  The namespace identifier
``string streamId``
  The stream identifier
``string index``
  The index
``string viewId``
  Optional view identifier


**Response**

  The response includes a status code and a response body containing a serialized event.
  Consider a stream of type Simple with the default QiStreamBehavior Mode of Interpolation and 
  ExtrapolationMode of All. In the following request, the specified index matches an existing stored event:

::

  api/Tenants/{tenantId}/Namespaces/{namespaceId}/Streams/Simple/Data/GetValue 
     ?index=2017-11-23T13:00:00Z``

The response will contain the event stored at the specified index:

**Response body**

::
  
  HTTP/1.1 200
  Content-Type: application/json

  {  
     "Time":"2017-11-23T13:00:00Z",
     "Measurement":10.0
  }

Note that State is not included in the JSON as its value is the default value.

The following request specifies an index for which no stored event exists:

::

  api/Tenants/{tenantId}/Namespaces/{namespaceId}/Streams/Simple/Data/GetValue 
      ?index=2017-11-23T13:30:00Z
      
Because the index is a valid type for interpolation and the stream behavior specifies a mode of interpolate, 
this request receives a response with an event interpolated at the specified index:
      
**Response body**

::

  HTTP/1.1 200
  Content-Type: application/json

  {  
     "Time":"2017-11-23T13:30:00Z",
     "Measurement":15.0
  }





**.NET Library**

::

  Task<T> GetValueAsync<T>(string streamId, string index, 
  string viewId = null);
  Task<T> GetValueAsync<T, T1>(string streamId, Tuple<T1> index, 
  string viewId = null);
  Task<T> GetValueAsync<T, T1, T2>(string streamId, Tuple<T1, T2> index, 
  string viewId = null);


**Security**

  Allowed for administrator and user accounts


***********************

``Get First Value``
--------------

Returns the first value in the stream. If no values exist in the stream, null is returned.


**Request**

::

    GET	api/Tenants/{tenantId}/Namespaces/{namespaceId}/Streams/{streamId}/Data/GetFirstValue
        ?viewId={viewId}




**Parameters**

``string tenantId``
  The tenant identifier
``string namespaceId``
  The namespace identifier
``string streamId``
  The stream identifier
``string viewId``
  Optional view identifier


**Response**

  The response includes a status code and a response body containing a serialized event.



**.NET Library**

::

  Task<T> GetFirstValueAsync<T>(string streamId, string viewId = null);
  
  

**Security**

  Allowed for administrator and user accounts


***********************

``Get Last Value``
--------------

Returns the last value in the stream. If no values exist in the stream, null is returned.


**Request**

::

    GET	api/Tenants/{tenantId}/Namespaces/{namespaceId}/Streams/{streamId}/Data/GetLastValue
        ?viewId={viewId}


**Parameters**

``string tenantId``
  The tenant identifier
``string namespaceId``
  The namespace identifier
``string streamId``
  The stream identifier
``string viewId``
  Optional view identifier


**Response**

  The response includes a status code and a response body containing a serialized event.


**.NET Library**

::

  Task<T> GetLastValueAsync<T>(string streamId, string viewId = null);


**Security**

  Allowed for administrator and user accounts


***********************

``Get Distinct Value``
---------------------

Returns the value at the specified index. If no value exists at the specified index, 
Get Distinct Value returns HTTP Status Code Not Found, 404.  The stream’s QiStreamBehavior 
does not affect Get Distinct Value.


**Request**

::

    GET	api/Tenants/{tenantId}/Namespaces/{namespaceId}/Streams/{streamId}/Data/GetDistinctValue
        ?index={index}&viewId={viewId}


**Parameters**

``string tenantId``
  The tenant identifier
``string namespaceId``
  The namespace identifier
``string streamId``
  The stream identifier
``string index``
  The index
``string viewId``
  Optional view identifier


**Response**

  The response includes a status code and a response body containing a serialized event.
  
  For a stream of type Simple, when making a Get Distinct Value request at an existing stored index: 

::

  api/Tenants/{tenantId}/Namespaces/{namespaceId}/Streams/Simple/Data/ 
    GetDistinctValue?index=2017-11-23T13:00:00Z 

The event at that index is returned in the response:

**Response body**

::
  
  HTTP/1.1 200
  Content-Type: application/json

  {  
     "Time":"2017-11-23T13:00:00Z",
     "Measurement":10.0
  }

Note that State is not included in the JSON as its value is the default value.

The following request specifies an index for which no stored event exists:

::

  api/Tenants/{tenantId}/Namespaces/{namespaceId}/Streams/Simple/Data/GetValue 
      ?index=2017-11-23T13:30:00Z
      
Because the index is a valid type for interpolation and the stream behavior specifies a mode of interpolate, 
this request receives a response with an event interpolated at the specified index:
      
**Response body**

::

  HTTP/1.1 200
  Content-Type: application/json

  {  
     "Time":"2017-11-23T13:00:00Z",
     "Measurement":10.0
  }

Note that State is not included in the JSON as its value is the default value.

For a request at an index for which no stored event exists:

::

  api/Tenants/{tenantId}/Namespaces/{namespaceId}/Streams/Simple/Data/ 
    GetDistinctValue?index=2017-11-23T13:30:00Z

No distinct value is found at the specified index, and an error response is returned:

**Response body**

::

  HTTP/1.1 404
  Content-Type: application/json

  {  
     "Message":"Resource not found" 
  }


**.NET Library**

::

  Task<T> GetDistinctValueAsync<T>(string streamId, string index, 
    string viewId = null);
  Task<T> GetDistinctValueAsync<T, T1>(string streamId, Tuple<T1> index, 
    string viewId = null);
  Task<T> GetDistinctValueAsync<T, T1, T2>(string streamId, Tuple<T1, T2> index, 
    string viewId = null);


**Security**

  Allowed for administrator and user accounts



***********************

``Find Distinct Value``
----------------------

Returns a stored event found based on the specified QiSearchMode and index. 


**Request**

::

    GET	api/Tenants/{tenantId}/Namespaces/{namespaceId}/Streams/{streamId}/Data/FindDistinctValue
        ?index={index}&mode={mode}&viewId={viewId}



**Parameters**

``string tenantId``
  The tenant identifier
``string namespaceId``
  The namespace identifier
``string streamId``
  The stream identifier
``string index``
  The index
``string mode``
  The QiSearchMode
``string viewId``
  Optional view identifier


**Response**

  The response includes a status code and a response body containing a serialized event.

For a stream of type Simple the following request, 


::

  api/Tenants/{tenantId}/Namespaces/{namespaceId}/Streams/Simple/Data/ 
      FindDistinctValue?index=2017-11-23T13:00:00Z&mode=Next

The request has an index that matches the index of an existing event, but because  
a QiSearchMode of ``next`` was specified, the response contains the next event in the stream after the 
specified index:

**Response body**

::
  
  HTTP/1.1 200
  Content-Type: application/json

  Formatted JSON Data
  {  
     "Time":"2017-11-23T14:00:00Z",
     "Measurement":20.0
  }


Note that State is not included in the JSON as its value is the default value.

For the following request,

::

  api/Tenants/{tenantId}/Namespaces/{namespaceId}/Streams/Simple/Data/ 
    FindDistinctValue?index=2017-11-23T13:30:00Z&mode=Next
      
The request specifies an index that does not match an index of an existing event. 
The next event in the stream is retrieved.
      
**Response body**

::

  HTTP/1.1 200
  Content-Type: application/json

  Formatted JSON Data
  {  
     "Time":"2017-11-23T14:00:00Z",
     "Measurement":20.0
  }






**.NET Library**

::

  Task<T> FindDistinctValueAsync<T>(string streamId, string index, 
          QiSearchMode mode, string viewId = null);
  Task<T> FindDistinctValueAsync<T, T1>(string streamId, Tuple<T1> index, 
          QiSearchMode mode, string viewId = null);
  Task<T> FindDistinctValueAsync<T, T1, T2>(string streamId, Tuple<T1, T2> index, 
          QiSearchMode mode, string viewId = null);



**Security**

  Allowed for administrator and user accounts


***********************

``Get Values``
--------------

Returns a collection of values at indexes based on request parameters. 

As with the single event call to Get Value, the stream’s type and behavior determine how events 
are calculated for indexes at which no stored event exists.

Get Values supports three ways of specifying which events to return. 

* A range can be specified with a start index, end index, and count. This will return the specified 
  count of events evenly spaced from start index to end index.
* Multiple indexes can be passed to the request in order to retrieve events at exactly those indexes.
* A filtered request accepts a :ref:`Qi_Filter_expressions_topic` that limits results by applying an expression against 
  event fields. Filter expressions are explained in detail in the :ref:`Qi_Filter_expressions_topic` section.


**Request (Ranged)**

::

    GET	api/Tenants/{tenantId}/Namespaces/{namespaceId}/Streams/{streamId}/Data/ 
      GetValues?startIndex={startIndex}&endIndex={endIndex}&count={count}&viewId={viewId}



**Parameters**

``string tenantId``
  The tenant identifier
``string namespaceId``
  The namespace identifier
``string streamId``
  The stream identifier
``string startIndex``
  The index defining the beginning of the range
``string endIndex``
  The index defining the end of the range  
``string count``
  The number of events to return. QiStreamBehavior determines how the form of the event.
``string viewId``
  Optional view identifier


**Response**

  The response includes a status code and a response body containing a serialized collection of events.
  
  For a stream of type Simple, the following request, 


::

  api/Tenants/{tenantId}}/Namespaces/{namespaceId}/Streams/Simple/Data/GetValues 
      ?startIndex=2017-11-23T13:00:00Z&endIndex=2017-11-23T15:00:00Z&count=3

For this request, the start and end fall exactly on event indexes and the number of events 
from start to end match the count of three (3).

**Response body**

::
  
  HTTP/1.1 200
  Content-Type: application/json

  [  
     {  
        "Time":"2017-11-23T13:00:00Z",
        "Measurement":10.0
     },
     {  
        "Time":"2017-11-23T14:00:00Z",
        "Measurement":20.0
     },
     {  
        "Time":"2017-11-23T15:00:00Z",
        "Measurement":30.0
     }
  ] 


Note that State is not included in the JSON as its value is the default value.


**.NET Library**

::

  Task<IEnumerable<T>> GetValuesAsync<T>(string streamId, string startIndex, 
       string endIndex, int count, string viewId = null);
  Task<IEnumerable<T>> GetValuesAsync<T, T1>(string streamId, T1 startIndex, 
       T1 endIndex, int count, string viewId = null);
  Task<IEnumerable<T>> GetValuesAsync<T, T1, T2>string streamId, Tuple<T1, T2> startIndex, 
       Tuple<T1, T2> endIndex, int count, string viewId = null);



**Security**

  Allowed for administrator and user accounts


**Request (Index collection)**

::

    GET api/Tenants/{tenantId}/Namespaces/{namespaceId}/Streams/{streamId}/Data/ 
       GetValues?index={index}[&index={index} …]&viewId={viewId}



**Parameters**

``string tenantId``
  The tenant identifier
``string namespaceId``
  The namespace identifier
``string streamId``
  The stream identifier
``string index``
  One or more indexes of values to retrieve
``string viewId``
  Optional view identifier


**Response**

  The response includes a status code and a response body containing a serialized collection of events.
  
  For a stream of type Simple, the following request, 


::

  api/Tenants/{tenantId}}/Namespaces/{namespaceId}/Streams/Simple/Data/GetValues 
      ?index=2017-11-23T12:30:00Z&index=2017-11-23T13:00:00Z&index=2017-11-23T14:00:00Z

For this request, the response contains events for each of the three specified indexes.

**Response body**

::
  
  HTTP/1.1 200
  Content-Type: application/json

  [  
     {  
        "Time":"2017-11-23T12:30:00Z",
        "Measurement":5.0
     },
     {  
        "Time":"2017-11-23T13:00:00Z",
        "Measurement":10.0
     },
     {  
        "Time":"2017-11-23T14:00:00Z",
        "Measurement":20.0
     }
  ] 


Note that State is not included in the JSON as its value is the default value.


**.NET Library**

::

  Task<IEnumerable<T>> GetValuesAsync<T>(string streamId, IEnumerable<string> index, 
       string viewId = null);
        
  Task<IEnumerable<T>> GetValuesAsync<T, T1>(string streamId, IEnumerable<T1> index,
       string viewId = null);

  Task<IEnumerable<T>> GetValuesAsync<T, T1, T2>(string streamId, 
       IEnumerable<Tuple< T1, T2>> index, string viewId = null);




**Security**

  Allowed for administrator and user accounts

**Request (Filtered)**

::

    GET api/Tenants/{tenantId}/Namespaces/{namespaceId}/Streams/{streamId}/Data/ 
       GetValues?filter={filter}&viewId={viewId}


**Parameters**

``string tenantId``
  The tenant identifier
``string namespaceId``
  The namespace identifier
``string streamId``
  The stream identifier
``string filter``
  The filter expression (see :ref:`Qi_Filter_expressions_topic`)
``string viewId``
  Optional view identifier


**Response**

  The response includes a status code and a response body containing a serialized collection of events.
  
  For a stream of type Simple, the following request, 

::

  api/Tenants/{tenantId}/Namespaces/{namespaceId}/Streams/Simple/Data/GetValues 
      ?filter=Measurement gt 10

The events in the stream whose Measurement is less than or equal to 10 are not returned.


**Response body**

::
  
  HTTP/1.1 200
  Content-Type: application/json

  [  
     {  
        "Time":"2017-11-23T14:00:00Z",
        "Measurement":20.0
     },
     {  
        "Time":"2017-11-23T15:00:00Z",
        "Measurement":30.0
     },
     {  
        "Time":"2017-11-23T16:00:00Z",
        "Measurement":40.0
     }
  ] 
 


Note that State is not included in the JSON as its value is the default value.


**.NET Library**

::

  Task<IEnumerable<T>> GetFilteredValuesAsync<T>(string streamId, string filter, 
      string viewId = null);



**Security**

  Allowed for administrator and user accounts



STOPPED HERE

***********************

``Get Value``
--------------

Returns the value at the specified index. If no stored event exists at the specified index, the stream’s 
:ref:`Qi_Stream_behavior_topic` determines how the returned event is calculated.


**Request**

::

    GET	api/Tenants/{tenantId}/Namespaces/{namespaceId}/Streams/{streamId}/Data/GetValue
        ?index={index}&viewId={viewId}



**Parameters**

``string tenantId``
  The tenant identifier
``string namespaceId``
  The namespace identifier
``string streamId``
  The stream identifier
``string index``
  The index
``string viewId``
  Optional view identifier


**Response**

  The response includes a status code and a response body containing a serialized event.
  Consider a stream of type Simple with the default QiStreamBehavior Mode of Interpolation and 
  ExtrapolationMode of All. In the following request, the specified index matches an existing stored event:

::

  api/Tenants/{tenantId}/Namespaces/{namespaceId}/Streams/Simple/Data/GetValue 
     ?index=2017-11-23T13:00:00Z``

The response will contain the event stored at the specified index:

**Response body**

::
  
  HTTP/1.1 200
  Content-Type: application/json

  {  
     "Time":"2017-11-23T13:00:00Z",
     "Measurement":10.0
  }

Note that State is not included in the JSON as its value is the default value.

The following request specifies an index for which no stored event exists:

::

  api/Tenants/{tenantId}/Namespaces/{namespaceId}/Streams/Simple/Data/GetValue 
      ?index=2017-11-23T13:30:00Z
      
Because the index is a valid type for interpolation and the stream behavior specifies a mode of interpolate, 
this request receives a response with an event interpolated at the specified index:
      
**Response body**

::

  HTTP/1.1 200
  Content-Type: application/json

  {  
     "Time":"2017-11-23T13:30:00Z",
     "Measurement":15.0
  }





**.NET Library**

::

  Task<T> GetValueAsync<T>(string streamId, string index, 
  string viewId = null);
  Task<T> GetValueAsync<T, T1>(string streamId, Tuple<T1> index, 
  string viewId = null);
  Task<T> GetValueAsync<T, T1, T2>(string streamId, Tuple<T1, T2> index, 
  string viewId = null);


**Security**

  Allowed for administrator and user accounts


***********************

``Get Value``
--------------

Returns the value at the specified index. If no stored event exists at the specified index, the stream’s 
:ref:`Qi_Stream_behavior_topic` determines how the returned event is calculated.


**Request**

::

    GET	api/Tenants/{tenantId}/Namespaces/{namespaceId}/Streams/{streamId}/Data/GetValue
        ?index={index}&viewId={viewId}



**Parameters**

``string tenantId``
  The tenant identifier
``string namespaceId``
  The namespace identifier
``string streamId``
  The stream identifier
``string index``
  The index
``string viewId``
  Optional view identifier


**Response**

  The response includes a status code and a response body containing a serialized event.
  Consider a stream of type Simple with the default QiStreamBehavior Mode of Interpolation and 
  ExtrapolationMode of All. In the following request, the specified index matches an existing stored event:

::

  api/Tenants/{tenantId}/Namespaces/{namespaceId}/Streams/Simple/Data/GetValue 
     ?index=2017-11-23T13:00:00Z``

The response will contain the event stored at the specified index:

**Response body**

::
  
  HTTP/1.1 200
  Content-Type: application/json

  {  
     "Time":"2017-11-23T13:00:00Z",
     "Measurement":10.0
  }

Note that State is not included in the JSON as its value is the default value.

The following request specifies an index for which no stored event exists:

::

  api/Tenants/{tenantId}/Namespaces/{namespaceId}/Streams/Simple/Data/GetValue 
      ?index=2017-11-23T13:30:00Z
      
Because the index is a valid type for interpolation and the stream behavior specifies a mode of interpolate, 
this request receives a response with an event interpolated at the specified index:
      
**Response body**

::

  HTTP/1.1 200
  Content-Type: application/json

  {  
     "Time":"2017-11-23T13:30:00Z",
     "Measurement":15.0
  }





**.NET Library**

::

  Task<T> GetValueAsync<T>(string streamId, string index, 
  string viewId = null);
  Task<T> GetValueAsync<T, T1>(string streamId, Tuple<T1> index, 
  string viewId = null);
  Task<T> GetValueAsync<T, T1, T2>(string streamId, Tuple<T1, T2> index, 
  string viewId = null);


**Security**

  Allowed for administrator and user accounts


***********************

``Get Value``
--------------

Returns the value at the specified index. If no stored event exists at the specified index, the stream’s 
:ref:`Qi_Stream_behavior_topic` determines how the returned event is calculated.


**Request**

::

    GET	api/Tenants/{tenantId}/Namespaces/{namespaceId}/Streams/{streamId}/Data/GetValue
        ?index={index}&viewId={viewId}



**Parameters**

``string tenantId``
  The tenant identifier
``string namespaceId``
  The namespace identifier
``string streamId``
  The stream identifier
``string index``
  The index
``string viewId``
  Optional view identifier


**Response**

  The response includes a status code and a response body containing a serialized event.
  Consider a stream of type Simple with the default QiStreamBehavior Mode of Interpolation and 
  ExtrapolationMode of All. In the following request, the specified index matches an existing stored event:

::

  api/Tenants/{tenantId}/Namespaces/{namespaceId}/Streams/Simple/Data/GetValue 
     ?index=2017-11-23T13:00:00Z``

The response will contain the event stored at the specified index:

**Response body**

::
  
  HTTP/1.1 200
  Content-Type: application/json

  {  
     "Time":"2017-11-23T13:00:00Z",
     "Measurement":10.0
  }

Note that State is not included in the JSON as its value is the default value.

The following request specifies an index for which no stored event exists:

::

  api/Tenants/{tenantId}/Namespaces/{namespaceId}/Streams/Simple/Data/GetValue 
      ?index=2017-11-23T13:30:00Z
      
Because the index is a valid type for interpolation and the stream behavior specifies a mode of interpolate, 
this request receives a response with an event interpolated at the specified index:
      
**Response body**

::

  HTTP/1.1 200
  Content-Type: application/json

  {  
     "Time":"2017-11-23T13:30:00Z",
     "Measurement":15.0
  }





**.NET Library**

::

  Task<T> GetValueAsync<T>(string streamId, string index, 
  string viewId = null);
  Task<T> GetValueAsync<T, T1>(string streamId, Tuple<T1> index, 
  string viewId = null);
  Task<T> GetValueAsync<T, T1, T2>(string streamId, Tuple<T1, T2> index, 
  string viewId = null);


**Security**

  Allowed for administrator and user accounts


***********************
