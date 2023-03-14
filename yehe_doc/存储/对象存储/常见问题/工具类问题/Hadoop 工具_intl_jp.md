## 使用/問い合わせに関するご質問

### Hadoop-COSツールとは何ですか。
Hadoop-COSはApache Hadoop、Spark、Tezなどのビッグデータコンピューティングフレームワークの統合をサポートし、HDFSにアクセスする場合と同じように、Tencent Cloud COSに保存されたデータの読み取り/書き込みを行うことができます。また、Druidなどの照会および分析エンジンのDeep Storageとすることも可能です。

### 自作のHadoopでHadoop-COS jarパッケージを使用するにはどうすればよいですか。

Hadoop-COS pomファイルを変更する場合はバージョンをHadoopのバージョンと同一のままにしてコンパイルした後、Hadoop-COS jarパッケージとCOS JAVA SDK jarパッケージをhadoop/share/hadoop/common/libディレクトリ下に入れます。具体的な設定については、[Hadoopツール](https://intl.cloud.tencent.com/document/product/436/6884)のドキュメントをご参照ください。

### Hadoop-COSツールにはごみ箱の仕組みはありますか。

HDFSのごみ箱機能はCOSには適用されません。Hadoop-COSを使用し、`hdfs fs`コマンドによってCOSデータを削除すると、データはcosn://user/${user.name}/.Trashディレクトリ下に移動しますが、実際の削除行為は発生せず、データはCOS上に残ったままです。また、`-skipTrash`パラメータを使用してごみ箱機能をスキップし、データを直接削除することもできます。HDFSのごみ箱機能のように、データの定期的な削除という目的を実現したい場合は、オブジェクトプレフィックスが`/user/${user.name}/.Trash/`のオブジェクトに対するライフサイクルルールを設定してください。設定ガイドについては[ライフサイクルルールの設定](https://intl.cloud.tencent.com/document/product/436/14605)をご参照ください。


## クラスCosFileSystemが見つからないことに関するご質問
### ロードの際に、クラスCosFileSystemが見つからないと表示されます。Error: java.lang.RuntimeException: java.lang.ClassNotFoundException: Class org.apache.hadoop.fs.CosFileSystem not foundと表示されます。

**考えられる原因1**
設定は正しくロードされているが、hadoop classpathにHadoop-COS jarパッケージの位置情報が含まれていない。

**対処方法**
ロードしたHadoop-COS jarパッケージをhadoop classpathに位置付けます。

**考えられる原因2**
設定ファイルmapred-site.xml内のmapreduce.application.classpathにHadoop-COS jarパッケージの位置情報が含まれていない。

**対処方法**
設定ファイルmapred-site.xml内で、mapreduce.application.classpathにcosn jarが存在するパスを追加し、サービスを再起動します。
![img](https://qcloudimg.tencent-cloud.cn/raw/04c63beec0bc34272e9acaa78141c7a9.png)

### 公式のHadoopを使用していますが、クラスCosFileSystemが見つからないと表示されました。

Hadoop-COSはHadoopの公式バージョンとHadoop-COSバージョンをメンテナンスしており、対応するfs.cosn.implとfs.AbstractFileSystem.cosn.implの設定が異なります。
- 公式Hadoopの設定：
```xml
<property>
        <name>fs.cosn.impl</name>
        <value>org.apache.hadoop.fs.cosn.CosNFileSystem</value>
</property>
<property>
        <name>fs.AbstractFileSystem.cosn.impl</name>
        <value>org.apache.hadoop.fs.cosn.CosN</value>
</property>
```
- tencent cosの設定：
```xml
<property>
        <name>fs.cosn.impl</name>
        <value>org.apache.hadoop.fs.CosFileSystem</value>
</property>
<property>
        <name>fs.AbstractFileSystem.cosn.impl</name>
        <value>org.apache.hadoop.fs.CosN</value>
</property>
```

## 頻度管理と帯域幅に関するご質問

### 503エラーが発生するのはなぜですか。
ビッグデータのシーンの、同時実行性が比較的高い状況では、COSの頻度管理がトリガーされ、503 Reduce your request rateエラーがスローされる場合があります。fs.cosn.maxRetriesパラメータを設定することで、エラーになったリクエストをリトライすることができます。このパラメータはデフォルトでは200回です。

### 帯域幅の速度制限を設定しましたが、有効にならないのはなぜですか。
新バージョンでは速度制限設定fs.cosn.traffic.limit(b/s)をサポートしています。この設定はtagが5.8.3およびそれ以降のバージョンでのみサポートされます。[Githubリポジトリ](https://github.com/tencentyun/hadoop-cos)で確認できます。

## パート分割に関するご質問

### Hadoop-COSにアップロードするパートのサイズを適切に設定するにはどうすればよいですか。
Hadoop-COSの内部ではパート分割の同時実行によって大容量ファイルを処理し、fs.cosn.upload.part.size(Byte)の設定によってCOSにアップロードするパートのサイズを制御しています。

COSのマルチパートアップロードでは最大10,000ブロックまでしかサポートできないため、使用できる最大1ファイルサイズを推定する必要があります。例えば、block sizeが8MBの場合、最大で78GBの単一ファイルのアップロードに対応します。block sizeは最大2GBまで対応可能で、1ファイルあたり最大19TBまで対応できます。10,000ブロックを超えるとエラー400がスローされます。この設定が正しいかどうかをチェックすることで確認できます。

### 比較的大容量のファイルをアップロードする際にCOS上のファイルを確認すると、遅延の可能性があるとのことですが、リアルタイムで表示することはできませんか。

Hadoop-COSは大容量ファイル、すなわち1つのblockSize（fs.cosn.upload.part.size)を超えるファイルについてはマルチパートアップロードを使用しており、すべてのパートがCOSにアップロードされてからでなければファイルを見ることができません。Hadoop-COSは現時点ではAppend操作をサポートしていません。

## Bufferに関するご質問

### アップロードのBufferタイプはどのように選択すればよいですか。これらの違いは何ですか。
Hadoop-COSアップロードではbufferのタイプを選択し、fs.cosn.upload.bufferパラメータを使用して設定を行うことができます。次の3つのうち1つを設定できます。
 - mapped_diskはデフォルトの設定です。タスクの実行時にディスクが一杯になることを避けるため、fs_cosn.tmp.dirは十分な容量があるディレクトリに設定する必要があります。
 - direct_memory ：JVMオフヒープメモリを使用します（この部分はJVMのコントロールを受けないため、設定は推奨しません）。
 - non_direct_memory：JVMヒープメモリを使用します。128Mに設定することをお勧めします。

### bufferタイプがmapped_diskの場合にbufferの作成に失敗したと表示されました。表示内容はcreate buffer failed. buffer type: mapped_disk, buffer factory:org.apache.hadoop.fs.buffer.CosNMappedBufferFactoryです。

**考えられる原因**
現在のユーザーがHadoop-COSの使用する一時ディレクトリに対して読み取り/書き込みおよびアクセス権限を持っていないことです。Hadoop-COSがデフォルトで使用する一時ディレクトリは/tmp/hadoop_cosです。あるいはユーザーがfs.cosn.tmp.dirを設定して指定することもできます。

**対処方法**
現在のユーザーに/tmp/hadoop_cosを付与するか、またはfs.cosn.tmp.dirの指定する一時ファイルディレクトリの読み取り/書き込み権限を付与します。

## 動作異常に関するご質問

### コンピューティングタスクの実行中に、エラーメッセージ java.net.ConnectException: Cannot assign requested address (connect failed) (state=42000,code=40000)がスローされましたが、どのように対処すればよいですか。
Cannot assign requested addressのエラーが発生するのは、一般的にユーザーが短時間のうちに大量のTCP短時間接続を確立する一方、接続を閉じた後にローカルポートがすぐには回収されず、デフォルトで60秒のタイムアウト時間経過後となるため、クライアントはこの時間中、Server側とのSocket接続の確立に使用できるポートがないことによるものです。
**解決方法**

`/etc/sysctl.conf`ファイルを変更し、次のカーネルパラメータを調整することで回避します。
```conf
net.ipv4.tcp_timestamps = 1     #TCPタイムスタンプのサポートを有効化
net.ipv4.tcp_tw_reuse = 1       #TIME_WAIT状態にあるsocketを新たなTCP接続に用いることをサポート
net.ipv4.tcp_tw_recycle = 1     #TIME-WAIT状態にあるsocketの迅速回収を有効化
net.ipv4.tcp_syncookies=1       #SYN Cookiesが有効であることを表します。SYN待機キューのオーバーフローが発生した際は、cookieを有効にして処理することで、少量のSYN攻撃を防ぐことができます。デフォルトでは0です
net.ipv4.tcp_fin_timeout = 10              #ポート開放後の待機時間
net.ipv4.tcp_keepalive_time = 1200           #TCPがKeepAliveメッセージを送信する頻度。デフォルトでは2時間ですが、20分に変更します
net.ipv4.ip_local_port_range = 1024 65000    #外部と接続するポートの範囲。デフォルトでは32768から61000ですが、1024から65000に変更します
net.ipv4.tcp_max_tw_buckets = 10240          #TIME_WAIT状態のSocketの数を制限し、この数を超過すると、新たなTIME_WAITソケットは直接開放されます。デフォルト値は180000です。このパラメータを適切に低下させることで、TIME_WAIT状態にあるSocketの数を減らすことができます
```

### ファイルのアップロード時にエラーjava.lang.Thread.State: TIME_WAITING (parking)があり、具体的なスタックにはorg.apache.hadoop.fs.BufferPoll.getBufferおよびjava.util.concurrent.locks.LinkedBlockingQueue.pollのロックされた状況が含まれます。

**考えられる原因**

ファイルのアップロード時にbufferを複数回初期化したが、実際の書き込み操作がトリガーされなかった。

**解決方法**

設定を次のように変更できます。
```xml
<property>
        <name>fs.cosn.upload.buffer</name>
        <value>mapped_disk</value>
</property>
<property>
        <name>fs.cosn.upload.buffer.size</name>
        <value>-1</value>
</property>
```


