A trigger condition expression is used to determine whether to trigger an alarm. The query analysis result of the monitoring object is input as a variable for the trigger expression. If the expression is true, an alarm will be triggered.

## Syntax Description

| Operator | Description | Example |
| --------------- | ------------------------------------------------------------ | -------------------------------------- |
| $N.keyname      | Imports the query analysis result. `N` is the monitoring object number, `keyname` is the field name in the **query analysis result** (which must start with a letter and can contain letters, digits, and underscores. We recommend you use the [AS syntax](https://intl.cloud.tencent.com/document/product/614/38731) to set an alias for the result.) | $1.ErrCount                            |
| +               | Addition operator                                                   | $1.ErrCount+$1.FatCount>10             |
| -               | Subtraction operator                                                   | $1.Count-$1.InfoCount>100              |
| *               | Multiplication operator                                                   | $1.RequestMilSec\*1000>10               |
| /               | Division operator                                                   | $1.RequestSec/1000>0.01                |
| %               | Modulo operator                                                   | $1.keyA%10==0                          |
| ==              | Comparison operator: equal to                                             | $1.ErrCount==100</br>$1.level=="Error"  |
| \>              | Comparison operator: greater than                                             | $1.ErrCount>100                        |
| <               | Comparison operator: less than                                             | $1.pv&lt;100                              |
| \>=             | Comparison operator: greater than or equal to                                         | $1.ErrCount>=100                       |
| \<=             | Comparison operator: less than or equal to                                         | $1.pv<=100                             |
| !=              | Comparison operator: not equal to                                           | $1.level!="Info"                       |
| ()              | Parentheses for controlling the operation priority                                         | ($1.a+$1.b)/$1.c>100                   |
| &&              | Logical operator: AND                                               | $1.ErrCount>100 && $1.level=="Error"   |
| \|\|            | Logical operator: OR                                               | $1.ErrCount>100 \|\| $1.level=="Error" |


- An alarm will be triggered only if the expression is true. For example, if the calculation result of `$1.a+$1.b` is 100, no alarms will be triggered; if the result is greater than or equal to 100, an alarm will be triggered.
- `keyname` in `$N.keyname` is the field name of the query analysis result. It must start with a letter and can contain letters, digits, and underscores, such as `level:error | select count(*) AS errCount`. `errCount` can be directly used as `keyname` in the trigger condition expression. If the field name contains special symbols, you need to enclose the imported variable with `[]`, such as `[$1.count(*)]`. **We recommend you use an [AS analysis statement](https://intl.cloud.tencent.com/document/product/614/38731) to set an alias for the result field name.**
- Up to three monitoring objects can be set in an alarm policy. Each one is identified by a number starting from 1. For example, `$1.key1` imports the `key1` field name in the query whose number is `1`, and `$2.key2` imports the `key2` field name in the query whose number is `2`.
- If multiple values are returned in the query analysis result, the expression will be calculated according to the values for up to 1,000 times or until the calculation result is `true`. For example, if the expression is `$1.a+$2.b>100`, analysis 1 returns m results, and analysis 2 returns n results, then the expression will be calculated for m \* n times, and calculation will stop when `$1.a+$2.b>100` is `true` or after 1,000 times of calculation.
  



