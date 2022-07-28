## Test Description
The latest version of CDWPG encapsulates Greenplum 6.x. Compared to 5.x, it features greatly improved CRUD (i.e., OLTP) capabilities in multiple concurrent scenarios. These improvements include:
1. Upgraded the PostgreSQL kernel to v9.4 and introduced lock optimizations such as fastpath.
2. Provided global deadlock detection.
3. Optimized global transactions.

Greenplum officially uses [TPC-B](http://www.tpc.org/tpcb/) to test the OLTP capabilities of v6.x. Therefore, CDWPG also uses this benchmark for testing.

## Test Environment
CDWPG offers **compute-intensive** and **storage-intensive** models. You can simply distinguish them from each other:
- Compute-intensive: The underlying hardware is SSD with strong random read/write capabilities. It is suitable for hot data analysis and scenarios with mixed loads.
- Storage-intensive: The underlying hardware is HDD with average random read/write capabilities but large disk capacity. It is suitable for storing and analyzing larger-scale historical data.

In conclusion, TPC-B requires the **compute-intensive** model. You can choose two nc2.large nodes and purchase them directly on the [purchase page](https://buy.cloud.tencent.com/snova#/).

## Test Tool
Use pgbench, the standard tool of PostgreSQL, for testing.
1. If the test environment is CentOS 7.x, you can download the already compiled tool [here](https://packagedown-online-1256722404.cos.ap-guangzhou.myqcloud.com/pgbench/pgbench).
2. For other environments, you can compile PostgreSQL yourself or directly install the binary package. PostgreSQL 9.4 is recommended for better compatibility.

## Test Steps
### Creating test database
```
CREATE DATABASE pgbench;
```

### Modifying query optimizer
```
ALTER DATABASE pgbench SET optimizer = off;
```
>?
>1. CDWPG is preconfigured with two query optimizers, GPORCA and Postgres Planner. The former is the default and suitable for complex query parsing, while the latter is required for OLTP queries.
>2. This parameter can also be set at the session level. For convenience, it is set directly at the database level; that is, Postgres Planner is used to access this database, while other databases are still accessed via GPORCA.

### Initializing test data
```
./pgbench -i pgbench -s 100 -p 5436 -h {host} -U {user} pgbench
```
>?10 million data records are tested here.

### Running test script
```
./pgbench -h {host} -p 5436 -r -n -c 32 -j 32 -T 120 -P 1 -U {user} pgbench
```

## Optimization
According to Greenplum's official data, v6.x has a peak TPS of about 5,000 in an ideal environment. You can modify the following parameters to reach a higher value in real tests in CDWPG:
<table>
	<thead>
	<tr>
	<th>Parameter</th>
  <th>Value</th>
	<th>Description</th>
	</tr>
	</thead>
<tbody>
	<tr>
		<td>log_statement</td>
    <td>none</td>
		<td>Disables the log output of the master node</td>
	</tr>
	<tr>
		<td>gp_enable_fast_sri</td>
		<td>on</td>
		<td>Improves the efficiency of a single `INSERT`</td>
	</tr>
	<tr>
		<td>gp_enable_gpperfmon</td>
		<td>off</td>
		<td>Disables monitoring sampling</td>
	</tr>
</tbody>
</table>

>?
>1. In addition to the above configuration, you also need to disable the standby master node for optimal performance.
>2. The above configuration is mainly used to test the extreme performance of CDWPG. Therefore, the above modifications are not recommended in actual production environments.
>2. As the configuration modification feature is not available in CDWPG yet, you can [contact us](https://intl.cloud.tencent.com/contact-us) if you need it. You need to restart the cluster after the modification.


