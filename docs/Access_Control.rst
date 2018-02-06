Granular access control 
=======================

Within OCS, granular access control to entities such as Namespaces, Streams, and so on, is managed using an Access Control 
List (ACL) and an Owner object assigned to each entity. ACLs control access to entities based on their OCS Roles. Owners 
are granted access for all operations regardless of the contents of the ACL. Not all entities in the OCS system support 
granular access control at this time, but the list will quickly grow and currently includes Namespaces and several unreleased 
entities.


Access Control Lists
--------------------

Access Control Lists (ACLs) contain sets of Access Control Entries (ACEs) each with a trustee (reference to an identity, such 
as a role, user, or application), AccessType, and AccessRights. 

A user or application that attempts to read, write, delete, or manage access control of an entity assigned an ACL must be 
assigned a trustee that has ``AccessType`` set to ``Allowed`` for that right corresponding to that operation.

AccessRights are the bitwise union of all of the access rights they encompass. For example, ``AccessRights 3`` indicates 
that Read and Write access is permitted.

*Note*
  If an operation requires more than one access right then an identity can obtain 
  those rights from multiple ACL entries.
	
*Note*
  ``AccessType.Denied`` takes precedence over ``Allowed``. For example, a role that is assigned ``AccessType.Denied`` for
  ``AccessRights.All`` will receive a ``forbidden`` for all  requests unless they are the owner of the entity.
  
*Note*
  Currently, Roles are the only TrusteeType supported for AccessControlList ACEs.



=======================  =====
TrusteeType              TypeId
-----------------------  -----
User                     1
Role                     3
Application              4
=======================  =====

=======================  =====
AccessType               TypeId
-----------------------  -----
Allowed                  0
Denied                   1
=======================  =====


+-----------------------+------+---------+
| AccessRights          | int  | bitwise |
+=======================+======+=========+
| None                  | 0    |    0000 |
+-----------------------+------+---------+
| Read                  | 1    |    0001 |
+-----------------------+------+---------+
| Write                 | 2    |    0010 |
+-----------------------+------+---------+
| Delete                | 4    |    0100 |
+-----------------------+------+---------+
| ManageAccessControl   | 8    |    1000 |
+-----------------------+------+---------+
| All                   | 15   |    1111 |
+=======================+======+=========+

The following code sample shows the structure and format for an ACL:

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
-----

Owner objects on OCS entities are used to grant access for all operations on the entity regardless of the 
entity's AccessControlList's AccessControlEntries. 

*Note*
  Currently, only Users and Applications are valid owners for entities.  

The following code sample shows the format and structure of an owner object:


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


