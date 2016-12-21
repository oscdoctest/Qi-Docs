**Indexes**

Indexes are used to speed up searches and to order results. A Key is a
property or collection of properties that are unique. In Qi, a QiType’s
Key is also an index. The Key is often referred to as the “Primary
Index”. All other Indexes are Secondaries.

A QiType used to define a QiStream must define its Key. When inserting
data into a QiStream, every Key value must be unique. Qi will not store
more than a single event for a given Key; an event with a particular Key
can be deleted or updated, but two events with the same Key cannot
exist.

In .NET, a type’s property is identified by using either an
OSIsoft.Qi.QiMemberAttribute and setting its IsKey to true or the
System.ComponentModel.DataAnnotations.KeyAttribute. In the QiType, the
Property or Properties representing the Key have their
QiTypeProperty.IsKey field set to true.

Secondary Indexes are defined on QiStreams. They are applied to a single
property. You can define many Secondaries.

Secondary Indexes need not be unique.

**Compound Indexes**

Often, a single property, such as DateTime, is adequate for defining an
Index, but for more complex scenarios Qi allows multiple properties to
be. Indexes defined by multiple properties are called “compound
indexes”.

When defining a Compound Index in .NET, apply the
OSIsoft.Qi.QiMemberAttribute on each of the type’s Properties that are
combined to define the Key. Set the IsKey to true and give the Order
field a value. The Order field defines the precedence of the property
when sorting, where a Property with an Order of 0 has highest
precedence. When defining Compound Indexes outside of .NET, specify the
IsKey and Order fields on the QiTypeProperty or Properties.

The Qi REST API methods that use tuples were created to assist you to
use compound indexes.

**Working with Indexes**

**Using .Net**

**Simple Indexes**

When working in .NET, use the QiTypeBuilder together with either the
OSIsoft.Qi.QiMemberAttribute or the
System.ComponentModel.DataAnnotations.KeyAttribute, to identify the
Property that defines the simple Key. Using QiTypeBuilder eliminates
potential errors that may occur when working with QiTypes manually.

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
    public Double Measurement { get; set; }
  }

  QiType simpleType = QiTypeBuilder.CreateQiType<Simple>();
  simpleType.Description = "Basic sample type";


To read data between two indexes, ordered by the Key, define a start and
an end index. For DateTime, use ISO 8601 representation of dates and
times. To query for a window of Simple values between January 1, 2010
and February 1, 2010, you would define indexes and query as follows.

::

  IEnumerable<Simple> values =
    client.GetWindowValuesAsync<Simple>(simpleStream.Id,
    "2010-01-01T08:00:00.000Z","2010-02-01T08:00:00.000Z").GetAwaiter().GetResult();


There is more information under the Reading Data section.

**Secondary Indexes**

Secondary Indexes are defined at the QiStream. To add indexes to a
QiStream, add them to the QiStream’s Indexes field.

To index the Simple type defined above by Measurement,

::

  QiStreamIndex measurementIndex = new QiStreamIndex()
  {
    QiTypePropertyId = simpleType.Properties.First(p =>p.Id.Equals("Measurement")).Id
  };

  QiStream streamWithSeconary = new QiStream()
  {
    Id = Guid.NewGuid().ToString(),
    TypeId = type.Id,
    Indexes = new List<QiStreamIndex>()
    {
      measurementIndex
    }
  };

To read data indexed by a Secondary Index, use a filtered Get.

