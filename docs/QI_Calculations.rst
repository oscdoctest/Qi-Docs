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

``string namespaceId``
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

Inserts or updates a package of scripts, types, schedules, and calculations

**Syntax**

.. highlight:: none

::

    Task AddCalculationsAsync(IList<QiCalculation> calculations);

**Http**

::

    POST /qi/{tenantId}/{namespaceId}/Calculations/$Batch


**Parameters**

``string tenantId``
  The Id of the tenant.

``string namespaceId``
  The Id of the Namespace

``calculation``
  The calculation to insert
  
::

  QiCalculationPackage {
    Scripts (Array[QiScript], optional): A list of QiScript objects to create or update. Validation is bypassed. ,
    Templates (Array[QiCalculationTemplate], optional): A list of QiCalculationTemplate objects to create or 
    update. Validation is bypassed. ,
    Calculations (Array[QiCalculation], optional): A list of QiCalculation objects to create or update. 
    Validation is bypassed unless, the Status is Enabled.
  }
  QiScript {
    Id (string): Unique Id for this script. Used when referencing this script in other objects such 
    as calculation types or other scripts. ,
    Name (string, optional): A Name for this script. ,
    Description (string, optional): A Description of this script. ,
    Source (string): The source code or implementation that represents the script. ,
    Type (string): The language used to write the script. = ['Undefined', 'JavaScript', 'TypeScript'],
    HasEntryPoint (boolean): Flag to say whether script has an entry point ,
    Attributes (string, optional): Flags that contain script attributes = ['None', 'CompilationSucceeded', 'HasEntryPoint'],
    ReferencedScripts (Array[QiScriptReference], optional): Scripts that must be included when compiling and running this script.
  }
  QiCalculationTemplate {
    Id (string): Unique Id for this calculation type. Used when referencing this calculation type or retrieving it. ,
    Name (string, optional): A name for this calculation type. ,
    Description (string, optional): A description for this calculation type. ,
    ScriptReference (QiScriptReference): A {OSIsoft.Qi.Calculation.Core.QiScriptReference} containing 
    enough information to locate the corresponding script. ,
    StreamAliasIds (Array[string], optional): The symbols that this calculation type uses. ,
    DefaultStreamAliases (Array[QiStreamAlias], optional): A list of default alias mappings used when 
    the aliases have not been resolved by the calculation. ,
    DefaultSchedule (IQiSchedule, optional): The scheduled used to determine how the calculation is 
    dispatched. This schedule can be overridden on the calculation. ,
    Trigger (string): The trigger type for this calculation type. 
      = ['Undefined', 'PeriodicSchedule', 'EventTriggeredSchedule', 'Manual']
  }
  QiCalculation {
    Id (string): Unique Id for this calculation. Used when referencing this calculation or retrieving it. ,
    Name (string, optional): A name for this calculation. ,
    Description (string, optional): A description of what this calculation does. ,
    TemplateId (string): The template to be used for this calculation. ,
    Schedule (IQiSchedule, optional): The scheduled used to determine how the calculation is 
    dispatched. If , then the schedule on the template will be used. ,
    StreamAliases (Array[QiStreamAlias], optional): A list of stream aliases used to map streams 
    to the alias Ids on the template. ,
    Status (string): Status of the calculation. = ['Undefined', 'InDevelopment', 'Enabled', 'InError']
  }
  QiScriptReference {
    ScriptId (string): The unique Id of the {OSIsoft.Qi.Calculation.Core.QiScript}
  }
  QiStreamAlias {
    AliasId (string): The Id of the alias being mapped. ,
    StreamId (string): The Id of the stream. ,
    NamespaceId (string, optional): The Id of the namespace. If , then the namespace the 
    calculation resides within will be used. ,
    TenantId (string, optional): The Id of the tenant. If , then the tenant the calculation resides within will be used.
  }
  IQiSchedule {
    ScheduleType (string, optional, read only): Returns the type of schedule the data contract 
    implements. = ['Undefined', 'Periodic', 'EventTriggered', 'Manual']
  }



Security
  Allowed by administrator and user accounts.

**Returns** 



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

``string tenantId``
  The Id of the tenant.

``string namespaceId``
  The Id of the Namespace

``calculation``
  The Id of the calculation
  

Security
  Allowed by administrator and user accounts.

**Returns** 

::

  QiCalculation {
    Id (string): Unique Id for this calculation. Used when referencing this calculation or retrieving it. ,
    Name (string, optional): A name for this calculation. ,
    Description (string, optional): A description of what this calculation does. ,
    TemplateId (string): The template to be used for this calculation. ,
    Schedule (IQiSchedule, optional): The scheduled used to determine how the calculation 
    is dispatched. If , then the schedule on the template will be used. ,
    StreamAliases (Array[QiStreamAlias], optional): A list of stream aliases used to map streams 
    to the alias Ids on the template. ,
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

``string tenantId``
  The Id of the tenant.

``string namespaceId``
  The Id of the Namespace

``templateId`` (optional)
  Query string parameter. If this parameter is set, only calculations with the specified template are returned.


Security
  Allowed by administrator and user accounts.

**Returns** 

::

  QiCalculation {
    Id (string): Unique Id for this calculation. Used when referencing this calculation or retrieving it. ,
    Name (string, optional): A name for this calculation. ,
    Description (string, optional): A description of what this calculation does. ,
    TemplateId (string): The template to be used for this calculation. ,
    Schedule (IQiSchedule, optional): The scheduled used to determine how the calculation 
    is dispatched. If , then the schedule on the template will be used. ,
    StreamAliases (Array[QiStreamAlias], optional): A list of stream aliases used to map streams 
    to the alias Ids on the template. ,
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
  
**Status code**

*  400 - One of the arguments is invalid or a referenced dependent object does not exist.
*  401 - The user is not authorized to perform this operation.
*  500 - An unexpected error occurred.
*  504 - A timeout occurred while trying to execute the operation.
 

**********************


``UpdateCalculationAsync()``
----------------------

Updates an existing QiCalculation in a namespace


**Syntax**

.. highlight:: none

::

    Task UpdateCalculationAsync(QiCalculation calculation);

**Http**

::

    PUT /qi/{tenantId}/{namespaceId}/Calculations


**Parameters**

``string tenantId``
  The Id of the tenant.

``string namespaceId``
  The Id of the Namespace

``QiClaculation calculation``
  The calculation to update.


Security
  Allowed by administrator and user accounts.

**Returns** 

::

  QiCalculation {
    Id (string): Unique Id for this calculation. Used when referencing this calculation or retrieving it. ,
    Name (string, optional): A name for this calculation. ,
    Description (string, optional): A description of what this calculation does. ,
    TemplateId (string): The template to be used for this calculation. ,
    Schedule (IQiSchedule, optional): The scheduled used to determine how the calculation 
    is dispatched. If , then the schedule on the template will be used. ,
    StreamAliases (Array[QiStreamAlias], optional): A list of stream aliases used to map streams 
    to the alias Ids on the template. ,
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

``string tenantId``
  The Id of the tenant.

``string namespaceId``
  The Id of the Namespace

``QiClaculation calculation``
  The Id of the calculation.




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
 

