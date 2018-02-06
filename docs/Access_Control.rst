Granular access control 
=======================

Within OCS, granular access control to entities such as Namespaces, Documents, Streams, and so on, is managed using an Access 
Control List (ACL) and an Owner object. 


Access Control Lists
--------------------

You use access control lists (ACLs) to control access to entities. Entities are assigned owners. 
Currently only users and applications are valid owners for entities. Roles are made up from a set of access control 
entries each with a trustee, AccessType, and AccessRights.

A user or application that attempts to read, write, delete, or manage access control of an entity using an access control list 
must be assigned a role that has ``AccessType`` set to ``Allowed`` for that operation. 

AccessRights are the bitwise union of all of the access rights they encompass. For example, ``AccessRights 3`` indicates that
Read and Write access is permitted. 

Roles are currently the only TrusteeType supported for AccessControlLists. Currently only Users and Applications are valid owners for entities.

*Note*
  If an operation requires more than one access right then an identity can obtain 
  those rights from multiple ACL entries.
	
*Note*
  ``AccessType.Denied`` takes precedence over ``Allowed``. For example, a role that is assigned ``AccessType.Denied`` for
  ``AccessRights.All`` will receive a forbidden for all  requests unless they are the owner of the entity.


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
entity's ACL's AccessControlEntries. 

Currently only Users and Applications are valid owners for entities.  

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