::

  DateTime t = DateTime.Now;
  client.UpdateValuesAsync<Simple>(secondary.Id, new List<Simple>()
  {
    new Simple()
    {
      Time = t,
      State = State.Ok,
      Measurement = 5
    },
    new Simple()
    {
      Time = t + TimeSpan.FromSeconds(1),
      State = State.Ok,
      Measurement = 4
    },
    new Simple()
    {
      Time = t + TimeSpan.FromSeconds(2),
      State = State.Ok,
      Measurement = 3
    },
    new Simple()
    {
      Time = t + TimeSpan.FromSeconds(3),
      State = State.Ok,
      Measurement = 2
    },
    new Simple()
    {
      Time = t + TimeSpan.FromSeconds(4),
      State = State.Ok,
      Measurement = 1
    },
  }).GetAwaiter().GetResult();

  IEnumerable<Simple> orderedBySecondary =
  client.GetValuesAsync<Simple>(secondary.Id,

    "Measurement gt 0 and Measurement lt 6").GetAwaiter().GetResult();

  // Output:
  // 12/13/2016 9:30:04 PM: 1
  // 12/13/2016 9:30:03 PM: 2
  // 12/13/2016 9:30:02 PM: 3
  // 12/13/2016 9:30:01 PM: 4
  // 12/13/2016 9:30:00 PM: 5

**Compound Indexes**

Compound indexes are defined using the QiMemberAttribute as follows:

::

  public class Simple
  {
    [QiMember(IsKey = true, Order = 0)]
    public DateTime Time { get; set; }
    public State State { get; set; }
    public Double Measurement { get; set; }
  }

  public class DerivedCompoundIndex : Simple
  {
    [QiMember(IsKey = true, Order = 1)]
    public DateTime Recorded { get; set; }
  }


Events of type DerivedCompoundIndex are sorted first by Time and then by
Recorded. Thus a collection of times would be sorted as follows:

+------------+----------------+-------------------+
| **Time**   | **Recorded**   | **Measurement**   |
+============+================+===================+
| 01:00      | 00:00          | 0                 |
+------------+----------------+-------------------+
| 01:00      | 01:00          | 2                 |
+------------+----------------+-------------------+
| 01:00      | 14:00          | 5                 |
+------------+----------------+-------------------+
| 02:00      | 00:00          | 1                 |
+------------+----------------+-------------------+
| 02:00      | 01:00          | 3                 |
+------------+----------------+-------------------+
| 02:00      | 02:00          | 4                 |
+------------+----------------+-------------------+
| 02:00      | 14:00          | 6                 |
+------------+----------------+-------------------+

Were the Order swapped, Recorded as zero, the results would sort as
follows:

+------------+----------------+-------------------+
| **Time**   | **Recorded**   | **Measurement**   |
+============+================+===================+
| 01:00      | 00:00          | 0                 |
+------------+----------------+-------------------+
| 02:00      | 00:00          | 1                 |
+------------+----------------+-------------------+
| 01:00      | 01:00          | 2                 |
+------------+----------------+-------------------+
| 02:00      | 01:00          | 3                 |
+------------+----------------+-------------------+
| 02:00      | 02:00          | 4                 |
+------------+----------------+-------------------+
| 01:00      | 14:00          | 5                 |
+------------+----------------+-------------------+
| 02:00      | 14:00          | 6                 |
+------------+----------------+-------------------+

Were we to add values as follows:

