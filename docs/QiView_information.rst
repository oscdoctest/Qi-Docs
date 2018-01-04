.. _Qi_View_topic:

==================
QiView information
==================

A QiView provides a way to map Stream data requests from one data type to another. You can apply 
a View to any read or GET operation. QiView is used to specify the mapping between source and target types.

Qi attempts to determine how to map Properties from the source to the destination. When the mapping 
is straightforward, such as when the properties are in the same position and of the same data type, 
or when the properties have the same name, Qi will map the properties automatically.

When Qi is unable to determine how to map a source property, the property is removed. If Qi encounters 
a target property that it cannot map to, the property is added and configured with a default value.

To map a property that is beyond the ability of Qi to map on its own, you should define a QiViewProperty 
and add it to the QiView’s Properties collection.


QiView
------

The following table shows the required and optional QiView fields. Fields that are not included are reserved for internal Qi use.

+------------------+-------------------------+-------------+-------------------------------------+
| Property         | Type                    | Optionality | Details                             |
+==================+=========================+=============+=====================================+
| Id               | String                  | Required    | Identifier for referencing the view |
+------------------+-------------------------+-------------+-------------------------------------+
| Name             | String                  | Optional    | Friendly name                       |
+------------------+-------------------------+-------------+-------------------------------------+
| Description      | String                  | Optional    | Description text                    |
+------------------+-------------------------+-------------+-------------------------------------+
| SourceTypeId     | String                  | Required    | Identifier of the QiType of the     |
|                  |                         |             | QiStream. The source type           |
+------------------+-------------------------+-------------+-------------------------------------+
| TargetTypeId     | String                  | Required    | Identifier of the QiType to convert |
|                  |                         |             | events to                           |
+------------------+-------------------------+-------------+-------------------------------------+
| Properties       | IList<QiViewProperty>   | Optional    | Property level mapping              |
+------------------+-------------------------+-------------+-------------------------------------+


**Rules for type identifier**

1. Is not case sensitive
2. Can contain spaces
3. Cannot begin with two underscores ("\_\_")
4. Cannot contain forward slash or backslash characters ("/" or "\\")
5. Can contain a maximum of 260 characters
6. Cannot start or end with a period.
7. Cannot contain consecutive periods.
8. Cannot consist of only periods.


Properties / QiViewProperty
---------------------------

The QiView Properties collection provides detailed instructions for specifying the mapping of 
event properties. Each QiViewProperty in the Properties collection defines the mapping of an 
event’s property. 

The following table shows the required and optional QiViewProperty fields.

+------------------+-------------------------+-------------+-------------------------------------+
| Property         | Type                    | Optionality | Details                             |
+==================+=========================+=============+=====================================+
| SourceId         | String                  | Required    | Identifier of the QiTypeProperty    |
|                  |                         |             | from the source QiType Properties   |
|                  |                         |             | list.                               |
+------------------+-------------------------+-------------+-------------------------------------+
| TargetId         | String                  | Required    | Identifier of the QiTypeProperty    |
|                  |                         |             | from the target QiType Properties   |
|                  |                         |             | list                                |
+------------------+-------------------------+-------------+-------------------------------------+
| QiView           | QiView                  | Optional    | Additional mapping instructions     |
|                  |                         |             | for derived types                   |
+------------------+-------------------------+-------------+-------------------------------------+

The QiView field supports nested Properties.

QiViewMap
---------

When a QiView is added, Qi defines a plan mapping. Plan details are retrieved as a QiViewMap. 
The QiViewMap provides a detailed Property-by-Property definition of the mapping. 

The following table shows the QiViewMap fields. The QiViewMap cannot be written to Qi, 
so required and optional have no meaning.

