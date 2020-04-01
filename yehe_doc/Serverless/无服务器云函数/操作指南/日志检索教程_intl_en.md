You can search for SCF logs by keyword or use query syntax to combine keywords for search.

## Query Syntax

The following query statements are supported:

| Syntax | Semantics |
| --------- | ------------------------------------------------------------ |
| key:value | Key-value search format. Here, `value` supports fuzzy match by using `?` or `*`. If `key` or `value` contains key characters such as spaces or colons, they must be enclosed in quotation marks. For the list of currently supported keys, please see [Preset Keys](#key). |
| A and B | "AND" logic that returns the intersection of A and B. If multiple keywords are used for search at a time, the default logic will be "AND" if they are separated by spaces. |
| A or B | "OR" logic that returns the union of A or B. |
| not B | "NOT" logic that returns the results excluding B. |
| A not B | "MINUS" logic that returns the results including A but excluding B, i.e., `A - B`. |
| 'a' | The character `a` will be considered as a regular character and will not be processed as a syntax keyword. |
| "A" | All characters in `A` will be considered as regular ones and will not be processed as syntax keywords. |
| \ | Escape character. An escaped character represents the literal meaning of the character, such as `\"` for quotation mark or `\:` for colon. |
| * | Fuzzy query of keywords that can match zero, single, or multiple random characters. `*` cannot be used as the first character. For example, if you enter `abc*`, all logs beginning with `abc` will be returned. |
| ? | Fuzzy query of keywords that can match a single character at a specific position. For example, if you enter `ab?c`, logs that begin with `ab`, end with `c`, and contain only one character between `ab` and `c` will be returned. |
| > | "GREATER THAN" logic, which is used for numeric fields. |
| >= | "GREATER THAN OR EQUAL TO" logic, which is used for numeric fields. |
| < | "LESS THAN" logic, which is used for numeric fields. |
| <= | "LESS THAN OR EQUAL TO" logic, which is used for numeric fields. |
| = | "EQUAL TO" logic, which can be used for numeric or text fields. (Fuzzy search is not supported. If you need fuzzy search, please see the key-value search `key:value`.) |
| in | It is used to query a numeric range. Brackets `[]` indicate a closed interval, while parentheses `()` indicate an open interval. For example, `(0 100]` indicates numbers greater than 0 but less than or equal to 100. |


>
>- The priority order of operators from high to low is: `:` > `"` > `()` > `and` > `not` > `or`.
>- If **b** is text, then, the difference between `a=b` and `a:b` lies in that **a** equals **b** in the former, while a contains **b** in the latter (the search is processed based on the word segmentation logic and fuzzy search is supported).
>- Syntax keywords are case-insensitive.
>- Searches are case-sensitive. If no result is returned, please check whether the letter case is correct and whether there are typos.



## Preset Keys<span id="key"></span>

| Key | Type | Description | Query Sample |
| ------------- | ------ | ------------ | ----------------- |
| SCF_RequestId | text | Request ID | SCF_RequestId:123 |
| SCF_Duration | double | Execution duration (ms) | SCF_Duration>20 |



## Samples

- Query logs that contain the keyword `error` or `fail`:
```
error or fail
```
- Query logs that contain the keyword `error` in a specified request:
```
SCF_RequestId:123 and error
```
- Query logs that run more than 20 ms and contain the keyword `error`:
```
SCF_Duration>20 and error
```
>To deduplicate request logs, you can search for `Report RequestId`. For example, if you want to query which requests run more than 20 ms, you can use the following statement:
`"Report RequestId" and SCF_Duration>20`.


## FAQs

#### 1. Why is "The search syntax is invalid" displayed?
Please note that the search cannot begin with `*` or `?`.

#### 2. There are matched keywords in a log, but why is it not returned in the search?
- Check whether the letter case is correct.
- Check whether there are spaces between the search and syntax keywords. For example, `SCF_Duration>20` is correct, while `SCF_Duration > 20` is incorrect.