::

  // estimates at 1/20/2017 00:00
  client.UpdateValuesAsync(compoundStream.Id, new List<Compound>()
  {
    new Compound()
    {
      Time = DateTime.Parse("1/20/2017 01:00"),
      Recorded = DateTime.Parse("1/20/2017 00:00"),
      State = State.Ok,
      Measurement = 0
    },
    new Compound()
    {
      Time = DateTime.Parse("1/20/2017 02:00"),
      Recorded = DateTime.Parse("1/20/2017 00:00"),
      State = State.Ok,
      Measurement = 1
    },
  }).GetAwaiter().GetResult();

  // measure and estimates at 1/20/2017 01:00
  client.UpdateValuesAsync(compoundStream.Id, new List<Compound>()
  {
    new Compound()
    {
      Time = DateTime.Parse("1/20/2017 01:00"),
      Recorded = DateTime.Parse("1/20/2017 01:00"),
      State = State.Ok,
      Measurement = 2
    },
    new Compound()
    {
      Time = DateTime.Parse("1/20/2017 02:00"),
      Recorded = DateTime.Parse("1/20/2017 01:00"),
      State = State.Ok,
      Measurement = 3
    },
  }).GetAwaiter().GetResult();

  // measure at 1/20/2017 02:00
  client.UpdateValuesAsync(compoundStream.Id, new List<Compound>()
  {
    new Compound()
    {
      Time = DateTime.Parse("1/20/2017 02:00"),
      Recorded = DateTime.Parse("1/20/2017 02:00"),
      State = State.Ok,
      Measurement = 4
    },
  }).GetAwaiter().GetResult();

  // adjust earlier values at 1/20/2017 14:00
  client.UpdateValuesAsync(compoundStream.Id, new List<Compound>()
  {
    new Compound()
    {
      Time = DateTime.Parse("1/20/2017 01:00"),
      Recorded = DateTime.Parse("1/20/2017 14:00"),
      State = State.Ok,
      Measurement = 5
    },
    new Compound()
    {
      Time = DateTime.Parse("1/20/2017 02:00"),
      Recorded = DateTime.Parse("1/20/2017 14:00"),
      State = State.Ok,
      Measurement = 6
    },
  }).GetAwaiter().GetResult();


We could query against the compound index as follows

::

  IEnumerable<Compound> compoundValues = client.GetWindowValuesAsync<Compound, DateTime, DateTime>(
    compoundStream.Id,
  new Tuple<DateTime, DateTime>(DateTime.Parse("1/20/2017 01:00"),
  DateTime.Parse("1/20/2017 00:00")),
  new Tuple<DateTime, DateTime>(DateTime.Parse("1/20/2017 02:00"),
  DateTime.Parse("1/20/2017 14:00"))).GetAwaiter().GetResult();

  foreach (Compound value in compoundValues)
    Console.WriteLine("{0}:{1} {2}", value.Time, value.Recorded,value.Measurement);
  Console.WriteLine();

  // Output:
  // 1/20/2017 1:00:00 AM:1/20/2017 12:00:00 AM 0
  // 1/20/2017 1:00:00 AM:1/20/2017 1:00:00 AM 2
  // 1/20/2017 1:00:00 AM:1/20/2017 2:00:00 PM 5
  // 1/20/2017 2:00:00 AM:1/20/2017 12:00:00 AM 1
  // 1/20/2017 2:00:00 AM:1/20/2017 1:00:00 AM 3
  // 1/20/2017 2:00:00 AM:1/20/2017 2:00:00 AM 4
  // 1/20/2017 2:00:00 AM:1/20/2017 2:00:00 PM 6


**Not Using .NET**

**Simple Indexes**

When the .NET QiTypeBuilder is unavailable, indexes must be built
manually.

The following discusses the types defined in our
`Python <https://github.com/osisoft/Qi-Samples/tree/master/Basic/Python>`__
and `Java
Script <https://github.com/osisoft/Qi-Samples/tree/master/Basic/JavaScript>`__
samples. Samples in other languages can be found
`here <https://github.com/osisoft/Qi-Samples/tree/master/Basic>`__.

If we wish to build a QiType representative of the following sample
class:

*Python*

::
  class State(Enum):
    Ok = 0
    Warning = 1
    Alarm = 2
    
  class Simple(object):
    Time = property(getTime, setTime)
    def getTime(self):
      return self.\_\_time
    def setTime(self, time):
      self.\_\_time = time
      
    State = property(getState, setState)
    def getState(self):
      return self.\_\_state
    def setState(self, state):
      self.\_\_state = state

  Measurement = property(getValue, setValue)
  def getValue(self):
    return self.\_\_measurement
  def setValue(self, measurement):
    self.\_\_measurement = measurement

*JavaScript*

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


