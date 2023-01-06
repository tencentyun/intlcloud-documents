### マイグレーションツールが途中で異常終了した場合はどうすればよいですか。

ツールはアップロード時の中断からの再開をサポートしています。大容量ファイルについては、途中で終了した場合やサービスの障害があった場合、ツールを再実行して、アップロードが完了していないファイルのアップロードを再開することができます。

### 移行に成功したファイルについて、ユーザーがコンソールまたはその他の方法でCOS上のファイルを削除した場合、マイグレーションツールはこれらのファイルを再アップロードしますか。

しません。その理由は、移行に成功したファイルはすべてdbに記録され、マイグレーションツールの実行前にdbディレクトリをスキャンして、記録があるファイルについては再アップロードを行わないためです。具体的な理由については、[移行のメカニズムとフロー](https://intl.cloud.tencent.com/document/product/436/15392)をご参照ください。

### 移行に失敗し、ログに403 Access Denyと表示されましたが、どのように対処すればよいですか。

キー情報、Bucket情報、Region情報が正しいかどうか、なおかつ操作権限があるかどうかを確認してください。 サブアカウントの場合は、親アカウントから対応する権限の承認を受けてください。ローカルからの移行および他のクラウドストレージからの移行の場合は、Bucketに対するデータ書き込みおよび読み取り権限が必要です。Bucket copyの場合は、ソースBucketに対するデータ読み取り権限も必要です。

### 他のクラウドストレージからCOSへの移行に失敗し、Read timed outと表示されましたが、どのように対処すればよいですか。

一般的に、このような失敗はネットワーク帯域幅の不足により、他のクラウドストレージからのデータダウンロードがタイムアウトとなることによるものです。例えば、AWSの海外データをCOSに移行する場合、データをローカルにダウンロードする際に、帯域幅能力の不足により高遅延となり、read time outが発生する場合があります。このため、対処方法としてはマシンのネットワーク帯域幅能力を増強することになります。移行の前にwgetを使用してダウンロード速度のテストを行うことをお勧めします。

### 移行に失敗し、ログに503 Slow Downと表示されましたが、どのように対処すればよいですか。

これは頻度制御がトリガーされたことによるものです。COSは現時点で1つのアカウントに対し每秒30000QPSの操作制限を行っています。小・中容量ファイルの同時実行数を低く設定しなおすことをお勧めします。その上でツールを再実行すると、失敗したものを再実行することができます。

### 移行に失敗し、ログに404 NoSuchBucketと表示されましたが、どのように対処すればよいですか。

キー情報、Bucket情報、Region情報が正しいかどうか確認してください。

### 動作異常が発生し、次のようなメッセージが表示されましたが、どうすればよいですか。

![img](https://main.qcloudimg.com/raw/9fdac231af66c991c13fe0440e8d7366.png)
この問題は、ツールがrocksdbを使用しているために発生したものです。64ビットのJDKを使用する場合は、JDKのバージョンがX64のJDKかどうかをチェックしてください。

### Windows環境下でrocksdbのjniライブラリが見つからないと表示されましたが、 どのように対処すればよいですか。
Windows環境下では、ツールはMicrosoft Visual Studio 2015環境下でコンパイルする必要があります。上記のエラーが発生した場合は、[Visual C++ Redistributable for Visual Studio 2015](https://www.microsoft.com/zh-CN/download/details.aspx?id=48145)をインストールする必要があります。

### ログレベルを変更するにはどうすればよいですか。
ファイルsrc/main/resources/log4j.propertiesを変更し、log4j.rootLoggerの値に、DEBUG、INFO、ERRORなどの対応するログレベルのものをコピーします。

### Linux環境下で、/tmp/librocksdbjnixxx.so: ELF file OS ABI invalidというエラーが発生しましたが、どのように対処すればよいですか。
Linux環境下では、ツールはIFUNCのサポートが必要です。実行環境のbinutilsのバージョンをチェックし、2.20以降のバージョンであることを確認してください。

### タスクの実行が完了していない状態で、error.logにjavaの異常"java.nio.file.FileSystemLoopException"が存在する場合はどのように対処すればよいですか。
error.logの異常情報は次のようなものです。

```
2022-XX-XX XX:XX:XX [ERROR] [main:xxx] [com.qcloud.cos_migrate_tool.task.MigrateLocalTaskExecutor:] [MigrateLocalTaskExecutor.java:183]
walk file tree error
java.nio.file.FileSystemLoopException: /dataseal/xx1/file1
at java.nio.file.FileTreeWalker.visit(FileTreeWalker.java:294)
at java.nio.file.FileTreeWalker.next(FileTreeWalker.java:372)
at java.nio.file.Files.walkFileTree(Files.java:2706)
at com.qcloud.cos_migrate_tool.task.MigrateLocalTaskExecutor.buildTask(MigrateLocalTaskExecutor.java:176)
at com.qcloud.cos_migrate_tool.task.TaskExecutor.run(TaskExecutor.java:244)
at com.qcloud.cos_migrate_tool.app.App.main(App.java:135)
```
移行対象のファイル"/dataseal/xx1/file1"が1つのソフトリンクであり、その親ディレクトリ内のリソースを指していることが原因の可能性があります。次のコマンドで確認できます

```
[root@TENCENT64 /dataseal/cos_migrate_tool_v5-master/log]# ll /dataseal/xx1/file1
lrwxrwxrwx 1 xx xx xx xx   x xxxx /dataseal/xx1/file1 -> ../xx1/
```

上記のように、ソフトリンクファイル"/dataseal/xx1/file1"が親ディレクトリ内の"/dataseal/xx1/"を指している場合、トラバーサルが無限ループに陥り、移行タスクが自動的に中止します。
この種のファイルを事前に削除しておくことをお勧めします（注意：設定項目「excludes」でこの種のファイルを除外する方法は無効です）。

そのほかに問題がありましたら、マイグレーションツールの再実行を試してください。それでも失敗する場合は、設定情報（キー情報は隠してください）とログディレクトリをパッケージングし、[お問い合わせ](https://intl.cloud.tencent.com/contact-sales)ください。
