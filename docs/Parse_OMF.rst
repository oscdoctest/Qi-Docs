Using OMF with Cloud Services
=============================

This document describes how the OSIsoft Message Format (OMF) is interpreted by OSIsoft Cloud Services (OCS) backend system. 

Headers
-------

A description of each of the headers can be found in the OMF documentation located here. When 
sending messages to OSIsoft Cloud Services, the value of the ``producertoken`` header must be 
set to a security token obtained from the OCS Portal. This security token is used to authenticate 
the sender and authorize for use with a particular Tenant and Device.

Message Types
-------------

OMF message types fall into three categories: Type, Container, and Data. 





