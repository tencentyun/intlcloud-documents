## 準備作業

1. Tencent Cloudの公式ウェブサイトでCHDFSファイルシステムとCHDFSマウントポイントを作成し、アクセス権限情報を設定します。
2. Tencent Cloud VPC環境のCVMマシンを介して、作成済みのCHDFSにアクセスします。詳細については、[CHDFSの作成](https://intl.cloud.tencent.com/document/product/1106/41961)をご参照ください。
3. マウントが成功したら、hadoopコマンドラインツールを開き、以下のコマンドを実行して、CHDFS検証機能が正常かどうかを検証します。
```bash
hadoop fs -ls ofs://f4xxxxxxxxxxxxxxx.chdfs.ap-beijing.myqcloud.com/
```
以下のような出力が表示される場合は、Cloud HDFS機能のすべてが正常であることを意味します。
![](https://main.qcloudimg.com/raw/3be9476976dd7da027ea6e634652c00b.png)

## 移行

準備ができたら、hadoopコミュニティ標準のDistcpツールを使用して、完全または増分のHDFSデータの移行を行うことができます。詳細については、[Distcp公式ガイドラインドキュメント](https://hadoop.apache.org/docs/r1.0.4/cn/distcp.html)をご参照ください。

#### 注意事項

hadoop distcpツールには、CHDFSと互換性のないパラメータがいくつか提供されています。次の表のパラメータのうちいくつかは、指定しても有効になりません。

| パラメータ| 説明                                        | 状態 |
| -------- | ----------------------------------------------- | -------- |
| -p[rbax] | r：replication，b：block-size，a：ACL，x：XATTR | 無効   |

#### 事例の説明

1. CHDFSの準備ができたら、以下のhadoopコマンドを実行してデータを移行します。
```bash
hadoop distcp hdfs://10.0.1.11:4007/testcp ofs://f4xxxxxxxx-xxxx.chdfs.ap-beijing.myqcloud.com/
```
そのうち`f4xxxxxxxx-xxxx.chdfs.ap-beijing.myqcloud.com`はマウントポイントのドメイン名であり、実際に申請したマウントポイント情報に基づいて置き換える必要があります。
2. Hadoopコマンドが実行された後、移行の具体的な詳細がログに印刷されます。以下に例を示します。
```plaintext
2019-12-31 10:59:31 [INFO ] [main:13300] [org.apache.hadoop.mapreduce.Job:] [Job.java:1385]
 Counters: 38
    File System Counters
        FILE: Number of bytes read=0
        FILE: Number of bytes written=387932
        FILE: Number of read operations=0
        FILE: Number of large read operations=0
        FILE: Number of write operations=0
        HDFS: Number of bytes read=1380
        HDFS: Number of bytes written=74
        HDFS: Number of read operations=21
        HDFS: Number of large read operations=0
        HDFS: Number of write operations=6
        OFS: Number of bytes read=0
        OFS: Number of bytes written=0
        OFS: Number of read operations=0
        OFS: Number of large read operations=0
        OFS: Number of write operations=0
    Job Counters
        Launched map tasks=3
        Other local map tasks=3
        Total time spent by all maps in occupied slots (ms)=419904
        Total time spent by all reduces in occupied slots (ms)=0
        Total time spent by all map tasks (ms)=6561
        Total vcore-milliseconds taken by all map tasks=6561
        Total megabyte-milliseconds taken by all map tasks=6718464
    Map-Reduce Framework
        Map input records=3
        Map output records=2
        Input split bytes=408
        Spilled Records=0
        Failed Shuffles=0
        Merged Map outputs=0
        GC time elapsed (ms)=179
        CPU time spent (ms)=4830
        Physical memory (bytes) snapshot=1051619328
        Virtual memory (bytes) snapshot=12525191168
        Total committed heap usage (bytes)=1383071744
    File Input Format Counters
        Bytes Read=972
File Output Format Counters
        Bytes Written=74
    org.apache.hadoop.tools.mapred.CopyMapper$Counter
        BYTESSKIPPED=5
        COPY=1
        SKIP=2
```

