Currently, the Spark component in EMR supports Spark 2.0.2, 2.2.1, and 2.3.2. The software environment information is as follows:
- By default, Spark is installed on a master node.
- After the log-in, run the `su hadoop` command then you can switch to the Hadoop user.
- The Spark software path is `/usr/local/service/spark`.
- The relevant logs are stored in `/data/emr`.

For more information, please see the [community documentation](http://spark.apache.org/docs/2.0.2/). Here is mainly about how to access COS through Spark.
