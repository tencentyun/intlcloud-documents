## 작업 시나리오

COS(Cloud Object Storage) 버킷에 대해 메타데이터 가속화가 활성화된 경우 Java 코드를 사용하여 Hadoop 명령 라인 및 빅 데이터 컴포넌트를 사용하는 것 외에도 Hadoop Filesystem API를 통해 버킷에 액세스할 수 있습니다. 본문에서는 그 방법을 설명합니다.

## 전제 조건

- 메타데이터 가속이 활성화되었고 환경 배포 및 HDFS 프로토콜 구성이 올바르게 수행되었는지 확인하십시오. 자세한 내용은 [HDFS 프로토콜을 사용하여 메타데이터 가속이 활성화된 버킷에 액세스](https://intl.cloud.tencent.com/document/product/436/46198)를 참고하십시오.
- Hadoop 환경이 있는 경우 Hadoop 명령 라인에 올바르게 액세스할 수 있는지 확인할 수 있습니다.

## 작업 단계

1. maven 프로젝트를 생성하고 maven의 pom.xml에 다음 종속 항목(실제 Hadoop 버전 및 환경에 따라 hadoop-common 패키지 버전 설정)을 추가합니다. 
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
2. 다음 hadoop 코드를 참고하여 변경합니다. 구성 항목은 [CHDFS 마운트](https://intl.cloud.tencent.com/document/product/1106/41965)에 설명된 대로 수정할 수 있습니다. **데이터 지속성 및 가시성 관련 지침에 특히 주의하십시오.**
   일부 자주 사용되는 파일 시스템 작업 인터페이스는 다음과 같습니다. 다른 API는 [Hadoop FileSystem API](https://hadoop.apache.org/docs/r2.8.2/api/org/apache/hadoop/fs/FileSystem.html)를 참고하십시오.
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
				// 구성 항목 참고: https://intl.cloud.tencent.com/document/product/1106/41965
				// 다음 구성은 필수 항목입니다

			conf.set("fs.cosn.trsf.fs.ofs.impl", "com.qcloud.chdfs.fs.CHDFSHadoopFileSystemAdapter");
				conf.set("fs.cosn.trsf.fs.AbstractFileSystem.ofs.impl", "com.qcloud.chdfs.fs.CHDFSDelegateFSAdapter");
				conf.set("fs.cosn.trsf.fs.ofs.tmp.cache.dir", "/data/chdfs_tmp_cache");
				// appid를 실제 appid로 교체
				conf.set("fs.cosn.trsf.fs.ofs.user.appid", "1250000000");
				// region을 실제 리전으로 교체
				conf.set("fs.cosn.trsf.fs.ofs.bucket.region", "ap-beijing")
				// 기타 옵션 설정 항목 참고: https://intl.cloud.tencent.com/document/product/1106/41965 

			String chdfsUrl = "cosn://examplebucket-12500000000/";
				return FileSystem.get(URI.create(chdfsUrl), conf);
			}

		private static void mkdir(FileSystem fs, Path filePath) throws IOException {
				fs.mkdirs(filePath);
			}

		private static void createFile(FileSystem fs, Path filePath) throws IOException {
				// 파일 생성 (이미 있는 경우 덮어쓰기）
				// if the parent dir does not exist, fs will create it!
				FSDataOutputStream out = fs.create(filePath, true);
				try {
						// 파일 입력
						String content = "test write file";
						out.write(content.getBytes());
				} finally {
						// close가 성공적으로 반환되면 데이터 쓰기가 성공한 것이며, 예외가 발생하면 데이터 쓰기가 실패한 것입니다
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


			// 기본 인증 유형은 COMPOSITE-CRC32C
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


			// 재귀 삭제 마크는 디렉터리 삭제에 사용됩니다
			// 재귀가 false 이고 dir이 비어있지 않으면 작업이 수행되지 않습니다
			private static void deleteFileOrDir(FileSystem fs, Path path, boolean recursive) throws IOException {
				fs.delete(path, recursive);
			}


			private static void closeFileSystem(FileSystem fs) throws IOException {
				fs.close();
			}


			public static void main(String[] args) throws IOException {
				// 파일 시스템 초기화
				FileSystem fs = initFS();


				// 파일 생성 
				Path chdfsFilePath = new Path("/folder/exampleobject.txt");
				createFile(fs, chdfsFilePath);


				// 파일 불러오기
				readFile(fs, chdfsFilePath);


				// 파일 또는 디렉터리 조회
				queryFileOrDirStatus(fs, chdfsFilePath);


				// 파일 검사합 가져오기
				getFileCheckSum(fs, chdfsFilePath);


				// 로컬에서 파일 복사 
				Path localFilePath = new Path("file:///home/hadoop/cosn_demo/data/exampleobject.txt");
				copyFileFromLocal(fs, chdfsFilePath, localFilePath);


				// 파일을 로컬로 가져오기
				Path localDownFilePath = new Path("file:///home/hadoop/cosn_demo/data/exampleobject.txt");
				copyFileToLocal(fs, chdfsFilePath, localDownFilePath);


				// 이름 변경
				Path newPath = new Path("/doc/example.txt");
				renamePath(fs, chdfsFilePath, newPath);


				// 파일 삭제
				deleteFileOrDir(fs, newPath, false);


				// 디렉터리 생성
				Path dirPath = new Path("/folder");
				mkdir(fs, dirPath);


				// 디렉터리에 파일 생성
				Path subFilePath = new Path("/folder/exampleobject.txt");
				createFile(fs, subFilePath);


				// 디렉터리 나열
				listDirPath(fs, dirPath);


				// 디렉터리 삭제
				deleteFileOrDir(fs, dirPath, true);


				// 파일 시스템 비활성화 
				closeFileSystem(fs);
			}
}
```
3. 프로젝트를 컴파일하고 실행합니다.
>?
> - 코드를 실행하기 전에 메타데이터 가속 버킷에 종속된 Hadoop common 패키지 및 Jar 패키지의 경로를 포함해야 하는 classpath를 올바르게 설정해야 합니다.
> - EMR 환경의 경우 [HDFS 프로토콜을 사용하여 메타데이터 가속이 활성화된 버킷에 액세스](https://intl.cloud.tencent.com/document/product/436/46198)에 설명된 단계를 따르면 Hadoop common 패키지는 일반적으로 `/usr/local/service/hadoop/share/hadoop/common/` 디렉터리에 있으며, 메타데이터 가속 버킷에 의존하는 Jar 패키지는 일반적으로 `/usr/local/service/hadoop/share/hadoop/common/lib/` 디렉터리에 있습니다.
> 
