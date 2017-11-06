======================
QiType information
======================


Qi stores streams of events and provides convenient ways find and associating events. Events are 
stored in streams, called QiStreams. A QiType defines the shape or structure of the event in a QiStream.

QiTypes can define simple atomic types, such as integers, floats, strings, arrays and dictionaries or 
they can define complex types using QiTypes. Define complex, nested types using the Properties collection of a QiType. 

A QiType used to define a QiStream must have a Key. A Key is a Property, or a combination of Properties 
that constitute an ordered, unique identity. The Key is ordered, so it functions as an index; it is 
known as the Primary Index. While a timestamp (DateTime) is a very common type of Key, any type that 
can be ordered is permitted. Other indexes (secondary indexes), are defined in the QiStream. 
Indexes are discussed in greater detail here: `Indexes <https://qi-docs.readthedocs.org/en/latest/indexes.html>`__.

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

A QiTypePropertyis used to define the collection of fields or Properties in a QiType. 
An instance of a QiType is represented by its Properties or members.

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


Working with QiTypes
--------------------

**Using .Net**

When working in .NET, use the QiTypeBuilder to create QiTypes. The QiTypeBuilder eliminates 
potential errors that can occur when working with QiTypes manually.

There are several ways to work with the builder. The most convenient is to use the static 
methods, as shown here:

::

  public enum State
  {
      Ok,
      Warning,
      Alarm
  }

  public class Simple
  {
      [QiMember(IsKey = true, Order = 0)]
      public DateTime Time { get; set; }
      public State State { get; set; }
      public Double Measurement { get; set; }
  }

  QiType simpleType = QiTypeBuilder.CreateQiType<Simple>();
  simpleType.Id = "Simple";
  simpleType.Name = "Simple";
  simpleType.Description = "Basic sample type";


QiTypeBuilder recognizes the ``System.ComponentModel.DataAnnotations.KeyAttribute`` and 
its own ``OSIsoft.Qi.QiMemberAttribute``. When using the QiMemberAttribute to specify 
the Primary Index, set the IsKey to true.

The type is created with the following parameters. QiTypeBuilder automatically generates 
unique identifiers. Note that the following table contains only a partial list of fields.


