[//]: # (chinagitpath:XXXXX)

**In order to enable Sparkling to ingest data from a database in Tencent Cloud, does the database need to have a public access address?**
If your cluster and database are deployed in the same region, Tencent Cloud will use a private network interconnection scheme to connect them, so you do not need to configure public access addresses for them, which greatly guarantees data security.

**Does Sparkling support data extraction and transformation?**
The data integration module of Sparkling supports lightweight extraction and transformation, so for relational databases, you can extract target data for ingestion into Sparkling at row or column levels. For unstructured and semi-structured data, the integration module supports structuring the data during ingestion.
