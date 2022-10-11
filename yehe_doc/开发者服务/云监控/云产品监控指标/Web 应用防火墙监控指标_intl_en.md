## Namespace

Namespace=QCE/WAF


>?Always select "Guangzhou" as `Region` when pulling WAF monitoring metric data.

## Monitoring Metrics

| Parameter | Metric Name | Unit | Dimension |
| ----------- | --------------- | ---- | --------------- |
| Access | Total access attempts | Count | domain, edition |
| Attack | Web attacks | Count | domain, edition |
| Cc | CC attacks | Count | domain, edition |
| Down | Downstream bandwidth | Byte/sec | domain, edition |
| Qps | Requests per second | Count | domain, edition |
| Up | Upstream bandwidth | Byte/sec | domain, edition |
| 4xx | 4xx status code | Count | domain, edition |
| 5xx | 5xx status code | Count | domain, edition |
| U4xx | Origin server 4xx status code | Count | domain, edition |
| U5xx | Origin server 5xx status code | Count | domain, edition |
| Bot | Bot attacks | Count | domain, edition |
| Ratio5xx | 5XX percentage | % | domain, edition |
| Ratio4xx | 4XX percentage | % | domain, edition |
| RatioAttack | Web attack percentage | % | domain, edition |
| RatioBot | Bot attack percentage | % | domain, edition |
| RatioCc | CC attack percentage | % | domain, edition |
| InBandwidth   | Inbound bandwidth    |  MB   | domain, edition |
| OutBandwidth     | Outbound bandwidth    |  MB | domain, edition |
|MetricnameCustomSecurity|Number of custom policy attacks| Count | domain, edition |

## Dimensions and Parameters

| Parameter | Dimension | Dimension Description | Format |
| ------------------------------ | -------- | ----------------------------- | ------------------------------------------------------- |
| Instances.N.Dimensions.0.Name | domain | Dimension name of the domain name in the client attack | Enter a string-type dimension name, such as `domain` |
| Instances.N.Dimensions.0.Value | domain | Domain name in the client attack | Enter the domain name in the client attack, such as `www.cloud.tencent.com` |
| Instances.N.Dimensions.1.Name | edition | Dimension name of the WAF instance type | Enter a string-type dimension name, such as `edition` |
| Instances.N.Dimensions.1.Value | edition | Type of the WAF instance | Enter a type of the WAF instance, such as `SaaS WAF` (with input parameter value being 0) or `CLB WAF` (with input parameter value being 1) |

## Input Parameters

**Values of the input parameters for pulling WAF monitoring data:**
&Namespace=QCE/WAF
&Instances.N.Dimensions.0.Name = `domain`
&Instances.N.Dimensions.0.Value = Domain name in the client attack
&Instances.N.Dimensions.1.Name = `edition`
&Instances.N.Dimensions.1.Value = Type of the WAF instance