+------------------+-------------------------+-------------+--------------------------------------+
| Field            | Values                                                                       |
+==================+=========================+=============+======================================+
| Id               | e8e39c7f-c8b0-3bda-b2f0-a73b2392ebc1                                         |
+------------------+-------------------------+-------------+--------------------------------------+
| Name             | Simple                                                                       |
+------------------+-------------------------+-------------+--------------------------------------+
| Description      | Basic sample type                                                            |
+------------------+-------------------------+-------------+--------------------------------------+
| Properties       | Count = 3                                                                    |
+------------------+-------------------------+-------------+--------------------------------------+
|   [0]            | Id                      | Time                                               |
+                  +-------------------------+-------------+--------------------------------------+
|                  | Name                    | Time                                               |
+                  +-------------------------+-------------+--------------------------------------+
|                  | Description             | null                                               |
+                  +-------------------------+-------------+--------------------------------------+
|                  | Order                   | 0                                                  |
+                  +-------------------------+-------------+--------------------------------------+
|                  | IsKey                   | true                                               |
+                  +-------------------------+-------------+--------------------------------------+
|                  | QiType                  | Id          | c48bfdf5-a271-384b-bf13-bd21d931c1bf |
+                  +                         +-------------+--------------------------------------+
|                  |                         | Name        | DateTime                             |
+                  +                         +-------------+--------------------------------------+
|                  |                         | Description | null                                 |
+                  +                         +-------------+--------------------------------------+
|                  |                         | Properties  | null                                 |
+                  +-------------------------+-------------+--------------------------------------+
|                  | Value                   | null                                               |
+------------------+-------------------------+-------------+--------------------------------------+
|   [1]            | Id                      | State                                              |
+                  +-------------------------+-------------+--------------------------------------+
|                  | Name                    | State                                              |
+                  +-------------------------+-------------+--------------------------------------+
|                  | Description             | null                                               |
+                  +-------------------------+-------------+--------------------------------------+
|                  | Order                   | 0                                                  |
+                  +-------------------------+-------------+--------------------------------------+
|                  | IsKey                   | false                                              |
+                  +-------------------------+-------------+--------------------------------------+
|                  | QiType                  | Id          | 02728a4f-4a2d-3588-b669-e08f19c35fe5 |
+                  +                         +-------------+--------------------------------------+
|                  |                         | Name        | State                                |
+                  +                         +-------------+--------------------------------------+
|                  |                         | Description | null                                 |
+                  +                         +-------------+--------------------------------------+
|                  |                         | Properties  | Count = 3                            |
+                  +                         +-------------+-------------------+------------------+
|                  |                         | [0]         | Id                | "OK"             |
+                  +                         +             +-------------------+------------------+
|                  |                         |             | Name              | null             |
+                  +                         +             +-------------------+------------------+
|                  |                         |             | Description       | null             |
+                  +                         +             +-------------------+------------------+
|                  |                         |             | Order             | 0                |
+                  +                         +             +-------------------+------------------+
|                  |                         |             | QiType            | null             |
+                  +                         +             +-------------------+------------------+
|                  |                         |             | Value             | Warning          |
+                  +                         +-------------+-------------------+------------------+
|                  |                         | [1]         | Id                | "OK"             |
+                  +                         +             +-------------------+------------------+
|                  |                         |             | Name              | null             |
+                  +                         +             +-------------------+------------------+
|                  |                         |             | Description       | null             |
+                  +                         +             +-------------------+------------------+
|                  |                         |             | Order             | 0                |
+                  +                         +             +-------------------+------------------+
|                  |                         |             | QiType            | null             |
+                  +                         +             +-------------------+------------------+
|                  |                         |             | Value             | Warning          |
+                  +                         +-------------+-------------------+------------------+
|                  |                         | [2]         | Id                | "Alarm"          |
+                  +                         +             +-------------------+------------------+
|                  |                         |             | Name              | null             |
+                  +                         +             +-------------------+------------------+
|                  |                         |             | Description       | null             |
+                  +                         +             +-------------------+------------------+
|                  |                         |             | Order             | 0                |
+                  +                         +             +-------------------+------------------+
|                  |                         |             | QiType            | null             |
+                  +                         +             +-------------------+------------------+
|                  |                         |             | Value             | Alarm            |
+                  +-------------------------+-------------+-------------------+------------------+
|                  | Value                   | null                                               |
+------------------+-------------------------+-------------+-------------------+------------------+
|   [2]            | Id                      | Value                                              |
+                  +-------------------------+-------------+--------------------------------------+
|                  | Name                    | Value                                              |
+                  +-------------------------+-------------+--------------------------------------+
|                  | Description             | null                                               |
+                  +-------------------------+-------------+--------------------------------------+
|                  | Order                   | 0                                                  |
+                  +-------------------------+-------------+--------------------------------------+
|                  | IsKey                   | false                                              |
+                  +-------------------------+-------------+--------------------------------------+
|                  | QiType                  | Id          | 0f4f147f-4369-3388-8e4b-71e20c96f9ad |
+                  +                         +-------------+--------------------------------------+
|                  |                         | Name        | Double                               |
+                  +                         +-------------+--------------------------------------+
|                  |                         | Description | null                                 |
+                  +                         +-------------+--------------------------------------+
|                  |                         | Properties  | null                                 |
+                  +-------------------------+-------------+--------------------------------------+
|                  | Value                   | null                                               |
+------------------+-------------------------+-------------+--------------------------------------+


The QiTypeBuilder also supports derived types. Note that you need not add the base types to 
Qi before using QiTypeBuilder.

Defining QiTypes when not using .NET
------------------------------------

QiTypes must be built manually when .NET QiTypeBuilder is unavailable. The following discussion 
refers to the types that are defined in  
`Python <https://github.com/osisoft/Qi-Samples/tree/master/Basic/Python>`__ and 
`JavaScript <https://github.com/osisoft/Qi-Samples/tree/master/Basic/JavaScript>`__ samples. 
Samples in other languages can be found here: `Samples <https://github.com/osisoft/Qi-Samples/tree/master/Basic>`__.

In the sample code, ``QiType``, ``QiTypeProperty``, and ``QiTypeCode`` are defined as in the code snippets shown here:

**Python**

