QiStream information
====================

A QiStream is the fundamental unit of storage in Qi. A stream
represents an ordered series of events or observations for a particular
item of interest.

QiStream management using the .NET Qi Client Libraries is performed through the ``IQiMetadataService`` interface, which may be accessed via the ``QiService.GetMetadataService()`` helper.

The following table shows the required and optional QiStream fields. Fields not listed are reserved
for internal Qi use. 


+---------------+------------------------------+-------------+----------------------------------------------+
| Property      | Type                         | Optionality |Details                                       |
+===============+==============================+=============+==============================================+
| Id            | String                       | Required    | An identifier for referencing the stream.    |
+---------------+------------------------------+-------------+----------------------------------------------+
| TypeId        | String                       | Required    | The QiType identifier of the type to be      |
|               |                              |             | used for this stream.                        |
+---------------+------------------------------+-------------+----------------------------------------------+
| Name          | String                       | Optional    | Friendly name                                |
+---------------+------------------------------+-------------+----------------------------------------------+
| Description   | String                       | Optional    | Description text                             |
+---------------+------------------------------+-------------+----------------------------------------------+
| BehaviorId    | String                       | Optional    | The identifier of the QiStreamBehavior for   |
|               |                              |             | this stream.                                 |
+---------------+------------------------------+-------------+----------------------------------------------+
| Tag           | String                       | Optional    | A collection of strings that permit          |
|               |                              |             | classifying and identifying individual       |
|               |                              |             | streams.                                     |
+---------------+------------------------------+-------------+----------------------------------------------+
| Metadata      | iDictionary<string, string>  | Optional    | A dictionary for users to store information  |
|               |                              |             | that is relevant to the stream               |
+---------------+------------------------------+-------------+----------------------------------------------+
| Indexes       | IList<QiStreamIndex>         | Optional    | Used to define secondary indexes for stream  |
+---------------+------------------------------+-------------+----------------------------------------------+

A stream is always referenced by its identifier or Id field. QiStream identifiers are unique within a Namespace.


A QiStream must include a TypeId that references the identifier of an existing QiType. The QiType 
defines the structure of the QiStream.


You can optionally set the BehaviorId field to the identifier of an existing QiStreamBehavior. If
BehaviorId is omitted, the default behavior mode is set to *continuous* and *extrapolation*
is set to *all*. See 
`QiStreamBehaviors <https://qi-docs-rst.readthedocs.org/en/latest/Qi_Stream_Behavior.html>`__
for more information.

**Rules for Identifier (QiStream.Id)**

1. Is not case sensitive.
2. Can contain spaces.
3. Cannot start with two underscores ("\_\_").
4. Can contain a maximum of 260 characters.
5. Cannot use the following characters: ( / : ? # [ ] @ ! $ & ' ( ) \\\* +
   , ; = %)
6. Cannot start or end with a period.
7. Cannot contain consecutive periods.
8. Cannot consist of only periods. 



Indexes
-------

The Key or Primary Index is defined at the QiType. Secondary
Indexes are defined at the QiStream.

Secondary Indexes are applied to a single property; there are no
compound secondary indexes. Only QiTypeCodes
that can be ordered are supported for use in a secondary index.

Indexes are discussed in greater detail here: `Indexes <https://qi-docs-rst.readthedocs.org/en/latest/indexes.html>`__
