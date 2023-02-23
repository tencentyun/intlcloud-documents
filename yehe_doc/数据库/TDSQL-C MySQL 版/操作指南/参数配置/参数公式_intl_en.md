TDSQL-C for MySQL supports formulas for certain parameter values to adapt to the database more intelligently. When the instance specification is changed, parameter values set with formulas will also be automatically changed accordingly to keep the database in the optimal or most stable status.

## Notes
- Currently, parameter formulas are only supported for numeric parameters with numeric values. Parameters of other data types cannot be converted into formulas.
- After a formula is set for a parameter, the parameter value will be changed along with the instance specification. If the calculated parameter value falls out of the value range, the minimum or maximum value of the range will be used, whichever is closest to the value you entered.
 Examples:
 - If the value of a parameter calculated by the formula is 7, but the value range of the parameter is 1–6, then the value will be set to 6.
 - If the value of a parameter calculated by the formula is 5, but the value range of the parameter is 6–10, then the value will be set to 6.
- Formula-based parameter values cannot be exported to or imported from a configuration file. When they are exported, they will be automatically converted into integer values.
- To guarantee the database availability, currently only certain parameters can be set with formulas. More parameters will be supported in subsequent iterations.

## Parameter formula description
<table>
<thead><tr><th>Parameter Formula Composition</th><th>Name</th><th>Description</th></tr></thead>
<tbody>
<tr>
<td rowspan="2">Variable</td>
<td>DBinitMemory</td><td>Instance memory in MB (integer type).</td></tr>	
<td>DBInitCpu</td><td>The number of CPU cores of the instance (integer type).</td></tr>	
<tr>
<td rowspan="2">Operator</td>
<td>Division operator (/)</td><td>It divides the dividend by the divisor and returns an integer quotient. If the calculation result is a decimal number, only the integer part will be retained.</td></tr>	
<td>Multiplication operator (*)</td><td>It multiplies two numbers and returns an integer product. If the calculation result is a decimal number, only the integer part will be retained.</td></tr>	
<tr>
<td rowspan="2">Function</td>
<td>MIN()</td><td>It returns the smallest value in an integer or parameter formula list.</td></tr>	
<td>MAX()</td><td>It returns the greatest value in an integer or parameter formula list.</td></tr>
</tbody></table>

**Sample:**
The parameter value calculated by the formula `MAX(DBInitCpu/2,4)` is the greater value between 4 and the number of CPU cores of the instance divided by 2.

## Parameters supported for formulas
The following parameters support formulas on the current version. All numeric parts in the default formulas can be customized as needed.

<table>
<thead><tr><th>Parameter</th><th>Description</th><th>Default Formula</th></tr></thead>
<tbody>
<tr>
<td>binlog_cache_size</td><td>The size of the memory buffer used to save changed binary logs during a transaction.</td><td>MIN(DBInitMemory/4000 * 32768,2097152)</td></tr>	
<td>max_heap_table_size</td><td>The maximum size that the memory allows a user-created table to grow to.
</td><td>MIN( DBInitMemory/1000 * 4194304,134217728)</td></tr>
<td>innodb_buffer_pool_size</td><td>The size of the buffer pool in bytes, i.e., the memory zone where InnoDB caches tables and index data.</td><td>min((DBInitMemory - 500), DBInitMemory*3/4)*1000000</td></tr>
<td>innodb_buffer_pool_instances</td><td>The number of zones in the InnoDB buffer pool.</td><td>MIN(DBInitMemory/2000,16)</td></tr>
<td>innodb_read_io_threads</td><td>The number of I/O threads in InnoDB used for read operations.</td><td>MAX(DBInitCpu/2,4)</td></tr>
<td>innodb_write_io_threads</td><td>The number of I/O threads in InnoDB used for write operations.</td><td>MAX(DBInitCpu/2,4)</td></tr>
<td>join_buffer_size</td><td>The minimum size of the buffer used for normal index scans, range index scans, and table joins that perform full-table scans.</td><td>MIN(DBInitMemory*128,262144)</td></tr>
<td>max_connections</td><td>The maximum number of connections.</td><td>MIN(DBInitMemory/4+500,100000)</td></tr>
<td>table_definition_cache</td><td>The number of opened table cache instances.</td><td>MAX(DBInitMemory*512/1000,2048)</td></tr>
<td>table_open_cache</td><td>The size of the table descriptor, which can reduce the file open/close times.</td><td>MIN(MAX(DBInitMemory*512/1000,2048), 65536)</td></tr>
<td>table_open_cache_instances</td><td>The number of zones where MySQL caches table handles.</td><td>MIN(DBInitMemory/1000,16)</td></tr>
<td>thread_pool_size</td><td>The number of thread groups in the thread pool. The default value means that the number of thread groups is the same as the number of CPU cores.</td><td>MIN(DBInitCpu,64)</td></tr>
<td>thread_cache_size</td><td>The number of threads that need to be retained in the cache for reuse.</td><td>MIN(DBInitMemory/125+8,512)</td></tr>
<td>tmp_table_size</td><td>The maximum size of a temp table in the internal memory.</td><td>MIN(DBInitMemory/1000*4194304,134217728)</td></tr>
</tbody></table>


