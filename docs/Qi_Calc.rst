Qi Calculation API
====================

.. toctree::

   Qi_Scripts
   Qi_Timezones
   Qi_Periodic_Schedules



The Qi Calculation API allows you to create custom calculations using JavaScript or TypeScript. The scripts you create 
can be either of the following types:

 - Scheduled
     Run on periodic schedule.
 - Triggered
     Run whenever a particular input stream receives an event.




The Qi Calculation API is provided using the ``IQiCalculationService`` interface, which may be accessed via the ``QiService.GetCalculationService( )`` helper.

The following table shows the required and optional Qi calculation properties:

+---------------+------------------------------+-------------+--------------------------------------------+
| Property      | Type                         | Optionality |Details                                     |
+===============+==============================+=============+============================================+
| ID            | String                       | Required    | An Identifier for referencing the stream.  |
+---------------+------------------------------+-------------+--------------------------------------------+
| TypeId        | String                       | Required    | The type to be used for this stream.       |
+---------------+------------------------------+-------------+--------------------------------------------+
| Name          | String                       | Optional    | The name of the stream.                    |
+---------------+------------------------------+-------------+--------------------------------------------+
| Description   | String                       | Optional    | Text that describes the stream.            |
+---------------+------------------------------+-------------+--------------------------------------------+
| BehaviorId    | String                       | Optional    | The stream behavior for this stream.       |
+---------------+------------------------------+-------------+--------------------------------------------+
| Tag           | String                       | Optional    | A collection of strings that permit        |
|               |                              |             | classifying and identifying individual     |
|               |                              |             | streams.                                   |
+---------------+------------------------------+-------------+--------------------------------------------+
| Metadata      | iDictionary<string, string>  | Optional    | A dictionary for users to store information|
|               |                              |             | that is relevant to the stream             |
+---------------+------------------------------+-------------+--------------------------------------------+
| Indexes       | IList<QiStreamIndex>         | Optional    | Used to define secondary indexes for stream|
+---------------+------------------------------+-------------+--------------------------------------------+

See
`Qi Calculation API <https://qi-docs-rst.readthedocs.org/en/latest/Qi_Calc_API.html>`__
for more information.

**Restrictions and limitations**

*Qi calculation ID*

1. Is not case sensitive.
2. Can contain spaces.
3. Cannot start with two underscores ("\_\_").
4. Can contain a maximum of 260 characters.
5. Cannot use the following characters: ( / : ? # [ ] @ ! $ & ' ( ) \* +
   , ; = %)
6. Cannot start or end with a period.
7. Cannot contain consecutive periods.
8. Cannot consist of only periods. 



