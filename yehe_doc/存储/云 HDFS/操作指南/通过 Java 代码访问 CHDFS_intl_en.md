## Overview

This document describes how to access CHDFS through Java code. After deploying the JAR package of CHDFS, in addition to manipulating CHDFS by using command lines, big data components, and other methods, you can also access CHDFS through Java code.

## Prerequisites

- The relevant JAR package of CHDFS has been deployed. For more information on the deployment, please see [Mounting CHDFS Instance](https://intl.cloud.tencent.com/document/product/1106/41965).
- The server that runs the Java program is in a VPC allowed to be accessed by the permission group of the mount point.

## Directions

1. Create a Maven project and add the following dependencies to `pom.xml` in Maven (please set the version of the `hadoop-common` package based on your actual Hadoop environment).
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
2. Run the Hadoop code for modification as detailed below. For the configuration items and their descriptions, please see [Mounting CHDFS Instance](https://intl.cloud.tencent.com/document/product/1106/41965).
Only certain common file system operation APIs are listed below. For other APIs, please see [Hadoop FileSystem APIs](https://hadoop.apache.org/docs/r2.8.2/api/org/apache/hadoop/fs/FileSystem.html).
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
				// For the CHDFS configuration items, please visit https://cloud.tencent.com/document/product/1105/36368
				// The following configuration items are required

			conf.set("fs.ofs.impl", "com.qcloud.chdfs.fs.CHDFSHadoopFileSystemAdapter");
				conf.set("fs.AbstractFileSystem.ofs.impl", "com.qcloud.chdfs.fs.CHDFSDelegateFSAdapter");
				conf.set("fs.ofs.tmp.cache.dir", "/data/chdfs_tmp_cache");
				conf.set("fs.ofs.user.appid", "1250000000");
				// For other optional configuration items, please visit https://cloud.tencent.com/document/product/1105/36368 

			String chdfsUrl = "ofs://f4maaabbb-ccdd.chdfs.ap-guangzhou.myqcloud.com/";
				return FileSystem.get(URI.create(chdfsUrl), conf);
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
				// Initialize a file
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
				Path localFilePath = new Path("file:///home/hadoop/ofs_demo/data/exampleobject.txt");
				copyFileFromLocal(fs, chdfsFilePath, localFilePath);


				// Get a file to the local system
				Path localDownFilePath = new Path("file:///home/hadoop/ofs_demo/data/exampleobject.txt");
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


				// Deletes a directory
				deleteFileOrDir(fs, dirPath, true);


				// Close a file system
				closeFileSystem(fs);
			}
}
```
3. Compile and run.
>? 
> - Before running the code, please be sure to correctly set `classpath`, which must contain the paths of the Hadoop `common` package and the CHDFS package.
> - For an EMR environment, if you follow the steps as detailed in [Mounting CHDFS Instance](https://intl.cloud.tencent.com/document/product/1106/41965), the Hadoop `common` package is generally in the `/usr/local/service/hadoop/share/hadoop/common/` directory, and the CHDFS package is generally in the `/usr/local/service/hadoop/share/hadoop/common/lib/` directory.
> 



