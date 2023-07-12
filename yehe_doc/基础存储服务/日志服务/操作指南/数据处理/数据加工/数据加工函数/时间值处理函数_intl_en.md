## Overview

CLS's time processing functions include functions for converting date values to string values, converting time field values to UTC time values and vice versa, and getting the current time.

## Function dt_str

#### Function definition

This function is used to convert a time field value (a date string in a specific format or timestamp) to a target date string of a specified time zone and format.

#### Syntax description

```sql
dt_str(Value, format="Formatted string", zone="")
```

#### Parameter description

| Parameter | Description | Parameter Type | Required | Default Value | Value Range |
|----------- | ----------- | ----------- | ----------- | -------------- | -------------- |
|data| Field value. For the parsing formats supported, see [dateparser](https://github.com/sisyphsu/dateparser).  | string | Yes | -  | -  |
|format | Formatted date. For more information, see [DateTimeFormatter](https://docs.oracle.com/javase/8/docs/api/java/time/format/DateTimeFormatter.html). | string | No | -  | -  |
|zone| Default UTC time, without a specified time zone. For time zone definitions, see [ZoneId](https://docs.oracle.com/javase/8/docs/api/java/time/ZoneId.html). |string| No |UTC+00:00| -  |

#### Example

Raw log:
```
{"date":"2014-04-26 13:13:44 +09:00"}
```
Processing rule:
```
fields_set("result", dt_str(v("date"), format="yyyy-MM-dd HH:mm:ss", zone="UTC+8"))
```
Processing result:
```
{"date":"2014-04-26 13:13:44 +09:00","result":"2014-04-26 12:13:44"}
```


## Function dt_to_timestamp

#### Function definition

This function is used to convert a time field value (a date string in a specified format; time zone specified) to a UTC timestamp.

#### Syntax description

```sql
dt_to_timestamp(Value, zone="")
```

#### Parameter description

| Parameter | Description | Parameter Type | Required | Default Value | Value Range |
|----------- | ----------- | ----------- | ----------- | -------------- | -------------- |
|data| Field value. For the parsing formats supported, see [dateparser](https://github.com/sisyphsu/dateparser).  | string | Yes | -  | -  |
|zone| UTC time is used by default, without a time zone specified. If you specify a time zone, make sure that it corresponds to the time field value. Otherwise, a time zone error occurs. For time zone definitions, see [ZoneId](https://docs.oracle.com/javase/8/docs/api/java/time/ZoneId.html). |string| No |UTC+00:00| -  |

#### Example 

Raw log:
```
{"date":"2021-10-26 15:48:15"}
```
Processing rule:
```
fields_set("result", dt_to_timestamp(v("date"), zone="UTC+8"))
```
Processing result:
```
{"date":"2021-10-26 15:48:15","result":"1635234495000"}
```


## Function dt_from_timestamp

#### Function definition

This function is used to convert a timestamp field value to a time string in the specified time zone.

#### Syntax description

```sql
dt_from_timestamp(Value, zone="")
```

#### Parameter description

| Parameter | Description | Parameter Type | Required | Default Value | Value Range |
|----------- | ----------- | ----------- | ----------- | -------------- | -------------- |
|data| Field value. For the parsing formats supported, see [dateparser](https://github.com/sisyphsu/dateparser).  | string | Yes | -  | -  |
|zone| Default UTC time, without a specified time zone. For time zone definitions, see [ZoneId](https://docs.oracle.com/javase/8/docs/api/java/time/ZoneId.html). |string| No |UTC+00:00| -  |


#### Example
Raw log:
```
{"date":"1635234495000"}
```
Processing rule:
```
fields_set("result", dt_from_timestamp(v("date"), zone="UTC+8"))
```
Processing result:
```
{"date":"1635234495000","result":"2021-10-26 15:48:15"}
```

## Function dt_now

#### Function definition

This function is used to obtain the current datetime of the processing calculation.

#### Syntax description

```
dt_now(format="Formatted string", zone="")
```

#### Parameter description

| Parameter | Description | Parameter Type | Required | Default Value | Value Range |
|----------- | ----------- | ----------- | ----------- | -------------- | -------------- |
|format | Formatted date. For more information, see [DateTimeFormatter](https://docs.oracle.com/javase/8/docs/api/java/time/format/DateTimeFormatter.html). | string | No | -  | -  |
|zone| Default UTC time, without a specified time zone. For time zone definitions, see [ZoneId](https://docs.oracle.com/javase/8/docs/api/java/time/ZoneId.html). |string| No |UTC+00:00| -  |

#### Example
Raw log:
```
{"date":"1635234495000"}
```
Processing rule:
```
fields_set("now", dt_now(format="yyyy-MM-dd HH:mm:ss", zone="UTC+8"))
```
Processing result: (The actual processing result depends on the system time, and the following is for reference only.)
```
{"date":"1635234495000","now":"2021-MM-dd HH:mm:ss"}
```
