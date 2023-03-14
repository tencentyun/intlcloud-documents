
## Test Tool
Sysbench 1.0.20 is the tool used to test the database benchmark performance.

#### Tool installation
Run the following code to install Sysbench 1.0.20:
```
git clone https://github.com/akopytov/sysbench.git
git checkout 1.0.20
yum install gcc gcc-c++ autoconf automake make libtool bzr mysql-devel git mysql
cd sysbench
./autogen.sh
./configure
make -j
make install
```

>?The installation directions above apply to performance stress testing on a CentOS CVM instance. For directions on installing the tool on other operating systems, see [the official Sysbench documentation](https://github.com/akopytov/sysbench?spm=a2c4g.11186623.2.12.36061072oZL2qS).

## Test Environment
| Type | Description |
| :----------------- | :----------------------------------------------------------- |
| Test instance specification       | Three common specifications, namely, 4-core CPU and 8 GB memory, 8-core CPU and 32 GB memory, and 16-core CPU and 128 GB memory |
| Client configuration | 64-core CPU and 128 GB memory |
| Client private network bandwidth | 23 Gbps |
| Test data volume         | Database instance memory * 1.2                                           |
| Test database instance versions | 5.6 20210630, 5.7 20210630, and 8.0 20210330                       |

- Note on client specification: High-spec client machines are used so as to ensure that the database instance performance can be measured through stress testing on a single client. For low-spec clients, we recommend you use multiple clients for concurrent stress testing and aggregate the results.
- Note on network latency: When performing the test, make sure that clients and database instances are in the same AZ to prevent the testing result from being affected by network factors.


## Test Method
### Test data preparations
```
sysbench --db-driver=mysql --mysql-host=xxxx --mysql-port=xxxx --mysql-user=xxxx --mysql-password=xxxx --mysql-db=sbtest --table_size=xxxx --tables=xxxx --events=0 --time=600 --threads=xxxx --percentile=95 --report-interval=1 oltp_read_write prepare
```

### Command for performance stress testing
```
sysbench --db-driver=mysql --mysql-host=xxxx --mysql-port=xxxx --mysql-user=xxxx --mysql-password=xxxx --mysql-db=sbtest --table_size=xxxx --tables=xxxx --events=0 --time=600 --threads=xxxx --percentile=95 --report-interval=1 oltp_read_write run
```

Descriptions of stress testing parameters:
- `oltp_read_write` indicates to implement the OLTP test by calling the `/usr/share/sysbench/oltp_read_write.lua` script.
- `--tables=xxxx` indicates the number of tables in this test.
- `--table_size=xxxx` indicates the number of table rows in this test.
- `--threads=xxxx` indicates the number of concurrent connections of the client in this test.
- `--report-interval=1` indicates that the test result is output once every second.
- `--percentile=95` indicates the sampling rate, which is 95% by default.
- `--time=600` indicates the execution time of this test, which is 600 seconds.

### Scenario model
The test cases in this document all use the Lua script of sysbench.
For the common configurations, performance testing is conducted for different parameter templates. The test results are as follows:

## Test result
#### v5.6 20210630
<table>
<thead><tr><th>CPU (Core)</th><th>Memory (GB)</th><th>Threads</th><th>Test Duration</th><th>Template</th><th>SysBench QPS</th><th>SysBench TPS</th><th>avg_lat</th></tr></thead>
<tbody><tr>
<td rowspan=3>4</td>
<td rowspan=3>8</td>
<td rowspan=3>32</td>
<td rowspan=3>10 min</td>
<td>Default template (disused)</td><td>34428.69</td><td>1721.43</td><td>18.59 ms</td></tr>
<tr>
<td>High-performance parameter template</td><td>35917.50</td><td>1795.87</td><td>17.82 ms</td></tr>
<tr>
<td>High-stability parameter template</td><td>34834.04</td><td>1741.70</td><td>18.37 ms</td></tr>
<tr>
<td rowspan=3>8</td>
<td rowspan=3>32</td>
<td rowspan=3>64</td>
<td rowspan=3>10 min</td>
<td>Default template (disused)</td><td>61210.19</td><td>3060.51</td><td>20.91 ms</td></tr>
<tr>
<td>High-performance parameter template</td><td>67719.55</td><td>3385.98</td><td>18.90 ms</td></tr>
<tr>
<td>High-stability parameter template</td><td>64910.09</td><td>3245.50</td><td>19.72 ms</td></tr>
<tr>
<td rowspan=3>16</td>
<td rowspan=3>128</td>
<td rowspan=3>128</td>
<td rowspan=3>10 min</td>
<td>Default template (disused)</td><td>106965.44</td><td>5348.27</td><td>23.93 ms</td></tr>
<tr>
<td>High-performance parameter template</td><td>127955.48</td><td>6397.77</td><td>20.00 ms</td></tr>
<tr>
<td>High-stability parameter template</td><td>119509.02</td><td>5975.45</td><td>21.41 ms</td></tr>
</tbody></table>

#### v5.7 20210630
<table>
<thead><tr><th>CPU (Core)</th><th>Memory (GB)</th><th>Threads</th><th>Test Duration</th><th>Template</th><th>SysBench QPS</th><th>SysBench TPS</th><th>avg_lat</th></tr></thead>
<tbody><tr>
<td rowspan=3>4</td>
<td rowspan=3>8</td>
<td rowspan=3>32</td>
<td rowspan=3>10 min</td>
<td>Default template (disused)</td><td>34428.69</td><td>1721.43</td><td>18.59 ms</td></tr>
<tr>
<td>High-performance parameter template</td><td>35917.50</td><td>1795.87</td><td>17.82 ms</td></tr>
<tr>
<td>High-stability parameter template</td><td>34834.04</td><td>1741.70</td><td>18.37 ms</td></tr>
<tr>
<td rowspan=3>8</td>
<td rowspan=3>32</td>
<td rowspan=3>64</td>
<td rowspan=3>10 min</td>
<td>Default template (disused)</td><td>61210.19</td><td>3060.51</td><td>20.91 ms</td></tr>
<tr>
<td>High-performance parameter template</td><td>67719.55</td><td>3385.98</td><td>18.90 ms</td></tr>
<tr>
<td>High-stability parameter template</td><td>64910.09</td><td>3245.50</td><td>19.72 ms</td></tr>
<tr>
<td rowspan=3>16</td>
<td rowspan=3>128</td>
<td rowspan=3>128</td>
<td rowspan=3>10 min</td>
<td>Default template (disused)</td><td>106965.44</td><td>5348.27</td><td>23.93 ms</td></tr>
<tr>
<td>High-performance parameter template</td><td>127955.48</td><td>6397.77</td><td>20.00 ms</td></tr>
<tr>
<td>High-stability parameter template</td><td>119509.02</td><td>5975.45</td><td>21.41 ms</td></tr>
</tbody></table>

#### v8.0 20210330
<table>
<thead><tr><th>CPU (Core)</th><th>Memory (GB)</th><th>Threads</th><th>Test Duration</th><th>Template</th><th>SysBench QPS</th><th>SysBench TPS</th><th>avg_lat</th></tr></thead>
<tbody><tr>
<td rowspan=3>4</td>
<td rowspan=3>8</td>
<td rowspan=3>32</td>
<td rowspan=3>10 min</td>
<td>Default template (disused)</td><td>32594.79</td><td>1629.74</td><td>19.63 ms</td></tr>
<tr>
<td>High-performance parameter template</td><td>33383.77</td><td>1669.19</td><td>19.17 ms</td></tr>
<tr>
<td>High-stability parameter template</td><td>32071.90</td><td>1603.60</td><td>19.95 ms</td></tr>
<tr>
<td rowspan=3>8</td>
<td rowspan=3>32</td>
<td rowspan=3>64</td>
<td rowspan=3>10 min</td>
<td>Default template (disused)</td><td>65718.22</td><td>3285.91</td><td>19.47 ms</td></tr>
<tr>
<td>High-performance parameter template</td><td>70195.37</td><td>3509.77</td><td>18.23 ms</td></tr>
<tr>
<td>High-stability parameter template</td><td>60704.69</td><td>3035.23</td><td>21.08 ms</td></tr>
<tr>
<td rowspan=3>16</td>
<td rowspan=3>128</td>
<td rowspan=3>128</td>
<td rowspan=3>10 min</td>
<td>Default template (disused)</td><td>132023.66</td><td>6601.18</td><td>19.38 ms</td></tr>
<tr>
<td>High-performance parameter template</td><td>151021.67</td><td>7551.08</td><td>16.95 ms</td></tr>
<tr>
<td>High-stability parameter template</td><td>132391.01</td><td>6619.55</td><td>19.33 ms</td></tr>
</tbody></table>