::

  class QiTypeCode(Enum):
      Empty = 0
      Object = 1
      DBNull = 2
      Boolean = 3
      Char = 4
        ...
  class QiTypeProperty(object):
      """Qi type property definition"""

      def __init__(self):
              self.__isKey = False

      @property
      def Id(self):
          return self.__id
      @Id.setter
      def Id(self, id):
          self.__id = id

        ...

      @property
      def IsKey(self):
          return self.__isKey
      @IsKey.setter
      def IsKey(self, iskey):
          self.__isKey = iskey

      @property
      def QiType(self):
          return self.__qiType
      @QiType.setter
      def QiType(self, qiType):
          self.__qiType=qiType
        ...

  class QiType(object):
      """Qi type definitions"""
      def __init__(self):
          self.QiTypeCode = QiTypeCode.Object

      @property
      def Id(self):
          return self.__id
      @Id.setter
      def Id(self, id):
          self.__id = id

        ...

      @property
      def BaseType(self):
          return self.__baseType
      @BaseType.setter
      def BaseType(self, baseType):
          self.__baseType = baseType

      @property
      def QiTypeCode(self):
          return self.__typeCode
      @QiTypeCode.setter
      def QiTypeCode(self, typeCode):
          self.__typeCode = typeCode

      @property
      def Properties(self):
          return self.__properties
      @Properties.setter
      def Properties(self, properties):
          self.__properties = properties

 
  
**JavaScript**

