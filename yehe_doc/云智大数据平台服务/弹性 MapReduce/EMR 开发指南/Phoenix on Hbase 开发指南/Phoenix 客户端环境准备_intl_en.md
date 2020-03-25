Apache Phoenix is a massively parallel relational database engine supporting OLTP for Hadoop with Apache HBase as its backing store. Phoenix compiles simple queries in just milliseconds and queries millions of rows of data in seconds. By default, Phoenix is enabled for EMR clusters included HBase component.

Phoenix version 4.8.1 is compiled in EMR environment. First, download phoenix-4.8.1-HBase-1.2 client.

- [Download Phoenix client](https://archive.apache.org/dist/phoenix/apache-phoenix-4.8.1-HBase-1.2/bin/)

- To prepare the environment for the client, copy and decompress the downloaded package to any directory in any node of the EMR cluster (preferably the Hadoop home directory), then enter the bin directory and copy the HBase configuration file Hbase-site.xml to the following directory:
    ``` shell
    cp /usr/local/service/hbase/conf/hbase-site.xml Target path
    ```
To switch to a Hadoop user, use the Phoenix command line for Python:
``` 
./sqlline.py
```
Once the environment for client is prepared, you will see the message on the screen:
![Configuration success](https://mc.qcloudimg.com/static/img/18a364f4f014c8df2edcd89ded877e34/5-4-1.png)
