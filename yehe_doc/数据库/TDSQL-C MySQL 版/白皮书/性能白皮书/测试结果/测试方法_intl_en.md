
This document describes the method of TDSQL-C for MySQL performance test.

## Scenario 1: Full Cache
List of table sizes and table quantities in the full cache test scenario:

<table>
<tr><th rowspan = "1"  width="33%">Specification</th>
<th rowspan = "1"  width="33%">Table Size</th>
<th rowspan = "1"  width="33%">Tables</th></tr>
<tr><td>2-core 16 GB MEM</td><td>25000</td><td>250</td></tr>
<tr><td>4-core 16 GB MEM</td><td>25000</td><td>250</td></tr>
<tr><td>4-core 32 GB MEM</td><td>25000</td><td>250</td></tr>
<tr><td>8-core 32 GB MEM</td><td>25000</td><td>250</td></tr>
<tr><td>8-core 64 GB MEM</td><td>25000</td><td>250</td></tr>
<tr><td>16-core 64 GB MEM</td><td>25000</td><td>250</td></tr>
<tr><td>16-core 96 GB MEM</td><td>25000</td><td>250</td></tr>
<tr><td>16-core 128 GB MEM</td><td>25000</td><td>250</td></tr>
<tr><td>32-core 128 GB MEM</td><td>25000</td><td>250</td></tr>
<tr><td>32-core 256 GB MEM</td><td>25000</td><td>250</td></tr>
<tr><td>64-core 256 GB MEM</td><td>25000</td><td>250</td></tr>
</table>

### Command execution
>?Replace XXX in the following commands with the private network address, port number, username, user password, and database name of the tested TDSQL-C for MySQL cluster, as well as the `table_size` and `tables` corresponding to the test scenario. Specific parameters are as described below:
>- -host: Private network address of the tested instance
>- -port: Port number
>- -user: Username
>- - password: Password of the username
>- -table_size: Data volume in one single table
>- -tables: Total number of tables
>- -mysql-db: Database name 

**1. Write**
```
sysbench --db-driver=mysql --mysql-host=XXX --mysql-port=XXX --mysql-user=XXX --mysql-password=XXX --mysql-db=XXX --table_size=XXX --tables=XXX oltp_write_only run
## Prepare data

sysbench --db-driver=mysql --mysql-host=XXX --mysql-port=XXX --mysql-user=XXX --mysql-password=XXX --mysql-db=XXX --table_size=XXX --tables=XXX --events=0 --time=600   --threads=192 --percentile=95 --report-interval=1 oltp_write_only run
## Run the workload

sysbench --db-driver=mysql --mysql-host=XXX --mysql-port=XXX --mysql-user=XXX --mysql-password=XXX --mysql-db=XXX --table_size=XXX --tables=XXX oltp_write_only cleanup
## Clear the data
```

**2. Read (POINT SELECT)**
```
sysbench --db-driver=mysql --mysql-host=XXX --mysql-port=XXX --mysql-user=XXX --mysql-password=XXX --mysql-db=XXX --table_size=XXX --tables=XXX oltp_read_only prepare
## Prepare data

sysbench --db-driver=mysql --mysql-host=XXX --mysql-port=XXX --mysql-user=XXX --mysql-password=XXX --mysql-db=XXX --table_size=XXX --tables=XXX --events=0 --time=600   --threads=512 --percentile=95 --range_selects=0 --skip-trx=1 --report-interval=1 oltp_read_only run
## Run the workload

sysbench --db-driver=mysql --mysql-host=XXX --mysql-port=XXX --mysql-user=XXX --mysql-password=XXX --mysql-db=XXX --table_size=XXX --tables=XXX oltp_read_only cleanup
## Clear the data
```

**3. Read (RANGE SELECT)**
```
sysbench --db-driver=mysql --mysql-host=XXX --mysql-port=XXX --mysql-user=XXX --mysql-password=XXX --mysql-db=XXX --table_size=XXX --tables=XXX oltp_read_only prepare
## Prepare data

sysbench --db-driver=mysql --mysql-host=XXX --mysql-port=XXX --mysql-user=XXX --mysql-password=XXX --mysql-db=XXX --table_size=XXX --tables=XXX --events=0 --time=600   --threads=512 --percentile=95 --skip-trx=1 --report-interval=1 oltp_read_only run
## Run the workload

sysbench --db-driver=mysql --mysql-host=XXX --mysql-port=XXX --mysql-user=XXX --mysql-password=XXX --mysql-db=XXX --table_size=XXX --tables=XXX oltp_read_only cleanup
## Clear the data
```

