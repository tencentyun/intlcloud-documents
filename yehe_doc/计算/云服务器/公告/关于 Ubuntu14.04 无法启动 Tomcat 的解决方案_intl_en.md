
Dear user,
It is found that when Tomcat and Hadoop are installed by using apt-get on the Ubuntu14.04 CVM purchased from Tencent Cloud official website, the port can be listened normally but cannot respond to requests. Luckily, a solution is now available. We recommend you follow the instructions to solve this issue.

### Causes
This issue is caused by a [known problem](http://bugs.java.com/bugdatabase/view_bug.do?bug_id=6202721) of Java Runtime Environment.

### Analysis
Both Tomcat and Hadoop are developed with Java using the API of `java.security.SecureRandom`.
The API is generated with '/dev/random' by default in some JREs, whereas '/dev/random' receives CPU temperature as well as noises of such hardware as keyboard to generate entropy. However, in the virtual machine environment of CVM, it is difficult to sense the signals such as CPU temperature and to generate entropy. For this reason, 'cat /dev/random' is almost blocked, thus preventing Tomcat and Hadoop from being started.

### Solution
#### Modifying the JRE configuration
Please change 'securerandom.source=file:/dev/urandom' in the original '/etc/java-7-openjdk/security/java.security' (the URL depends on the situation) to 'securerandom.source=file:/dev/./urandom' to solve this problem.




