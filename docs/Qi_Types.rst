.. _Qi_Types_topic:


Qi Types
========


Qi stores streams of events and provides convenient ways find and associating events. Events are 
stored in streams, called QiStreams. A QiType defines the shape or structure of the event in a QiStream.

QiTypes can define simple atomic types, such as integers, floats, strings, arrays and dictionaries or 
they can define complex types using QiTypes. Define complex, nested types using the Properties collection of a QiType. 

A QiType used to define a QiStream must have a Key. A Key is a Property, or a combination of Properties 
that constitute an ordered, unique identity. The Key is ordered, so it functions as an index; it is 
known as the Primary Index. While a timestamp (DateTime) is a very common type of Key, any type that 
can be ordered is permitted. Other indexes (secondary indexes), are defined in the QiStream. 
Indexes are discussed in greater detail here: :doc:`indexes`

A QiType is referenced by its identifier or Id field. QiType identifiers must be unique within a Namespace.

QiTypes are immutable; after a QiType is created it cannot be changed, and it can only be deleted if no streams reference it.

QiType management using the .NET Qi Client Libraries is performed through the ``IQiMetadataService``. 
Create the IQiMetadataService using one of the ``QiService.GetMetadataService()`` factory methods.

Only QiTypes used to define QiStreams need to be added to Qi. QiTypes that define Properties or base types 
are contained within the parent QiType and do not need to be added to Qi independently.

The .NET libraries provide QiTypeBuilder to help build QiTypes from .NET types. QiTypeBuilder is 
discussed in greater detail below.

The following table shows the required and optional QiType fields. Fields that are not included are reserved for internal Qi use.


+------------------+-------------------------+-------------+-------------------------------------+
| Property         | Type                    | Optionality | Details                             |
+==================+=========================+=============+=====================================+
| Id               | String                  | Required    | Identifier for referencing the type |
+------------------+-------------------------+-------------+-------------------------------------+
| Name             | String                  | Optional    | Friendly name                       |
+------------------+-------------------------+-------------+-------------------------------------+
| Description      | String                  | Optional    | Description text                    |
+------------------+-------------------------+-------------+-------------------------------------+
| QiTypeCode       | QiTypeCode              | Required    | Numeric code identifying the base   |
|                  |                         |             | QiType                              |
+------------------+-------------------------+-------------+-------------------------------------+
| BaseType         | QiType                  | Optional    | QiType the class derives from       |
+------------------+-------------------------+-------------+-------------------------------------+
| IsGenericType    | Boolean                 |             | Identifies the type as a generic    |
|                  |                         |             | (or Template in C++), containing    |
|                  |                         |             | one or more type argument.          |
+------------------+-------------------------+-------------+-------------------------------------+
| GenericArguments | IList<QiType>           | Optional    | List of type arguments satisfying   |
|                  |                         |             | the generic                         |
+------------------+-------------------------+-------------+-------------------------------------+
| Properties       | IList<QiTypeProperty>   | Optional    | List of QiTypeProperty items        |
+------------------+-------------------------+-------------+-------------------------------------+


**Rules for typeId**

1. Is not case sensitive
2. Can contain spaces
3. Cannot begin with two underscores ("\_\_")
4. Cannot contain forward slash or backslash characters ("/" or "\\")
5. Can contain a maximum of 260 characters
6. Cannot start or end with a period.
7. Cannot contain consecutive periods.
8. Cannot consist of only periods.


QiTypeCode
----------

The QiTypeCode is a numeric identifier used by Qi to identify QiTypes. A QiTypeCode exists for 
every supported type.

Atomic types, such as strings, floats and arrays, are defined entirely by the QiTypeCode. Atomic 
types do not need QiType Properties defined.

Types requiring additional definition, such as enums and objects, are identified using a generic 
QiTypeCode, such as ByteEnum, Int32Enum, NullableInt32Enum, or Object, and are defined using Properties.


Supported Types
----------------

The following types are supported and defined by the QiTypeCode:


=======================  =====
Type                     QiTypeCode
-----------------------  -----
Array                    400
Boolean                  3
BooleanArray             203
Byte                     6
ByteArray                206
ByteEnum                 606
Char                     4
CharArray                204
DateTime                 16
DateTimeArray            216
DateTimeOffset           20
DateTimeOffsetArray      220
DBNull                   2
Decimal                  15
DecimalArray             215
Double                   14
DoubleArray              214
Empty                    0
Guid                     19
GuidArray                219
IDictionary              402
IEnumerable              403
IList                    401
Int16                    7
Int16Array               207
Int16Enum                607
Int32                    9
Int32Array               209
Int32Enum                609
Int64                    11
Int64Array               211
Int64Enum                611
NullableBoolean          103
NullableByte             106
NullableByteEnum         706
NullableChar             104
NullableDateTime         116
NullableDateTimeOffset   120
NullableDecimal          115
NullableDouble           114
NullableGuid             119
NullableInt16            107
NullableInt16Enum        707
NullableInt32            109
NullableInt32Enum        709
NullableInt64            111
NullableInt64Enum        711
NullableSByte            105
NullableSByteEnum        705
NullableSingle           113
NullableTimeSpan         121
NullableUInt16           108
NullableUInt16Enum       708
NullableUInt32           110
NullableUInt32Enum       710
NullableUInt64           112
NullableUInt64Enum       712
Object                   1
QiColumn                 510
QiObject                 512
QiStream                 507
QiStreamIndex            508
QiTable                  509
QiType                   501
QiTypeProperty           502
QiValues                 511
QiView                   503
QiViewMap                505
QiViewMapProperty        506
QiViewProperty           504
SByte                    5
SByteArray               205
SByteEnum                605
Single                   13
SingleArray              213
String                   18
StringArray              218
TimeSpan                 21
TimeSpanArray            221
UInt16                   8
UInt16Array              208
UInt16Enum               608
UInt32                   10
UInt32Array              210
UInt32Enum               610
UInt64                   12
UInt64Array              212
UInt64Enum               612
Version                  22
VersionArray             222
=======================  =====



QiTypeProperty
--------------

A QiTypeProperty is used to define the collection of fields or Properties in a QiType. 
An instance of a QiType is represented by its Properties or members. The maximum number of 
Properties that can define a compound key is three.

The following table shows the required and optional QiTypeProperty fields. Fields that 
are not included are reserved for internal Qi use.

+------------------+-------------------------+-------------+-------------------------------------+
| Property         | Type                    | Optionality | Details                             |
+==================+=========================+=============+=====================================+
| Id               | String                  | Required    | Identifier for referencing the type |
+------------------+-------------------------+-------------+-------------------------------------+
| Name             | String                  | Optional    | Friendly name                       |
+------------------+-------------------------+-------------+-------------------------------------+
| Description      | String                  | Optional    | Description text                    |
+------------------+-------------------------+-------------+-------------------------------------+
| QiType           | QiType                  | Required    | Field defining the property's       |
|                  |                         |             | Type                                |
+------------------+-------------------------+-------------+-------------------------------------+
| IsKey            | Boolean                 | Required    | Identifies the property as the Key  |
|                  |                         |             | (Primary Index)                     |
+------------------+-------------------------+-------------+-------------------------------------+
| Value            | Object                  | Optional    | Value of the property               |
+------------------+-------------------------+-------------+-------------------------------------+
| Order            | Int                     | Optional    | Order of comparison within a        |
|                  |                         |             | compound index. Also used           |
|                  |                         |             | internally                          |
+------------------+-------------------------+-------------+-------------------------------------+


The QiTypeProperty’s identifier follows the same rules as the QiType’s identifier.

IsKey is a Boolean value used to identify the QiType’s Key. A Key defined by more than one 
Property is called a compound key. In a compound key, each Property that is included in the 
Key is specified as IsKey. The Order field defines the precedence of fields applied to the Index.

The Value field is used for properties that represent a value. An example of a property with a 
value is an enum’s named constant. When representing an enum in a QiType, the QiType’s 
Properies collection defines the enum’s constant list. The QiTypeProperty’s Identifier represents 
the constant’s name and the QiTypeProperty’s Value represents the constant’s value.






