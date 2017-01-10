======================
QiType information
======================

This section contains information about how to configure and use QiTypes. To use Qi, you define QiTypes that describe the kinds of data you want to store in QiStreams. QiTypes are the model that define QiStreams.

QiTypes can define simple atomic types, such as integers, floats or strings, or they can define complex types by grouping properties of other QiTypes. You can construct complex, nested data types by using the Properties collection of a QiType. QiTypes that define atomic types do not need Properties defined. 

A QiType that is used to define a QiStream must have a Key, a Property, or a combination of Properties that constitute an ordered, unique identity. The Key is ordered, so it functions as an index; it is also known as the Primary Index. While a timestamp (DateTime) is a very common type of Key, any ordered value is permitted. Other indexes (secondary indexes), are defined in the QiStream.

You refer to a QiType by its identifier, or Id field. QiType identifiers must be unique within a Namespace.

QiTypes are immutable; after a QiType is created it cannot be changed, and it can only be deleted if no streams reference it.

QiType management using the .NET Qi Client Libraries is performed through the ``IQiMetadataService`` interface, which is accessed using the ``QiService.GetMetadataService()`` helper. 

Only QiTypes that are used to define QiStreams need to be added to Qi. QiTypes that define Properties or the base type are contained within the parent  QiType.

The .NET libraries provide QiTypeBuilder to help build QiTypes.

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

The QiTypeCode is a numeric identifier used by Qi to identify QiTypes. A QiTypeCode exists for every supported type.

Atomic types, such as strings and floats, are defined thoroughly by the QiTypeCode.  

Types requiring additional definition, such as enums and objects, must have a more generic QiTypeCode, such as ByteEnum, Int32Enum, NullableInt32Enum, or Object and are defined using Properties. 


Supported Types
----------------

The following types are supported and defined by the QiTypeCode:

======================   =================   =======================
Array                    Boolean             BooleanArray
Byte                     ByteArray           ByteEnum
Char                     CharArray           DateTime
DateTimeArray            DateTimeOffset      DateTimeOffsetArray
DBNull                   Decimal             DecimalArray
Double                   DoubleArray         Empty
Guid                     GuidArray           IDictionary
IEnumerable              IList               Int16
Int16Array               Int16Enum           Int32
Int32Array               Int32Enum           Int64
Int64Array               Int64Enum           NullableBoolean
NullableByte             NullableChar        NullableDateTime
NullableDateTimeOffset   NullableDecimal     NullableDouble
NullableGuid             NullableInt16       NullableInt32
NullableInt64            NullableSByte       NullableSingle
NullableTimeSpan         NullableUInt16      NullableUInt32
NullableUInt64           Object              SByte
SByteArray               SByteEnum           Single
SingleArray              String              StringArray
TimeSpan                 TimeSpanArray       UInt16
UInt16Array              UInt16Enum          UInt32
UInt32Array              UInt32Enum          UInt64
UInt64Array              UInt64Enum          Version
VersionArray
======================   =================   =======================

QiTypeProperty
--------------

The collection of Properties for a QiType are defined by a QiTypeProperty.

The following table shows the required and optional QiTypeProperty fields. Fields that are not included are reserved for internal Qi use.

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


The QiTypeProperty’s identifier follows the same rules as the QiType.Id.

IsKey is a Boolean value used to identify the QiType’s Key. A Key defined by more than one Property is a compound key. In a compound key, each Property that is included in the Key is specified as IsKey. The Order field is used to define the precedence of fields applied to the Index.

The Value field is used for properties that represent a value. An example of a property with a value is an enum’s named constant. When representing an enum in a QiType, the QiType’s Properies collection defines the enum’s constant list.  The QiTypeProperty’s Identifier represents the constant’s name and the QiTypeProperty’s Value represents the constant’s value.

Indexes
-------

Indexes are used to speed up searching and to order results. A Key is a property or collection of properties that are unique. In Qi, the Key is also an index; it is ordered. The Key is often referred to as the Primary Index. All other Indexes are Secondaries.
Indexes are discussed in greater detail here: `Indexes <https://qi-docs-rst.readthedocs.org/en/latest/Indexes.html>`__.

Working with QiTypes
--------------------

**Using .Net**

When working in .NET, use the QiTypeBuilder to create QiTypes. The QiTypeBuilder eliminates potential errors that can occur when working with QiTypes manually.

There are several ways to work with the builder. The most convenient is to use the static methods, as shown here:

::

  public enum State
  {
      Ok,
      Warning,
      Aalrm
  }

  public class Simple
  {
      [Key]
      public DateTime Time { get; set; }
      public State State { get; set; }
      public Double Value { get; set; }
  }
  QiType simpleType = QiTypeBuilder.CreateQiType<Simple>();
  simpleType.Description = "Basic sample type";

QiTypeBuilder recognizes the ``System.ComponentModel.DataAnnotations.KeyAttribute`` and its own ``OSIsoft.Qi.QiMemberAttribute``.  When using the QiMemberAttribute to specify the Primary Index, set the IsKey to true.

::

  public class Simple
  {
      [QiMember(IsKey = true)]
      public DateTime Time { get; set; }
      public State State { get; set; }
      public Double Value { get; set; }
  }


The type is created with the following parameters. QiTypeBuilder automatically generates unique identifiers. Note that the following table contains only a partial list of parameters.