+---------------------------+--------------------------+--------------+--------------------------------------------------+
| Property                  | Type                     | Optionality  | Details                                          |
+===========================+==========================+==============+==================================================+
| Id                        | String                   | Required     | Identifier of referencing the QiView             |
+---------------------------+--------------------------+--------------+--------------------------------------------------+
| Name                      | String                   | Optional     | QiView friendly name                             |
+---------------------------+--------------------------+--------------+--------------------------------------------------+
| Description               | String                   | Optional     | QiView description                               |
+---------------------------+--------------------------+--------------+--------------------------------------------------+
| SourceTypeId              | String                   | Required     | Identifier of the QiType of the QiStream. The    |
|                           |                          |              | source type                                      |
+---------------------------+--------------------------+--------------+--------------------------------------------------+
| TargetTypeId              | String                   | Required     | Identifier of the QiType to convert events to    |
+---------------------------+--------------------------+--------------+--------------------------------------------------+
| Properties                | IList<QiViewMapProperty> | Optional     | Property level mapping                           |
+---------------------------+--------------------------+--------------+--------------------------------------------------+

Properties / QiViewMapProperty
------------------------------

The QiViewMapProperty is similar a QiViewProperty but adds a Mode detailing one or more actions taken on 
the Property.

The following table shows the QiViewMapProperty fields. The QiViewMap cannot be written, it can only be 
retrieved from Qi, so required and optional have no meaning.

+---------------------------+--------------------------------+--------------------------------------------------+
| Property                  | Type                           | Details                                          |
+===========================+================================+==================================================+
| SourceTypeId              | String                         | Identifier of the QiType of the QiStream. The    |
|                           |                                | source type                                      |
+---------------------------+--------------------------------+--------------------------------------------------+
| TargetTypeId              | String                         | Identifier of the QiType to convert events to    |
+---------------------------+--------------------------------+--------------------------------------------------+
| Mode                      | QiViewMode                     | Aggregate of actions applied to the properties.  |
|                           |                                | QiViewModes are combined via binary arithmetic   |
+---------------------------+--------------------------------+--------------------------------------------------+
| QiViewMap                 | QiViewMap                      | Mapping for derived types                        |
+---------------------------+--------------------------------+--------------------------------------------------+

The available QiViewModes are shown in the table below.

+---------------------------+--------------------------------+--------------------------------------------------+
| Name                      | Value                          | Description                                      |
+===========================+================================+==================================================+
| None                      | 0x0000                         | No action                                        |
+---------------------------+--------------------------------+--------------------------------------------------+
| FieldAdd                  | 0x0001                         | Add a property matching the specified            |
|                           |                                | QiTypeProperty                                   |
+---------------------------+--------------------------------+--------------------------------------------------+
| FieldRemove               | 0x0002                         | Remove the property matching the specified       |
|                           |                                | QiTypeProperty                                   |
+---------------------------+--------------------------------+--------------------------------------------------+
| FieldRename               | 0x0004                         | Rename the property matching the source          |
|                           |                                | QiTypeProperty to the target QiTypeProperty      |
+---------------------------+--------------------------------+--------------------------------------------------+
| FieldMove                 | 0x0008                         | Move the property from the location in the       |
|                           |                                | source to the location in the target             |
+---------------------------+--------------------------------+--------------------------------------------------+
| FieldConversion           | 0x0016                         | Converts the source property to the target type  |
+---------------------------+--------------------------------+--------------------------------------------------+
| InvalidFieldConversion    | 0x0032                         | Cannot perform the specified mapping             |
+---------------------------+--------------------------------+--------------------------------------------------+

Changing Stream Type
--------------------

Views can be used to change the Type defining a Stream. You cannot modify the QiType; types are immutable. 
But you map a stream from its current type to a new type.

To update a Stream Type, define a QiView and PUT the view to the following:

::

   api/Tenants/{tenantId}/Namespaces/{namespaceId}/Streams/{streamId}/Type?viewId={viewId}


For details, see QiView API.

Working with QiViews
--------------------

**Using .Net**

When working in .NET, use the Qi Client libraries’ IQiMetadataService.

