Hadoop (2.7.2 or above) tool provides the capability to run computing tasks using Tencent Cloud COS as the underlying file storage system. The Hadoop cluster can be launched in three modes: stand-alone, pseudo-distributed, and fully-distributed. This document uses Hadoop-2.7.4 as an example to describe how to build a fully-distributed Hadoop environment and how to use wordcount to execute a simple test.

## Preparation
1. Prepare several servers.
2. Install and configure the system: [CentOS-7-x86_64-DVD-1611.iso](http://isoredirect.centos.org/centos/7/isos/x86_64/)。.
3. Install the Java environment. For more information, see [Installing and Configuring Java](https://intl.cloud.tencent.com/document/product/436/10865).
4. Install the available Hadoop package: [Apache Hadoop Releases Download](http://hadoop.apache.org/releases.html#16+April%2C+2018%3A+Release+2.7.6+available)。 .

#### Network Configuration
Use `ifconfig -a` to check the IP of each server, then use the ping command to check if they can ping each other, and record the IP of each server.

## Configuring CentOS
#### Configure hosts
```
vi /etc/hosts
```
Edit the content:
```
202.xxx.xxx.xxx master
202.xxx.xxx.xxx slave1
202.xxx.xxx.xxx slave2
202.xxx.xxx.xxx slave3
//Replace IPs with the real ones
```
#### Turn off firewall
```
systemctl status firewalld.service  //Check firewall status
systemctl stop firewalld.service  //Turn off firewall
systemctl disable firewalld.service  //Disable firewall to start on boot
```
#### Time synchronization
```
yum install -y ntp  //Install ntp service
ntpdate cn.pool.ntp.org  //Sync network time
```
#### Install and configure JDK
Upload JDK installer package (such as jdk-8u144-linux-x64.tar.gz) to the `root` directory.
```
mkdir /usr/java
tar -zxvf jdk-8u144-linux-x64.tar.gz -C /usr/java/
rm -rf jdk-8u144-linux-x64.tar.gz
```
#### Copy JDKs among hosts
```
scp -r /usr/java slave1:/usr
scp -r /usr/java slave2:/usr
scp -r /usr/java slave3:/usr
.......
```
#### Configure environment variables for JDK of each host
```
vi /etc/profile
```
Edit the content:
```
export JAVA_HOME=/usr/java/jdk1.8.0_144
export PATH=$JAVA_HOME/bin:$PATH
export CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
source/etc/profile    //Make the configuration file take effect
java -version       //View Java version
```
#### Configuring Keyless Access via SSH
Check the SSH service status on each host:
```
systemctl status sshd.service  //Check the SSH service status.
yum install openssh-server openssh-clients  //Install the SSH service. Ignore this step if it is already installed.
systemctl start sshd.service  //Enable the SSH service. Ignore this step if it is already enabled.
```
Generate a key on each host:
```
ssh-keygen -t rsa  //Generate Keys
```
On slave1:
```
cp ~/.ssh/id_rsa.pub ~/.ssh/slave1.id_rsa.pub
scp ~/.ssh/slave1.id_rsa.pub master:~/.ssh
```
On slave2:
```
cp ~/.ssh/id_rsa.pub ~/.ssh/slave2.id_rsa.pub
scp ~/.ssh/slave2.id_rsa.pub master:~/.ssh
```
And so on...

On master:
```
cd ~/.ssh
cat id_rsa.pub >> authorized_keys
cat slave1.id_rsa.pub >>authorized_keys
cat slave2.id_rsa.pub >>authorized_keys
scp authorized_keys slave1:~/.ssh
scp authorized_keys slave2:~/.ssh
scp authorized_keys slave3:~/.ssh
```
## Installing and Configuring Hadoop
### Installing Hadoop
Upload the Hadoop installer package (such as hadoop-2.7.4.tar.gz) to the `root` directory.
```
tar -zxvf hadoop-2.7.4.tar.gz -C /usr
rm -rf hadoop-2.7.4.tar.gz
mkdir /usr/hadoop-2.7.4/tmp
mkdir /usr/hadoop-2.7.4/logs
mkdir /usr/hadoop-2.7.4/hdf
mkdir /usr/hadoop-2.7.4/hdf/data
mkdir /usr/hadoop-2.7.4/hdf/name
```
Go to the `hadoop-2.7.4/etc/hadoop` directory and proceed to the next step.
### Configure Hadoop
#### 1. Add the following to the `hadoop-env.sh` file.
```
export JAVA_HOME=/usr/java/jdk1.8.0_144 
```
If the SSH port is not 22 (default value), modify it in the `hadoop-env.sh` file:
```
export HADOOP_SSH_OPTS="-p 1234"
```
#### 2. Modify `yarn-env.sh`
```
export JAVA_HOME=/usr/java/jdk1.8.0_144
```
#### 3. Modify `slaves`
Configure the content:
```
Delete:
localhost
Add:
slave1
slave2
slave3
```
#### 4. Modify `core-site.xml`
```
<configuration>
  <property>
    <name>fs.default.name</name>
    <value>hdfs://master:9000</value>
  </property>
  <property>
    <name>hadoop.tmp.dir</name>
    <value>file:/usr/hadoop-2.7.4/tmp</value>
  </property>
</configuration>
```
#### 5. Modify `hdfs-site.xml`
```
<configuration>
  <property>
    <name>dfs.datanode.data.dir</name>
    <value>/usr/hadoop-2.7.4/hdf/data</value>
    <final>true</final>
  </property>
  <property>
    <name>dfs.namenode.name.dir</name>
    <value>/usr/hadoop-2.7.4/hdf/name</value>
    <final>true</final>
  </property>
</configuration>
```
#### 6. Modify `mapred-site.xml`
```
<configuration>
  <property>
    <name>mapreduce.framework.name</name>
    <value>yarn</value>
  </property>
  <property>
    <name>mapreduce.jobhistory.address</name>
    <value>master:10020</value>
  </property>
  <property>
    <name>mapreduce.jobhistory.webapp.address</name>
    <value>master:19888</value>
  </property>
</configuration>
```
#### 7. Modify `yarn-site.xml`
```
<configuration>
  <property>
    <name>yarn.nodemanager.aux-services.mapreduce.shuffle.class</name>
    <value>org.apache.mapred.ShuffleHandler</value>
  </property>
  <property>
      <name>yarn.nodemanager.aux-services</name>
      <value>mapreduce_shuffle</value>
  </property>
  <property>
    <name>yarn.resourcemanager.address</name>
    <value>master:8032</value>
  </property>
  <property>
    <name>yarn.resourcemanager.scheduler.address</name>
    <value>master:8030</value>
  </property>
  <property>
    <name>yarn.resourcemanager.resource-tracker.address</name>
    <value>master:8031</value>
  </property>
  <property>
    <name>yarn.resourcemanager.admin.address</name>
    <value>master:8033</value>
  </property>
  <property>
    <name>yarn.resourcemanager.webapp.address</name>
    <value>master:8088</value>
  </property>
</configuration>
```
#### 8. Copy Hadoop among hosts
```
scp -r /usr/ hadoop-2.7.4 slave1:/usr
scp -r /usr/ hadoop-2.7.4 slave2:/usr
scp -r /usr/ hadoop-2.7.4 slave3:/usr
```
#### 9. Configure environment variables for Hadoop of each host
Open the configuration file:
```
vi /etc/profile
```
Edit the content:
```
export HADOOP_HOME=/usr/hadoop-2.7.4
export PATH=$HADOOP_HOME/bin:$HADOOP_HOME/sbin:$PATH
export HADOOP_LOG_DIR=/usr/hadoop-2.7.4/logs
export YARN_LOG_DIR=$HADOOP_LOG_DIR
```
Implement the configuration file:
```
source /etc/profile
```
### Start Hadoop
#### 1. Format namenode
```
cd /usr/hadoop-2.7.4/sbin
hdfs namenode -format
```
#### 2. Start
```
cd /usr/hadoop-2.7.4/sbin
start-all.sh
```
#### 3. Check processes
If processes on master contain ResourceManager, SecondaryNameNode and NameNode, Hadoop starts successfully. For example:
```
2212 ResourceManager
2484 Jps
1917 NameNode
2078 SecondaryNameNode
```
If processes on each slave contain DataNode and NodeManager, Hadoop starts successfully. For example:
```
17153 DataNode
17334 Jps
17241 NodeManager
```
## Running wordcount
The wordcount built in Hadoop can be called directly. After Hadoop starts, use the following command to work with files in HDFS:
```
hadoop fs -mkdir input
hadoop fs -put input.txt /input
hadoop jar share/hadoop/mapreduce/hadoop-mapreduce-examples-2.7.4.jar wordcount /input /output/
```
![](//mc.qcloudimg.com/static/img/50a03d9e0504301d54d12631cc8da075/image.jpg)
The above result shows that Hadoop is installed successfully.

#### View output directory
```
hadoop fs -ls /output
```

#### View output result
```
hadoop fs -cat /output/part-r-00000
```
![](//mc.qcloudimg.com/static/img/6d777bc87c16b0fb10713bbecda1636d/image.jpg)


>?For more information on how to run Hadoop in stand-alone and pseudo-distributed modes, see [Get Started with Hadoop](https://hadoop.apache.org/docs/r1.0.4/cn/quickstart.html) on the official website.

