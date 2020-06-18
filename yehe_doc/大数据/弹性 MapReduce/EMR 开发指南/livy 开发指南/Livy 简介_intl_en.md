Apache Livy enables easy interaction with a Spark cluster over RESTful APIs. It allows easy submission of Spark jobs or snippets of Spark code, synch and async result search, as well as Spark context management. It also simplifies the interaction between Spark and application servers, thus enabling the use of Spark for interactive web/mobile applications.

**Other features:**
- Long running Spark contexts can be used for multiple Spark jobs by multiple clients.
- Cached RDDs or data frames can be shared across multiple jobs and clients.
- Multiple Spark contexts can be managed simultaneously, and the Spark contexts run on the cluster (YARN/Mesos) instead of the Livy server for better fault tolerance and concurrency.
- Jobs can be submitted as precompiled jars or snippets of code or through Java/Scala client APIs.
- Security can be ensured through secure authenticated communication.

![](https://main.qcloudimg.com/raw/4dc71e49b36d1790760e97cdd54543b6.png)

## Using Livy
1. 	Access `http://IP:8998/ui` to enter the web UI of Livy (**IP is the public IP. Please apply for a public IP for the server where Livy is installed and enable the corresponding security group policy for access**).
2.	Create an interactive session.
```
curl -X POST --data '{"kind":"spark"}' -H "Content-Type:application/json" IP:8998/sessions
```
3.	View the live sessions on Livy.
```
curl IP:8998/sessions
```
4.	Execute the code snippet to perform a simple addition operation (here, specify session 0, or specify another session if there are multiple sessions).
```
curl -X POST IP:8998/sessions/0/statements -H "Content-Type:application/json" -d '{"code":"1+1"}'
```
5.	Calculate the pi (execute the jar package).
```
curl -H "Content-Type: application/json" -X POST -d '{ "file":"/usr/local/service/spark/examples/jars/spark-examples_2.11-2.4.3.jar", "className":"org.apache.spark.examples.SparkPi" }' IP:8998/batches
```
6.	Check whether the code snippet has been successfully executed. You can also view it in the web UI `http://IP:8998/ui/session/0`.
```
curl IP:8998/sessions/0/statements/0
```
7.	Delete the session.
```
curl -X DELETE IP:8998/sessions/0
```

## Notes
### Open configuration files
Currently, open configuration files include `livy.conf` and `livy-env.sh`, both of which can be used to modify the configuration through configuration distribution. Please check the EMR Console for the actual open configuration files.

### Changing the port used by Livy
By default, Livy runs on port 8998, which can be changed with the `livy.server.port` configuration option in the `livy.conf` configuration file.

If Hue is installed in the cluster, due to the connectivity between Hue and Livy, the port for Hue also needs to be changed with the `livy_server_port=8998` configuration option in the `pseudo-distributed.ini` configuration file at `/usr/local/service/hue/desktop/conf`. The service needs to be restarted after the change.

**Unless necessary, you are not recommended to modify the port used by Livy. Instead, you can control the access by using a security group for security reasons. Any change may cause other potential problems.**

### Deployment of Livy
Currently, Livy is deployed on all master nodes by default. You can also deploy it on router nodes by scaling out router nodes.
