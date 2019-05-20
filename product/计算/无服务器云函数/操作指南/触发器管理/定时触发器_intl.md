You can write an SCF function to handle a scheduled task (which can be triggered in seconds). The timer will automatically trigger the function at the specified time. Timer triggers have the following characteristics:
- **Push model**: The timer directly calls the Invoke API of the function to trigger it at the specified time. The event source mapping is retained in the SCF function.
- **Async call**: A timer trigger always calls a function asynchronously, and the result is not returned to the caller. For more information about calling types, see [Calling Types](https://cloud.tencent.com/document/product/583/9694#.E8.B0.83.E7.94.A8.E7.B1.BB.E5.9E.8B).

## Timer Trigger Configurations

- Timer name (required): It can contain up to 60 characters, including `a-z`, `A-Z`, `0-9`, `-`, and `_`. It must begin with a letter and be unique under the same function.
- Triggering cycle (required): This is the specified function triggering time. You can use the default value in the console or customize a standard cron expression to decide when to trigger the function. For more information about cron expressions, see below.
- Input parameter (optional): It can be a string or JSON data structure of up to 4 KB, which can be obtained from the "event" parameter of the entry function.

## Cron Expression

When creating a timer trigger, you can customize the triggering time using a standard cron expression. Timer triggers can trigger functions in a matter of seconds. In order to be compatible with older timer triggers, cron expressions can be written in two ways:

 

### Cron Expression Syntax 1 (Recommended)

A cron expression has seven required fields, separated by spaces.
						
| First | Second | Third | Fourth | Fifth | Sixth | Seventh |
|----------|----------|----------|---------|----------|----------|----------|
| Second | Minute | Hour | Day | Month | Week | Year |

Each field has a corresponding value range:

| Field | Value | Wildcards |
|-------|-------|--------|
| Second | An integer between 0 and 59 | , - * / |
| Minute | An integer between 0 and 59 | , - * / |
| Hours | An integer between 0 and 23 | , - * / |
| Day | An integer between 1 and 31 (the number of days in the month needs to be considered) | , - * / |
| Month | An integer between 1 and 12 or JAN, FEB, MAR, APR, MAY, JUN, JUL, AUG, SEP, OCT, NOV, DEC | , - * / |
| Week | An integer between 0 and 6 or MON, TUE, WED, THU, FRI, SAT, SUN; where 0 means Monday, 1 means Tuesday, and so on |, - * / |
| Year | An integer between 1970 and 2099 | , - * / |

### Cron Expression Syntax 2 (Not Recommended)

A cron expression has five required fields, separated by spaces.

| First | Second | Third | Fourth | Fifth |
|----------|----------|----------|---------|------ ----|
| Minute | Hour | Day | Month | Week |

Each field has a corresponding value range:

| Field | Value | Wildcards |
|---------|---------|---------|
| Minute | An integer between 0 and 59 | , - * / |
| Hours | An integer between 0 and 23 | , - * / |
| Day | An integer between 1 and 31 (the number of days in the month needs to be considered) | , - * / |
| Month | An integer between 1 and 12 or JAN, FEB, MAR, APR, MAY, JUN, JUL, AUG, SEP, OCT, NOV, DEC | , - * / |
| Week | An integer between 0 and 6 or MON, TUE, WED, THU, FRI, SAT, SUN; where 0 means Monday, 1 means Tuesday, and so on |, - * / |

### Wildcards

| Wildcard | Meaning |
|--|--|
| , (comma) | It represents the union of characters separated by commas. For example, 1, 2, 3 in the "Hour" field means 1:00, 2:00 and 3:00 |
|- (dash) | It contains all values in the specified range. For example, in the "Day" field, 1-15 contains the 1st to the 15th day of the specified month |
| \* (asterisk) | It means all values. For example, in the "Hour" field, \* means every o'clock |
| / (forward slash) | It specifies the increment. For example, in the "Minute" field, you can enter 1/10 to specify repeating every ten minutes from the first minute on (e.g., at the 11th minute, the 21st minute, the 31st minute, and so on) |

### Precautions

When both the "Day" and "Week" fields in a cron expression are specified, they are in an "or" relationship, i.e., the conditions of both are effective separately.

### Sample

Below are some examples of cron expressions and their meanings:
- `*/5 * * * * * *` means triggering every 5 seconds
- `0 0 2 1 * * *` means triggering at 2 am on the 1st day of every month
- `0 15 10 * * MON-FRI *` means triggering every day at 10:15 am Monday through Friday
- `0 0 10,14,16 * * * *` means triggering every day at 10 am, 2 pm, and 4 pm
- `0 */30 9-17 * * * *` means triggering every half hour from 9 am to 5 pm every day
- `0 0 12 * * WED *` means triggering at 12:00 noon every Wednesday

## Input Parameters of Timer Triggers

When a timer trigger triggers a function, the following data structures are encapsulated in "event" and passed to the function. In addition, you can specify to pass the "message" for a timer trigger, which is null by default.
```
{
    "Type":"timer",
    "TriggerName":"EveryDay",
    "Time":"2019-02-21T11:49:00Z",
    "Message":"user define msg body"
}
```
| Field | Meaning |
|--|--|
| Type | Type of the trigger, whose value is timer |
| TriggerName | Name of the timer trigger. It can contain up to 60 characters, including `a-z`, `A-Z`, `0-9`, `-`, and `_`. It must begin with a letter and be unique under the same function |
| Time | Trigger creation time, in UTC+0 |
| Message | String or JSON data structure |
