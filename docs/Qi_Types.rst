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










The QiTypeBuilder supports derived types as well.  Note that you need not add the base types to Qi prior to using QiTypeBuilder.

Defining QiTypes when not using .NET
------------------------------------

QiTypes must be built manually when .NET QiTypeBuilder is unavailable. The following discussion refers to the types that are defined in the `Python <https://github.com/osisoft/Qi-Samples/tree/master/Basic/Python>`__ and `JavaScript <https://github.com/osisoft/Qi-Samples/tree/master/Basic/JavaScript>`__ samples. Samples in other languages can be found here: `Samples <https://github.com/osisoft/Qi-Samples/tree/master/Basic>`__.

In the sample code, QiType, QiTypeProperty, and QiTypeCode are defined as in the code snippets shown here:

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


Suppose you had the following class defined (both Python and JavaScript classes are shown):

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

      Value = property(getValue, setValue)
      def getValue(self):
          return self.__value
      def setValue(self, value):
          self.__value = value

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
      this.Value = null;
  }
 
You can define the QiType for the previous classes as follows:

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
    value.Id = "Value"
    value.Name = "Value"
    value.QiType = QiType()
    value.QiType.Id = "Double"
    value.QiType.Name = "Double"
    
    # Create the Simple QiType
    simple = QiType()
    simple.Id = str(uuid.uuid4())
    simple.Name = "Simple"
    simple.Description = "Basic sample type"
    simple.QiTypeCode = QiTypeCode.Object
    simple.Properties = [ time ]


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

  // Value property is a simple non-indexed, pre-defined type
  var valueProperty = new QiObjects.QiTypeProperty({
      "Id": "Value",
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
      "Properties": [timeProperty, stateProperty, valueProperty]
  });

Now suppose that you have the following derived class:

::

  class Derrived(Simple):
      @property
      def Observation(self):
          return self.__observation
      @Observation.setter
      def Observation(self, observation):
          self.__observation = observation


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
    derived.Id = str(uuid.uuid4())
    derived.Name = "Derived"
    derived.Description = "Derived sample type"
    derived.BaseType = simple # Set the base type to the derived type
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
      "Description": "This is a derieved Qi type for storing events",
      "BaseType": simpleType,
      "QiTypeCode": QiObjects.qiTypeCodeMap.Object,
      "Properties": [ observationProprety ]
  });


