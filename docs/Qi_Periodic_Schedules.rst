Qi Periodic Schedules
=====================

The API calls in this section are all used to create, delete, and manage periodic schedules within a namespace. Schedules can be referenced by calculations. 

``periodic()``
-------------------

Removes a periodic schedule from the namespace. 


**Syntax**

.. highlight:: none

::

    Task<QiNamespace> GetNamespaceAsync(string namespaceId);

**Http**

::

    GET "Qi/{tenantId}/NamespaceId/schedules/periodic{Id}”


**Parameters**

``string tenantId``
  The ID of the tenant.
  
``string NamespaceId``
  The ID of the namespace.
  
``string Id``
  The Id of the schedule.
 
Security
  Allowed by administrator and user accounts.

**Returns** 
  Returns a namespace.
  
**Status code**
  200 - OK
  400 - BadRequest
  500 - InternalServerError
 

**********************

``periodic()``
-------------------

Retrieves a periodic schedule that is associated with the specified Id. 


**Syntax**

.. highlight:: none

::

    Task<QiNamespace> GetNamespaceAsync(string namespaceId);

**Http**

::

    GET "/qi/{tenantId}/{namespaceId}/schedules/periodic/{id}"


**Parameters**

``string Id``
  Unique Id for this schedule. Used when referencing this schedule or retrieving it.
``string Name``
  A name for this schedule.
``string TimeZoneId`` (optional)
  The Id of the time zone used for this schedule. Used only when the schedule uses daily, monthly, or yearly schedules.
``string ScheduleType``
  Used to determine how the time interval is expressed = ['TimeInterval', 'Daily', 'Monthly', 'Yearly']
``string Interval`` (optional)
  The interval expressed as hh:mm[:ss[.ff]] where hh is the number of hours, mm is the number of minutes, ss is the optional number of seconds, and ff is the number of fractional seconds. Used only when the ScheduleType is TimeInterval.
``string Offset`` (optional)
  An offset applied to the schedule. If a TimeInterval schedule has an Interval of 01:00, or one hour, and an offset of 00:05, then it will be dispatched at five minutes after the hour, every hour.
 
Security
  Allowed by administrator and user accounts.

**Returns** 
  Returns a namespace.

**********************

``periodic()``
-------------------

Removes a periodic schedule from the namespace. 


**Syntax**

.. highlight:: none

::

    Task<QiNamespace> GetNamespaceAsync(string namespaceId);

**Http**

::

    GET "/qi/{tenantId}/{namespaceId}/schedules/periodic”


**Parameters**

``string Id``
  Unique Id for this schedule. Used when referencing this schedule or retrieving it.
``string Name``
  A name for this schedule.
``string TimeZoneId`` (optional)
  The Id of the time zone used for this schedule. Used only when the schedule uses daily, monthly, or yearly schedules.
``string ScheduleType``
  Used to determine how the time interval is expressed = ['TimeInterval', 'Daily', 'Monthly', 'Yearly']
``string Interval`` (optional)
  The interval expressed as hh:mm[:ss[.ff]] where hh is the number of hours, mm is the number of minutes, ss is the optional number of seconds, and ff is the number of fractional seconds. Used only when the ScheduleType is TimeInterval.
``string Offset`` (optional)
  An offset applied to the schedule. If a TimeInterval schedule has an Interval of 01:00, or one hour, and an offset of 00:05, then it will be dispatched at five minutes after the hour, every hour.
 
Security
  Allowed by administrator and user accounts.

**Returns** 
  Returns a namespace.

**Status code**
  400 - BadRequest
  500 - InternalServerError

 


**********************

``periodic()``
-------------------

 Inserts a new periodic schedule into the namespace. The schedule can be referenced by calculations. 


**Syntax**

.. highlight:: none

::

    Task<QiNamespace> GetNamespaceAsync(string namespaceId);

**Http**

::

    GET "/qi/{tenantId}/{namespaceId}/schedules/periodic”


**Parameters**

``string Id``
  Unique Id for this schedule. Used when referencing this schedule or retrieving it.
``string Name``
  A name for this schedule.
``string TimeZoneId`` (optional)
  The Id of the time zone used for this schedule. Used only when the schedule uses daily, monthly, or yearly schedules.
``string ScheduleType``
  Used to determine how the time interval is expressed = ['TimeInterval', 'Daily', 'Monthly', 'Yearly']
``string Interval`` (optional)
  The interval expressed as hh:mm[:ss[.ff]] where hh is the number of hours, mm is the number of minutes, ss is the optional number of seconds, and ff is the number of fractional seconds. Used only when the ScheduleType is TimeInterval.
``string Offset`` (optional)
  An offset applied to the schedule. If a TimeInterval schedule has an Interval of 01:00, or one hour, and an offset of 00:05, then it will be dispatched at five minutes after the hour, every hour.
 
Security
  Allowed by administrator and user accounts.

**Returns** 
  Returns a namespace.

**Status code**
  400 - BadRequest
  500 - InternalServerError

 

**********************


