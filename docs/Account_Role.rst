Role
=======================================================

A Role is an entity that is used to authorize API requests.

	The following code shows the JSON-serialized Role object for HTTP requests and responses:

.. _RoleObj: 

.. highlight:: C#

::

 {
	"Id": "id",                            //GUID for this Role. Generated by the server upon Creation.
	"Name": "name",                        //Name of this Role.
	"Description": "description",          //Description of this Role.
	"RoleScope": 0,                        //Scope of this Role.
	"TenantId": "tenantid",                //GUID of Tenant for this Role, if this is a Account Role, null otherwise.
	"CommunityId": "communityid",          //GUID of Community for this Role, if this is a Community Role, null otherwise.
	"RoleTypeId": "roletypeid"             //GUID of Role Type for this Role, if this is a Account Role and is not a customer defined Role.
 }

``GetAccountRole()``
--------------------------------------------------------------------

Retrieves an Account Role based on the specified Account Id and Role Id.

**Http**

::

	GET api/Tenants/{tenantId}/Roles/{roleId}

**Parameters**

``String tenantId``
	The Account identifier for this request
``String roleId``
	The Role identifier for this request

**Security**
	Allowed by Account Administrator :ref:`Role <RoleObj>`

**Returns**
	The :ref:`Role <RoleObj>` with Id roleId



|

**********************

``GetAccountRoles()``
--------------------------------------------------------------------

Retrieves all Account Roles for the specified Account Id.

**Http**

::

	GET api/Tenants/{tenantId}/Roles

**Parameters**

``String tenantId``
	The Account identifier for this request
``String skip``
	Number of :ref:`Role <RoleObj>` to ignore
``String count``
	Number of :ref:`Role <RoleObj>` to be returned
``String query``
	Unsupported parameter

**Security**
	If the current principle has a Cluster role or is an Account Administrator for the specified Account

**Returns**
	An array of :ref:`Role <RoleObj>` objects 



|

**********************

``GetCommunityRoles()``
--------------------------------------------------------------------

Retrieces all Community Roles for the specified Community Id.

**Http**

::

	GET api/Communities/{communityId}/Roles

**Parameters**

``String communityId``
	The Account identifier for this request
``String skip``
	Number of :ref:`Role <RoleObj>` to ignore
``String count``
	Number of :ref:`Role <RoleObj>` to be returned
``String query``
	Unsupported parameter

**Security**
	If the current principle has a Cluster role or is a Community Lead for the specified Community

**Returns**
	An array of :ref:`Role <RoleObj>` objects 



|

**********************