::

  qiTypeCodeMap: {
      Empty: 0,
      "Object": 1,
      DBNull: 2,
      "Boolean": 3,
      Char: 4,
      ...
  QiTypeProperty: function (qiTypeProperty) {
      if (qiTypeProperty.Id) {
          this.Id = qiTypeProperty.Id;
      }
      if (qiTypeProperty.Name) {
          this.Name = qiTypeProperty.Name;
      }
      if (qiTypeProperty.Description) {
          this.Description = qiTypeProperty.Description;
      }
      if (qiTypeProperty.QiType) {
          this.QiType = qiTypeProperty.QiType;
      }
      if (qiTypeProperty.IsKey) {
          this.IsKey = qiTypeProperty.IsKey;
      }
  },
  QiType: function (qiType) {
      if (qiType.Id) {
          this.Id = qiType.Id
      }
      if (qiType.Name) {
          this.Name = qiType.Name;
      }
      if (qiType.Description) {
          this.Description = qiType.Description;
      }
      if (qiType.QiTypeCode) {
          this.QiTypeCode = qiType.QiTypeCode;
      }
      if (qiType.Properties) {
          this.Properties = qiType.Properties;
      }
  },



Working with the following types (both Python and JavaScript classes are shown):


**Python**

::

  class State(Enum):
      Ok = 0
      Warning = 1
      Alarm = 2

  class Simple(object):
      Time = property(getTime, setTime)
      def getTime(self):
          return self.__time
      def setTime(self, time):
          self.__time = time

      State = property(getState, setState)
      def getState(self):
          return self.__state
      def setState(self, state):
          self.__state = state

      Measurement = property(getMeasurement, setMeasurement)
      def getMeasurement(self):
          return self.__measurement
      def setMeasurement(self, measurement):
          self.__measurement = measurement


**JavaScript**

::

  var State =
    {
        Ok: 0,
        Warning: 1,
        Aalrm: 2,
    }
 
    var Simple = function () {
        this.Time = null;
        this.State = null;
        this.Measurement = null;
    }

 
Define the QiType as follows:

**Python**

::

    # Create the properties

  # Time is the primary key
  time = QiTypeProperty()
  time.Id = "Time"
  time.Name = "Time"
  time.IsKey = True
  time.QiType = QiType()
  time.QiType.Id = "DateTime"
  time.QiType.Name = "DateTime"
  time.QiType.QiTypeCode = QiTypeCode.DateTime

  # State is not a pre-defined type. A QiType must be defined to represent the enum
  stateTypePropertyOk = QiTypeProperty()
  stateTypePropertyOk.Id = "Ok"
  stateTypePropertyOk.Value = State.Ok
  stateTypePropertyWarning = QiTypeProperty()
  stateTypePropertyWarning.Id = "Warning"
  stateTypePropertyWarning.Value = State.Warning
  stateTypePropertyAlarm = QiTypeProperty()
  stateTypePropertyAlarm.Id = "Alarm"
  stateTypePropertyAlarm.Value = State.Alarm

  stateType = QiType()
  stateType.Id = "State"
  stateType.Name = "State"
  stateType.Properties = [ stateTypePropertyOk, stateTypePropertyWarning, \
                          stateTypePropertyAlarm ]

  state = QiTypeProperty()
  state.Id = "State"
  state.Name = "State"
  state.QiType = stateType

  # Value property is a simple non-indexed, pre-defined type
  value = QiTypeProperty()
  value.Id = "Measurement"
  value.Name = "Measurement"
  value.QiType = QiType()
  value.QiType.Id = "Double"
  value.QiType.Name = "Double"

  # Create the Simple QiType
  simpleType = QiType()
  simpleType.Id = "Simple"
  simpleType.Name = "Simple"
  simpleType.Description = "Basic sample type"
  simpleType.QiTypeCode = QiTypeCode.Object
  simpleType.Properties = [ time ]


**JavaScript**

::

  // Time is the primary key
  var timeProperty = new QiObjects.QiTypeProperty({
      "Id": "Time",
      "IsKey": true,
      "QiType": new QiObjects.QiType({
          "Id": "dateType",
          "QiTypeCode": QiObjects.qiTypeCodeMap.DateTime
      })
  });

  // State is not a pre-defined type. A QiType must be defined to represent the enum
  var stateTypePropertyOk = new QiObjects.QiTypeProperty({
      "Id": "Ok",
      "Value": State.Ok
  });
  var stateTypePropertyWarning = new QiObjects.QiTypeProperty({
      "Id": "Warning",
      "Value": State.Warning
  });
  var stateTypePropertyAlarm = new QiObjects.QiTypeProperty({
      "Id": "Alarm",
      "Value": State.Alarm
  });

  var stateType = new QiObjects.QiType({
      "Id": "State",
      "Name": "State",
      "QiTypeCode": QiObjects.qiTypeCodeMap.Int32Enum,
      "Properties": [stateTypePropertyOk, stateTypePropertyWarning,
          stateTypePropertyAlarm, stateTypePropertyRed]
  });

  // Measurement property is a simple non-indexed, pre-defined type
  var measurementProperty = new QiObjects.QiTypeProperty({
      "Id": "Measurement",
      "Name": "Measurement",
      "QiType": new QiObjects.QiType({
          "Id": "doubleType",
          "QiTypeCode": QiObjects.qiTypeCodeMap.Double
      })
  });

  // Create the Simple QiType
  var simpleType = new QiObjects.QiType({
      "Id": "Simple",
      "Name": "Simple", 
      "Description": " This is a simple Qi type ",
      "QiTypeCode": QiObjects.qiTypeCodeMap.Object,
      "Properties": [timeProperty, stateProperty, measurementProperty]
  });


 Working with a derived class is easy. For the following derived class:

::

  class Derrived(Simple):
      @property
      def Observation(self):
          return self.__observation
      @Observation.setter
      def Observation(self, observation):
          self.__observation = observation


Extend the QiType as follows:

**Python**

::

  # Observation property is a simple non-inexed, standard data type
  observation = QiTypeProperty()
  observation.Id = "Observation"
  observation.Name = "Observation"
  observation.QiType = QiType()
  observation.QiType.Id = "String"
  observation.QiType.Name = "String"
  observation.QiType.QiTypeCode = QiTypeCode.String

  # Create the Derived QiType
  derived = QiType()
  derived.Id = "Derived"
  derived.Name = "Derived"
  derived.Description = "Derived sample type"
  derived.BaseType = simpleType # Set the base type to the derived type
  derived.QiTypeCode = QiTypeCode.Object
  derived.Properties = [ observation ]
    

**JavaScript**

::

  var observationProprety = new QiObjects.QiTypeProperty({
      "Id": "Observation",
      "QiType": new QiObjects.QiType({
          "Id": "strType",
          "QiTypeCode": QiObjects.qiTypeCodeMap.String
      })
  });

  var derivedType = new QiObjects.QiType({
      "Id": "Derived",
      "Name": "Derived",
      "Description": " Derived sample type",
      "BaseType": simpleType,
      "QiTypeCode": QiObjects.qiTypeCodeMap.Object,
      "Properties": [ observationProprety ]
  });