To identify the Time property as the Key, define its QiTypeProperty as
follows:

*Python*

::

  # Time is the primary key
  time = QiTypeProperty()
  time.Id = "Time"
  time.Name = "Time"
  time.IsKey = True
  time.QiType = QiType()
  time.QiType.Id = "DateTime"
  time.QiType.Name = "DateTime"
  time.QiType.QiTypeCode = QiTypeCode.DateTime


*JavaScript*

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


Note that the time.IsKey field is set to true.

To read data using the Key, define a start and end index. For DateTime,
use ISO 8601 representation of dates and times. To query for a window of
values between January 1, 2010 and February 1, 2010, you would define
indexes as "2010-01-01T08:00:00.000Z" and "2010-02-01T08:00:00.000Z",
respectively.

There is more information under the Reading Data section.

**Secondary Indexes**

Secondary Indexes are defined at the QiStream. To create a QiStream
using the Simple class and add a Secondary index on the Measurement, we
will use the QiType defined as follows

*Python*

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
  stateTypePropertyOk.Measurement = State.Ok
  stateTypePropertyWarning = QiTypeProperty()
  stateTypePropertyWarning.Id = "Warning"
  stateTypePropertyWarning.Measurement = State.Warning
  stateTypePropertyAlarm = QiTypeProperty()
  stateTypePropertyAlarm.Id = "Alarm"
  stateTypePropertyAlarm.Measurement = State.Alarm

  stateType = QiType()
  stateType.Id = "State"
  stateType.Name = "State"
  stateType.Properties = [ stateTypePropertyOk, stateTypePropertyWarning,\
                         stateTypePropertyAlarm ]
  state = QiTypeProperty()
  state.Id = "State"
  state.Name = "State"
  state.QiType = stateType

  # Measurement property is a simple non-indexed, pre-defined type
  measurement = QiTypeProperty()
  measurement.Id = "Measurement"
  measurement.Name = "Measurement"
  measurement.QiType = QiType()
  measurement.QiType.Id = "Double"
  measurement.QiType.Name = "Double"

  # Create the Simple QiType
  simple = QiType()
  simple.Id = str(uuid.uuid4())
  simple.Name = "Simple"
  simple.Description = "Basic sample type"
  simple.QiTypeCode = QiTypeCode.Object
  simple.Properties = [ time, state, measurement ]


*JavaScript*

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
    "Description": "This is a simple Qi type",
    "QiTypeCode": QiObjects.qiTypeCodeMap.Object,
    "Properties": [timeProperty, stateProperty, valueProperty]
  });

  Creating the QiStream with the Measurement as a Secondary Index is accomplished as follows:


*Python*

::

  measurementIndex = QiStreamIndex()
  measurementIndex.QiTypePropertyId = measurement.Id
  
  stream = QiStream()
  stream.Id = str(uuid.uuid4())
  stream.Name = "SimpleWithSecond"
  stream.Description = "Simple with secondary index"
  stream.TypeId = simple.Id
  stream.Indexes = [ measurementIndex ]

*JavaScript*

::

  var measurementIndex = new QiObjects.QiStreamIndex({
    "QiTypePropertyId": valueProperty.Id
  });

  var stream = new QiObjects.QiStream({
    "Id": "SimpleWithSecond",
    "Name": "SimpleWithSecond",
    "Description": "Simple with secondary index",
    "TypeId": simpleTypeId,
    "Indexes": [ measurementIndex ]
  });


**Compound Indexes**


Consider the following types:

*Python*

::

  class Simple(object):
    # First-order Key property
    Time = property(getTime, setTime)
    def getTime(self):
      return self.\_\_time
    def setTime(self, time):
      self.\_\_time = time
      
  State = property(getState, setState)
  def getState(self):
    return self.\_\_state
  def setState(self, state):
    self.\_\_state = state

  Measurement = property(getValue, setValue)
  def getValue(self):
    return self.\_\_measurement
  def setValue(self, measurement):
    self.\_\_measurement = measurement

  class DerivedCompoundIndex(Simple):
  # Second-order Key property
  @property
  def Recorded(self):
    return self.\_\_recorded
  @Recorded.setter
  def Recorded(self, recorded):
    self.\_\_recorded = recorded

