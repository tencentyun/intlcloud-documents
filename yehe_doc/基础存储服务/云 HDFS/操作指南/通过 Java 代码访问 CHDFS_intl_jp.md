## 操作シナリオ

Cloud HDFS(CHDFS)のJARパッケージをデプロイすると、コマンドラインやビッグデータコンポーネントなどを使用してCHDFSを操作するだけでなく、Javaコードを介してCHDFSにアクセスすることもできます。ここでは、Javaコードを介してCHDFSにアクセスする方法についてご説明します。

## 前提条件

- CHDFSに関連するJARパッケージがデプロイされていることを確認します。詳細については、[CHDFSのマウント](https://intl.cloud.tencent.com/document/product/1106/41965)をご参照ください。
- Javaプログラムを実行しているマシンが、マウントポイント権限グループによりアクセスを許可されているVPC内にあることを確認します。

## 操作手順

1. mavenプロジェクトを新規作成し、mavenのpom.xmlに次の依存項目を追加します（実際のhadoop環境に応じてhadoop-commonパッケージのバージョンを設定してください）。
```plaintext
<dependencies>
        <dependency>
            <groupId>org.apache.hadoop</groupId>
            <artifactId>hadoop-common</artifactId>
            <version>2.8.5</version>
            <scope>provided</scope>
        </dependency>
</dependencies>
```
2. 以下を参照して、Hadoopを操作するためのコードを変更します。設定項目とその説明については、[CHDFSのマウント](https://intl.cloud.tencent.com/document/product/1106/41965)をご参照ください。
以下に、一般的なファイルシステム操作インターフェースの一部を示します。その他のインターフェースについては、[Hadoop FileSystemインターフェースドキュメント](https://hadoop.apache.org/docs/r2.8.2/api/org/apache/hadoop/fs/FileSystem.html)をご参照ください。
```java
package com.qcloud.chdfs.demo;

import org.apache.commons.io.IOUtils;
import org.apache.hadoop.conf.Configuration;
import org.apache.hadoop.fs.FSDataInputStream;
import org.apache.hadoop.fs.FSDataOutputStream;
import org.apache.hadoop.fs.FileChecksum;
import org.apache.hadoop.fs.FileStatus;
import org.apache.hadoop.fs.FileSystem;
import org.apache.hadoop.fs.Path;

import java.io.IOException;
import java.net.URI;
import java.nio.ByteBuffer;

public class Demo {
			private static FileSystem initFS() throws IOException {
				Configuration conf = new Configuration();
				// CHDFSの設定項目については、https://cloud.tencent.com/document/product/1105/36368をご参照ください
				// 以下の設定は、入力必須項目です

			conf.set("fs.ofs.impl", "com.qcloud.chdfs.fs.CHDFSHadoopFileSystemAdapter");
				conf.set("fs.AbstractFileSystem.ofs.impl", "com.qcloud.chdfs.fs.CHDFSDelegateFSAdapter");
				conf.set("fs.ofs.tmp.cache.dir", "/data/chdfs_tmp_cache");
				conf.set("fs.ofs.user.appid", "1250000000");
				// その他のオプションの設定項目については、https://cloud.tencent.com/document/product/1105/36368をご参照ください 

			String chdfsUrl = "ofs://f4maaabbb-ccdd.chdfs.ap-guangzhou.myqcloud.com/";
				return FileSystem.get(URI.create(chdfsUrl), conf);
			}

		private static void mkdir(FileSystem fs, Path filePath) throws IOException {
				fs.mkdirs(filePath);
			}

		private static void createFile(FileSystem fs, Path filePath) throws IOException {
				// ファイルを作成します（存在する場合は上書きします）
				// if the parent dir does not exist, fs will create it!
				FSDataOutputStream out = fs.create(filePath, true);
				try {
						// ファイルに書き込みます
						String content = "test write file";
						out.write(content.getBytes());
				} finally {
						IOUtils.closeQuietly(out);
				}
			}

		private static void readFile(FileSystem fs, Path filePath) throws IOException {
				FSDataInputStream in = fs.open(filePath);
				try {
						byte[] buf = new byte[4096];
						int readLen = -1;
						do {
								readLen = in.read(buf);
						} while (readLen >= 0);
				} finally {
						IOUtils.closeQuietly(in);
				}
			}


			private static void queryFileOrDirStatus(FileSystem fs, Path path) throws IOException {
				FileStatus fileStatus = fs.getFileStatus(path);
				if (fileStatus.isDirectory()) {
						System.out.printf("path %s is dir\n", path);
						return;
				}

			long fileLen = fileStatus.getLen();
				long accessTime = fileStatus.getAccessTime();
				long modifyTime = fileStatus.getModificationTime();
				String owner = fileStatus.getOwner();
				String group = fileStatus.getGroup();


				System.out.printf("path %s is file, fileLen: %d, accessTime: %d, modifyTime: %d, owner: %s, group: %s\n",
						path, fileLen, accessTime, modifyTime, owner, group);
			}


			// デフォルトのチェックタイプはCOMPOSITE-CRC32Cです
			private static void getFileCheckSum(FileSystem fs, Path path) throws IOException {
				FileChecksum checksum = fs.getFileChecksum(path);
				System.out.printf("path %s, checkSumType: %s, checkSumCrcVal: %d\n",
						path, checksum.getAlgorithmName(), ByteBuffer.wrap(checksum.getBytes()).getInt());
			}


			private static void copyFileFromLocal(FileSystem fs, Path chdfsPath, Path localPath) throws  IOException {
				fs.copyFromLocalFile(localPath, chdfsPath);
			}


			private static void copyFileToLocal(FileSystem fs, Path chdfsPath, Path localPath) throws  IOException {
				fs.copyToLocalFile(chdfsPath, localPath);
			}


			private static void renamePath(FileSystem fs, Path oldPath, Path newPath) throws IOException {
				fs.rename(oldPath, newPath);
			}


			private static void listDirPath(FileSystem fs, Path dirPath) throws IOException {
				FileStatus[] dirMemberArray = fs.listStatus(dirPath);


				for (FileStatus dirMember : dirMemberArray) {
						System.out.printf("dirMember path %s, fileLen: %d\n", dirMember.getPath(), dirMember.getLen());
				}
			}


			// 再帰的削除フラグは、ディレクトリを削除するために用いられます
			// 再帰がfalseで、dirが空でない場合、操作は失敗します
			private static void deleteFileOrDir(FileSystem fs, Path path, boolean recursive) throws IOException {
				fs.delete(path, recursive);
			}


			private static void closeFileSystem(FileSystem fs) throws IOException {
				fs.close();
			}


			public static void main(String[] args) throws IOException {
				// ファイルの初期化
				FileSystem fs = initFS();


				// ファイルの作成
				Path chdfsFilePath = new Path("/folder/exampleobject.txt");
				createFile(fs, chdfsFilePath);


				// ファイルの読み取り
				readFile(fs, chdfsFilePath);


				// ファイルまたはディレクトリの照会
				queryFileOrDirStatus(fs, chdfsFilePath);


				// ファイルのチェックサムの取得
				getFileCheckSum(fs, chdfsFilePath);


				// ローカルからファイルをコピーする
				Path localFilePath = new Path("file:///home/hadoop/ofs_demo/data/exampleobject.txt");
				copyFileFromLocal(fs, chdfsFilePath, localFilePath);


				// ファイルをローカルで取得する
				Path localDownFilePath = new Path("file:///home/hadoop/ofs_demo/data/exampleobject.txt");
				copyFileToLocal(fs, chdfsFilePath, localDownFilePath);


				// リネーム
				Path newPath = new Path("/doc/example.txt");
				renamePath(fs, chdfsFilePath, newPath);


				// ファイルの削除
				deleteFileOrDir(fs, newPath, false);


				// ディレクトリの作成
				Path dirPath = new Path("/folder");
				mkdir(fs, dirPath);


				// ディレクトリにファイルを作成する
				Path subFilePath = new Path("/folder/exampleobject.txt");
				createFile(fs, subFilePath);


				// ディレクトリのリストアップ
				listDirPath(fs, dirPath);


				// ディレクトリの削除
				deleteFileOrDir(fs, dirPath, true);


				// ファイルシステムを閉じる
				closeFileSystem(fs);
			}
}
```
3. コンパイルと実行。
>? 
> - 実行する前に、classpathが正しく設定されていることを確認してください。classpathには、Hadoop commonパッケージとCHDFSパッケージのパスが含まれる必要があります。
> - EMR環境の場合、[CHDFSのマウント](https://intl.cloud.tencent.com/document/product/1106/41965)を手順に従って操作した場合、Hadoop commonパッケージは通常、`/usr/local/service/hadoop/share/hadoop/common/`ディレクトリ下にあり、CHDFSパッケージは通常、`/usr/local/service/hadoop/share/hadoop/common/lib/`ディレクトリ下にあります。
> 