Given the following:

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
      public double Measurement { get; set; }
  }

  QiType simpleType = QiTypeBuilder.CreateQiType<Simple>();
  simpleType.Id = "Simple";
  simpleType.Name = "Simple";
  await config.GetOrCreateTypeAsync(simpleType);//.CreateOrUpdateTypeAsync(simpleType);//.GetOrCreateTypeAsync(simpleType);

  QiStream simpleStream = await config.GetOrCreateStreamAsync(new QiStream()
  {
      Id = "Simple",
      Name = "Simple",
      TypeId = simpleType.Id
  });

  DateTime start = new DateTime(2017, 4, 1).ToUniversalTime();

  for (int i = 0; i < 10; i++)
  {
      Simple value = new Simple()
      {
          Time = start + TimeSpan.FromMinutes(i),
          State = State.Warning,
          Measurement = i
      };
      await client.InsertValueAsync(simpleStream.Id, value);
  }

  IEnumerable<Simple> simpleValues = await client.GetWindowValuesAsync<Simple>(simpleStream.Id, start.ToString("o"),
      start.Add(TimeSpan.FromMinutes(10)).ToString("o"));
  foreach (Simple value in simpleValues)
      Console.WriteLine($"{value.Time}: {value.State}, {value.Measurement}");

  // The example displays the following output:
  //  4 / 1 / 2017 7:00:00 AM: Warning, 0
  //  4 / 1 / 2017 7:01:00 AM: Warning, 1
  //  4 / 1 / 2017 7:02:00 AM: Warning, 2
  //  4 / 1 / 2017 7:03:00 AM: Warning, 3
  //  4 / 1 / 2017 7:04:00 AM: Warning, 4
  //  4 / 1 / 2017 7:05:00 AM: Warning, 5
  //  4 / 1 / 2017 7:06:00 AM: Warning, 6
  //  4 / 1 / 2017 7:07:00 AM: Warning, 7
  //  4 / 1 / 2017 7:08:00 AM: Warning, 8
  //  4 / 1 / 2017 7:09:00 AM: Warning, 9

To map the Measurement property to a property in the same location of the same type, allow Qi to 
automatically determine mapping.

::

  public class Simple1
  {
      [QiMember(IsKey = true, Order = 0)]
      public DateTime Time { get; set; }
      public State State { get; set; }
      public double Value { get; set; }
  }

  QiType simple1Type = QiTypeBuilder.CreateQiType<Simple1>();
  simple1Type.Id = "Simple1";
  simple1Type.Name = "Simple1";
  simple1Type = await config.GetOrCreateTypeAsync(simple1Type);

  QiView view = new QiView()
  {
      Id = "View",
      Name = "View",
      SourceTypeId = simpleType.Id,
      TargetTypeId = simple1Type.Id,
  };
  view = await config.GetOrCreateViewAsync(view);

  QiViewMap map = await config.GetViewMapAsync(view.Id);
  Console.WriteLine($"{map.Id}: {map.SourceTypeId} to {map.TargetTypeId}");
  for (int i = 0; i < map.Properties.Count; i++)
      Console.WriteLine($"\t{i}) {map.Properties[i].SourceId} to {map.Properties[i].TargetId} - {map.Properties[i].Mode}");
  Console.WriteLine();

  IEnumerable<Simple1> simple1Values = await client.GetWindowValuesAsync<Simple1>(simpleStream.Id, start.ToString("o"),
      start.Add(TimeSpan.FromMinutes(10)).ToString("o"), view.Id);
  foreach (Simple1 value in simple1Values)
      Console.WriteLine($"{value.Time}: {value.State}, {value.Value}");

  // The example displays the following output:
  //    View: Simple to Simple1
  //        0) Time to Time - None
  //        1) State to State - None
  //        2) Measurement to Value - FieldRename
  //
  //  4 / 1 / 2017 7:00:00 AM: Warning, 0
  //  4 / 1 / 2017 7:01:00 AM: Warning, 1
  //  4 / 1 / 2017 7:02:00 AM: Warning, 2
  //  4 / 1 / 2017 7:03:00 AM: Warning, 3
  //  4 / 1 / 2017 7:04:00 AM: Warning, 4
  //  4 / 1 / 2017 7:05:00 AM: Warning, 5
  //  4 / 1 / 2017 7:06:00 AM: Warning, 6
  //  4 / 1 / 2017 7:07:00 AM: Warning, 7
  //  4 / 1 / 2017 7:08:00 AM: Warning, 8
  //  4 / 1 / 2017 7:09:00 AM: Warning, 9

A quick look at the QiViewMap shows that Qi was able to determine that mapping from Measurement 
to Value involved a rename.

