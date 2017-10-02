QiView information
******************

Views provide a way to map Stream data, on a request, from one Type to another. A View can be applied 
to any read or GET. The QiView specifies mapping using a source and target type. 

Qi attempts to determine how to map Properties from the source to the destination. 
When the mapping is straightforward, such as when the properties are in the same position and of the same type, or when 
the properties are of the same name, Qi will map the properties automatically. 

When Qi is unable to determine how to map a source property, the property is removed. When Qi encounters 
a property on the target that it cannot map to, it will add the property and leave it at the default value.

To map a property that is beyond the ability of Qi to map on its own, you should define a QiViewProperty 
and add it to the QiVeiw’s Properties collection.

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

Measurement to a double Value. Then map a double Measurement to an int Measurement. Then show the 
failure to map a double Measurement to an int Value … introduce Properties

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

The following table shows the QiViewMap fields. The QiVeiwMap cannot be written to Qi, 
so required and optional have no meaning.

+---------------------------+--------------------------------+--------------------------------------------------+
| Property                  | Type                           | Details                                          |
+===========================+================================+==================================================+
| Id                        | String                         | Identifier of referencing the QiView             |
+---------------------------+--------------------------------+--------------------------------------------------+
| Name                      | String                         | QiView friendly name                             |
+---------------------------+--------------------------------+--------------------------------------------------+
|Description                | String                         | QiView description                               |
+---------------------------+--------------------------------+--------------------------------------------------+
| SourceTypeId              | String                         | Identifier of the QiType of the QiStream. The    |
|                           |                                | source type                                      |
+---------------------------+--------------------------------+--------------------------------------------------+
| TargetTypeId              | String                         | Identifier of the QiType to convert events to    |
+---------------------------+--------------------------------+--------------------------------------------------+
| Properties                | IList<QiViewMapProperty>       | Property level mapping                           |
+---------------------------+--------------------------------+--------------------------------------------------+






