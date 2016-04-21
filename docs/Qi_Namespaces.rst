Qi Namespaces
#############

A Qi tenant is divided into one or more Namespaces. Each Namespace is a logical entity 
within a tenant and holds its own set of Qi Types, Qi Streams, and Qi Stream Behaviors.
For more information see `Qi Architecture <https://qi-docs.readthedocs.org/en/latest/Introducing_Qi.html#architecture>`__.

Within a Qi Tenant you must have at least one Namespace in which to work.
You may create up to five namespaces within a tenant. If you use all five of your namespaces 
and want to create another, you can first delete an existing namespace and then create a new one. 
Contact OSIsoft if you require more than five namespaces within a tenant.

You can create, delete, or obtain information about your namespaces using the methods outlined in this topic.  Namespace management via the Qi Client Libraries is performed through the ``IQiAdministrationService`` interface, which may be accessed via the ``QiService.GetAdministrationService( )`` helper.

The following table shows the required and optional Qi namespace properties:

+---------------+-------------------------+----------------------------------------+
| Property      | Type                    | Details                                |
+===============+=========================+========================================+
| Id            | String                  | Required ID for referencing the        |
|               |                         | namespace                              | 
+---------------+-------------------------+----------------------------------------+

**Rules for namespaceId**

1. Not case sensitive
2. Spaces are allowed
3. Cannot start with two underscores ("\_\_")
4. Cannot contain forward slash or backslash characters ("/" or "\\")
5. Maximum length of 260 characters


``GetNamespace( )``
-------------------

Retrieves an existing namespace.

**Syntax**

.. highlight:: none

::

    Task<QiNamespace> GetNamespaceAsync(string namespaceId);

**Http**

::

    GET "Qi/{tenantId}/Namespaces/{namespaceId}”


**Parameters**

``string tenantId``
  The tenant identifier for the request
``string namespaceId``
  The namespace identifier for the request


Security
  Allowed by administrator and user accounts.

**Returns** 
  Returns a namespace.


``GetNamespaces( )``
----------------

Retrieves a list of existing namespaces.

**Syntax**

::

    Task<IEnumerable<QiNamespace>> GetNamespacesAsync();


*Http*

::

    GET "Qi/{tenantId}/Namespaces"


**Parameters**

``string tenantId``
  The tenant identifier for the request
``string namespaceId``
  The namespace identifier for the request
  
Security
  Allowed by administrator and user accounts.

**Returns**
  Returns a list of namespaces.


``GetOrCreateNamespace( )``
----------------

Returns the namespace with the specified namespaceId, or creates the namespace if the namespace does not already exist. 
If the namespace exists, it is returned to the caller unchanged. For security, this method is 
executable only by an administrator account.

::

    Task<QiNamespace> GetOrCreateNamespaceAsync(QiNamespace qinamespace);

**Http**

::

    POST "Qi/{tenantId}/Namespaces/"


**Parameters**

``string tenantId``
  The tenant identifier for the request.
``QiNamespace qinamespaceId``
  The QiNamespace object for which the request is being made.

**Security**
  Allowed by administrator account.

**Returns** 
  Returns a namespace.


``DeleteNamespace( )``
----------------

Deletes the namespace with the specified namespaceId from the tenant specified by the tenantId.

**Syntax**

::

    Task DeleteNamespaceAsync(string namespaceId);

**Http**

::

    DELETE "Qi/{tenantId}/Namespaces/{namespaceId}”

**Parameters**

``string tenantId``
  The tenant identifier for the request
``string namespaceId``
  The namespace identifier for the request
  

**Security** 
  Allowed by administrator account.

**Returns** 
  void
  
**Notes**
  You must have at least one namespace in a tenant. If a tenant contains only one namespace, the namespace cannot be deleted. 
  Deleting a namespace does not change the maximum number of allowed namespaces within a tenant. 
