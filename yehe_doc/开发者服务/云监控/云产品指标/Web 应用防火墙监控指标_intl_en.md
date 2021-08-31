## Namespace

Namespace=QCE/WAF


>?Please always select "Guangzhou" as `Region` when pulling WAF monitoring metric data.

## Monitoring Metrics

| Metric | Description | Unit | Dimension |
| ----------- | --------------- | ---- | --------------- |
| Access | Total access attempts | - | domain, edition |
| Attack | Web attacks | - | domain, edition |
| Cc | CC attacks | - | domain, edition |
| Down | Downstream bandwidth | B/S | domain, edition |
| Qps | Requests per second | - | domain, edition |
| Up | Upstream bandwidth | B/S | domain, edition |
| 4xx | 4xx status codes | - | domain, edition |
| 5xx | 5xx status codes | - | domain, edition |
| U4xx | Real server 4xx status codes | - | domain, edition |
| U5xx | Real server 5xx status codes | - | domain, edition |
| Bot | Bot attacks | - | domain, edition |
| Ratio5xx | 5XX ratio | % | domain, edition |
| Ratio4xx | 4XX ratio | % | domain, edition |
| RatioAttack | Web attack ratio | % | domain, edition |
| RatioBot | Bot attack ratio | % | domain, edition |
| RatioCc | CC attack ratio | % | domain, edition |

## Overview of Parameters in Each Dimension

| Parameter | Dimension | Dimension Description | Format |
| ------------------------------ | -------- | ----------------------------- | ------------------------------------------------------- |
| Instances.N.Dimensions.0.Name | domain | Domain dimension name of client attack | Enter a String-type dimension name: domain |
| Instances.N.Dimensions.0.Value | domain | Specific domain name in client attack | Enter a specific domain name in the client attack, such as `www.cloud.tencent.com` |
| Instances.N.Dimensions.0.Name  | edition  | WAF instance type dimension name | Enter a String-type dimension name: edition                       |
| Instances.N.Dimensions.0.Value | edition  | Specific WAF instance type     | Enter a specific WAF instance type, such as SaaS WAF (with input parameter value of 0) or CLB WAF (with input parameter value of 1) |

## Input Parameter Description

**To query the monitoring data by domain name in the client attack, use the following input parameters:**
&Namespace=QCE/WAF
&Instances.N.Dimensions.0.Name=domain
&Instances.N.Dimensions.0.Value=Specific domain name in client attack

**To query the monitoring data by WAF instance, use the following input parameters:**
&Namespace=QCE/WAF
&Instances.N.Dimensions.0.Name=edition
&Instances.N.Dimensions.0.Value=Specific WAF instance type

