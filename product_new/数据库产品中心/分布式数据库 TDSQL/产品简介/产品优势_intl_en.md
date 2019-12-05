## Ultra-high Performance
- A single shard can sustain up to 240,000 QPS, and the performance of an entire instance can be linearly improved as the number of shards increases.
- There is no performance bottleneck that can be seen in the middleware + database scheme, that is, TProxy can also be linearly scaled.
- The performance of strong sync is comparable to that of async replication, allowing you to achieve high performance without data loss.

## Professional Reliability
- TDSQL has been massively verified by various types of Tencent's core products for over 10 years, such as social networking, ecommerce, payment, audio and video services.
- It has comprehensive features of data backup, disaster recovery, and quick upgrade.
- It boasts a complete monitoring and alarming system, where most of failures can be recovered through automated program processing.
- It supports various cutting-edge features in the distributed database world, such as distributed multi-table join, small table broadcast, distributed transaction, and SQL passthrough.

## Ease of Use
- Except for a small number of syntax differences from native MySQL and MariaDB, TDSQL can be used just like a standalone database, and the sharding process is imperceptible to the business and requires no manual intervention.
- It is compatible with MySQL protocols (i.e., supporting kernels such as MySQL and MariaDB).
- It provides a web-based console, read-write separation capability, and dedicated OPS and commands.
