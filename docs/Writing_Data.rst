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

**Parameters**

``string tenantId``
  The tenant identifier
``string namespaceId``
  The namespace identifier
``string streamId``
  The stream identifier
  

Response Format
---------------

Supported response formats include JSON, verbose JSON, and Qi. 

The default response format for reading data is JSON, which is used in all examples in this document. 
Default JSON responses do not include any values that are equal to the default value for their type.

Verbose JSON responses include all values in the returned JSON payload, including defaults.
To specify verbose JSON return, add the header ``Accept-Verbosity`` with a value of ``verbose`` to the request. 

Verbose has no impact on writes; writes return only error messages.

To specify Qi format, set the ``Accept`` header in the request to ``application/qi``.

Indexes
-------

Qi writes rely on the primary index for positioning within streams and locating existing events. 
Most writes use the index as specified by the value. Deletes are the exception to this rule. When deleting, 
indexes are specified as strings in the URI, or, when using the Qi Client libraries, the index may be 
passed as-is to delete methods that take the index type as a generic argument. More details about working 
with indexes can be found on the :ref:`Qi_Indexes_topic` page. 

To specify compound indexes in the URI, specify each field that composes the index, in the specified order, 
separated by the pipe character, ‘|’.

Examples
--------

Many of the API methods described below contain sample JSON. 

When specifying a parameter of type ``enum``, the API accepts both the name of the field and the numeric 
value of the field. Samples vary to highlight enum flexibility.

Samples use the following types:

* Type with a simple index, named *Simple*:

**.NET**

::


  public enum State 
  {
    Ok,
    Warning,
    Alarm
  }

  public class Simple
  {
    [QiMember(IsKey = true, Order = 0) ] 
    public DateTime Time { get; set; }
    public State State { get; set; }
    public Double Measurement { get; set; }
  }

**Python**

::

  class State(Enum):
    Ok = 0
    Warning = 1
    Alarm = 2

  class Simple(object):
    Time = property(getTime, setTime)
    def getTime(self):
      return self.__time
    def setTime(self, time):
      self.__time = time

    State = property(getState, setState)
    def getState(self):
      return self.__state
    def setState(self, state):
      self.__state = state

    Measurement = property(getValue, setValue)
    def getValue(self):
      return self.__measurement
    def setValue(self, measurement):
      self.__measurement = measurement

**JavaScript**

::

  var State =
  {
    Ok: 0,
    Warning: 1,
    Aalrm: 2,
  }

  var Simple = function () {
    this.Time = null;
    this.State = null;
    this.Value = null;
  }
  
  
Has values as follows:

::

  11/23/2017 12:00:00 PM: Ok  0
  11/23/2017  1:00:00 PM: Ok 10
  11/23/2017  2:00:00 PM: Ok 20
  11/23/2017  3:00:00 PM: Ok 30
  11/23/2017  4:00:00 PM: Ok 40

* Type with Compound Index, named DerivedCompoundIndex

.NET

::

  public class Simple
  {
    [QiMember(IsKey = true, Order = 0)]
    public DateTime Time { get; set; }
    public State State { get; set; }
    public Double Measurement { get; set; }
  }

  public class DerivedCompoundIndex : Simple
  {
    [QiMember(IsKey = true, Order = 1)]
    public DateTime Recorded { get; set; }
  }
  
Python

::

  class Simple(object):
  # First-order Key property
  Time = property(getTime, setTime)
  def getTime(self):
    return self.__time
  def setTime(self, time):
    self.__time = time

  State = property(getState, setState)
  def getState(self):
    return self.__state
  def setState(self, state):
    self.__state = state

  Measurement = property(getValue, setValue)
  def getValue(self):
    return self.__measurement
  def setValue(self, measurement):
    self.__measurement = measurement

  class DerivedCompoundIndex(Simple):
  # Second-order Key property
  @property
  def Recorded(self):
    return self.__recorded
   @Recorded.setter
  def Recorded(self, recorded):
    self.__recorded = recorded

JavaScript

::

  var Simple = function () {
    this.Time = null;
    this.State = null;
    this.Value = null;
  }

  var DerivedCompoundIndex = function() {
    Simple.call(this);
    this.Recorded = null;
  }
  
Has values as follows:

::

  1/20/2017 1:00:00 AM : 1/20/2017 12:00:00 AM 	0
  1/20/2017 1:00:00 AM : 1/20/2017  1:00:00 AM 	2
  1/20/2017 1:00:00 AM : 1/20/2017  2:00:00 PM 	5
  1/20/2017 2:00:00 AM : 1/20/2017 12:00:00 AM 	1
  1/20/2017 2:00:00 AM : 1/20/2017  1:00:00 AM 	3
  1/20/2017 2:00:00 AM : 1/20/2017  2:00:00 AM 	4
  1/20/2017 2:00:00 AM : 1/20/2017  2:00:00 PM 	6
  
All times are represented at offset 0, GMT.


***********************

``Insert value``
----------------

Inserts an event into the specified stream. If an event exists at the same primary index, 
insert fails, returning HTTP Status Code Conflict, 409.


**Request**

::

    POST	api/Tenants/{tenantId}/Namespaces/{namespaceId}/Streams/{streamId}/Data/InsertValue


**Parameters**

``string tenantId``
  The tenant identifier
``string namespaceId``
  The namespace identifier
``string streamId``
  The stream identifier

The request content is the serialized object matching the stream type. If you are not 
using the Qi client libraries, we recommend using JSON.

A sample of serialized Simple type content is shown here:

::

  {  
     "Time":"2017-11-23T12:00:00Z",
     "State":0,
     "Measurement":1000.0
  }



**Response**

  The response includes a status code. On error, the response body contains a serialized description of the error.



**.NET Library**

::

  Task InsertValueAsync<T>(string streamId, T item);


**Security**

  Allowed for administrator accounts.


***********************




