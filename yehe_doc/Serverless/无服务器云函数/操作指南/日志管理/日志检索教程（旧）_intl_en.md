>!SCF was fully connected to [CLS](https://intl.cloud.tencent.com/document/product/614) on January 29, 2021, invocation logs of newly created functions have been delivered to CLS by default since then, and logs can be output in real time. If your function was created before January 29, 2021, and the advanced retrieval page is as shown below, please do so as instructed in this document.
>![](https://main.qcloudimg.com/raw/6e3543a033bccf644d85348d81595474.png)






With the advanced search feature of SCF, you can search for logs by using query syntax to combine keywords.

## Search Syntax

The following query statements are supported:

| Syntax | Semantics |
| --------- | ------------------------------------------------------------ |
| key:value | Key-value search format. Here, `value` supports fuzzy match by using `?` or `*`. If `key` or `value` contains certain characters such as spaces or colons, they must be enclosed in quotation marks. For the list of currently supported keys, please see [Preset Keys](#key). |
| AND | Logical AND operator, such as `SCF_RequestId:85a82ecf-xxx AND SCF_Duration:1`. |
| OR | Logical OR operator, such as `SCF_RequestId:85a82ecf-xxx OR SCF_Duration:1`. |
| NOT | Logical NOT operator, such as `SCF_RequestId:85a82ecf-xxx NOT SCF_Duration:1`. |
| TO | Logical TO operator, such as  `SCF_Duration:[0.1 TO 1.0]`. |
| 'a' | The character `a` will be considered as a regular character and will not be processed as a syntax keyword. |
| "A" | All characters in `A` will be considered as regular ones and will not be processed as syntax keywords. |
| \ | Escape character. An escaped character represents the literal meaning of the character, such as `url:\/images\/favicon.ico"`. |
| * | Wildcard, which can match zero, one, or multiple characters, such as `host:www.test*.com`. |
| ? | Wildcard, which can match one single character, such as `host:www.te?t.com`. |
| :> | Range operator, which means greater than a certain value for numeric fields, such as `SCF_Duration:>1`. |
| :>= | Range operator, which means greater than or equal to a certain value for numeric fields, such as `SCF_Duration:>=1`. |
| :< | Range operator, which means less than a certain value for numeric fields, such as `SCF_Duration:<1`. |
| :<= | Range operator, which means less than or equal to a certain value for numeric fields, such as `SCF_Duration:<=1`. |
|: | Colon, which indicates the manipulated key field, i.e., key-value search, such as `SCF_RequestId:85a82ecf-xxx` or `SCF_Duration:1`. |



>!
>- The syntactic operators are case sensitive. For example, `AND` and `OR` represent logical search operators, while `and` and `or` are regarded as common words.
>- When multiple search statements are connected with spaces, they are regarded as in the "OR" logic; for example, `warning error` indicates to return results containing the `warning` keyword or `error` keyword.
>- All the characters in the syntax are reserved characters. If a search keyword contains these syntactically reserved characters, they need to be escaped.
>- For key-value search (in the format of `key:value`), the key name (key) must be in the [list of supported keys](#key).

[](id:key)

## Preset Keys

| Key | Type | Description | Query Sample |
| ------------- | ------ | -------------- | ----------------- |
| SCF_RequestId | text | Request ID | SCF_RequestId:123 |
| SCF_Duration | double | Execution duration (in ms) | SCF_Duration:>20 |



## Samples

- Query logs that contain the keyword `error` or `fail`:
```
error OR fail
```

- Query logs that contain the keyword `error` in a specified request:
```
SCF_RequestId:123 AND error
```

- Query logs that run more than 20 ms and contain the keyword `error`:
```
SCF_Duration:>20 AND error
```




>!To deduplicate request logs, you can search for "Report RequestId". For example, if you want to query which requests run more than 20 ms, you can use the following statement:
>```
>"Report RequestId" AND SCF_Duration:>20
>```




## FAQs

#### 1. Why is "The search syntax is invalid" displayed?

Please note that the search cannot begin with `*` or `?`.

#### 2. There are matched keywords in a log, but why is it not returned in the search?

- Check whether the letter case is correct.
- Check whether there are spaces between the search and syntax keywords. For example, `SCF_Duration:>20` is correct, while `SCF_Duration : > 20` is incorrect.
