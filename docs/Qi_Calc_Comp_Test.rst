Qi test API calls
=========================

You use the API calls in this section create test calls for your scripts.


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

``TestCalculationAsync()``
-----------------------

Runs a calculation template in test mode. This method allows read calls to be sent to Qi while preventing write calls from 
being sent. All calls get stored in the AuditTrail.

**Syntax**

.. highlight:: none

::

    TestCalculationTemplateAsync(string templateId, DateTime timestamp, IList<QiStreamAlias> streamAliases);
    
**Http**

::

  POST /qi/{tenantId}/{namespaceId}/CalculationTemplates/{templateId}/Test


**Parameters**

``string TenantId``

``string NamespaceId``

``string Message``

``streamAliases``
  
::

  [
    {
      "AliasId": "string",
      "StreamId": "string",
      "NamespaceId": "string",
      "TenantId": "string"
    }
  ]

Security
  Allowed by administrator and user accounts.

**Returns** 

::

  QiTestModeResult {
    LogMessages (Array[QiTestModeMessage], optional): List of console.log outputs ,
    ErrorMessages (Array[QiTestModeMessage], optional): List of console.error outputs ,
    AuditTrail (Array[QiTestModeAuditData], optional): List of Qi RPCs that were called
  }
  QiTestModeMessage {
    TenantId (string, optional): The Id of the Tenant ,
    NamespaceId (string, optional): The Id of the Namespace ,
    Message (string, optional): The message that was output to the console ,
    Timestamp (string, optional): The timestamp when the console output occurred
  }
  QiTestModeAuditData {
    MethodName (string, optional): Method that was run ,
    Value (string, optional): Value that was sent in body ,
    StreamId (string, optional): The Id of the Stream the method requested ,
    Parameters (object, optional): Other parameters that were sent with request ,
    Timestamp (string, optional): Time the audit was created
  }


**Status code**

*  400 - One of the arguments is invalid or a referenced dependent object does not exist.
*  401 - The user is not authorized to perform this operation.
*  500 - An unexpected error occurred.
*  504 - A timeout occurred while trying to execute the operation.
 

**********************

