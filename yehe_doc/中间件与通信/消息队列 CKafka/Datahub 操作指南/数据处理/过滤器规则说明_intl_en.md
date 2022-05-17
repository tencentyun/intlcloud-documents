The filter allows you to configure filtering rules such as field sizes to filter data. Only data that meets the specified rules will be retained.

## Notes

- Filter matching is case-sensitive and accurate down to the character. During matching, no standardized operations will be performed on strings.
- Values to be matched must be in JSON format, which include strings and numeric values enclosed in quotation marks as well as keywords not enclosed in quotation marks (`true`, `false`, and `null`).

## Prefix Match

You can perform key value matching by comparing a specified prefix with the prefix in data.

For example, for data `{"password":"topicname"}`, you can specify `top` as the prefix of the `password` value so that `{"password":"topicname"}` can be normally matched.

## Suffix Match

You can perform key value matching by comparing a specified suffix with the suffix in data.

For example, for data `{"password":"topicname"}`, you can specify `name` as the suffix of the `password` value so that `{"password":"topicname"}` can be normally matched.

## Inclusion Match

You can specify a field to be included in data as a match condition.

For example, for data `{"password":"topicname"}`, you can specify `na` to be included in the `password` value so that `{"password":"topicname"}` can be normally matched.

## Exclusion Match

You can specify a field to be excluded from data as a match condition.

For example, for data `{"password":"topicname"}`, you can specify `topicname` to be excluded from the `password` value so that `{"password":"topicname"}` cannot be normally matched.

## Numeric Match

You can specify the value or value range of a certain field as a match condition.

For example, for data `{ "numeric": 10}`, you can specify the value of `numeric` to be less than 15 (`<15`) as a match condition so that `{ "numeric": 10}` can be normally matched.
<dx-alert infotype="explain" title="The following are examples of value match rules:">
<ul style = "margin-bottom: 0px;"><li>Greater than 10: Enter `>10`</li>
<li>Greater than or equal to 10: Enter `>=10`</li>
<li>Greater than or equal to 10, and less than or equal to 20: Enter `>=10&<=20`</li>
<li>Greater than or equal to 10, or less than or equal to 5: Enter `>=10|<=5`</li></ul>
</dx-alert>




## IP Match

You can specify an IP in CIDR notation as a match condition. For example, you can enter `1.2.3.4/24` to match IPs whose leading 24 bits start with "1.2.3.".

