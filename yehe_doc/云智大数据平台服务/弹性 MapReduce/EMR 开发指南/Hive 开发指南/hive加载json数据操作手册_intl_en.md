### 1. Connect to Hive
Log in to a master node of the EMR cluster, switch to the "hadoop" user, go to the Hive directory, and connect to Hive by running the following command:

```
[root@10 ~]# su hadoop
[hadoop@10 root]$ cd /usr/local/service/hive
```

### 2. Prepare data
Create a data file in JSON format. Compile the following code and save:
```
vim test.data
{"name":"Mary","age":12,"course":[{"name":"math","location":"b208"},{"name":"english","location":"b702"}],"grade":[99,98,95]}
{"name":"Bob","age":20,"course":[{"name":"music","location":"b108"},{"name":"history","location":"b711"}],"grade":[91,92,93]}
```

Store the data file in HDFS:
```
hadoop fs -put ./test.data /
```

### 3. Create a table
Connect to Hive:
```
[hadoop@10 hive]$ hive
```
    
Create a table based on the mapping:
```
hive> CREATE TABLE test ( name string, age int, course array<map<string,string>>, grade array<int>) ROW FORMAT SERDE 'org.apache.hive.hcatalog.data.JsonSerDe' STORED AS TEXTFILE;
```
### 4. Import data
```
hive>LOAD DATA INPATH '/test.data' into table test;
```
### 5. Check whether data import is successful
Query all data:
```
hive> select * from test;
OK
Mary	12	[{"name":"math","location":"b208"},{"name":"english","location":"b702"}]    [99,98,95]
Bob	20	[{"name":"music","location":"b108"},{"name":"history","location":"b711"}]   [91,92,93]
Time taken: 0.153 seconds, Fetched: 2 row(s)
```
Query the first score of each record:
```
hive> select grade[0] from test;
OK
99
91
Time taken: 0.374 seconds, Fetched: 2 row(s)
```
Query the name and location of the first course of each record:
```
hive> select course[0]['name'], course[0]['location'] from test;
OK
math	b208
music	b108
Time taken: 0.162 seconds, Fetched: 2 row(s)
```
