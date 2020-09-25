## Namespace

Namespace=QCE/WAF

## Monitoring Metrics

| Metric | Description | Unit | Dimension |
| ----------- | --------------- | ---- | --------------- |
| Access | Total access attempts | Count | domain and edition |
| Attack | Web attacks | Count | domain and edition |
| Cc | CC attacks | Count | domain and edition |
| Down | Downstream bandwidth | B/S | domain and edition |
| Qps | Requests per second | Count | domain and edition |
| Up | Upstream bandwidth | B/S | domain and edition |
| 4xx | 4xx status code | Count | domain and edition |
| 5xx | 5xx status code | Count | domain and edition |
| U4xx | Origin server 4xx status code | Count | domain and edition |
| U5xx | Origin server 5xx status code | Count | domain and edition |
| Bot | Bot attacks | Count | domain and edition |
| Ratio5xx | 5XX ratio | % | domain and edition |
| Ratio4xx | 4XX ratio | % | domain and edition |
| RatioAttack | Web attack ratio | % | domain and edition |
| RatioBot | Bot attack ratio | % | domain and edition |
| RatioCc | CC attack ratio | % | domain and edition |

## Overview of the Parameters in Each Dimension

| Parameter | Dimension Name | Dimension Description | Format |
| ------------------------------ | -------- | ----------------------------- | ------------------------------------------------------- |
| Instances.N.Dimensions.0.Name | domain | Dimension name of the domain name in the client attack | Enter a string-type dimension name, such as domain |
| Instances.N.Dimensions.0.Value | domain | Specific domain name in the client attack | Enter the specific domain name in the client attack, such as www.cloud.tencent.com |
| Instances.N.Dimensions.0.Name | edition | Dimension name of the web application firewall instance type | Enter a string-type dimension name, such as edition |
| Instances.N.Dimensions.0.Value | edition | Specific type of the web application firewall instance | Enter a specific type of the web application firewall instance, such as SaaS WAF or CLB WAF |

## Input Parameters

**For queries of monitoring data by domain name in client attacks, the input parameters are as follows:**
&Namespace=QCE/WAF
&Instances.N.Dimensions.0.Name=domain
&Instances.N.Dimensions.0.Value=<Specific domain name in the client attack>

**For queries of monitoring data by web application firewall instance, the input parameters are as follows:**
&Namespace=QCE/WAF
&Instances.N.Dimensions.0.Name=edition
&Instances.N.Dimensions.0.Value=<Specific type of the web application firewall instance>

