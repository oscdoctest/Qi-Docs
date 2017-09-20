OMF Ingress into Cloud Services
===============================

High-throughput asynchronous data ingress into the OCS data store is achieved 
with the help of messages crafted using the OSIsoft Message Format (OMF).
A producer of OMF messages for OCS is called a Publisher and the messages
are sent to a queue called a Topic. A Subscription recieves messages from
a Topic and either writes them to the OCS data store, or makes them available
to an external consumer. 

.. toctree::
   OMF_Ingress_Specification.rst