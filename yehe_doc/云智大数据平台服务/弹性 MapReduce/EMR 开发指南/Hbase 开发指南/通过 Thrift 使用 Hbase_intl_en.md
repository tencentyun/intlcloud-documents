Apache Thrift is a software framework used for scalable cross-language services development. It allows you to define data types and service interfaces in a Thrift File through interface definition language (IDL). The Thrift compiler generates your Thrift File into source code which is to be used to build different clients and servers that communicate seamlessly across programming languages.
The Apache Thrift software framework, for scalable cross-language services development, combines a software stack with a code generation engine to build services that work efficiently and seamlessly between C++, Java, Python, PHP, Ruby, Erlang, Perl, Haskell, C#, Cocoa, JavaScript, Node.js, Smalltalk and OCaml and other languages.

Thrift server is a Hive-compatible interface for HBase used to support multi-language APIs. The HBase Thrift interface allows other languages to access HBase over Thrift by connecting to a Thrift server that interfaces with the Java client. This section will describe how to connect HBase with Python and Thrift.

## 1. Preparations for Development
- Confirm that you have activated Tencent Cloud and created an EMR cluster. When creating the EMR cluster, select the HBase component on the software configuration page.

## 2. Using HBase with the Python API
HBase on EMR is integrated with Thrift by default, and the Thrift server is started on the Master1 node (the node with a public IP).
Log in to any node (preferably a master one) in the EMR cluster. For more information on how to log in to EMR, please see [Logging in to Linux Instances](https://intl.cloud.tencent.com/document/product/213/5436). Here, you can choose to log in with WebShell. Click "Log in" on the right of the desired CVM instance to enter the login page. The default username is `root`, and the password is the one you set when creating the EMR cluster. Once the correct credentials are entered, you can enter the command line interface.

Run the following command on the EMR command-line interface to switch to the Hadoop user and go to the HBase folder:
```
[root@172 ~]# su hadoop
[hadoop@172 root]$ cd /usr/local/service/hbase/
[hadoop@172 hbase]$
```
View the IP address and port number of Thrift in HBase's configuration file:
```
[hadoop@172 hbase]$ vim conf/hbase-site.xml

<property>
        <name>hbase.master.hostname</name>
        <value>$thriftIP</value>
</property>
<property>
        <name>hbase.regionserver.thrift.port</name>
        <value>$port</value>
</property>
```
Here, $port is the port number of the Thrift server.
By default, HBase is connected with Thrift for EMR clusters. So you don’t need to install and configure Thrift. Run the following command to check whether the Thrift server has been started:
```
[hadoop@172 hbase]$ jps

4711 ThriftServer
```
The message above indicates that the Thrift server is already running in the background. Now you can operate HBase directly with Python.

### Preparing data
Use HBase Shell to create a HBase table. If you have already created one through HBase on EMR, skip this step:
```
[hadoop@172 hbase]$ hbase shell 

hbase(main):001:0> create 'thrift_test', 'cf'
hbase(main):005:0> list
thrift_test                                                                                     
1 row(s) in 0.2270 seconds

hbase(main):001:0> quit
```

### Viewing a table in HBase with Python
First, you need to install the Python dependencies. Switch to the root user with the password that is same as the one for EMR cluster, install the python-pip tool first and then dependencies:
```
[hadoop@172 hbase]$ su
Password: ********
[root@172 hbase]# yum install python-pip
[root@172 hbase]# pip install hbase-thrift
```
Then, switch back to the Hadoop user, create a Python file Hbase_client.py, and add the following code to it:
```
#! /usr/bin/env python
#coding=utf-8

from thrift.transport import TSocket,TTransport
from thrift.protocol import TBinaryProtocol
from hbase import Hbase

socket = TSocket.TSocket('$thriftIP ', $port)
socket.setTimeout(5000)

transport = TTransport.TBufferedTransport(socket)
protocol = TBinaryProtocol.TBinaryProtocol(transport)

client = Hbase.Client(protocol)
transport.open()

print client.getTableNames()
```
>Here, $thriftIP is the IP address of the master node on the private network, and $port is the port number of ThriftService.

Save and run the file, and the table in HBase will be shown in the console:
```
[hadoop@172 hbase]$ python Hbase_client.py
['thrift_test']
```

### Creating an HBase table with Python
Create a Python file Create_table.py, and add the following code to it:
```
#! /usr/bin/env python
#coding=utf-8

from thrift import Thrift
from thrift.transport import TSocket,TTransport
from thrift.protocol import TBinaryProtocol
from hbase import Hbase
from hbase.ttypes import ColumnDescriptor,Mutation,BatchMutation,TRegionInfo
from hbase.ttypes import IOError,AlreadyExists

socket = TSocket.TSocket('$thriftIP ',$port)
socket.setTimeout(5000)

transport = TTransport.TBufferedTransport(socket)
protocol = TBinaryProtocol.TBinaryProtocol(transport)

client = Hbase.Client(protocol)
transport.open()

new_table = ColumnDescriptor(name = 'cf:',maxVersions = 1)
client.createTable('thrift_test_1',[new_table])

tables = client.getTableNames()
socket.close()

print tables
```
The program will add a new table thrift_test_1 in HBase and output all existing tables:
```
[hadoop@172 hbase]$ python Create_table.py
['thrift_test', 'thrift_test_1']
```

### Inserting data into an HBase table with Python
Create a Python file Insert.py and add the following code to it:
```
#! /usr/bin/env python
#coding=utf-8

from thrift import Thrift
from thrift.transport import TSocket,TTransport
from thrift.protocol import TBinaryProtocol
from hbase import Hbase
from hbase.ttypes import ColumnDescriptor,Mutation,BatchMutation,TRegionInfo
from hbase.ttypes import IOError,AlreadyExists

socket = TSocket.TSocket('$thriftIP ', $port)
socket.setTimeout(5000)

transport = TTransport.TBufferedTransport(socket)
protocol = TBinaryProtocol.TBinaryProtocol(transport)

client = Hbase.Client(protocol)
transport.open()

mutation1 = [Mutation(column = "cf:a",value = "value1")]
client.mutateRow('thrift_test_1',"row1",mutation1)

mutation2 = [Mutation(column = "cf:b",value = "value2")]
client.mutateRow('thrift_test_1',"row1",mutation2)

mutation1 = [Mutation(column = "cf:a",value = "value3")]
client.mutateRow('thrift_test_1',"row2",mutation1)

mutation2 = [Mutation(column = "cf:b",value = "value4")]
client.mutateRow('thrift_test_1',"row2",mutation2)

socket.close()
```
The program will add two rows of data to the thrift_test_1 table in HBase, each with two data entries, which can be viewed in HBase Shell:
```
hbase(main):005:0> scan 'thrift_test_1'
ROW       COLUMN+CELL                                                             
row1       column=cf:a, timestamp=1530697238581, value=value1                      
row1       column=cf:b, timestamp=1530697238587, value=value2                      
row2       column=cf:a, timestamp=1530704886969, value=value3                      
row2       column=cf:b, timestamp=1530704886975, value=value4                      
2 row(s) in 0.0190 seconds
```

### Viewing data in an HBase table with Python
You can view the data by row or scan the entire dataset. Create a Python file Scan_table.py and add the following code to it:
```
#! /usr/bin/env python
#coding=utf-8

from thrift import Thrift
from thrift.transport import TSocket,TTransport
from thrift.protocol import TBinaryProtocol
from hbase import Hbase
from hbase.ttypes import ColumnDescriptor,Mutation,BatchMutation,TRegionInfo
from hbase.ttypes import IOError,AlreadyExists

socket = TSocket.TSocket('$thriftIP ', $port)
socket.setTimeout(5000)

transport = TTransport.TBufferedTransport(socket)
protocol = TBinaryProtocol.TBinaryProtocol(transport)

client = Hbase.Client(protocol)
transport.open()

result1 = client.getRow("thrift_test_1","row1")
print result1
for r in result1:
        print 'the rowname is ',r.row
        print 'the frist value is ',r.columns.get('cf:a').value
        print 'the second value is ',r.columns.get('cf:b').value

scanId = client.scannerOpen('thrift_test_1',"",["cf"])
result2 = client.scannerGetList(scanId,10)
print result2

client.scannerClose(scanId)
socket.close()
```
Use GetRow to get the data of one row, or use scannerGetList to get all the data in the table. The output of the program is as follows:
```
[hadoop@172 hbase]$ python Scan_table.py
[TRowResult(columns={'cf:a': TCell(timestamp=1530697238581, value='value1'), 'cf:b': TCell(timestamp=1530697238587, value='value2')}, row='row1')]
the rowname is  row1
the frist value is  value1
the second value is  value2

[TRowResult(columns={'cf:a': TCell(timestamp=1530697238581, value='value1'), 'cf:b': TCell(timestamp=1530697238587, value='value2')}, row='row1'), TRowResult(columns={'cf:a': TCell(timestamp=1530704886969, value='value3'), 'cf:b': TCell(timestamp=1530704886975, value='value4')}, row='row2')]
```
As you can see, the data of the first row and the data of the entire table are outputted separately.

### Deleting data from HBase with Python
Create a Python file Delete_row.py and add the following code to it:
```
#! /usr/bin/env python
#coding=utf-8

from thrift import Thrift
from thrift.transport import TSocket,TTransport
from thrift.protocol import TBinaryProtocol
from hbase import Hbase
from hbase.ttypes import *

socket = TSocket.TSocket('$thriftIP ',$port)
socket.setTimeout(5000)

transport = TTransport.TBufferedTransport(socket)
protocol = TBinaryProtocol.TBinaryProtocol(transport)

client = Hbase.Client(protocol)
transport.open()

client.deleteAllRow("thrift_test_1","row2")

socket.close()
```
The program will delete the second row of data in the test table. After the program is executed, you can view the table in HBase Shell:
```
[hadoop@172 hbase]$ python Delete_row.py
[hadoop@172 hbase]$ hbase shell

hbase(main):004:0> scan 'thrift_test_1'
ROW     COLUMN+CELL                                                                             
 row1     column=cf:a, timestamp=1530697238581, value=value1                                     
 row1     column=cf:b, timestamp=1530697238587, value=value2                                     
1 row(s) in 0.2050 seconds
```
Now the table contains only the data in the first row
For more information on Thrift operations, please see [How to Use Thrift](http://blog.cloudera.com/blog/2013/09/how-to-use-the-hbase-thrift-interface-part-1/?spm=5176.doc53887.2.4.6Nfd1X).
