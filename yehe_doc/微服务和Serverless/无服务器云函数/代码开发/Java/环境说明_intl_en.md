### Java Version Selection

Currently, SCF supports the following versions of Java programming language:

- Java 11 (Kona JDK)
- Java 8 (Open JDK)

You can choose Java 8 or Java 11 as the runtime environment when creating a function.

SCF Java 11 is provided based on Tencent Kona. Tencent Kona is based on OpenJDK and maintained, optimized, and safeguarded by Tencent's professional technical team. The Tencent Cloud team has further developed and optimized Kona's support and features in cloud scenarios, making it more suitable for Java cloud businesses and delivering the best Java cloud production environment and solution.

### Environment Variables
The environment variables built in the Java 8 and Java 11 runtime environments are as shown in the table below:

#### Java 11  

| Environment Variable Key | Specific Value or Value Source |
| ------------ | --------------------------------------------- |
| `CLASSPATH`  | /var/runtime/java11:/var/runtime/java11/lib/* |

#### Java 8 

| Environment Variable Key | Specific Value or Value Source |
| ------------ | ------------------------------------------------ |
| `CLASSPATH`  | /var/runtime/java8:/var/runtime/java8/lib/*:/opt |

For more information on environment variables, see [Environment Variables](https://intl.cloud.tencent.com/document/product/583/32748).

### Notes

As the Java language can be executed in JVM only after compilation, it is used in SCF in a different way from scripting languages such as Python and Node.js, with the following restrictions:
- Code upload is not supported: When Java is used, only developed, compiled, and packaged ZIP or JAR packages can be uploaded. The SCF environment does not provide Java compiling capability.
- Online editing is not supported: Because code cannot be uploaded, online code editing is not supported. The code page of a Java runtime function only lists the ways to upload the code through the page or submit the code through COS.
