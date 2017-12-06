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
