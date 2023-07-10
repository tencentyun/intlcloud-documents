The custom redirect feature in charts allows for redirecting to the set URL by clicking a value in the chart. Variables can be referenced in the URL.

## Directions

1. Log in to the [CLS console](https://console.cloud.tencent.com/cls).
2. On the left sidebar, click **Search and Analysis** or **Dashboard** and create a statistical analysis chart of the table type.
3. In **Chart Configuration**, click **Custom Redirect** > **+ Add**.

4. Configure the URL, reference variables in the URL as needed, and set whether to open the URL in a new window.




## Variable description
- `${__field.Name}`: References the field name of the clicked value.
As shown below, clicking **8.4s** triggers the redirect URL embedded with the **${__field.Name}** variable, which will reference the field name of the value, that is, populate **timecost** in the URL.
<img src="https://qcloudimg.tencent-cloud.cn/raw/9d8a8e8f799f2b5b1c7c6a5040b3c8a0.png" width="65%">
- `${__value.raw}`: References the clicked value (populated in the original format).
As shown below, clicking **8.4s** triggers the redirect URL embedded with the **${__value.raw}** variable, which will reference the raw data of the clicked value, that is, the value **8.4125** without unit or decimal place processing.
<img src="https://qcloudimg.tencent-cloud.cn/raw/5df105178ea53964a91f38bceeb4fa8b.png" width="65%">
- `${__value.Text}`: References the clicked value (populated in the string format).
As shown below, clicking **2020-10-27 17:21:00** triggers the redirect URL embedded with the **${__value.Text}** variable, which will reference the clicked value and convert it into a string, that is, **2020-10-27%2017:21:00** (here, `%20` is a URL-encoded space).
<img src="https://qcloudimg.tencent-cloud.cn/raw/8335224af1fe9fa117856453360fc20a.png" width="65%">
- `${__value.Numeric}`: References the clicked value (populated in the numeric format).
As shown below, clicking **8.4s** triggers the redirect URL embedded with the **${__value.Numeric}** variable, which will reference the clicked value and convert it into a number, that is **8.4125**. Here, a time value will be converted into a Unix timestamp in the numeric format, and a string value will fail to be referenced.
<img src="https://qcloudimg.tencent-cloud.cn/raw/6472842ee24664a5f2f99b0d773a40a2.png" width="65%">
- `${__value.Time}`: The timestamp of the clicked value (populated in the Unix time format).
As shown below, clicking **8.4s** triggers the redirect URL embedded with the **${__value.Time}** variable, which will reference the timestamp in the same line as the clicked value, that is, **2022-10-27 17:21:00** of `analytic_time`. The value will be further converted into the Unix format and populated as **1666891260000**. If there is no such timestamp, reference will fail.
<img src="https://qcloudimg.tencent-cloud.cn/raw/ec3a44ecb721dba8cb0740cd8ad0f510.png" width="65%">
- `${__Fields.specific field}`: Field value in the same line.
As shown below, clicking **8.4s** triggers the redirect URL embedded with the **${__Fields.protocol_type}** variable, which will reference the field value in the same line as the clicked value, that is, **http2** of `protocol_type`.

	<img src="https://qcloudimg.tencent-cloud.cn/raw/7a030f3c40c03d6eb52882a5b1a5d6ae.png" width="65%">




## Use case

Scenario: The following counts the top error rates of server IPs. In case of an IP with a high error rate, you need to be redirected to the search and analysis page, where you can view the IP logs with the 4XX status code.

```
https://console.cloud.tencent.com/cls/search?region=xxxxxxx&topic_id=xxxxxxxx&query=server_addr:${__value.text} AND status:[400 TO 499]&time=now-1h,now
```
After the target IP is clicked, the search page will be opened automatically for search and display of the search result.
