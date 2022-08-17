By default, you need to manually add the `ON CLUSTER XXX` syntax when performing DDL operations such as table creation at the cluster level. CDWCH 21.8.8.12 offers the new feature of DDL On Cluster, which can automatically add a cluster when performing DDL operations. This feature is disabled by default.

New ClickHouse parameters:
```xml
<!--`default_on_cluster` specifies the added cluster, which is "" by default.-->
<default_on_cluster>default_cluster</default_on_cluster>
<!--`enable_default_on_cluster` specifies whether to enable the DDL On Cluster feature, which is 0 by default.-->
<enable_default_on_cluster>1</enable_default_on_cluster>
```
## Directions
### 1. Configure in the configuration file permanently
Add the following parameters to `users.xml`, with no restart required after the configuration:
```xml
<yandex>
	<!-- Profiles of settings. -->
	<profiles>
		<default_on_cluster>default_cluster</default_on_cluster>
		<enable_default_on_cluster>1</enable_default_on_cluster>
	</profiles>
</yandex>
```
### 2. Modify temporarily at the session level
```sql
set default_on_cluster='default_cluster';
set enable_default_on_cluster=1;
```
