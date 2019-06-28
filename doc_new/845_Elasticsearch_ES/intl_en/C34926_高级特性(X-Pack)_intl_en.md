## Overview
Elastic Stack (formerly X-Pack) features are Elasticsearch's official commercial features, including security, SQL, alerting, machine learning, and monitoring. It helps Elasticsearch service application development and operations. ES offers editions that come with such features, which you can select when purchasing and creating a cluster. The features in different editions are detailed below.

## Purchase Guide
![](https://main.qcloudimg.com/raw/f5c67db43be36b578fb9d1f9d20e2531.png)
As shown in the figure above, there are options for the Elastic Stack features on the ES purchase page. ES offers three editions that have different Elastic Stack features as follows:

| Item | Basic | Platinum | Open Source |
| ----------------- | ------ | ------ | ------ |
| Elastic Stack included | ✓      | ✓      | ✕      |
| Elastic Stack completeness | Partial | All | None |

**Purchase Suggestions**  
In order to be able to use more advanced features in ES, we recommend that you choose the **Platinum Edition** when you create a cluster. The specific features and differences of each edition are detailed below. For pricing information, see [Pricing](https://intl.cloud.tencent.com/document/product/845/18376).

## Elastic Stack Overview
This document describes some of the commonly used Elastic Stack features. For more information, see Elasticsearch's official [Elastic Stack descriptions](https://www.elastic.co/products/stack) and [API documentation](https://www.elastic.co/guide/en/elasticsearch/reference/6.4/xpack-api.html).

>- Some features vary by editions (Basic, Platinum, and Open Source). For the specific differences, see the descriptions in this document.
>- Security, alerting, and machine learning are only available in the ** Platinum Edition**.

- **Security**  
This feature supports refined read/write permission control at the index and field levels and effectively protects data security by enabling data security protection and business access isolation, granting access to the right people, and preventing malicious attacks and data leakage.
![](https://main.qcloudimg.com/raw/ec7529df345ebbf27db0453292eafe8d.png)
- **Alerting**  
This feature provides alerting capabilities for data changes and notifies users via email or other channels. For example, together with the querying and statistics collection features of Elasticsearch, it can trigger alarms in log analysis scenarios when the number of certain error logs increases sharply and exceeds the specified threshold.
![](https://main.qcloudimg.com/raw/aece0801646fce642856f0b349b79379.png)
- **Machine learning**  
In the application scenario of custom data alerting, it is sometimes difficult to set rules and thresholds to define the changes. In this case, the trend in data changes and reasonable fluctuation range can be predicted by the unattended machine learning feature, and when the data deviates from the normal trend, alarms will be triggered and notifications sent.

>Monitoring and SQL are only available in the **Platinum Edition and Basic Edition**. However, in terms of SQL support, the Open Source Edition integrates with other SQL plugins. For more information, see [elasticsearch-sql](https://github.com/NLPchina/elasticsearch-sql).

- **Monitoring**   
Monitoring information can be comprehensively collected at multiple levels such as cluster, node, and index, helping you understand the cluster operations in real time and facilitating your application development and OPS.  
![](https://main.qcloudimg.com/raw/012416b4755bed7e6cf8b57d0d0fa23a.png)
- **SQL**  
This feature makes full-text search and statistical analysis of Elasticsearch data possible through traditional database SQL tools. CLI and REST access methods are supported. **The Platinum Edition further supports JDBC connection**. This feature enables you to seamlessly connect ES with your existing business systems and thus reduces your learning costs for new technologies.
![](https://main.qcloudimg.com/raw/ca19a8665919a85b9a08b5d9451ec3de.png)

### Detailed Comparison among Editions
This section compares some of the key features in each edition. For a complete feature comparison, see Elasticsearch's official [Elastic Edition Feature Descriptions](https://www.elastic.co/subscriptions).

>In the table below, ⚫, ◑, and - are used to indicate the feature completeness. ⚫: all; ◑: partial; -: none.

<table class="tg">
  <tr>
    <th class="tg-s268">Module</th>
    <th class="tg-s268">Feature</th>
    <th class="tg-s268">Open Source</th>
    <th class="tg-s268">Basic</th>
    <th class="tg-s268">Platinum</th>
  </tr>
  <tr>
    <td class="tg-0lax" rowspan="7">Elasticsearch</td>
    <td class="tg-s268">Scalability and resiliency</td>
    <td class="tg-s6z2">◑</td>
    <td class="tg-s6z2">◑</td>
    <td class="tg-s6z2">⚫</td>
  </tr>
  <tr>
    <td class="tg-s268">Query and analytics</td>
    <td class="tg-s6z2">◑</td>
    <td class="tg-s6z2">◑</td>
    <td class="tg-s6z2">⚫</td>
  </tr>
  <tr>
    <td class="tg-s268">Data enrichment</td>
    <td class="tg-s6z2">⚫</td>
    <td class="tg-s6z2">⚫</td>
    <td class="tg-s6z2">⚫</td>
  </tr>
  <tr>
    <td class="tg-s268"><a href="#manage_tool">Management and tooling</a></td>
    <td class="tg-s6z2">◑</td>
    <td class="tg-s6z2">◑</td>
    <td class="tg-s6z2">⚫</td>
  </tr>
  <tr>
    <td class="tg-s268"><a href="#Security">Security</a></td>
    <td class="tg-s6z2">-</td>
    <td class="tg-s6z2">-</td>
    <td class="tg-s6z2">⚫</td>
  </tr>
  <tr>
    <td class="tg-s268"><a href="#Alerting">Alerting</a></td>
    <td class="tg-s6z2">-</td>
    <td class="tg-s6z2">-</td>
    <td class="tg-s6z2">⚫</td>
  </tr>
  <tr>
    <td class="tg-s268"><a href="#machine_learning">Machine Learning</a></td>
    <td class="tg-s6z2">-</td>
    <td class="tg-s6z2">-</td>
    <td class="tg-s6z2">⚫</td>
  </tr>
  <tr>
    <td class="tg-0lax" rowspan="8">Kibana</td>
    <td class="tg-0lax">Explore and visualize</td>
    <td class="tg-baqh">◑</td>
    <td class="tg-baqh">◑</td>
    <td class="tg-baqh">⚫</td>
  </tr>
  <tr>
    <td class="tg-0lax">Stack management and tooling</td>
    <td class="tg-baqh">◑</td>
    <td class="tg-baqh">◑</td>
    <td class="tg-baqh">⚫</td>
  </tr>
  <tr>
    <td class="tg-0lax">Stack monitoring</td>
    <td class="tg-baqh">-</td>
    <td class="tg-baqh">◑</td>
    <td class="tg-baqh">⚫</td>
  </tr>
  <tr>
    <td class="tg-0lax">Share and collaborate</td>
    <td class="tg-baqh">◑</td>
    <td class="tg-baqh">◑</td>
    <td class="tg-baqh">⚫</td>
  </tr>
  <tr>
    <td class="tg-0lax">Localized UI</td>
    <td class="tg-baqh">◑</td>
    <td class="tg-baqh">◑</td>
    <td class="tg-baqh">⚫</td>
  </tr>
  <tr>
    <td class="tg-0lax">Security</td>
    <td class="tg-baqh">-</td>
    <td class="tg-baqh">-</td>
    <td class="tg-baqh">⚫</td>
  </tr>
  <tr>
    <td class="tg-0lax">Alerting</td>
    <td class="tg-baqh">-</td>
    <td class="tg-baqh">-</td>
    <td class="tg-baqh">⚫</td>
  </tr>
  <tr>
    <td class="tg-0lax">Machine learning</td>
    <td class="tg-baqh">-</td>
    <td class="tg-baqh">-</td>
    <td class="tg-baqh">⚫</td>
  </tr>
  <tr>
    <td class="tg-0lax" rowspan="4">Beats</td>
    <td class="tg-0lax">Data collection</td>
    <td class="tg-baqh">◑</td>
    <td class="tg-baqh">◑</td>
    <td class="tg-baqh">⚫</td>
  </tr>
  <tr>
    <td class="tg-0lax">Data shipping</td>
    <td class="tg-baqh">◑</td>
    <td class="tg-baqh">◑</td>
    <td class="tg-baqh">⚫</td>
  </tr>
  <tr>
    <td class="tg-0lax">Module</td>
    <td class="tg-baqh">◑</td>
    <td class="tg-baqh">◑</td>
    <td class="tg-baqh">⚫</td>
  </tr>
  <tr>
    <td class="tg-0lax">Monitoring and management</td>
    <td class="tg-baqh">-</td>
    <td class="tg-baqh">◑</td>
    <td class="tg-baqh">⚫</td>
  </tr>
  <tr>
    <td class="tg-0lax" rowspan="5">Logstash</td>
    <td class="tg-0lax">Data collection</td>
    <td class="tg-baqh">⚫</td>
    <td class="tg-baqh">⚫</td>
    <td class="tg-baqh">⚫</td>
  </tr>
  <tr>
    <td class="tg-0lax">Data enrichment</td>
    <td class="tg-baqh">⚫</td>
    <td class="tg-baqh">⚫</td>
    <td class="tg-baqh">⚫</td>
  </tr>
  <tr>
    <td class="tg-0lax">Data shipping</td>
    <td class="tg-baqh">⚫</td>
    <td class="tg-baqh">⚫</td>
    <td class="tg-baqh">⚫</td>
  </tr>
  <tr>
    <td class="tg-0lax">Module</td>
    <td class="tg-baqh">◑</td>
    <td class="tg-baqh">⚫</td>
    <td class="tg-baqh">⚫</td>
  </tr>
  <tr>
    <td class="tg-0lax">Monitoring and management</td>
    <td class="tg-baqh">-</td>
    <td class="tg-baqh">◑</td>
    <td class="tg-baqh">⚫</td>
  </tr>
  <tr>
    <td class="tg-0lax" rowspan="7">Elastic APM</td>
    <td class="tg-0lax">APM server</td>
    <td class="tg-baqh">⚫</td>
    <td class="tg-baqh">⚫</td>
    <td class="tg-baqh">⚫</td>
  </tr>
  <tr>
    <td class="tg-0lax">APM agents</td>
    <td class="tg-baqh">⚫</td>
    <td class="tg-baqh">⚫</td>
    <td class="tg-baqh">⚫</td>
  </tr>
  <tr>
    <td class="tg-0lax">APM dashboards in Kibana</td>
    <td class="tg-baqh">⚫</td>
    <td class="tg-baqh">⚫</td>
    <td class="tg-baqh">⚫</td>
  </tr>
  <tr>
    <td class="tg-0lax">APM UI</td>
    <td class="tg-baqh">-</td>
    <td class="tg-baqh">⚫</td>
    <td class="tg-baqh">⚫</td>
  </tr>
  <tr>
    <td class="tg-0lax">Distributed tracing</td>
    <td class="tg-baqh">-</td>
    <td class="tg-baqh">⚫</td>
    <td class="tg-baqh">⚫</td>
  </tr>
  <tr>
    <td class="tg-0lax">Alerting integration</td>
    <td class="tg-baqh">-</td>
    <td class="tg-baqh">-</td>
    <td class="tg-baqh">⚫</td>
  </tr>
  <tr>
    <td class="tg-0lax">Machine learning integration</td>
    <td class="tg-baqh">-</td>
    <td class="tg-baqh">-</td>
    <td class="tg-baqh">⚫</td>
  </tr>
  <tr>
    <td class="tg-0lax" rowspan="3">Elastic Logs</td>
    <td class="tg-0lax">Log shipper (Filebeat)</td>
    <td class="tg-baqh">⚫</td>
    <td class="tg-baqh">⚫</td>
    <td class="tg-baqh">⚫</td>
  </tr>
  <tr>
    <td class="tg-0lax">Dashboards for common data sources</td>
    <td class="tg-baqh">⚫</td>
    <td class="tg-baqh">⚫</td>
    <td class="tg-baqh">⚫</td>
  </tr>
  <tr>
    <td class="tg-0lax">Logs UI</td>
    <td class="tg-baqh">-</td>
    <td class="tg-baqh">⚫</td>
    <td class="tg-baqh">⚫</td>
  </tr>
  <tr>
    <td class="tg-0lax" rowspan="3">Elastic Infrastructure</td>
    <td class="tg-0lax">Metric shipper (Metricbeat)</td>
    <td class="tg-baqh">⚫</td>
    <td class="tg-baqh">⚫</td>
    <td class="tg-baqh">⚫</td>
  </tr>
  <tr>
    <td class="tg-0lax">Dashboards for common data sources</td>
    <td class="tg-baqh">⚫</td>
    <td class="tg-baqh">⚫</td>
    <td class="tg-baqh">⚫</td>
  </tr>
  <tr>
    <td class="tg-0lax">Infrastructure UI</td>
    <td class="tg-baqh">-</td>
    <td class="tg-baqh">⚫</td>
    <td class="tg-baqh">⚫</td>
  </tr>
  <tr>
    <td class="tg-0lax" rowspan="3">Elastic Uptime</td>
    <td class="tg-0lax">Uptime monitor (Heartbeat)</td>
    <td class="tg-baqh">⚫</td>
    <td class="tg-baqh">⚫</td>
    <td class="tg-baqh">⚫</td>
  </tr>
  <tr>
    <td class="tg-0lax">Uptime dashboards in Kibana</td>
    <td class="tg-baqh">⚫</td>
    <td class="tg-baqh">⚫</td>
    <td class="tg-baqh">⚫</td>
  </tr>
  <tr>
    <td class="tg-0lax">Uptime UI</td>
    <td class="tg-baqh">-</td>
    <td class="tg-baqh">⚫</td>
    <td class="tg-baqh">⚫</td>
  </tr>
</table>

**Detailed descriptions of certain Elasticsearch features:**

>In the table below, ✓ means the feature is available, - not available.

<table class="tg">
  <tr>
    <th class="tg-s268">Elasticsearch Feature Module</th>
    <th class="tg-s268">Item</th>
    <th class="tg-s268">Open Source</th>
    <th class="tg-s268">Basic</th>
    <th class="tg-s268">Platinum</th>
  </tr>
  <tr>
    <td class="tg-0lax" rowspan="11"><a id="manage_tool">Management and Tooling</a></td>
    <td class="tg-s268">REST APIs</td>
    <td class="tg-s268">✓</td>
    <td class="tg-s268">✓</td>
    <td class="tg-s268">✓</td>
  </tr>
  <tr>
    <td class="tg-s268">Language clients</td>
    <td class="tg-s268">✓</td>
    <td class="tg-s268">✓</td>
    <td class="tg-s268">✓</td>
  </tr>
  <tr>
    <td class="tg-s268">Snapshot/restore</td>
    <td class="tg-s268">✓</td>
    <td class="tg-s268">✓</td>
    <td class="tg-s268">✓</td>
  </tr>
  <tr>
    <td class="tg-s268">_source only snapshot</td>
    <td class="tg-s268">-</td>
    <td class="tg-s268">✓</td>
    <td class="tg-s268">✓</td>
  </tr>
  <tr>
    <td class="tg-s268">SQL interpreter CLI</td>
    <td class="tg-s268">-</td>
    <td class="tg-s268">✓</td>
    <td class="tg-s268">✓</td>
  </tr>
  <tr>
    <td class="tg-s268">Data rollups</td>
    <td class="tg-s268">-</td>
    <td class="tg-s268">✓</td>
    <td class="tg-s268">✓</td>
  </tr>
  <tr>
    <td class="tg-s268">Index lifecycle management</td>
    <td class="tg-s268">-</td>
    <td class="tg-s268">✓</td>
    <td class="tg-s268">✓</td>
  </tr>
  <tr>
    <td class="tg-s268">Frozen indices</td>
    <td class="tg-s268">-</td>
    <td class="tg-s268">✓</td>
    <td class="tg-s268">✓</td>
  </tr>
  <tr>
    <td class="tg-s268">Upgrade Assistant APIs</td>
    <td class="tg-s268">-</td>
    <td class="tg-s268">✓</td>
    <td class="tg-s268">✓</td>
  </tr>
  <tr>
    <td class="tg-s268">JDBC client</td>
    <td class="tg-s268">-</td>
    <td class="tg-s268">-</td>
    <td class="tg-s268">✓</td>
  </tr>
  <tr>
    <td class="tg-s268">ODBC client</td>
    <td class="tg-s268">-</td>
    <td class="tg-s268">-</td>
    <td class="tg-s268">✓</td>
  </tr>
  <tr>
    <td class="tg-0lax" rowspan="6"><a id="Security">Security</a></td>
    <td class="tg-s268">Encrypted communications</td>
    <td class="tg-s268">-</td>
    <td class="tg-s268">✓</td>
    <td class="tg-s268">✓</td>
  </tr>
  <tr>
    <td class="tg-s268">Role-based access control</td>
    <td class="tg-s268">-</td>
    <td class="tg-s268">✓</td>
    <td class="tg-s268">✓</td>
  </tr>
  <tr>
    <td class="tg-s268">File and native authentication</td>
    <td class="tg-s268">-</td>
    <td class="tg-s268">✓</td>
    <td class="tg-s268">✓</td>
  </tr>
  <tr>
    <td class="tg-s268">Audit logging</td>
    <td class="tg-s268">-</td>
    <td class="tg-s268">-</td>
    <td class="tg-s268">✓</td>
  </tr>
  <tr>
    <td class="tg-s268">Attribute-based access control</td>
    <td class="tg-s268">-</td>
    <td class="tg-s268">-</td>
    <td class="tg-s268">✓</td>
  </tr>
  <tr>
    <td class="tg-s268">Field- and document-level security</td>
    <td class="tg-s268">-</td>
    <td class="tg-s268">-</td>
    <td class="tg-s268">✓</td>
  </tr>
  <tr>
    <td class="tg-0lax" rowspan="1"><a id="Alerting">Alerting</a></td>
    <td class="tg-s268">Highly available, scalable alerting</td>
    <td class="tg-s268">-</td>
    <td class="tg-s268">-</td>
    <td class="tg-s268">✓</td>
  </tr>
  <tr>
    <td class="tg-0lax" rowspan="6"><a id="machine_learning">Machine Learning</a></td>
    <td class="tg-s268">Anomaly detection on time series</td>
    <td class="tg-s268">-</td>
    <td class="tg-s268">-</td>
    <td class="tg-s268">✓</td>
  </tr>
  <tr>
    <td class="tg-s268">Population/entity analysis</td>
    <td class="tg-s268">-</td>
    <td class="tg-s268">-</td>
    <td class="tg-s268">✓</td>
  </tr>
  <tr>
    <td class="tg-s268">Log message categorization</td>
    <td class="tg-s268">-</td>
    <td class="tg-s268">-</td>
    <td class="tg-s268">✓</td>
  </tr>
  <tr>
    <td class="tg-s268">Root cause indication</td>
    <td class="tg-s268">-</td>
    <td class="tg-s268">-</td>
    <td class="tg-s268">✓</td>
  </tr>
  <tr>
    <td class="tg-s268">Alerting on anomalies</td>
    <td class="tg-s268">-</td>
    <td class="tg-s268">-</td>
    <td class="tg-s268">✓</td>
  </tr>
  <tr>
    <td class="tg-s268">Forecasting on time series</td>
    <td class="tg-s268">-</td>
    <td class="tg-s268">-</td>
    <td class="tg-s268">✓</td>
  </tr>
</table>


