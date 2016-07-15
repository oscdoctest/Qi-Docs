Qi Calculations
==========

You use the API calls in this section create, delete, and manage scripts.


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

``DeleteScriptAsync()``
----------------------


Removes a script from the specified namespace. 


**Syntax**

.. highlight:: none

::

    Task DeleteScriptAsync(string scriptId);

**Http**

::

    DELETE /qi/{tenantId}/{namespaceId}/Scripts/{scriptId}


**Parameters**

``string Id``
  Unique Id for this script. Used when referencing this script in other objects such as calculation types or other scripts.
 

Security
  Allowed by administrator and user accounts.

**Returns** 

::


  
  
**Status code**

*  200 - OK
*  400 - BadRequest
*  500 - InternalServerError
 

**********************

``GetScriptAsync()``
----------------------

Retrieves a script from the namespace with the specified Id.  


**Syntax**

.. highlight:: none

::

    Task<QiScript> GetScriptAsync(string scriptId);

**Http**

::

    GET /qi/{tenantId}/{namespaceId}/Scripts/{scriptId}


**Parameters**

``string Id``
  Unique Id for this script. Used when referencing this script in other objects such as calculation types or other scripts.
 
``string name``
  A Name for this script.

``string Description`` (optional)
  A Discription of this script.

``string Source``
  The source code or implementation that represents the script.

``string Type``
  The language used to write the sript = ['JavaScript', 'TypeScript']

``Array[QiScriptReference] ReferencedScripts`` (optional)
  Scripts that must be included when compiling and running this script.
 

Security
  Allowed by administrator and user accounts.

**Returns** 

::


  
**Status code**

*  400 - BadRequest
*  404 - NotFound
*  500 - InternalServerError
 

**********************

``GetScriptsAsync()``
----------------------


Retrieves a list of scripts from the specified namespace. 


**Syntax**

.. highlight:: none

::

    Task<QiScript> GetScriptsAsync(string scriptId);

**Http**

::

    GET /qi/{tenantId}/{namespaceId}/Scripts


**Parameters**

``string Id``
  Unique Id for this script. Used when referencing this script in other objects such as calculation types or other scripts.
 
``string name``
  A Name for this script.

``string Description`` (optional)
  A Discription of this script.

``string Source``
  The source code or implementation that represents the script.

``string Type``
  The language used to write the sript = ['JavaScript', 'TypeScript']

``Array[QiScriptReference] ReferencedScripts`` (optional)
  Scripts that must be included when compiling and running this script.
 

Security
  Allowed by administrator and user accounts.

**Returns** 

::


  
**Status code**

*  400 - BadRequest
*  404 - NotFound
*  500 - InternalServerError
 

**********************

``UpdateScriptAsync()``
----------------------

Updates a script in the specified namespace. 


**Syntax**

.. highlight:: none

::

    Task UpdateScriptAsync(QiScript script);

**Http**

::

    PUT /qi/{tenantId}/{namespaceId}/Scripts


**Parameters**

``string Id``
  Unique Id for this script. Used when referencing this script in other objects such as calculation types or other scripts.
 
``string name``
  A Name for this script.

``string Description`` (optional)
  A Discription of this script.

``string Source``
  The source code or implementation that represents the script.

``string Type``
  The language used to write the sript = ['JavaScript', 'TypeScript']

``Array[QiScriptReference] ReferencedScripts`` (optional)
  Scripts that must be included when compiling and running this script.
 

Security
  Allowed by administrator and user accounts.

**Returns** 

::

  QiScript {Id (string): Unique Id for this script. Used when referencing this script in other objects such as calculation types or other scripts.
  Name (string): A Name for this script.
  Description (string, optional): A Discription of this script.
  Source (string): The source code or implementation that represents the script.
  Type (string): The language used to write the sript.
  = ['JavaScript', 'TypeScript']
  ReferencedScripts (Array[QiScriptReference], optional): Scripts that must be included when compiling and running this script.
  }
  QiScriptReference {
  ScriptId (string): The unique Id of the {OSIsoft.Qi.Calculation.Core.QiScript}
} 

  
  
**Status code**

*  200 - OK
*  400 - BadRequest
*  500 - InternalServerError
 


