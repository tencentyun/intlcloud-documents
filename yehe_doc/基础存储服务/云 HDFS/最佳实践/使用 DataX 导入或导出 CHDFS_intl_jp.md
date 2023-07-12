## 環境の依存

- [CHDFS_JAR](https://github.com/tencentyun/chdfs-hadoop-plugin)。
- DataXバージョン：DataX-3.0。

### ダウンロードとインストール

#### CHDFS JARの取得

公式Githubで[CHDFS_JAR](https://github.com/tencentyun/chdfs-hadoop-plugin)をダウンロードします。

#### DataXソフトウェアパッケージの取得

公式Githubで[DataX](http://datax-opensource.oss-cn-hangzhou.aliyuncs.com/datax.tar.gz)をダウンロードします。

#### CHDFS JARのインストール

CHDFS JARをダウンロードした後、`chdfs_hadoop_plugin_network-1.7.jar`をDatax解凍パス`plugin/reader/hdfsreader/libs/`および`plugin/writer/hdfswriter/libs/`にコピーします。

## 使用方法

### DataXの設定

#### datax.pyスクリプトの変更

DataX解凍ディレクトリ下のbin/datax.pyスクリプトを開き、スクリプトのCLASS_PATH変数を次のように変更します。

```plaintext
CLASS_PATH = ("%s/lib/*:%s/plugin/reader/hdfsreader/libs/*:%s/plugin/writer/hdfswriter/libs/*:.") % (DATAX_HOME, DATAX_HOME, DATAX_HOME)
```

#### JSON設定ファイルでhdfsreaderとhdfswriterを設定します

サンプルJSONは次のとおりです。

```json
{
	"job": {
		"setting": {
			"speed": {
				"byte": 10485760
			},
			"errorLimit": {
				"record": 0,
				"percentage": 0.02
			}
		},
		"content": [{
			"reader": {
				"name": "hdfsreader",
				"parameter": {
					"path": "testfile",
					"defaultFS": "ofs://f4xxxxxxxxx-hxT9.chdfs.ap-beijing.myqcloud.com/",
					"column": ["*"],
					"fileType": "text",
					"encoding": "UTF-8",
					"hadoopConfig": {
						"fs.AbstractFileSystem.ofs.impl": "com.qcloud.chdfs.fs.CHDFSDelegateFSAdapter",
						"fs.ofs.impl": "com.qcloud.chdfs.fs.CHDFSHadoopFileSystemAdapter",
						"fs.ofs.tmp.cache.dir": "/data/chdfs_tmp_cache",
						"fs.ofs.user.appid": "1250000000"
					},
					"fieldDelimiter": ","
				}
			},
			"writer": {
				"name": "hdfswriter",
				"parameter": {
					"path": "/user/hadoop/",
					"fileName": "testfile1",
					"defaultFS": "ofs://f4xxxxxxxxx-hxT9.chdfs.ap-beijing.myqcloud.com/",
					"column": [{
							"name": "col",
							"type": "string"
						},
						{
							"name": "col1",
							"type": "string"
						},
						{
							"name": "col2",
							"type": "string"
						}
					],
					"fileType": "text",
					"encoding": "UTF-8",
					"hadoopConfig": {
						"fs.AbstractFileSystem.ofs.impl": "com.qcloud.chdfs.fs.CHDFSDelegateFSAdapter",
						"fs.ofs.impl": "com.qcloud.chdfs.fs.CHDFSHadoopFileSystemAdapter",
						"fs.ofs.tmp.cache.dir": "/data/chdfs_tmp_cache",
						"fs.ofs.user.appid": "1250000000"
					},
					"fieldDelimiter": ":",
					"writeMode": "append"
				}
			}
		}]
	}
}
```

そのうち、hadoopConfigの設定はCHDFSに必要な設定であり、defaultFSはCHDFSのパスとして記入します。例えば、`ofs://f4xxxxxxxxx-hxT9.chdfs.ap-beijing.myqcloud.com/`の場合、他の設定はhdfsの設定項目と同様でかまいません。

### データマイグレーションの実行

設定ファイルをhdfs_job.jsonとしてjobディレクトリ下に保存し、以下のコマンドラインを実行します。
```bash
bin/datax.py job/hdfs_job.json
```

次のように画面の通常出力を観察します。

```plaintext
2020-03-09 16:49:59.543 [job-0] INFO  JobContainer - 
         [total cpu info] => 
                averageCpu                     | maxDeltaCpu                    | minDeltaCpu                    
                -1.00%                         | -1.00%                         | -1.00%
                        

         [total gc info] => 
                 NAME                 | totalGCCount       | maxDeltaGCCount    | minDeltaGCCount    | totalGCTime        | maxDeltaGCTime     | minDeltaGCTime     
                 PS MarkSweep         | 1                  | 1                  | 1                  | 0.024s             | 0.024s             | 0.024s             
                 PS Scavenge          | 1                  | 1                  | 1                  | 0.014s             | 0.014s             | 0.014s             

2020-03-09 16:49:59.543 [job-0] INFO  JobContainer - PerfTrace not enable!
2020-03-09 16:49:59.543 [job-0] INFO  StandAloneJobContainerCommunicator - Total 2 records, 33 bytes | Speed 3B/s, 0 records/s | Error 0 records, 0 bytes |  All Task WaitWriterTime 0.000s |  All Task WaitReaderTime 0.033s | Percentage 100.00%
2020-03-09 16:49:59.544 [job-0] INFO  JobContainer - 
タスク開始時刻                    : 2020-03-09 16:49:48
タスク終了時刻                    : 2020-03-09 16:49:59
タスク総所要時間                    :                 11s
タスク平均トラフィック                    :                3B/s
記録書き込み速度                    :              0rec/s
読み出し記録総数                    :                   2
読み取り・書き込み失敗総数                    :                   0
```


