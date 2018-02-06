Granular Access Control 
=======================

Entities (e.g. Namespaces, Documents, Streams...) in the OCS system support granular access control through the use of an AccessControlList and Owner. 



AccessControlLists
--------------------

AccessControlLists control access to an entity based on a Identity's (User or Application) set of roles.
They consist of a set of access control entries each with a trustee, AccessType, and AccessRights.
A user or application attempting to Read/Write/Delete/ManageAccessControl a entity with an access control list must be assigned 
a role with Allowed AccessType for that operation. 
AccessRights are the bitwise union of all the access rights they encompass (i.e. AccessRights 3 means Read or Write. 
Roles are currently the only TrusteeType supported for AccessControlLists.

*Note*
	If an operation requires more than one access right then an identity can obtain those rights from multiple AccessControlEntries.
	
*Note*
	AccessType.Denied takes precedence over Allowed (e.g. an role assigned AccessType.Denied for AccessRights.All will receive a forbidden for all
	requests unless they are the owner of the entity)

=======================  =====
TrusteeType              TypeId
-----------------------  -----
User 						1
Role 						3
Application					4
=======================  =====

=======================  =====
AccessType               TypeId
-----------------------  -----
Allowed						0
Denied						1
=======================  =====

=======================  ===== ==========
AccessRights              int   bitwise
-----------------------  ----- ----------
None						0	0000
Read						1	0001
Write						2	0010
Delete						4	0100
ManageAccessControl			8	1000
All							15	1111
=======================  ===== =========


**Body**
  
  Sample  body:
  
::

  HTTP/1.1 200
  Content-Type: application/json

  "AccessControlList": {
	"RoleTrusteeAccessControlEntries": [
		{
			"Trustee": {
				"Type": 3,
				"RoleId": "55555555-5555-5555-5555-555555555551"
			},
			"AccessType": 0,
			"AccessRights": 3
		},
		{
			"Trustee": {
				"Type": 3,
				"RoleId": "55555555-5555-5555-5555-555555555552"
			},
			"AccessType": 0,
			"AccessRights": 15
		},
		{
			"Trustee": {
				"Type": 3,
				"RoleId": "55555555-5555-5555-5555-555555555553"
			},
			"AccessType": 0,
			"AccessRights": 1
		}
	],
	}
	
Owner
--------------------
Owner objects on OCS entities grant access for all operations on the entity regardless of the entity's AccessControlList's AccessControlEntries. 
Currently only Users and Applications are valid owners for entities.  

**User Owner Body**

::
	"Owner": {
		"Type": 1,
		"TenantId": "55555555-5555-5555-5555-555555555555",
		"ObjectId": "55555555-5555-5555-5555-555555555551"
	},
	
**Application Owner Body**

::
	"Owner": {
		"Type": 4,
		"TenantId": "55555555-5555-5555-5555-555555555555",
		"ApplicationId": "55555555-5555-5555-5555-555555555551"
	},

