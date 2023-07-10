Hadoopツールは、Hadoop-2.7.2以降のバージョンに依存して、基盤となるファイルストレージシステムとしてTencent Cloud COSを使用し、上位層のコンピューティングタスクを実行する機能を実装しています。Hadoopクラスターを起動するには、主にスタンドアロン、疑似分散、完全分散という3つの主なモードがあります。ここでは主に、Hadoop-2.7.4バージョンを例として、完全分散Hadoop環境をビルド、およびwordcountの簡単なテストをご紹介します。

## 環境の準備
1. 複数のマシンを準備します。
2. システム：[CentOS-7-x86_64-DVD-1611.iso](http://isoredirect.centos.org/centos/7/isos/x86_64/)をインストールして設定します。
3. Java環境をインストールします。操作の詳細については、[Javaのインストールと設定](/doc/product/436/10865)をご参照ください。
4. Hadoopの利用可能なパッケージ[Apache Hadoop Releases Download](http://hadoop.apache.org/releases.html#16+April%2C+2018%3A+Release+2.7.6+available)をインストールします。 

### ネットワークの設定
`ifconfig -a`を使用して各マシンのIPを確認し、pingコマンドを使用して相互にpingを送信できるかどうかを確認し、各マシンのIPを記録します。

## CentOSの設定
#### hostsの設定
```
vi /etc/hosts
```
コンテンツの編集：
```
202.xxx.xxx.xxx master
202.xxx.xxx.xxx slave1
202.xxx.xxx.xxx slave2
202.xxx.xxx.xxx slave3
//IPアドレスを実際のIPに置き換えます
```
#### ファイアウォールの無効化
```
systemctl status firewalld.service  //ファイアウォールのステータスをチェックします
systemctl stop firewalld.service  //ファイアウォールを無効にします
systemctl disable firewalld.service  //ファイアウォールの起動を無効にします
```
#### 時刻同期
```
yum install -y ntp  //ntpサービスをインストールします
ntpdate cn.pool.ntp.org  //ネットワークの時刻を同期させます
```
#### JDKのインストールと設定
JDKインストールパッケージ（jdk-8u144-linux-x64.tar.gzなど）を`root`ルートディレクトリにアップロードします。
```
mkdir /usr/java
tar -zxvf jdk-8u144-linux-x64.tar.gz -C /usr/java/
rm -rf jdk-8u144-linux-x64.tar.gz
```
#### 各ホスト間でのJDKのコピー
```
scp -r /usr/java slave1:/usr
scp -r /usr/java slave2:/usr
scp -r /usr/java slave3:/usr
.......
```
#### 各ホストのJDK環境変数の設定
```
vi /etc/profile
```
コンテンツの編集：
```
export JAVA_HOME=/usr/java/jdk1.8.0_144
export PATH=$JAVA_HOME/bin:$PATH
export CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
source/etc/profile    //設定ファイルを有効にします
java -version       //Javaのバージョンを確認します
```
#### SSHキーレスアクセスの設定
各ホストのSSHサービスステータスを個別にチェックします。
```
systemctl status sshd.service  //SSHサービスのステータスをチェックします
yum install openssh-server openssh-clients  //SSHサービスをインストールします。すでにインストールされている場合は、この手順は不要です
systemctl start sshd.service  //SSHサービスを開始します。すでにインストールされている場合は、この手順は不要です
```
各ホストで個別にキーを発行します
```
ssh-keygen -t rsa  //キーの発行
```
slave1の場合：
```
cp ~/.ssh/id_rsa.pub ~/.ssh/slave1.id_rsa.pub
scp ~/.ssh/slave1.id_rsa.pub master:~/.ssh
```
slave2の場合：
```
cp ~/.ssh/id_rsa.pub ~/.ssh/slave2.id_rsa.pub
scp ~/.ssh/slave2.id_rsa.pub master:~/.ssh
```
という感じで..
masterの場合：
```
cd ~/.ssh
cat id_rsa.pub >> authorized_keys
cat slave1.id_rsa.pub >>authorized_keys
cat slave2.id_rsa.pub >>authorized_keys
scp authorized_keys slave1:~/.ssh
scp authorized_keys slave2:~/.ssh
scp authorized_keys slave3:~/.ssh
```
## Hadoopのインストールと設定
### Hadoopのインストール
hadoopインストールパッケージ（hadoop-2.7.4.tar.gzなど）を`root`ルートディレクトリにアップロードします。
```
tar -zxvf hadoop-2.7.4.tar.gz -C /usr
rm -rf hadoop-2.7.4.tar.gz
mkdir /usr/hadoop-2.7.4/tmp
mkdir /usr/hadoop-2.7.4/logs
mkdir /usr/hadoop-2.7.4/hdf
mkdir /usr/hadoop-2.7.4/hdf/data
mkdir /usr/hadoop-2.7.4/hdf/name
```
`hadoop-2.7.4/etc/hadoop`ディレクトリに移動し、次の操作に進みます。
### Hadoopの設定
#### 1. `hadoop-env.sh`ファイルを変更して、以下を追加します
```
export JAVA_HOME=/usr/java/jdk1.8.0_144 
```
SSHポートがデフォルトの22でない場合は、`hadoop-env.sh`ファイルで以下のように変更します。
```
export HADOOP_SSH_OPTS="-p 1234"
```
#### 2. `yarn-env.sh`を変更します
```
export JAVA_HOME=/usr/java/jdk1.8.0_144
```
#### 3. `slaves`を変更します
設定内容：
```
削除：
localhost
追加：
slave1
slave2
slave3
```
#### 4. `core-site.xml`を変更します
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
#### 5. `hdfs-site.xml`を変更します
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
#### 6. `mapred-site.xml`を変更します
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
#### 7. `yarn-site.xml`を変更します
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
#### 8. ホスト間でHadoopを複製します
```
scp -r /usr/ hadoop-2.7.4 slave1:/usr
scp -r /usr/ hadoop-2.7.4 slave2:/usr
scp -r /usr/ hadoop-2.7.4 slave3:/usr
```
#### 9. 各ホストのHadoop環境変数を設定します
設定ファイルを開きます。
```
vi /etc/profile
```
コンテンツの編集：
```
export HADOOP_HOME=/usr/hadoop-2.7.4
export PATH=$HADOOP_HOME/bin:$HADOOP_HOME/sbin:$PATH
export HADOOP_LOG_DIR=/usr/hadoop-2.7.4/logs
export YARN_LOG_DIR=$HADOOP_LOG_DIR
```
設定ファイルを有効にします。
```
source /etc/profile
```
### Hadoopの起動
#### 1. namenodeのフォーマット
```
cd /usr/hadoop-2.7.4/sbin
hdfs namenode -format
```
#### 2. 起動
```
cd /usr/hadoop-2.7.4/sbin
start-all.sh
```
#### 3. プロセスのチェック
masterホストにResourceManager、SecondaryNameNode、NameNodeなどが含まれている場合は、次のような表示があれば起動に成功しています。
```
2212 ResourceManager
2484 Jps
1917 NameNode
2078 SecondaryNameNode
```
各slaveホストにDataNode、NodeManagerなどが含まれている場合は、次のような表示があれば起動に成功しています。
```
17153 DataNode
17334 Jps
17241 NodeManager
```
## wordcountの実行
Hadoopにはwordcountルーチンが付属されているため、直接呼び出すことができます。Hadoopを起動した後、以下のコマンドを使用すれば、HDFS内のファイルを操作することができます。
```
hadoop fs -mkdir input
hadoop fs -put input.txt /input
hadoop jar share/hadoop/mapreduce/hadoop-mapreduce-examples-2.7.4.jar wordcount /input /output/
```
![6762940-439379efda5b4ad6_レプリカ](//mc.qcloudimg.com/static/img/50a03d9e0504301d54d12631cc8da075/image.jpg)
上図に示されている結果は、Hadoopのインストールが成功したことを示しています。

### 出力ディレクトリの確認
```
hadoop fs -ls /output
```

### 出力結果の確認
```
hadoop fs -cat /output/part-r-00000
```
![6762940-623e7b1c1b81cb4c_レプリカ](//mc.qcloudimg.com/static/img/6d777bc87c16b0fb10713bbecda1636d/image.jpg)

>? スタンドアロンモードと疑似分散モードの詳細な操作方法については、公式サイトの[Hadoop入門](https://hadoop.apache.org/docs/r1.0.4/cn/quickstart.html)をご参照ください。
