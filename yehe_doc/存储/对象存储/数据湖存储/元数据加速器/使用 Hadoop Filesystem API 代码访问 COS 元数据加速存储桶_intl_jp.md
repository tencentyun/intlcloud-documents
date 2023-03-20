## ユースケース

Cloud Object Storage（COS）バケットでメタデータアクセラレーションを有効にしている場合は、Hadoopコマンドライン、ビッグデータコンポーネントなどの方法による操作のほか、Hadoop Filesystem APIによって、Javaコードを使用してメタデータアクセラレーションバケットにアクセスすることができます。ここではJavaコードによってメタデータアクセラレーションバケットにアクセスする方法についてご説明します。

##  前提条件

- メタデータアクセラレーションをアクティブ化済みであり、かつ環境デプロイとHDFSプロトコルの設定が正しく行われている必要があります。具体的なデプロイと設定の詳細については、[メタデータアクセラレーターを有効にしたバケットへのHDFSプロトコルを使用したアクセス](https://intl.cloud.tencent.com/document/product/436/46198)をご参照ください。
- Hadoop環境がある場合は、Hadoopコマンドラインによって正しくアクセスできるかどうかを検証することができます。

## 操作手順

1. mavenプロジェクトを新規作成し、mavenのpom.xmlに次の依存項目を追加します（実際のHadoopバージョンおよび環境に応じてhadoop-commonパッケージのバージョンを設定してください）。
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
2. 以下のHadoopのコードを参照して変更します。設定項目については[設定項目の説明](https://intl.cloud.tencent.com/document/product/1106/41965)のドキュメントを参照して変更できます。**また、その中のデータの永続化と可視性に関する説明に特にご注意ください。**
   以下に示すのは、一般的なファイルシステムの一部の操作のみです。その他のインターフェースについては、[Hadoop FileSystemインターフェースドキュメント](https://hadoop.apache.org/docs/r2.8.2/api/org/apache/hadoop/fs/FileSystem.html)をご参照ください。
```java
package com.qcloud.cos.demo;

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
				// 設定項目についてはhttps://intl.cloud.tencent.com/document/product/1106/41965をご参照ください
				// 以下の設定は、入力必須項目です

			conf.set("fs.cosn.trsf.fs.ofs.impl", "com.qcloud.chdfs.fs.CHDFSHadoopFileSystemAdapter");
				conf.set("fs.cosn.trsf.fs.AbstractFileSystem.ofs.impl", "com.qcloud.chdfs.fs.CHDFSDelegateFSAdapter");
				conf.set("fs.cosn.trsf.fs.ofs.tmp.cache.dir", "/data/chdfs_tmp_cache");
				// appidは実際のappidに置き換えます
				conf.set("fs.cosn.trsf.fs.ofs.user.appid", "1250000000");
				// regionは実際のリージョンに置き換えます
				conf.set("fs.cosn.trsf.fs.ofs.bucket.region", "ap-beijing")
				// その他のオプションの設定項目については、https://intl.cloud.tencent.com/document/product/1106/41965をご参照ください 

			String chdfsUrl = "cosn://examplebucket-12500000000/";
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
						// closeが返された場合はデータの書き込みに成功したことを表します。エラーがスローされた場合はデータ書き込みに失敗したことを表します
						out.close();
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
				// ファイルシステムの初期化
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
				Path localFilePath = new Path("file:///home/hadoop/cosn_demo/data/exampleobject.txt");
				copyFileFromLocal(fs, chdfsFilePath, localFilePath);


				// ファイルをローカルで取得する
				Path localDownFilePath = new Path("file:///home/hadoop/cosn_demo/data/exampleobject.txt");
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
> - 実行する前に、classpathが正しく設定されていることを確認してください。classpathには、Hadoop commonパッケージおよびメタデータアクセラレーションバケットが依存するjarパッケージのパスが含まれる必要があります。
> - EMR環境の場合、[メタデータアクセラレーターを有効にしたバケットへのHDFSプロトコルを使用したアクセス](https://intl.cloud.tencent.com/document/product/436/46198)の手順に従って操作した場合、Hadoop commonパッケージは通常、`/usr/local/service/hadoop/share/hadoop/common/`ディレクトリ下にあり、メタデータアクセラレーションバケットが依存するjarパッケージは通常、`/usr/local/service/hadoop/share/hadoop/common/lib/`ディレクトリ下にあります。
> 