Qi can also determine mapping of properties of the same name but different type. Note that the 
location of the Measurement property is also different yet it is still mapped.

::

  public class Simple2
  {
      [QiMember(IsKey = true, Order = 0)]
      public DateTime Time { get; set; }
      public int Measurement { get; set; }
      public State State { get; set; }
  }

  QiType simple2Type = QiTypeBuilder.CreateQiType<Simple2>();
  simple2Type.Id = "Simple2";
  simple2Type.Name = "Simple2";
  simple2Type = await config.GetOrCreateTypeAsync(simple2Type);

  view = new QiView()
  {
      Id = "View1",
      Name = "View1",
      SourceTypeId = simpleType.Id,
      TargetTypeId = simple2Type.Id,
  };
  view = await config.GetOrCreateViewAsync(view);

  map = await config.GetViewMapAsync(view.Id);
  Console.WriteLine($"{map.Id}: {map.SourceTypeId} to {map.TargetTypeId}");
  for (int i = 0; i < map.Properties.Count; i++)
      Console.WriteLine($"\t{i}) {map.Properties[i].SourceId} to {map.Properties[i].TargetId} - {map.Properties[i].Mode}");
  Console.WriteLine();

  IEnumerable<Simple2> simple2Values = await client.GetWindowValuesAsync<Simple2>(simpleStream.Id, start.ToString("o"),
      start.Add(TimeSpan.FromMinutes(10)).ToString("o"), view.Id);
  foreach (Simple2 value in simple2Values)
      Console.WriteLine($"{value.Time}: {value.State}, {value.Measurement}");

  //The example displays the following output:
  //    View: Simple to Simple2
  //        0) Time to Time - None
  //        1) State to State - None
  //        2) Measurement to Measurement - FieldConversion
  //
  //    4 / 1 / 2017 7:00:00 AM: Warning, 0
  //    4 / 1 / 2017 7:01:00 AM: Warning, 1
  //    4 / 1 / 2017 7:02:00 AM: Warning, 2
  //    4 / 1 / 2017 7:03:00 AM: Warning, 3
  //    4 / 1 / 2017 7:04:00 AM: Warning, 4
  //    4 / 1 / 2017 7:05:00 AM: Warning, 5
  //    4 / 1 / 2017 7:06:00 AM: Warning, 6
  //    4 / 1 / 2017 7:07:00 AM: Warning, 7
  //    4 / 1 / 2017 7:08:00 AM: Warning, 8
  //    4 / 1 / 2017 7:09:00 AM: Warning, 9


The QiViewMap shows that the source, floating point Measurement is converted to the target, integer Measurement.

When neither the field name nor field type and location match, Qi does not determine mapping. 
The source is eliminated and target is added and assigned the default value.

::

  public class Simple3
  {
      [QiMember(IsKey = true, Order = 0)]
      public DateTime Time { get; set; }
      public State State { get; set; }
      public int Value { get; set; }
  }

  QiType simple3Type = QiTypeBuilder.CreateQiType<Simple3>();
  simple3Type.Id = "Simple3";
  simple3Type.Name = "Simple3";
  simple3Type = await config.GetOrCreateTypeAsync(simple3Type);

  view = new QiView()
  {
      Id = "View2",
      Name = "View2",
      SourceTypeId = simpleType.Id,
      TargetTypeId = simple3Type.Id,
  };
  view = await config.GetOrCreateViewAsync(view);

  map = await config.GetViewMapAsync(view.Id);
  Console.WriteLine($"{map.Id}: {map.SourceTypeId} to {map.TargetTypeId}");
  for (int i = 0; i < map.Properties.Count; i++)
      Console.WriteLine($"\t{i}) {map.Properties[i].SourceId} to {map.Properties[i].TargetId} - {map.Properties[i].Mode}");
  Console.WriteLine();

  IEnumerable<Simple3> simple3Values = await client.GetWindowValuesAsync<Simple3>(simpleStream.Id, start.ToString("o"),
      start.Add(TimeSpan.FromMinutes(10)).ToString("o"), view.Id);
  foreach (Simple3 value in simple3Values)
      Console.WriteLine($"{value.Time}: {value.State}, {value.Value}");

  //The example displays the following output:
  //    View2 : Simple to Simple3
  //        0) Time to Time - None
  //        1) State to State - None
  //        2) Measurement to  -FieldRemove
  //        3)  to Value -FieldAdd
  //
  // 4 / 1 / 2017 7:00:00 AM: Warning, 0
  // 4 / 1 / 2017 7:01:00 AM: Warning, 0
  // 4 / 1 / 2017 7:02:00 AM: Warning, 0
  // 4 / 1 / 2017 7:03:00 AM: Warning, 0
  // 4 / 1 / 2017 7:04:00 AM: Warning, 0
  // 4 / 1 / 2017 7:05:00 AM: Warning, 0
  // 4 / 1 / 2017 7:06:00 AM: Warning, 0
  // 4 / 1 / 2017 7:07:00 AM: Warning, 0
  // 4 / 1 / 2017 7:08:00 AM: Warning, 0
  // 4 / 1 / 2017 7:09:00 AM: Warning, 0


