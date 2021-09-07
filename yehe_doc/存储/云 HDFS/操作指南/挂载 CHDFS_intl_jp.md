
CHDFSとマウントポイントを作成すると、マウントポイントを介してCHDFSをマウントできるようになります。ここでは、CHDFSをマウントする方法について詳しくご説明します。

## 前提条件
- マウントされたマシンまたはコンテナにJava1.8がインストールされていることを確認します。
- マウントされたマシンまたはコンテナのVPCが、マウントポイントの指定されたVPCと同じであることを確認します。
- マウントされたマシンまたはコンテナのVPC IPが、マウントポイントの指定された権限グループのうち1つの権限ルールの権限を付与されたアドレスと一致することを確認します。

## 操作手順
1.  [CHDFS-Hadoop](https://github.com/tencentyun/chdfs-hadoop-plugin)でJARパッケージをダウンロードします。
2.	JARパッケージを対応するディレクトリ下に配置します。EMRクラスターの場合、すべてのノードの`/usr/local/service/hadoop/share/hadoop/common/lib/`ディレクトリ下に同期できます。
3.	core-site.xmlファイルを編集し、次の基本設定を追加します。
```
<!--chdfsの実装クラス-->
<property>
		 <name>fs.AbstractFileSystem.ofs.impl</name>
		 <value>com.qcloud.chdfs.fs.CHDFSDelegateFSAdapter</value>
</property>
<property>
		 <name>fs.ofs.impl</name>
		 <value>com.qcloud.chdfs.fs.CHDFSHadoopFileSystemAdapter</value>
</property>
<!--ローカルcacheの一時ディレクトリ。データの読み取りと書き込みの場合、メモリcacheが不足すると、ローカルディスクに書き込まれます。このパスが存在しない場合は、自動的に作成されます-->
<property>
		 <name>fs.ofs.tmp.cache.dir</name>
		 <value>/data/chdfs_tmp_cache</value>
</property>
<!--appId-->      
<property>
		 <name>fs.ofs.user.appid</name>
		 <value>1250000000</value>
</property>
```
4.	core-site.xmlをすべてのhadoopノードに同期します。
>?EMRクラスターの場合、EMRコンソールのコンポーネント管理で上記の手順3と4において、HDFSの設定を変更することができます。
5.	hadoop fsコマンドラインツールを使用して、`hadoop fs –ls ofs://${mountpoint}/`コマンドを実行します。ここで、mountpointはマウントアドレスです。ファイルリストが正常にリストアップされている場合は、CHDFSが正常にマウントされたことを意味します。
6.	ユーザーは、hadoopの他の設定項目またはmrタスクを使用してCHDFSでデータタスクを実行することもできます。mrタスクの場合、`-Dfs.defaultFS=ofs://${mountpoint}/`によって、このタスクのデフォルトの入力・出力FSをCHDFSに変更することができます。

## その他の設定項目

|        設定項目      |                             説明                             |  デフォルト値   | 入力必須かどうか |
| :------------------------------| :----------------------------------------------------| :-------| :------ |
|       fs.ofs.tmp.cache.dir        |   一時データの保存    |    なし    |    はい    |
|       fs.ofs.map.block.size       | chdfsファイルシステムのblockサイズ。単位はバイト、デフォルトは128MBです（mapのセグメンテーションにのみ影響を与え、chdfs最下層のストレージロックサイズとは関係ありません） | 134217728 |    いいえ    |
| fs.ofs.data.transfer.thread.count |               chdfsデータ転送時の並列スレッドの数                |    32     |    いいえ    | 
| fs.ofs.block.max.memory.cache.mb  | chdfsプラグインによって使用されるメモリbufferのサイズ。単位はMBです。（読み取りと書き込みのアクセラレーション効果あり） |    16     |    いいえ    |
|  fs.ofs.block.max.file.cache.mb   |  chdfsプラグインによって使用されるディスクbufferrのサイズ。単位はMBです。（書き込みにアクセラレーション効果あり）  |    256    |    いいえ    |
|   fs.ofs.prev.read.block.count    | 読み取り時の先行読み取りchdfs block数（chdfsの最下層blockのサイズは通常4MB）|     4     |    いいえ    |
|      fs.ofs.plugin.info.log       |          プラグインのデバッグログを印刷するかどうか。ログはinfoレベルごとに印刷されます。 オプション値はtrue、falseです |   false   |    いいえ    |

