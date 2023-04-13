Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# CRON Expressions

Share Feedback

On this page

  * Expression Syntax
  * Format
  * Field Values

CRON expressions are user-defined strings that use standard cron job syntax to
define when a scheduled trigger should execute. Whenever all of the fields in
a CRON expression match the current date and time, Atlas fires the trigger
associated with the expression.

## Expression Syntax

### Format

CRON expressions are strings composed of five space-delimited fields. Each
field defines a granular portion of the schedule on which its associated
trigger executes:

    
    
    * * * * *  
      
    │ │ │ │ └── weekday...........[0 (SUN) - 6 (SAT)]  
    │ │ │ └──── month.............[1 (JAN) - 12 (DEC)]  
    │ │ └────── dayOfMonth........[1 - 31]  
    │ └──────── hour..............[0 - 23]  
    └────────── minute............[0 - 59]  
  
Field

|

Valid Values

|

Description  
  
||  
  
`minute`

|

[0 - 59]

|

Represents one or more minutes within an hour.

## Example

If the `minute` field of a CRON expression has a value of `10`, the field
matches any time ten minutes after the hour (e.g. `9:10 AM`).  
  
`hour`

|

[0 - 23]

|

Represents one or more hours within a day on a 24-hour clock.

## Example

If the `hour` field of a CRON expression has a value of `15`, the field
matches any time between `3:00 PM` and `3:59 PM`.  
  
`dayOfMonth`

|

[1 - 31]

|

Represents one or more days within a month.

## Example

If the `dayOfMonth` field of a CRON expression has a value of `3`, the field
matches any time on the third day of the month.  
  
`month`

|

`1 (JAN)` `7 (JUL)`

`2 (FEB)` `8 (AUG)`

`3 (MAR)` `9 (SEP)`

`4 (APR)` `10 (OCT)`

`5 (MAY)` `11 (NOV)`

`6 (JUN)` `12 (DEC)`

|

Represents one or more months within a year.

A month can be represented by either a number (e.g. `2` for February) or a
three-letter string (e.g. `APR` for April).

## Example

If the `month` field of a CRON expression has a value of `9`, the field
matches any time in the month of September.  
  
`weekday`

|

`0 (SUN)`

`1 (MON)`

`2 (TUE)`

`3 (WED)`

`4 (THU)`

`5 (FRI)`

`6 (SAT)`

|

Represents one or more days within a week.

A weekday can be represented by either a number (e.g. `2` for a Tuesday) or a
three-letter string (e.g. `THU` for a Thursday).

## Example

If the `weekday` field of a CRON expression has a value of `3`, the field
matches any time on a Wednesday.  
  
### Field Values

Each field in a CRON expression can contain either a specific value or an
expression that evaluates to a set of values. The following table describes
valid field values and expressions:

Expression Type

|

Description  
  
|  
  
 **All Values**

(`*`)

|

Matches all possible field values.

Available in all expression fields.

## Example

The following CRON expression schedules a trigger to execute once every minute
of every day:

    
    
    | * * * * *  
      
  
 **Specific Value**

(`<Value>`)

|

Matches a specific field value. For fields other than `weekday` and `month`
this value will always be an integer. A `weekday` or `month` field can be
either an integer or a three-letter string (e.g. `TUE` or `AUG`).

Available in all expression fields.

## Example

The following CRON expression schedules a trigger to execute once every day at
11:00 AM UTC:

    
    
    | 0 11 * * *  
      
  
 **List of Values**

(`<Expression1>,<Expression2>,...`)

|

Matches a list of two or more field expressions or specific values.

Available in all expression fields.

## Example

The following CRON expression schedules a trigger to execute once every day in
January, March, and July at 11:00 AM UTC:

    
    
    | 0 11 * 1,3,7 *  
      
  
 **Range of Values**

(`<Start Value>-<End Value>`)

|

Matches a continuous range of field values between and including two specific
field values.

Available in all expression fields.

## Example

The following CRON expression schedules a trigger to execute once every day
from January 1st through the end of April at 11:00 AM UTC:

    
    
    | 0 11 * 1-4 *  
      
  
 **Modular Time Step**

(`<Field Expression>/<Step Value>`)

|

Matches any time where the step value evenly divides the field value with no
remainder (i.e. when `Value % Step == 0`).

Available in the `minute` and `hour` expression fields.

## Example

The following CRON expression schedules a trigger to execute on the 0th, 25th,
and 50th minutes of every hour:

    
    
    | */25 * * * *  
      
  
← Send Trigger Events to AWS EventBridgeExternal Dependencies →