*JavaScript*

::

  var Simple = function () {
    this.Time = null;
    this.State = null;
    this.Value = null;
  }

  var DerivedCompoundIndex = function() {
    Simple.call(this);
    this.Recorded = null;
  }

To turn the simple QiType from above into a type supporting the
DerivedCompoundIndex type with a compound index based on the Simple.Time
and DerivedCompoundIndex.Recorded, you would extend the type as follows

*Python*

# We set the Order for this property. The order of the key in Simple defaults to 0

::

  recorded = QiTypeProperty()
  recorded.Id = "Recorded"
  recorded.Name = "Recorded"
  recorded.IsKey = True
  recorded.Order = 1
  recorded.QiType = QiType()
  recorded.QiType.Id = "DateTime"
  recorded.QiType.Name = "DateTime"
  recorded.QiType.QiTypeCode = QiTypeCode.DateTime

  # Create the Derived QiType
  derived = QiType()
  derived.Id = str(uuid.uuid4())
  derived.Name = "Compound"
  derived.Description = "Derived compound index sample type"
  derived.BaseType = simple
  derived.QiTypeCode = QiTypeCode.Object
  derived.Properties = [ recorded ]

*JavaScript*

::

  // We set the Order for this property. The order of the key in Simple defaults to 0
  var recordedProperty = new QiObjects.QiTypeProperty({
    "Id": "Recorded",
    "Name": "Recorded",
    "IsKey": true,
    "Order": 1,
    "QiType": new QiObjects.QiType({
      "Id": "DateTime",
      "Name": "DateTime",
      "QiTypeCode": QiObjects.qiTypeCodeMap.DateTime
    })
  });

  // Create the Derived QiType
  var derivedType = new QiObjects.QiTyp({
    "Id": "Compound",
    "Name": "Compound",
    "Description": "Derived compound index sample type",
    "BaseType": simpleType,
    "QiTypeCode": QiObjects.qiTypeCodeMap.Object,
    "Properties": [recordedProperty]
  });

Events are ordered first by Time and then by Recorded. Thus a collection
of times would be sorted as follows

+------------+----------------+-------------------+
| **Time**   | **Recorded**   | **Measurement**   |
+============+================+===================+
| 01:00      | 00:00          | 0                 |
+------------+----------------+-------------------+
| 01:00      | 01:00          | 2                 |
+------------+----------------+-------------------+
| 01:00      | 14:00          | 5                 |
+------------+----------------+-------------------+
| 02:00      | 00:00          | 1                 |
+------------+----------------+-------------------+
| 02:00      | 01:00          | 3                 |
+------------+----------------+-------------------+
| 02:00      | 02:00          | 4                 |
+------------+----------------+-------------------+
| 02:00      | 14:00          | 6                 |
+------------+----------------+-------------------+

Were the Order swapped, Recorded as zero, the results would sort as
follows

+------------+----------------+-------------------+
| **Time**   | **Recorded**   | **Measurement**   |
+============+================+===================+
| 01:00      | 00:00          | 0                 |
+------------+----------------+-------------------+
| 02:00      | 00:00          | 1                 |
+------------+----------------+-------------------+
| 01:00      | 01:00          | 2                 |
+------------+----------------+-------------------+
| 02:00      | 01:00          | 3                 |
+------------+----------------+-------------------+
| 02:00      | 02:00          | 4                 |
+------------+----------------+-------------------+
| 01:00      | 14:00          | 5                 |
+------------+----------------+-------------------+
| 02:00      | 14:00          | 6                 |
+------------+----------------+-------------------+
