It has been detected that when Tomcat or Hadoop is installed via apt-get command on a Ubuntu14.04 CVM purchased from Tencent Cloud, it can listen to the port but cannot respond to requests. A solution is now available. We recommend following the instructions below if you encounter this issue. 

### Causes
This issue is caused by a [known Java Runtime Environment issue](http://bugs.java.com/bugdatabase/view_bug.do?bug_id=6202721).

### Analysis
Both Tomcat and Hadoop are developed using the Java `java.security.SecureRandom` API.
This API uses `/dev/random` as a random number generator by default in some JREs. `/dev/random` accesses environmental noises collected from devices such as CPU temperature or keyboard timings to generate entropy. However, the virtual environment of CVMs makes it difficult to access such noises and generate entropy, causing `cat /dev/random` to block Tomcat and Hadoop from being started.

### Solution
#### Modifying the JRE configuration
Please change `securerandom.source=file:/dev/urandom` in the original `/etc/java-7-openjdk/security/java.security` (use actual URL) to `securerandom.source=file:/dev/./urandom` to resolve this issue.




