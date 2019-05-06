Hadoop(2.7.2 이상) 도구는 Tencent Cloud COS를 기본 저장소로 사용하는 파일 시스템에서 상위 계층 컴퓨팅 작업을 실행할 수 있는 기능을 제공합니다. Hadoop 클러스터는 독립 실행 형, 의사 분산형 및 완전 분산형의 세 가지 모드로 시동할 수 있습니다. 이 문서에서는 Hadoop-2.7.4를 예제로 사용하여 완전히 분산 된 Hadoop 환경을 구축하는 방법과 wordcount를 사용하여 간단한 테스트를 수행하는 방법을 설명합니다.

## 준비
1. 여러 서버를 준비하십시오.
2. 구성 시스템을 설치하십시오. [CentOS-7-x86_64-DVD-1611.iso](http://isoredirect.centos.org/centos/7/isos/x86_64/).
3. Java 환경을 설치하십시오. 자세한 내용은 [Java 설치 및 구성](/doc/product/436/10865)을 참조하십시오.
4. 사용 가능한 Hadoop 패키지를 설치하십시오. [Apache Hadoop Releases Download](http://hadoop.apache.org/releases.html#16+April%2C+2018%3A+Release+2.7.6+available).

### 네트워크 구성
`ifconfig -a`를 사용하여 각 서버의 IP를 확인한 다음 ping 명령을 사용하여 서로 핑(ping) 할 수 있는지 확인하고 각 서버의 IP를 기록하십시오.

## CentOS 구성
### 호스트 구성
```
vi /etc/hosts
```
콘텐츠 편집:
```
202.xxx.xxx.xxx master
202.xxx.xxx.xxx slave1
202.xxx.xxx.xxx slave2
202.xxx.xxx.xxx slave3
//IP 주소를 실제 IP로 바꾸십시오.
```
### 방화벽 끄기
```
systemctl status firewalld.service  // 방화벽 상태 확인
systemctl stop firewalld.service  // 방화벽 끄기
systemctl disable firewalld.service  // 부팅 할 때 방화벽을 시동하지 않도록 설정
```
### 시간 동기화
```
yum install -y ntp  // ntp 서비스 설치
ntpdate cn.pool.ntp.org  // 네트워크 시간 동기화
```
### JDK 설치 및 구성
JDK 설치 프로그램 패키지(예 : jdk-8u144-linux-x64.tar.gz)를`root` 디렉토리에 업로드하십시오.
```
mkdir /usr/java
tar -zxvf jdk-8u144-linux-x64.tar.gz -C /usr/java/
rm -rf jdk-8u144-linux-x64.tar.gz
```
### 각 CVM 서버 간의 JDK 복사
```
scp -r /usr/java slave1:/usr
scp -r /usr/java slave2:/usr
scp -r /usr/java slave3:/usr
.......
```
### 각 CVM 서버의 JDK에 대한 환경 변수 구성
```
vi /etc/profile
```
콘텐츠 편집:
```
export JAVA_HOME=/usr/java/jdk1.8.0_144
export PATH=$JAVA_HOME/bin:$PATH
export CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
source/etc/profile    // 구성 파일을 적용하십시오.
java -version       //Java 버전 보기
```
### SSH를 키 없이 접근 구성
각 CVM 서버에서 SSH 서비스 상태를 확인하십시오.
```
systemctl status sshd.service  //SSH 서비스 상태를 확인하십시오.
yum install openssh-server openssh-clients  //SSH 서비스를 설치하십시오. 이미 활성화 된 경우 이 단계를 무시하십시오.
systemctl start sshd.service  //SSH 서비스를 시동하십시오. 이미 활성화 된 경우 이 단계를 무시하십시오.
```
각 CVM 서버에서 키 생성:
```
ssh-keygen -t rsa  //키 생성
```
slave1에서 :
```
cp ~/.ssh/id_rsa.pub~/.ssh/slave1.id_rsa.pub
scp~/.ssh/slave1.id_rsa.pub master:~/.ssh
```
slave2에서:
```
cp ~/.ssh/id_rsa.pub~/.ssh/slave2.id_rsa.pub
scp ~/.ssh/slave2.id_rsa.pubmaster:~/.ssh
```
등등...
마스터에서:
```
cd ~/.ssh
cat id_rsa.pub >> authorized_keys
cat slave1.id_rsa.pub >>authorized_keys
cat slave2.id_rsa.pub >>authorized_keys
scp authorized_keys slave1:~/.ssh
scp authorized_keys slave2:~/.ssh
scp authorized_keys slave3:~/.ssh
```
## Hadoop 설치 및 구성
### Hadoop 설치
Hadoop 설치 프로그램 패키지(예: hadoop-2.7.4.tar.gz)를 `root` 디렉토리에 업로드하십시오.
```
tar -zxvf hadoop-2.7.4.tar.gz -C /usr
rm -rf hadoop-2.7.4.tar.gz
mkdir /usr/hadoop-2.7.4/tmp
mkdir /usr/hadoop-2.7.4/logs
mkdir /usr/hadoop-2.7.4/hdf
mkdir /usr/hadoop-2.7.4/hdf/data
mkdir /usr/hadoop-2.7.4/hdf/name
```
`hadoop-2.7.4/etc/hadoop` 디렉토리로 가서 다음 단계로 진행하십시오.
### Hadoop 구성
#### 1. `hadoop-env.sh` 파일을 수정하고 다음을 추가하십시오.
```
export JAVA_HOME=/usr/java/jdk1.8.0_144
```
SSH 포트가 22(기본값)가 아니면 `hadoop-env.sh` 파일에서 수정하십시오.
```
export HADOOP_SSH_OPTS="-p 1234"
```
#### 2. `yarn-env.sh` 수정하십시오.
```
export JAVA_HOME=/usr/java/jdk1.8.0_144
```
#### 3. `slaves` 수정하십시오.
콘텐츠 구성:
```
삭제:
localhost
추가:
slave1
slave2
slave3
```
#### 4. `core-site.xml`을 수정하십시오.
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
#### 5. `hdfs-site.xml`을 수정하십시오.
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
#### 6. `mapred-site.xml`을 수정하십시오.
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
#### 7. `yarn-site.xml`을 수정하십시오.
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
#### 8. 각 CVM 서버 간에 Hadoop을 복사하십시오.
```
scp -r /usr/ hadoop-2.7.4 slave1:/usr
scp -r /usr/ hadoop-2.7.4 slave2:/usr
scp -r /usr/ hadoop-2.7.4 slave3:/usr
```
#### 9. 각 CVM 서버의 Hadoop에 대한 환경 변수 구성하십시오.
구성 파일을 열기:
```
vi /etc/profile
```
콘텐츠 편집:
```
export HADOOP_HOME=/usr/hadoop-2.7.4
export PATH=$HADOOP_HOME/bin:$HADOOP_HOME/sbin:$PATH
export HADOOP_LOG_DIR=/usr/hadoop-2.7.4/logs
export YARN_LOG_DIR=$HADOOP_LOG_DIR
```
구성 파일을 활성화:
```
source /etc/profile
```
### Hadoop 시동
#### 1. namenode 포맷
```
cd /usr/hadoop-2.7.4/sbin
hdfs namenode -format
```
#### 2. 시동하기
```
cd /usr/hadoop-2.7.4/sbin
start-all.sh
```
#### 3. 프로세스 확인하기
마스터 CVM 서버에 ResourceManager, SecondaryNameNode 및 NameNode가 있으면 Hadoop이 성공적으로 시동됩니다. 예를들어,
```
2212 ResourceManager
2484 Jps
1917 NameNode
2078 SecondaryNameNode
```
각 슬레이브의 CVM 서버가 DataNode 및 NodeManager를 포함하면 Hadoop이 성공적으로 시동됩니다.
```
17153 DataNode
17334 Jps
17241 NodeManager
```
## wordcount 실행
wordcount이 내장된 Hadoop가 직접 호출 할 수 있습니다. Hadoop이 시작된 후 다음 명령을 사용하여 HDFS의 파일을 작업하십시오.
```
hadoop fs -mkdir input
hadoop fs -put input.txt /input
hadoop jar share/hadoop/mapreduce/hadoop-mapreduce-examples-2.7.4.jar wordcount /input /output/
```
![6762940-439379efda5b4ad6_복사본](//mc.qcloudimg.com/static/img/50a03d9e0504301d54d12631cc8da075/image.jpg)
위의 결과가 나타나면 Hadoop이 성공적으로 설치되었습니다.

### 출력 디렉토리 보기
```
hadoop fs -ls /output
```

### 출력 결과 보기
```
hadoop fs -cat /output/part-r-00000
```
![6762940-623e7b1c1b81cb4c_복사본](//mc.qcloudimg.com/static/img/6d777bc87c16b0fb10713bbecda1636d/image.jpg)

> <font color="#0000cc">**주의:** </font>
> 독립 실행 모드 및 의사 분산 모드에서 Hadoop을 실행하는 방법에 대한 자세한 내용은 [Hadoop 시작하기](https://hadoop.apache.org/docs/r1.0.4/cn/quickstart.html)를 참조하십시오.
