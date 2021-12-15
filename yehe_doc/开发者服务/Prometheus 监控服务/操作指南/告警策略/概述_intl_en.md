
TMP allows you to define alert conditions based on Prometheus expressions. Once a metric reaches an alert condition, you will receive notifications through email and SMS, so you can take corresponding measures promptly.

>? Alerting in TMP combines the alarming capabilities of Cloud Monitor and the alerting capabilities of the open-source Prometheus ecosystem, making alerting more accurate and reasonable.

## Features
- TMP supports Alertmanager features such as grouping and silencing to make alerts more reasonable.
- You can group the metric data and regularly check and calculate the alerting rules to make alerting quicker and more convenient.
- Alerting rules can be defined based on PromQL, making alerting more flexible.
- Cloud Monitor's alarm notification templates can be used, which support multiple receiving channels such as email and SMS.

## Components
<table>
<tr>
<th>Term</th>
<th>Description</th>
</tr>
<tr>
<td>Rule name</td>
<td>Custom alerting rule name.</td>
</tr>
<tr>
<td>Alerting rule</td>
<td>It contains alert trigger condition and duration and should be defined through PromQL.</td>
</tr>
<tr>
<td>Alert object</td>
<td>Custom alert title.</td>
</tr>
<tr>
<td>Alert message</td>
<td>Custom alert content.</td>
</tr>
<tr>
<td>Label</td>
<td>A set of specified labels to be added to the alert.</td>
</tr>
<tr>
<td>Annotation</td>
<td>Custom additional alert message.</td>
</tr>
<tr>
<td>Notification template</td>
<td>It contains the template name, notification type, recipient, receiving channel. You can define the receiving channel and grouping method.</td>
</tr>
</table>
