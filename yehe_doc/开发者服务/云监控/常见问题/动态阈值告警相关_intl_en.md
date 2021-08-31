
### What is the sensitivity of dynamic alarm thresholds?
The sensitivity of dynamic thresholds is the extent to which metrics can deviate from their acceptable ranges before alarms are triggered. It varies with your monitoring needs.
<escape>
<table>
<tr>
<th>Sensitivity</th>
<th>Note</th>
</tr>
<tr>
<td>High</td>
<td>The tolerance of deviation is low, and you receive a relatively large amount of alarm notifications.</td>
</tr>
<tr>
<td>Medium</td>
<td>The tolerance of deviation is medium, and you receive a medium amount of alarm notifications. This is the default setting.</td>
</tr>
<tr>
<td>Low</td>
<td>The tolerance of deviation is high, and you receive a small amount of alarm notifications.</td>
</tr>
</table>
</escape>

>?
>
>- On the product level, you can set the sensitivity of alarms to high, medium, or low, which corresponds to different backend configuration. Sensitivity is a hyperparameter, whose value is determined by the model through a continuous learning process and is inaccessible to users.
>- After a sensitivity level is selected, the allowed deviation, which is calculated dynamically, for metrics that fluctuate widely tends to be big, and that for metrics that change less dramatically tends to be small.
You can use the shading graph of dynamic alarm thresholds to determine which sensitivity level fits your needs, or accept the default setting (medium), which delivers satisfactory results in most application scenarios, especially on percentage and delay metrics.

### Can I create only 20 policies for dynamic alarm thresholds at most?
The free quota for dynamic alarm threshold policies is 20, and you can create up to 20 alarm objects (or dimension combinations) under each policy by default. To use additional dynamic threshold policies beyond the free quota, you can [submit a ticket](https://console.cloud.tencent.com/workorder/category) to purchase a package.

### What documents has Tencent Cloud published on dynamic alarm thresholds?
**Operation Guide Documentation**
[Dynamic Threshold Alarm Overview](https://intl.cloud.tencent.com/document/product/248/39021)
[Using Dynamic Threshold Alarm](https://intl.cloud.tencent.com/document/product/248/39022)
**Best Practice Documentation**
[Best Practice > Dynamic Alarm Threshold](https://intl.cloud.tencent.com/document/product/248/39443)
