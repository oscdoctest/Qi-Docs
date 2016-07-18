Qi Calculations
==========

You use the API calls in this section create, delete, and manage calculations.


``GetOrCreateCalculationAsync()``
----------------------

Retrieves or inserts a QiCalculation in the specified namespace. 


**Syntax**

.. highlight:: none

::

    Task<QiCalculation> GetOrCreateCalculationAsync(QiCalculation calculation);

**Http**

::

    POST /qi/{tenantId}/{namespaceId}/Calculations


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

*  201 - The object was added successfully
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