To map when Qi cannot determine mapping, use QiView Properties.

::

  view = new QiView()
  {
      Id = "View3",
      Name = "View3",
      SourceTypeId = simpleType.Id,
      TargetTypeId = simple3Type.Id,
      Properties = new List<QiViewProperty>()
      {
          new QiViewProperty()
          {
              SourceId = "Time",
              TargetId = "Time"
          },
          new QiViewProperty()
          {
              SourceId = "Status",
              TargetId = "Status"
          },
          new QiViewProperty()
          {
              SourceId = "Measurement",
              TargetId = "Value"
          }
      }
  };
  view = await config.GetOrCreateViewAsync(view);

  map = await config.GetViewMapAsync(view.Id);
  Console.WriteLine($"{map.Id}: {map.SourceTypeId} to {map.TargetTypeId}");
  for (int i = 0; i < map.Properties.Count; i++)
      Console.WriteLine($"\t{i}) {map.Properties[i].SourceId} to {map.Properties[i].TargetId} - {map.Properties[i].Mode}");
  Console.WriteLine();

  simple3Values = await client.GetWindowValuesAsync<Simple3>(simpleStream.Id, start.ToString("o"),
      start.Add(TimeSpan.FromMinutes(10)).ToString("o"), view.Id);
  foreach (Simple3 value in simple3Values)
      Console.WriteLine($"{value.Time}: {value.State}, {value.Value}");

  //The example displays the following output:
  //    View3 : Simple to Simple3
  //        0) Time to Time - None
  //        1) State to State - None
  //        2) Measurement to Value - FieldRename, FieldConversion
  //
  //    4 / 1 / 2017 7:00:00 AM: Warning, 0
  //    4 / 1 / 2017 7:01:00 AM: Warning, 1
  //    4 / 1 / 2017 7:02:00 AM: Warning, 2
  //    4 / 1 / 2017 7:03:00 AM: Warning, 3
  //    4 / 1 / 2017 7:04:00 AM: Warning, 4
  //    4 / 1 / 2017 7:05:00 AM: Warning, 5
  //    4 / 1 / 2017 7:06:00 AM: Warning, 6
  //    4 / 1 / 2017 7:07:00 AM: Warning, 7
  //    4 / 1 / 2017 7:08:00 AM: Warning, 8
  //    4 / 1 / 2017 7:09:00 AM: Warning, 9


Working with QiViews when not using .NET
----------------------------------------

When working with Views and not using .NET, either invoke HTTP directly or use some of 
the sample code. Both Python and JavaScript samples have QiView definitions.

The JSON for a simple mapping between a source type with identifier Sample and a target 
type with identifier Sample1 would appear as follows.

::

  {  
     "Id":"View",
     "Name":"View",
     "SourceTypeId":"Simple",
     "TargetTypeId":"Simple1"
  }

The QiViewMap would appear as follows.

::
 
  {  
     "SourceTypeId":"Simple",
     "TargetTypeId":"Simple1",
     "Properties":[  
        {  
           "SourceId":"Time",
           "TargetId":"Time"
        },
        {  
           "SourceId":"State",
           "TargetId":"State"
        },
        {  
           "SourceId":"Measurement",
           "TargetId":"Value",
           "Mode":4
        }
     ]
  }








