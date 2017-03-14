Qi compile and test calls
=========================

You use the API calls in this section compile Qi calculation scripts and to create test calls.


``CompileScriptAsync()``
-----------------------

Runs a calculation in test mode. This method allows read calls to be sent to Qi while preventing write calls from 
being sent. All calls get stored in the AuditTrail.

**Syntax**

.. highlight:: none

::

    Task<QiCalculationTestResult> TestCalculationAsync(string calculationId, DateTime timestamp);
    
**Http**

::

    POST qi/{tenantId}/{namespaceId}/Calculations/{calculationId}/Test

**Parameters**

``string TenantId``

``string NamespaceId``

``string Message``

``string Timestamp``
  

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
 

**********************

``CompileScriptAsync()``
----------------------

Compiles a script and, if errors exist, returns them as a string.

**Syntax**

.. highlight:: none

::

    Task<string> CompileScriptAsync(QiScript script, bool requireRunFunction);

**Http**

::

    POST qi/{tenantId}/{namespaceId}/Scripts/Compile


**Parameters**

``string tenantId``

``string namespaceId``

``boolean requireRun``

``script``
 
:: 

 {
    "Id": "string",
    "Name": "string",
    "Description": "string",
    "Source": "string",
    "Type": "Undefined",
    "HasEntryPoint": true,
    "Attributes": "None",
    "ReferencedScripts": [
      {
        "ScriptId": "string"
      }
    ]
  }  


Security
  Allowed by administrator and user accounts.

**Returns** 

::

  {
    "Id": "string",
    "Name": "string",
    "Description": "string",
    "Source": "string",
    "Type": "Undefined",
    "HasEntryPoint": true,
    "Attributes": "None",
    "ReferencedScripts": [
      {
        "ScriptId": "string"
      }
    ]
  }
  
  
**Status code**

*  201 - The object was successfully added.
*  400 - One of the arguments is invalid or a referenced dependent object does not exist.
*  500 - An unexpected error occurred.
*  504 - A timeout occurred while trying to execute the operation.
 

**********************



