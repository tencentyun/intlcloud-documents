You can write an SCF function to handle a scheduled task (which can be triggered in seconds). The timer will automatically trigger the function at the specified time. Timer triggers have the following characteristics:
- **Push model**: the timer directly calls the `Invoke` API of the function to trigger it at the specified time. The event source mapping is retained in the SCF function.
- **Async invocation**: a timer trigger always invokes a function asynchronously, and the result is not returned to the invoker. For more information on invocation types, please see [Invocation Types](https://intl.cloud.tencent.com/document/product/583/9694).

## Timer Trigger Attributes

- Timer name (required): it can contain up to 60 characters out of `a-z`, `A-Z`, `0-9`, `-`, and `_` and must begin with a letter and be unique under the same function.
- Triggering cycle (required): this is the specified function triggering time. You can use the default value in the console or customize a standard cron expression to decide when to trigger the function. For more information on cron expressions, please see below.
- Input parameter (optional): it can be a string of up to 4 KB, which can be obtained from the `event` parameter of the entry function.

## Cron Expression
When creating a timer trigger, you can customize the triggering time by using a standard cron expression. Timer triggers can trigger functions in a matter of seconds. In order to be compatible with legacy timer triggers, cron expressions can be written in two ways:


### Cron expression syntax 1 (recommended)
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
| Week | An integer between 0 and 6 or SUN, MON, TUE, WED, THU, FRI, SAT; where 0 means Sunday, 1 means Monday, and so on | , - * / |
| Year | An integer between 1970 and 2099 | , - * / |

### Cron expression syntax 2 (not recommended)
A cron expression has five required fields, separated by spaces.

| First | Second | Third | Fourth | Fifth |
|----------|----------|----------|---------|----------|
| Minute | Hour | Day | Month | Week |

Each field has a corresponding value range:

| Field | Value | Wildcards |
|---------|---------|---------|
| Minute | An integer between 0 and 59 | , - * / |
| Hours | An integer between 0 and 23 | , - * / |
| Day | An integer between 1 and 31 (the number of days in the month needs to be considered) | , - * / |
| Month | An integer between 1 and 12 or JAN, FEB, MAR, APR, MAY, JUN, JUL, AUG, SEP, OCT, NOV, DEC | , - * / |
| Week | An integer between 0 and 6 or SUN, MON, TUE, WED, THU, FRI, SAT; where 0 means Sunday, 1 means Monday, and so on | , - * / |

### Wildcards
<table>
	<tr>
		<th>Wildcard</th>
		<th>Description</th>
	</tr>
	<tr>
		<td width="15%">, (comma)</td>
		<td> It represents the union of characters separated by commas; for example, 1, 2, 3 in the "Hour" field means 1:00, 2:00 and 3:00</td>
	</tr>
	<tr>
		<td>- (hyphen)</td>
		<td> It contains all values in the specified range; for example, in the "Day" field, 1-15 contains the 1st to the 15th day of the specified month</td>
	</tr>
	<tr>
		<td>* (asterisk)</td>
		<td>It means all values; for example, in the "Hour" field, * means every o'clock</td>
	</tr>
	<tr>
		<td>/ (forward slash)</td>
		<td>It specifies the increment; for example, in the "Minute" field, you can enter 1/10 to specify repeating every ten minutes from the first minute on (e.g., at the 11th minute, the 21st minute, the 31st minute, and so on)</td>
	</tr>
</table>

### Precautions
When both the "Day" and "Week" fields in a cron expression are specified, they are in an "or" relationship, i.e., the conditions of both are effective separately.

### Sample
Below are some examples of cron expressions and their meanings:

| Expression | Description | 
|---------|---------|
| `*/5 * * * * * *` | Triggers once every 5 seconds | 
|`0 15 10 * * MON-FRI *`| Triggers at 2 am on the 1st day of every month |
|`0 15 10 * * MON-FRI *`| Triggers every day at 10:15 am Monday through Friday |
|`0 0 10,14,16 * * * *`| Triggers every day at 10 am, 2 pm, and 4 pm |
|`0 */30 9-17 * * * *`| Triggers every half hour from 9 am to 5 pm every day |
|`0 0 12 * * WED *`| Triggers at 12:00 noon every Wednesday |




## Input Parameters of Timer Triggers
When a timer trigger triggers a function, the following data structures will be encapsulated in `event` and passed to the function. In addition, you can specify to pass the `message` for a timer trigger, which is empty by default.
```
{
    "Type":"Timer",
    "TriggerName":"EveryDay",
    "Time":"2019-02-21T11:49:00Z",
    "Message":"user define msg body"
}
```
| Field | Description |
|--|--|
| Type | Type of the trigger, whose value is `Timer` |
|TriggerName | Timer name, which can contain up to 60 characters out of `a-z`, `A-Z`, `0-9`, `-`, and `_` and must begin with a letter and be unique under the same function |
| Time | Trigger creation time, in UTC+0 |
|Message| String type |



