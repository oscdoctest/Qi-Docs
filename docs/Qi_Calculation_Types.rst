Qi Calculation templates
========================

The APIs in this topic are used to create, delete, and update Qi calculation templates



``GetOrCreateTemplateAsync()``
----------------------------

Retrieves the QiCalculationTemplate from the specified namespaceId, or creates the QiCalculationTemplate if it does not already exist. If the QiCalculationTemplate exists, it is returned to the caller unchanged.


**Syntax**

.. highlight:: none

::

    Task<QiCalculationTemplate> GetOrCreateTemplateAsync(QiCalculationTemplate template);

**Http**

::

    POST /qi/{tenantId}/{namespaceId}/CalculationTemplates


**Parameters**

``string Id`` (optional)
  
``string Id``
  Unique Id for this calculation template. Used when referencing this calculation template or retrieving it.

``string Name`` (optional)
  A name for this calculation template.
  
``string Description`` (optional)
  A description for this calculation template.
  
``QiScriptReference ScriptReference``
  A {OSIsoft.Qi.Calculation.Core.QiScriptReference} containing enough information to locate the corresponding script.

``Array[string] StreamAliasIds`` (optional)
  The symbols that this calculation template uses.
  
``Array[QiStreamAlias] DefaultStreamAliases`` (optional)
  A list of default alias mappings used when the aliases have not been resolved by the calculation.
  
``IQiSchedule DefaultSchedule`` (optional)
  The schedule used to determine how the calculation is dispatched. This schedule can be overridden on the calculation.
  
``string Trigger``
  The trigger type for this calculation template = ['Undefined', 'PeriodicSchedule', 'EventTriggeredSchedule', 'Manual']

  ::

  QiScriptReference {
    ScriptId (string): The unique Id of the {OSIsoft.Qi.Calculation.Core.QiScript}
  }
  QiStreamAlias {
    AliasId (string): The Id of the alias being mapped. ,
    StreamId (string): The Id of the stream. ,
    NamespaceId (string, optional): The Id of the namespace. If , then the namespace the calculation resides within will be used. ,
    TenantId (string, optional): The Id of the tenant. If , then the tenant the calculation resides within will be used.
}
  IQiSchedule {
    ScheduleType (string, optional, read only): Returns the type of schedule the data contract implements. 
      = ['Undefined', 'Periodic', 'EventTriggered', 'Manual']} 



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

``GetTemplateAsync()``
----------------------

Retrieves a QiCalculationTemplate from a namespace. 


**Syntax**

.. highlight:: none

::

    Task<QiCalculationTemplate> GetTemplateAsync(string templateId);

**Http**

::

   GET /qi/{tenantId}/{namespaceId}/CalculationTemplates/{templateId}


**Parameters**

``string Id`` (optional)
  
``string Id``
  Unique Id for this calculation template. Used when referencing this calculation template or retrieving it.

``string Name`` (optional)
  A name for this calculation template.
  
``string Description`` (optional)
  A description for this calculation template.
  
``QiScriptReference ScriptReference``
  A {OSIsoft.Qi.Calculation.Core.QiScriptReference} containing enough information to locate the corresponding script.

``Array[string] StreamAliasIds`` (optional)
  The symbols that this calculation template uses.
  
``Array[QiStreamAlias] DefaultStreamAliases`` (optional)
  A list of default alias mappings used when the aliases have not been resolved by the calculation.
  
``IQiSchedule DefaultSchedule`` (optional)
  The schedule used to determine how the calculation is dispatched. This schedule can be overridden on the calculation.
  
``string Trigger``
  The trigger type for this calculation template = ['Undefined', 'PeriodicSchedule', 'EventTriggeredSchedule', 'Manual']

  ::

  QiScriptReference {
    ScriptId (string): The unique Id of the {OSIsoft.Qi.Calculation.Core.QiScript}
  }
  QiStreamAlias {
    AliasId (string): The Id of the alias being mapped. ,
    StreamId (string): The Id of the stream. ,
    NamespaceId (string, optional): The Id of the namespace. If , then the namespace the calculation resides within will be used. ,
    TenantId (string, optional): The Id of the tenant. If , then the tenant the calculation resides within will be used.
}
  IQiSchedule {
    ScheduleType (string, optional, read only): Returns the type of schedule the data contract implements. 
      = ['Undefined', 'Periodic', 'EventTriggered', 'Manual']} 


Security
  Allowed by administrator and user accounts.

**Returns** 


  
**Status code**

*  400 - One of the arguments is invalid or a referenced dependent object does not exist.
*  401 - The user is not authorized to perform this operation.
*  500 - An unexpected error occurred.
*  504 - A timeout occurred while trying to execute the operation.
 

**********************

``GetTemplatesAsync()``
----------------------

Retrieves a list of QiCalculationTemplate objects in a namespace.


**Syntax**

.. highlight:: none

