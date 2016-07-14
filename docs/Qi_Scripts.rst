Qi Scripts
==========

The API calls in this section are all used to create, delete, and manage scripts.

``GetOrCreateScriptAsync()``
----------------------

Inserts a new script into the specified namespace. The script can be used by calculations. 


**Syntax**

.. highlight:: none

::

    Task DeletePeriodicScheduleAsync(string scheduleId);

**Http**

::

    DELETE /qi/{tenantId}/{namespaceId}/Schedules/Periodic/{scheduleId}


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
 

**********************

