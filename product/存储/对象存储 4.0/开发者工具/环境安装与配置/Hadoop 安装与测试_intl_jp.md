Hadoopツールは、Hadoop-2.7.2以降のバージョンに依存します。Tencent Cloud COSが最下層ストレージファイルシステムとして上位計算タスクを実行する機能を果たします。Hadoopクラスタの起動は主にスタンドアロン、疑似分散、完全分散の3つのモードがあります。本書は、Hadoop-2.7.4バージョンを例に挙げてHadoopの完全分散型環境構築とwordcount簡易テストを説明します。

## 準備環境
1. 複数台のマシンを用意します。
2. 構成システムのインストール：[CentOS-7-x86_64-DVD-1611.iso](http://isoredirect.centos.org/centos/7/isos/x86_64/)。
3. Java環境をインストールします。詳細については、[Javaのインストールと構成](/doc/product/436/10865)を参照してください。
4. Hadoop使用可能パッケージのインストール：[Apache Hadoop Releases Download](http://hadoop.apache.org/releases.html#16+April%2C+2018%3A+Release+2.7.6+available)。

### ネットワーク構成
`ifconfig -a`を使って各マシンのIPを表示し、互いにpingコマンドを実行して疎通確認を行います。同時に各マシンのIPを記録します。

## CentOS構成
### hosts構成
```
vi /etc/hosts
```
編集内容：
```
202.xxx.xxx.xxx master
202.xxx.xxx.xxx slave1
202.xxx.xxx.xxx slave2
202.xxx.xxx.xxx slave3
//IPアドレスを実IPに置き換える
```
### ファイアウォールを無効にする
```
systemctl status firewalld.service  //ファイアウォールステータスを確認する
systemctl stop firewalld.service  //ファイアウォールを無効にする
systemctl disable firewalld.service  //起動後のファイアウォール起動を無効にする
```
### 時間の同期
```
yum install -y ntp  //ntpサービスをインストールする
ntpdate cn.pool.ntp.org  //ネットワーク時間を同期する
```
### JDKのインストールと構成
JDKインストールパッケージ（例えば、jdk-8u144-linux-x64.tar.gz）を`root`ルートディレクトリにアップロードします。
```
mkdir /usr/java
tar -zxvf jdk-8u144-linux-x64.tar.gz -C /usr/java/
rm -rf jdk-8u144-linux-x64.tar.gz
```
### 各CVMの間にJDKをレプリケーションする
```
scp -r /usr/java slave1:/usr
scp -r /usr/java slave2:/usr
scp -r /usr/java slave3:/usr
.......
```
### 各CVMのJDK環境変数を構成する
```
vi /etc/profile
```
編集内容：
```
export JAVA_HOME=/usr/java/jdk1.8.0_144
export PATH=$JAVA_HOME/bin:$PATH
export CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
source/etc/profile    //構成ファイルを有効にする
java -version       //javaバージョンを表示する
```
### SSHの暗号鍵フリーアクセスを構成する
各CVMにてSSHサービスステータスを確認する。
```
systemctl status sshd.service  //SSHサービスステータスを確認する
yum install openssh-server openssh-clients  //SSHサービスをインストールする。インストール済みの場合、このステップを実行する必要がありません
systemctl start sshd.service  //SSHサービスを有効にする。インストール済みの場合、このステップを実行する必要がありません
```
各CVMで暗号鍵を生成する。
```
ssh-keygen -t rsa  //暗号鍵の生成
```
slave1：
```
cp ~/.ssh/id_rsa.pub~/.ssh/slave1.id_rsa.pub
scp~/.ssh/slave1.id_rsa.pub master:~/.ssh
```
slave2：
```
cp ~/.ssh/id_rsa.pub~/.ssh/slave2.id_rsa.pub
scp ~/.ssh/slave2.id_rsa.pubmaster:~/.ssh
```
これによって類推する...
master：
```
cd ~/.ssh
cat id_rsa.pub >> authorized_keys
cat slave1.id_rsa.pub >>authorized_keys
cat slave2.id_rsa.pub >>authorized_keys
scp authorized_keys slave1:~/.ssh
scp authorized_keys slave2:~/.ssh
scp authorized_keys slave3:~/.ssh
```
## Hadoopのインストールと構成
### Hadoopのインストール
hadoopのインストールパッケージ（例えば、hadoop-2.7.4.tar.gz）を`root`ルートディレクトリにアップロードします。
```
tar -zxvf hadoop-2.7.4.tar.gz -C /usr
rm -rf hadoop-2.7.4.tar.gz
mkdir /usr/hadoop-2.7.4/tmp
mkdir /usr/hadoop-2.7.4/logs
mkdir /usr/hadoop-2.7.4/hdf
mkdir /usr/hadoop-2.7.4/hdf/data
mkdir /usr/hadoop-2.7.4/hdf/name
```
`hadoop-2.7.4/etc/hadoop`ディレクトリに入り、次の操作を行います。
### Hadoopの構成
#### 1. `hadoop-env.sh`ファイルを変更する。追加
```
export JAVA_HOME=/usr/java/jdk1.8.0_144
```
SSHポートはデフォルト値22でなければ、`hadoop-env.sh`ファイルに変更できます。
```
export HADOOP_SSH_OPTS="-p 1234"
```
#### 2. `yarn-env.sh`を変更する
```
export JAVA_HOME=/usr/java/jdk1.8.0_144
```
#### 3. `slaves`を変更する
構成内容：
```
削除：
localhost
追加：
slave1
slave2
slave3
```
#### 4. `core-site.xml`を変更する
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
#### 5. `hdfs-site.xml`を変更する
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
#### 6. `mapred-site.xml`を変更する
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
#### 7. `yarn-site.xml`を変更する
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
#### 8. 各CVMの間にHadoopレプリケーションを行う
```
scp -r /usr/ hadoop-2.7.4 slave1:/usr
scp -r /usr/ hadoop-2.7.4 slave2:/usr
scp -r /usr/ hadoop-2.7.4 slave3:/usr
```
#### 9. 各CVMにHadoop環境変数を構成する
構成ファイルを開きます。
```
vi /etc/profile
```
編集内容：
```
export HADOOP_HOME=/usr/hadoop-2.7.4
export PATH=$HADOOP_HOME/bin:$HADOOP_HOME/sbin:$PATH
export HADOOP_LOG_DIR=/usr/hadoop-2.7.4/logs
export YARN_LOG_DIR=$HADOOP_LOG_DIR
```
構成ファイルを有効にします。
```
source /etc/profile
```
### Hadoopを起動する
#### 1. namenodeをフォーマットする
```
cd /usr/hadoop-2.7.4/sbin
hdfs namenode -format
```
#### 2. 起動する
```
cd /usr/hadoop-2.7.4/sbin
start-all.sh
```
#### 3. プロセスを確認する
master CVMは、ResourceManager、SecondaryNameNode、NameNodeなどを含む場合、起動成功を表します。例えば：
```
2212 ResourceManager
2484 Jps
1917 NameNode
2078 SecondaryNameNode
```
各slave CVMは、DataNode、NodeManagerなどを含む場合、起動成功を表します。例えば：
```
17153 DataNode
17334 Jps
17241 NodeManager
```
## wordcountを実行する
Hadoopにwordcountルーチンが付属されるため、直接的に呼び出すことができます。Hadoopを起動した後、以下のコマンドを通じてHDFSのファイルを操作できます。
```
hadoop fs -mkdir input
hadoop fs -put input.txt /input
hadoop jar share/hadoop/mapreduce/hadoop-mapreduce-examples-2.7.4.jar wordcount /input /output/
```
![6762940-439379efda5b4ad6_コピー](//mc.qcloudimg.com/static/img/50a03d9e0504301d54d12631cc8da075/image.jpg)
上図の結果が表示されるとHadoopが正常にインストールされたことを示します。

### 出力ディレクトリの表示
```
hadoop fs -ls /output
```

### 出力結果の表示
```
hadoop fs -cat /output/part-r-00000
```
![6762940-623e7b1c1b81cb4c_コピー](//mc.qcloudimg.com/static/img/6d777bc87c16b0fb10713bbecda1636d/image.jpg)

> <font color="#0000cc">**注意：** </font>
> スタンドアロンモードと疑似分散モードの操作方法の詳細プロセスについては、公式サイト：[Hadoop入門](https://hadoop.apache.org/docs/r1.0.4/cn/quickstart.html)を参考してください。