::

    Task<IList<QiCalculationTemplate>> GetTemplatesAsync();

**Http**

::

   GET /qi/{tenantId}/{namespaceId}/CalculationTemplates


**Parameters**

``string Id``
  Unique Id for this calculation template. Used when referencing this calculation template or retrieving it.

``string Name`` (optional)
  A name for this calculation template.
  
``string Description`` (optional)
  A description for this calculation template.
  
``QiScriptReference ScriptReference``
  A {OSIsoft.Qi.Calculation.Core.QiScriptReference} containing enough information to locate the corresponding script.

``Array[string] StreamAliasIds`` (optional)
  The symbols that this calculation template uses.
  
``Array[QiStreamAlias] DefaultStreamAliases`` (optional)
  A list of default alias mappings used when the aliases have not been resolved by the calculation.
  
``IQiSchedule DefaultSchedule`` (optional)
  The schedule used to determine how the calculation is dispatched. This schedule can be overridden on the calculation.
  
``string Trigger``
  The trigger type for this calculation template = ['Undefined', 'PeriodicSchedule', 'EventTriggeredSchedule', 'Manual']

  ::

  QiScriptReference {
    ScriptId (string): The unique Id of the {OSIsoft.Qi.Calculation.Core.QiScript}
  }
  QiStreamAlias {
    AliasId (string): The Id of the alias being mapped. ,
    StreamId (string): The Id of the stream. ,
    NamespaceId (string, optional): The Id of the namespace. If , then the namespace the calculation resides within will be used. ,
    TenantId (string, optional): The Id of the tenant. If , then the tenant the calculation resides within will be used.
}
  IQiSchedule {
    ScheduleType (string, optional, read only): Returns the type of schedule the data contract implements. 
      = ['Undefined', 'Periodic', 'EventTriggered', 'Manual']} 



Security
  Allowed by administrator and user accounts.

**Returns** 


  
**Status code**

*  400 - One of the arguments is invalid or a referenced dependent object does not exist.
*  401 - The user is not authorized to perform this operation.
*  500 - An unexpected error occurred.
*  504 - A timeout occurred while trying to execute the operation.
 

**********************



``UpdateTemplateAsync()``
----------------------

Updates an existing QiCalculationTemplate in a namespace. 


**Syntax**

.. highlight:: none

::

    Task UpdateTemplateAsync(QiCalculationTemplate template);

**Http**

::

   PUT /qi/{tenantId}/{namespaceId}/Calculationemplates


**Parameters**

``string Id``
  Unique Id for this calculation template. Used when referencing this calculation template or retrieving it.

``string Name`` (optional)
  A name for this calculation template.
  
``string Description`` (optional)
  A description for this calculation template.
  
``QiScriptReference ScriptReference``
  A {OSIsoft.Qi.Calculation.Core.QiScriptReference} containing enough information to locate the corresponding script.

``Array[string] StreamAliasIds`` (optional)
  The symbols that this calculation template uses.
  
``Array[QiStreamAlias] DefaultStreamAliases`` (optional)
  A list of default alias mappings used when the aliases have not been resolved by the calculation.
  
``IQiSchedule DefaultSchedule`` (optional)
  The schedule used to determine how the calculation is dispatched. This schedule can be overridden on the calculation.
  
``string Trigger``
  The trigger type for this calculation template = ['Undefined', 'PeriodicSchedule', 'EventTriggeredSchedule', 'Manual']

  ::

  QiScriptReference {
    ScriptId (string): The unique Id of the {OSIsoft.Qi.Calculation.Core.QiScript}
  }
  QiStreamAlias {
    AliasId (string): The Id of the alias being mapped. ,
    StreamId (string): The Id of the stream. ,
    NamespaceId (string, optional): The Id of the namespace. If , then the namespace the calculation resides within will be used. ,
    TenantId (string, optional): The Id of the tenant. If , then the tenant the calculation resides within will be used.
}
  IQiSchedule {
    ScheduleType (string, optional, read only): Returns the type of schedule the data contract implements. 
      = ['Undefined', 'Periodic', 'EventTriggered', 'Manual']} 



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


``DeleteTemplateAsync()``
----------------------

Removes a QiCalculationTemplate from a namespace. 


**Syntax**

.. highlight:: none

::

    Task DeleteTemplateAsync(string templateId);

**Http**

::

    DELETE /qi/{tenantId}/{namespaceId}/CalculationTemplates/{templateId}


**Parameters**

``string tenantId``
  The Id of the tenant.

``string namespaceiD``
  The Id of the namespace.
  
``string templateId``
  The Id of the template.
  


Security
  Allowed by administrator and user accounts.

**Returns** 


  
**Status code**

*  400 - One of the arguments is invalid or a referenced dependent object does not exist.
*  401 - The user is not authorized to perform this operation.
*  500 - An unexpected error occurred.
*  504 - A timeout occurred while trying to execute the operation.
 

**********************

