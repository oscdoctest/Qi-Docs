.. _Qi_Stream_topic:

QiStream information
====================

Qi stores collections of events and provides convenient ways to find and associating events. Events 
of consistent structure are stored in streams, called QiStreams.  A QiType defines the structure 
of events in a QiStream.

QiStreams are referenced by their identifier or Id field. QiStream identifiers must be unique 
within a Namespace.

A QiStream must include a TypeId that references the identifier of an existing QiType. Once 
they contain data, QiStreams are immutable. The type of the stream cannot be replaced.

Behavior determines read characteristics on the stream. If BehaviorId is omitted, the default 
behavior mode is set to continuous and extrapolation is set to all. Set the BehaviorId field 
to the identifier of an existing QiStreamBehavior. See 
`QiStreamBehaviors <https://qi-docs-rst.readthedocs.org/en/latest/Qi_Stream_Behavior.html>`__ 
for more information.

QiStream management using the .NET Qi Client Libraries is performed through IQiMetadataService. 
Create the IQiMetadataService, using one of the ``QiService.GetMetadataService()`` factory methods.

The following table shows the required and optional QiStream fields. Fields not listed are reserved
for internal Qi use. 


+---------------+------------------------------+-------------+----------------------------------------------+
| Property      | Type                         | Optionality |Details                                       |
+===============+==============================+=============+==============================================+
| Id            | String                       | Required    | An identifier for referencing the stream.    |
+---------------+------------------------------+-------------+----------------------------------------------+
| TypeId        | String                       | Required    | The QiType identifier of the type to be      |
|               |                              |             | used for this stream.                        |
+---------------+------------------------------+-------------+----------------------------------------------+
| Name          | String                       | Optional    | Friendly name                                |
+---------------+------------------------------+-------------+----------------------------------------------+
| Description   | String                       | Optional    | Description text                             |
+---------------+------------------------------+-------------+----------------------------------------------+
| BehaviorId    | String                       | Optional    | The identifier of the QiStreamBehavior for   |
|               |                              |             | this stream.                                 |
+---------------+------------------------------+-------------+----------------------------------------------+
| Indexes       | IList<QiStreamIndex>         | Optional    | Used to define secondary indexes for stream  |
+---------------+------------------------------+-------------+----------------------------------------------+


**Rules for Identifier (QiStream.Id)**

1. Is not case sensitive.
2. Can contain spaces.
3. Cannot start with two underscores ("\_\_").
4. Can contain a maximum of 260 characters.
5. Cannot use the following characters: ( / : ? # [ ] @ ! $ & ' ( ) \\\* +
   , ; = %)
6. Cannot start or end with a period.
7. Cannot contain consecutive periods.
8. Cannot consist of only periods. 



Indexes
-------

The Key or Primary Index is defined at the QiType. Secondary
Indexes are defined at the QiStream.

Secondary Indexes are applied to a single property; there are no
compound secondary indexes. Only QiTypeCodes
that can be ordered are supported for use in a secondary index.

Indexes are discussed in greater detail here: `Indexes <https://qi-docs-rst.readthedocs.org/en/latest/indexes.html>`__
