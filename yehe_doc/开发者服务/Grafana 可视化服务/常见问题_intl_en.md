[](id:que1)
### What are the strengths of TCMG over self-built Grafana in the cloud?

TCMG is a native visualization solution offered by Tencent Cloud in collaboration with Grafana Lab. It is preconfigured with many Tencent Cloud data sources, utilizes SSO and network access control to enhance data security, and eliminates the workloads of setup, OPS, and upgrade.

[](id:que2)
### Can TCMG be used with open-source and third-party plugins?
TCMG is fully compatible with open-source ecosystems, so you can use their capabilities.

[](id:que3)
### What is the relationship between TCMG and Grafana Enterprise?

We currently manage open-source Grafana and will provide paid options for upgrade in the future, so that you can upgrade to Grafana Enterprise, connect to various data sources, such as GitLab, Honeycomb, MongoDB, New Relic, Salesforce, ServiceNow, and Snowflake, and get enterprise-grade capabilities such as scheduled reports.

[](id:que4)

### How do I access data sources in my VPC from TCMG?

You can directly access data sources in the same VPC from TCMG without additional operations; for cross-VPC data access, you can use the peer connection feature of Tencent Cloud VPC.

[](id:que5)

### Which Grafana data source plugins are supported?

- Tencent Cloud data sources: CM, TMP, TKE, ES, and CLS.
- Third-Party data sources: Alertmanager, Amazon CloudWatch, Azure Monitor, Elasticsearch, Google Cloud Monitoring, Graphite, InfluxDB, Loki, Microsoft SQL Server (MSSQL), MySQL, OpenTSDB, PostgreSQL, Prometheus, Jaeger, Zipkin, Tempo, and TestData.

