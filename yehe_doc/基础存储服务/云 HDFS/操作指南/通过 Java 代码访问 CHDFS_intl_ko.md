## 작업 시나리오

Cloud HDFS(CHDFS)의 JAR 패키지를 설치하면 명령어, 빅 데이터 컴포넌트 등 방식 외에도 Java 코드로 CHDFS에 액세스할 수 있습니다. 본 문서는 Java 코드로 CHDFS 에 액세스하는 방법을 소개합니다. 

## 전제 조건

- CHDFS 관련 JAR 패키지 설치. 자세한 내용은 [CHDFS 마운트](https://intl.cloud.tencent.com/document/product/1106/41965)를 참고하십시오.
- Java 프로그램을 실행할 기기가 마운트 포인트 권한 그룹에서 액세스를 허용한 VPC에 있어야 합니다. 

## 작업 절차

1. maven 프로젝트를 생성하고 maven pom.xml에 다음 종속 항목(본인의 실제 hadoop 환경에 맞춰 hadoop-common 패키지 버전 설정)을 추가합니다. 
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
2. 다음 hadoop 작업 코드를 참고하여 수정합니다. 설정 항목 및 관련 설명은 [CHDFS 마운트](https://intl.cloud.tencent.com/document/product/1106/41965)를 참고하십시오. 
일부 자주 사용되는 파일 시스템 작업 인터페이스는 다음과 같습니다. 기타 인터페이스는 [Hadoop FileSystem 인터페이스 문서](https://hadoop.apache.org/docs/r2.8.2/api/org/apache/hadoop/fs/FileSystem.html)를 참고하십시오.
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
				// CHDFS 구성 항목은 https://cloud.tencent.com/document/product/1105/36368을 참고하십시오. 
				// 다음 설정은 필수 항목입니다. 

			conf.set("fs.ofs.impl", "com.qcloud.chdfs.fs.CHDFSHadoopFileSystemAdapter");
				conf.set("fs.AbstractFileSystem.ofs.impl", "com.qcloud.chdfs.fs.CHDFSDelegateFSAdapter");
				conf.set("fs.ofs.tmp.cache.dir", "/data/chdfs_tmp_cache");
				conf.set("fs.ofs.user.appid", "1250000000");
				// 기타 옵션 설정 항목은 https://cloud.tencent.com/document/product/1105/36368을 참고하십시오.  

			String chdfsUrl = "ofs://f4maaabbb-ccdd.chdfs.ap-guangzhou.myqcloud.com/";
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


			// 기본 인증 유형은 COMPOSITE-CRC32C임.
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


			// 재귀 삭제 마크는 디렉터리 삭제에 사용됩니다. 
			// 재귀가 false 이고 dir가 비어있지 않으면 작업이 수행되지 않습니다. 
			private static void deleteFileOrDir(FileSystem fs, Path path, boolean recursive) throws IOException {
				fs.delete(path, recursive);
			}


			private static void closeFileSystem(FileSystem fs) throws IOException {
				fs.close();
			}


			public static void main(String[] args) throws IOException {
				// 파일 초기화
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
				Path localFilePath = new Path("file:///home/hadoop/ofs_demo/data/exampleobject.txt");
				copyFileFromLocal(fs, chdfsFilePath, localFilePath);


				// 파일을 로컬로 가져오기
				Path localDownFilePath = new Path("file:///home/hadoop/ofs_demo/data/exampleobject.txt");
				copyFileToLocal(fs, chdfsFilePath, localDownFilePath);


				// 이름 변경
				Path newPath = new Path("/doc/example.txt");
				renamePath(fs, chdfsFilePath, newPath);


				// 파일 삭제
				deleteFileOrDir(fs, newPath, false);


				// 디렉터리 생성
				Path dirPath = new Path("/folder");
				mkdir(fs, dirPath);


				//디렉터리에 파일 생성
				Path subFilePath = new Path("/folder/exampleobject.txt");
				createFile(fs, subFilePath);


				// 디렉터리 나열
				listDirPath(fs, dirPath);


				// 디렉터리 삭제
				deleteFileOrDir(fs, dirPath, true);


				//파일 시스템 비활성화 
				closeFileSystem(fs);
			}
}
```
3. 컴파일 및 실행
>? 
> - 실행 전에 classpath를 정확히 설정했는지 확인하십시오. classpath에는 Hadoop common 패키지 및 CHDFS 패키지 경로가 포함되어야 합니다. 
> - EMR 환경의 경우, [CHDFS 마운트](https://intl.cloud.tencent.com/document/product/1106/41965)에 따라 작업하면 Hadoop common 패키지는 일반적으로 `/usr/local/service/hadoop/share/hadoop/common/` 디렉터리에, CHDFS 패키지는`/usr/local/service/hadoop/share/hadoop/common/lib/` 디렉터리에 위치합니다.  
> 



