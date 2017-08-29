Quick start
###########

.. contents:: Topics in this section:
    :depth: 3

Qi quick start
--------------

Qi is a sophisticated data store. The information in this section describes a very simple interaction with Qi.
To follow along with the steps in this section, you will first need a Tenant and associated security credentials. 
If you have not already acquired a tenant, email Qi support at: `OSIsoft Cloud Services <cloudservices@osisoft.com>`__.

The Preview is limited; contacting OSIsoft does not assure participation. 

Throughout this guide, you will be instructed to interact with the Portal. To access the section 
identified, you must sign into the Portal using the credentials associated with the Tenant.

You will also need a Namespace and administrative client keys.  See Namespace information and API Client Keys.


Step 1: Acquire a Namespace
**************************

`Architecture <https://qi-docs-rst.readthedocs.org/en/latest/Introducing_Qi.html#architecture>`__

Navigate to the OSIsoft Cloud Services page. Then, select the Manage tab and select Namespaces. For the 
steps in this section, you can use either an existing Namespace or you can create a new Namespace.


Step 2: Acquire client keys
***************************

For this example, the application acts as a confidential client – an application that is capable 
of securely maintaining a secret. In Azure Active Directory, the confidential client authentication 
flow is accomplished via an Application Identity. OSIsoft Cloud Services supports this authentication 
with Client Key and Secret.

To acquire the Client Key from the portal, select Client Keys under Manage, as shown in the following image:

.. image:: images/Acquire_Client_Key.png

You can either select an existing key or create a new key. Click the eye icon next to the desired key 
to see configuration information. You will need the Tenant Identity, Client Identity and Client Secret.  
These will be used to acquire a security Token from an identity provider, Azure Active Directory.




