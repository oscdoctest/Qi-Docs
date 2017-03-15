Qi Calculations
===============

You use the API calls in this section create, delete, and manage calculations.


``GetOrCreateCalculationAsync()``
--------------------------------

Retrieves the QiCalculation within the specified namespaceId, or creates the QiCalculation if it does not already exist. If the QiCalculation exists, it is returned to the caller unchanged.


**Syntax**

.. highlight:: none

::

    Task<QiCalculation> GetOrCreateCalculationAsync(QiCalculation calculation);


**Http**

::

    POST /qi/{tenantId}/{namespaceId}/Calculations


**Parameters**

``string tenantId``
  The Id of the tenant.

``string namespaceId`
  The Id of the Namespace

``calculation``
  The calculation to insert
  
::

  QiCalculation {
    Id (string): Unique Id for this calculation. Used when referencing this calculation or retrieving it. ,
    Name (string, optional): A name for this calculation. ,
    Description (string, optional): A description of what this calculation does. ,
    TemplateId (string): The template to be used for this calculation. ,
    Schedule (IQiSchedule, optional): The scheduled used to determine how the calculation is dispatched. 
      If , then the schedule on the template will be used. ,
    StreamAliases (Array[QiStreamAlias], optional): A list of stream aliases used to map streams to the alias Ids on the template. ,
    Status (string): Status of the calculation. = ['Undefined', 'InDevelopment', 'Enabled', 'InError']
    }
  IQiSchedule {
    ScheduleType (string, optional, read only): Returns the type of schedule the data contract 
      implements. = ['Undefined', 'Periodic', 'EventTriggered', 'Manual']
    }
  QiStreamAlias {
    AliasId (string): The Id of the alias being mapped. ,
    StreamId (string): The Id of the stream. ,
    NamespaceId (string, optional): The Id of the namespace. If , then the namespace the calculation resides within will be used. ,
    TenantId (string, optional): The Id of the tenant. If , then the tenant the calculation resides within will be used.
  }




Security
  Allowed by administrator and user accounts.

**Returns** 

  
**Status code**

*  201 - The object was added successfully
*  400 - One of the arguments is invalid or a referenced dependent object does not exist.
*  401 - The user is not authorized to perform this operation.
*  500 - An unexpected error occurred.
*  504 - A timeout occurred while trying to execute the operation.
 

**********************

``AddCalculationsAsync()``
----------------------

Inserts list of QiCalculation into a namespace. 


**Syntax**

.. highlight:: none

::

    Task AddCalculationsAsync(IList<QiCalculation> calculations);

**Http**

::

    POST /qi/{tenantId}/{namespaceId}/Calculations/$Batch


**Parameters**

``string Id``

``string name`` (optional)

``string Description`` (optional)
 

``string TypeId``
  

``string ScheduleId``
  
  
``Array [QiSymbolSettings] SymbolSettings`` (optional)
  
  ::

  QiSymbolSettings {
    SymbolId (string, optional),
    ProviderSettings (object, optional)
  } 
  
  
``boolean IsEnabled``

``string Status`` = ['Undefined', 'InDevelopment', 'Running', 'InError']



Security
  Allowed by administrator and user accounts.

**Returns** 

::

  QiCalculation {
    Id (string),
    Name (string, optional),
    Description (string, optional),
    TypeId (string),
    ScheduleId (string),
    SymbolSettings (Array[QiSymbolSettings], optional),
    IsEnabled (boolean),
    Status (string) = ['Undefined', 'InDevelopment', 'Running', 'InError']
  }
  QiSymbolSettings {
    SymbolId (string, optional),
    ProviderSettings (object, optional)
  } 

  
**Status code**

*  201 - The list of objects were successfully inserted.
*  400 - One of the arguments is invalid or a referenced dependent object does not exist.
*  401 - The user is not authorized to perform this operation.
*  500 - An unexpected error occurred.
*  504 - A timeout occurred while trying to execute the operation.
 

**********************




``GetCalculationAsync()``
----------------------

Retrieves a QiCalculation from the specified namespace. 


**Syntax**

.. highlight:: none

::

    Task<QiCalculation> GetCalculationAsync(string calculationId);

**Http**

::

   GET /qi/{tenantId}/{namespaceId}/Calculations/{calculationId}


**Parameters**

``string Id``
  
 
``string name`` (optional)
  

``string Description`` (optional)
  

``string TypeId``
  

``string ScheduleId``
  
  
``Array [QiSymbolSettings] SymbolSettings`` (optional)
  
  ::

  QiSymbolSettings {
    SymbolId (string, optional),
    ProviderSettings (object, optional)
  } 
  
  
``boolean IsEnabled``

``string Status`` = ['Undefined', 'InDevelopment', 'Running', 'InError']



Security
  Allowed by administrator and user accounts.

**Returns** 


  
**Status code**

*  400 - One of the arguments is invalid or a referenced dependent object does not exist.
*  401 - The user is not authorized to perform this operation.
*  500 - An unexpected error occurred.
*  504 - A timeout occurred while trying to execute the operation.
 

**********************

``GetCalculationsAsync()``
----------------------

Retrieves a list of QiCalculation objects in a namespace. 


**Syntax**

.. highlight:: none

::

    Task<IList<QiCalculation>> GetCalculationsAsync();

**Http**

::

   GET /qi/{tenantId}/{namespaceId}/Calculations


**Parameters**

``string Id``
  
 
``string name`` (optional)
  

``string Description`` (optional)
  

``string TypeId``
  

``string ScheduleId``
  
  
``Array [QiSymbolSettings] SymbolSettings`` (optional)
  
  ::

  QiSymbolSettings {
    SymbolId (string, optional),
    ProviderSettings (object, optional)
  } 
  
  
``boolean IsEnabled``

``string Status`` = ['Undefined', 'InDevelopment', 'Running', 'InError']



Security
  Allowed by administrator and user accounts.

**Returns** 


  
**Status code**

*  400 - One of the arguments is invalid or a referenced dependent object does not exist.
*  401 - The user is not authorized to perform this operation.
*  500 - An unexpected error occurred.
*  504 - A timeout occurred while trying to execute the operation.
 

**********************


``UpdateCalculationAsync()``
----------------------

Retrieves or inserts a QiCalculation in the specified namespace. 


**Syntax**

.. highlight:: none

::

    Task UpdateCalculationAsync(QiCalculation calculation);

**Http**

::

    PUT /qi/{tenantId}/{namespaceId}/Calculations


**Parameters**

``string Id``
  
 
``string name`` (optional)
  

``string Description`` (optional)
  

``string TypeId``
  

``string ScheduleId``
  
  
``Array [QiSymbolSettings] SymbolSettings`` (optional)
  
  ::

  QiSymbolSettings {
    SymbolId (string, optional),
    ProviderSettings (object, optional)
  } 
  
  
``boolean IsEnabled``

``string Status`` = ['Undefined', 'InDevelopment', 'Running', 'InError']



Security
  Allowed by administrator and user accounts.

**Returns** 


  
**Status code**

*  200 - The object was successfully updated.
*  400 - One of the arguments is invalid or a referenced dependent object does not exist.
*  401 - The user is not authorized to perform this operation.
*  500 - An unexpected error occurred.
*  504 - A timeout occurred while trying to execute the operation.
 

**********************


``DeleteCalculationAsync()``
----------------------

Removes a QiCalculation from a namespace. 


**Syntax**

.. highlight:: none

::

    Task DeleteCalculationAsync(string calculationId);

**Http**

::

   DELETE /qi/{tenantId}/{namespaceId}/Calculations/{calculationId}


**Parameters**

``string Id``
  
 
``string name`` (optional)
  

``string Description`` (optional)
  

``string TypeId``
  

``string ScheduleId``
  
  
``Array [QiSymbolSettings] SymbolSettings`` (optional)
  
  ::

  QiSymbolSettings {
    SymbolId (string, optional),
    ProviderSettings (object, optional)
  } 
  
  
``boolean IsEnabled``

``string Status`` = ['Undefined', 'InDevelopment', 'Running', 'InError']



Security
  Allowed by administrator and user accounts.

**Returns** 


  
**Status code**

*  200 - The object was successfully updated.
*  400 - One of the arguments is invalid or a referenced dependent object does not exist.
*  401 - The user is not authorized to perform this operation.
*  500 - An unexpected error occurred.
*  504 - A timeout occurred while trying to execute the operation.
 

**********************

``TestCalculationAsync()``
-----------------------

Runs a calculation in test mode. This method allows read calls to be sent to Qi while preventing write calls from 
being sent. All calls get stored in the AuditTrail.

**Syntax**

.. highlight:: none

::

    Task<QiCalculationTestResult> TestCalculationAsync(string calculationId, DateTime timestamp);
    
**Http**

::

    POST /qi/{tenantId}/{namespaceId}/Calculations/{calculationId}/Test

**Parameters**

``string TenantId``
  The Id of the tenant.

``string namespaceId``
  The Id of the namespace.

``string calculationId``
  The Id of the calculation to run in test mode.

``string timestamp``
  The time context to emulate.


Security
  Allowed by administrator and user accounts.

**Returns** 

::

  {
    "LogMessages": [
      {
        "TenantId": "string",
        "NamespaceId": "string",
        "Message": "string",
        "Timestamp": "string"
      }
    ],
    "ErrorMessages": [
      {
        "TenantId": "string",
        "NamespaceId": "string",
        "Message": "string",
        "Timestamp": "string"
      }
    ],
    "AuditTrail": [
      {
        "MethodName": "string",
        "Value": "string",
        "StreamId": "string",
        "Parameters": {},
        "Timestamp": "string"
      }
    ] 
  }
  
**Status code**

*  400 - One of the arguments is invalid or a referenced dependent object does not exist.
*  401 - The user is not authorized to perform this operation.
*  500 - An unexpected error occurred.
*  504 - A timeout occurred while trying to execute the operation.
 

