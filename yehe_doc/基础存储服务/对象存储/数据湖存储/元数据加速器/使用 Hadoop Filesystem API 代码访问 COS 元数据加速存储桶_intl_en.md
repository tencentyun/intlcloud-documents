## Overview

If metadata acceleration is enabled for a COS bucket, you can use Java code to access the bucket through Hadoop FileSystem API in addition to using the Hadoop command line and big data components. This document describes how to do so.

## Prerequisites

- Make sure that metadata acceleration has been enabled, and the environment deployment and HDFS protocol configuration have been performed correctly. For more information, see [Using HDFS to Access a Bucket with Metadata Acceleration Enabled](https://intl.cloud.tencent.com/document/product/436/46198).
- If there is a Hadoop environment, you can verify whether the Hadoop command line can be accessed correctly.

## Directions

1. Create a Maven project and add the following dependencies to `pom.xml` in Maven (set the versions of the `hadoop-common`, `hadoop-cos`, and `cos_api-bundle` packages based on your actual Hadoop version and environment).
```plaintext
<dependencies>
        <dependency>
            <groupId>org.apache.hadoop</groupId>
            <artifactId>hadoop-common</artifactId>
            <version>2.8.5</version>
            <scope>provided</scope>
        </dependency>
         <dependency>
            <groupId>com.qcloud.cos</groupId>
            <artifactId>hadoop-cos</artifactId>
            <version>xxx</version>
        </dependency>
        <dependency>
            <groupId>com.qcloud</groupId>
            <artifactId>cos_api-bundle</artifactId>
            <version>xxx</version>
        </dependency>
        
</dependencies>
```
2. Refer to the following Hadoop code to make changes. The configuration items can be modified as instructed in [Mounting CHDFS Instance](https://intl.cloud.tencent.com/document/product/1106/41965). **Pay special attention to the instructions related to data persistence and visibility.**
   Only certain common file system operations are listed below. For other APIs, see [Hadoop FileSystem APIs](https://hadoop.apache.org/docs/r2.8.2/api/org/apache/hadoop/fs/FileSystem.html).

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
               // For more information on the configuration items, visit https://cloud.tencent.com/document/product/436/6884#.E4.B8.8B.E8.BD.BD.E4.B8.8E.E5.AE.89.E8.A3.85.
               // The following configuration items are required

               conf.set("fs.cosn.impl", "org.apache.hadoop.fs.CosFileSystem");
               conf.set("fs.AbstractFileSystem.cosn.impl", "org.apache.hadoop.fs.CosN");
               conf.set("fs.cosn.userinfo.secretId", "xxxxxx");
               conf.set("fs.cosn.userinfo.secretKey", "xxxxxx");
               conf.set("fs.cosn.bucket.region", "xxxxxx");
               conf.set("fs.cosn.tmp.dir", "/data/chdfs_tmp_cache");

               // For more information on the configuration items, visit https://cloud.tencent.com/document/product/436/71550.
               // Required configuration items for the POSIX access mode (recommended)
               conf.set("fs.cosn.trsf.fs.AbstractFileSystem.ofs.impl", "com.qcloud.chdfs.fs.CHDFSDelegateFSAdapter");
               conf.set("fs.cosn.trsf.fs.ofs.impl", "com.qcloud.chdfs.fs.CHDFSHadoopFileSystemAdapter");
               conf.set("fs.cosn.trsf.fs.ofs.tmp.cache.dir", "com.qcloud.chdfs.fs.CHDFSHadoopFileSystemAdapter");
               conf.set("fs.cosn.trsf.fs.ofs.impl", "com.qcloud.chdfs.fs.CHDFSHadoopFileSystemAdapter");
               conf.set("fs.cosn.trsf.fs.ofs.tmp.cache.dir", "/data/chdfs_tmp_cache");
               
               // Replace `appid` with your actual `appid`
               conf.set("fs.cosn.trsf.fs.ofs.user.appid", "1250000000");
               // Replace `region` with your actual region
               conf.set("fs.cosn.trsf.fs.ofs.bucket.region", "ap-beijing");
               // For more information on the optional configuration items, visit https://cloud.tencent.com/document/product/436/6884#.E4.B8.8B.E8.BD.BD.E4.B8.8E.E5.AE.89.E8.A3.85.
               // Whether to enable CRC-64 checksum. It is disabled by default, meaning that you can't run the `hadoop fs -checksum` command to obtain the CRC-64 checksum of a file.
               conf.set("fs.cosn.crc64.checksum.enabled", "true");
               String cosHadoopFSUrl = "cosn://examplebucket-12500000000/";
               return FileSystem.get(URI.create(cosHadoopFSUrl), conf);
			}

		private static void mkdir(FileSystem fs, Path filePath) throws IOException {
				fs.mkdirs(filePath);
			}

		private static void createFile(FileSystem fs, Path filePath) throws IOException {
				// Create a file (if it already exists, it will be overwritten)
				// if the parent dir does not exist, fs will create it!
				FSDataOutputStream out = fs.create(filePath, true);
				try {
						// Write a file
						String content = "test write file";
						out.write(content.getBytes());
				} finally {
						// If `close` is returned successfully, the data write has succeeded. If an exception is thrown, the data write has failed.
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


			// The default verification type is `COMPOSITE-CRC32C`
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


			// The recursive deletion flag is used to delete directories
			// If recursion is `false` and `dir` is not empty, the operation will fail
			private static void deleteFileOrDir(FileSystem fs, Path path, boolean recursive) throws IOException {
				fs.delete(path, recursive);
			}


			private static void closeFileSystem(FileSystem fs) throws IOException {
				fs.close();
			}


			public static void main(String[] args) throws IOException {
				// Initialize the file system
				FileSystem fs = initFS();


				// Create a file
				Path chdfsFilePath = new Path("/folder/exampleobject.txt");
				createFile(fs, chdfsFilePath);


				// Read a file
				readFile(fs, chdfsFilePath);


				// Query a file or directory
				queryFileOrDirStatus(fs, chdfsFilePath);


				// Get a file checksum
				getFileCheckSum(fs, chdfsFilePath);


				// Copy a file from the local system
				Path localFilePath = new Path("file:///home/hadoop/cosn_demo/data/exampleobject.txt");
				copyFileFromLocal(fs, chdfsFilePath, localFilePath);


				// Download a file to the local file system
				Path localDownFilePath = new Path("file:///home/hadoop/cosn_demo/data/exampleobject.txt");
				copyFileToLocal(fs, chdfsFilePath, localDownFilePath);


				// Rename
				Path newPath = new Path("/doc/example.txt");
				renamePath(fs, chdfsFilePath, newPath);


				// Delete a file
				deleteFileOrDir(fs, newPath, false);


				// Create a directory
				Path dirPath = new Path("/folder");
				mkdir(fs, dirPath);


				// Create a file in a directory
				Path subFilePath = new Path("/folder/exampleobject.txt");
				createFile(fs, subFilePath);


				// List directories
				listDirPath(fs, dirPath);


				// Delete a directory
				deleteFileOrDir(fs, dirPath, true);


				// Close a file system
				closeFileSystem(fs);
			}
}
```

3. Compile and run the project.
>?
> - Before running the code, be sure to correctly set `classpath`, which must contain the paths of the Hadoop `common` package and the JAR package depended on by the metadata acceleration bucket.
> - For an EMR environment, if you follow the steps as detailed in [Using HDFS to Access a Bucket with Metadata Acceleration Enabled](https://intl.cloud.tencent.com/document/product/436/46198), the Hadoop `common` package is generally in the `/usr/local/service/hadoop/share/hadoop/common/` directory, and the JAR package depended on by the metadata acceleration bucket is generally in the `/usr/local/service/hadoop/share/hadoop/common/lib/` directory.
> 