**4. Read-write (POINT SELECT)**
```
sysbench --db-driver=mysql --mysql-host=XXX --mysql-port=XXX --mysql-user=XXX --mysql-password=XXX --mysql-db=XXX --table_size=XXX --tables=XXX oltp_read_write run
## Prepare data

sysbench --db-driver=mysql  --mysql-host=XXX --mysql-port=XXX --mysql-user=XXX --mysql-password=XXX --mysql-db=XXX --table_size=XXX --tables=XXX --events=0 --time=600  --range_selects=0 --threads=XXX --percentile=95 --report-interval=1 oltp_read_write run
## Run the workload

sysbench --db-driver=mysql --mysql-host=XXX --mysql-port=XXX --mysql-user=XXX --mysql-password=XXX --mysql-db=XXX --table_size=XXX --tables=XXX oltp_read_write cleanup
## Clear the data
```

**5. Read-write (RANGE SELECT)**
```
sysbench --db-driver=mysql --mysql-host=XXX --mysql-port=XXX --mysql-user=XXX --mysql-password=XXX --mysql-db=XXX --table_size=XXX --tables=XXX oltp_read_write run
## Prepare data

sysbench --db-driver=mysql  --mysql-host=XXX --mysql-port=XXX --mysql-user=XXX --mysql-password=XXX --mysql-db=XXX --table_size=XXX --tables=XXX --events=0 --time=600   --threads=XXX --percentile=95 --report-interval=1 oltp_read_write run
## Run the workload

sysbench --db-driver=mysql --mysql-host=XXX --mysql-port=XXX --mysql-user=XXX --mysql-password=XXX --mysql-db=XXX --table_size=XXX --tables=XXX oltp_read_write cleanup
## Clear the data
```

## Scenario 2: Big Dataset
List of table sizes and table quantities in the big dataset test scenario:
<table>
<tr><th rowspan = "1"  width="33%">Specification</th>
<th rowspan = "1"  width="33%">Table Size</th>
<th rowspan = "1"  width="33%">Tables</th></tr>
<tr><td>2-core 16 GB MEM</td><td>800000</td><td>150</td></tr>
<tr><td>4-core 16 GB MEM</td><td>800000</td><td>300</td></tr>
<tr><td>4-core 32 GB MEM</td><td>800000</td><td>300</td></tr>
<tr><td>8-core 32 GB MEM</td><td>800000</td><td>300</td></tr>
<tr><td>8-core 64 GB MEM</td><td>800000</td><td>450</td></tr>
<tr><td>16-core 64 GB MEM</td><td>800000</td><td>450</td></tr>
<tr><td>16-core 96 GB MEM</td><td>800000</td><td>600</td></tr>
<tr><td>16-core 128 GB MEM</td><td>5000000</td><td>300</td></tr>
<tr><td>32-core 128 GB MEM</td><td>5000000</td><td>300</td></tr>
<tr><td>32-core 256 GB MEM</td><td>5000000</td><td>400</td></tr>
<tr><td>64-core 256 GB MEM</td><td>6000000</td><td>450</td></tr>
</table>

### Command execution
The commands are the same as those in each full cache test scenario. You only need to replace the `table_size` and `tables` in the commands.

## Scenario 3: 1 TB Single Table
List of table sizes and table quantities in the 1 TB single table test scenario:
<table>
<tr><th rowspan = "1"  width="33%">Specification</th>
<th rowspan = "1"  width="33%">Table Size</th>
<th rowspan = "1"  width="33%">Tables</th></tr>
<tr><td>2-core 16 GB MEM</td><td>4000000000</td><td>1</td></tr>
<tr><td>4-core 16 GB MEM</td><td>4000000000</td><td>1</td></tr>
<tr><td>4-core 32 GB MEM</td><td>4000000000</td><td>1</td></tr>
<tr><td>8-core 32 GB MEM</td><td>4000000000</td><td>1</td></tr>
<tr><td>8-core 64 GB MEM</td><td>4000000000</td><td>1</td></tr>
<tr><td>16-core 64 GB MEM</td><td>4000000000</td><td>1</td></tr>
<tr><td>16-core 96 GB MEM</td><td>4000000000</td><td>1</td></tr>
<tr><td>16-core 128 GB MEM</td><td>4000000000</td><td>1</td></tr>
<tr><td>32-core 128 GB MEM</td><td>4000000000</td><td>1</td></tr>
<tr><td>32-core 256 GB MEM</td><td>4000000000</td><td>1</td></tr>
<tr><td>64-core 256 GB MEM</td><td>4000000000</td><td>1</td></tr>
</table>

### Command execution
The commands are the same as those in each full cache test scenario. You only need to replace the `table_size` and `tables` in the commands.

