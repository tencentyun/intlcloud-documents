| Operation |	Syntax	| Description |
|--|--|--|
|cat	| cat "path"	| Print the content of a file in Alluxio to the console.
|checkConsistency|	checkConsistency "path"	| Check the metadata consistency between Alluxio and the under storage.
|checksum |	checksum "path"	| Calculate the md5 checksum for a file.
|chgrp	|chgrp "group" "path"	| Change the group of a file or directory in Alluxio.
|chmod	| chmod "permission" "path" |	Change the permission of the directory or file in Alluxio.
|chown	| chown "owner" "path"	| Change the owner of a file or directory in Alluxio.
|copyFromLocal	| copyFromLocal "source path""remote path" | Copy the file specified by "source path" to the path in Alluxio specified by "remote path". This command will fail if "remote path" already exists.
|copyToLocal|	copyToLocal "remote path" "local path" |	Copy the file specified by "remote path" in Alluxio to a local destination.
|count |	count "path"	| Display the number of folders and files matching the specified prefix in "path".
|cp	| cp "src" "dst"|	Copy a file or directory within the Alluxio file system.
|du	| du "path" |	Display the size of the file or directory specified by the input path.
|fileInfo|	fileInfo "path" |	Print the information of the blocks of a specified file.
|free	| free "path"|	Free a file or all files under a directory from Alluxio. If the file/directory is also in under storage, it will still be available there.
|getCapacityBytes	|getCapacityBytes	| Get the capacity of the Alluxio file system.
|getUsedBytes	|getUsedBytes|	Get the number of bytes used in the Alluxio file system.
|help	|help "cmd"	| Print help information for the given command. If no command is given, print help information for all supported commands.
|leader	| leader |	Print the current Alluxio leader master host name.
|load	|load "path"	| Load the data of a file or a directory from under storage into Alluxio.
|loadMetadata	|loadMetadata "path"	| Load the metadata of a file or directory from under storage into Alluxio.
|location	|location "path" |	Display a list of hosts that have the specified file data.
|ls	| ls "path" |	List all the files and directories directly under the given path with information such as size.
|masterInfo	| masterInfo	| Print information regarding Alluxio master fault tolerance such as leader address, list of master addresses, and configured Zookeeper address.
|mkdir	| mkdir "path1" ... "pathn" |	Create one or more directories under the given paths, along with any necessary parent directories. Multiple paths are separated by spaces or tabs. This command will fail if any of the given paths already exist.
|mount	| mount "path" "uri"	| Mount the underlying file system path "uri" into the Alluxio namespace as "path". The "path" is assumed not to exist and is created by the operation. No data or metadata is loaded from under storage into Alluxio. After a path is mounted, operations on objects under the mounted path are mirror to the mounted under storage.
|mv	| mv "source" "destination"	| Move a file or directory specified by "source" to a new location "destination". This command will fail if "destination" already exists.
|persist |	persist "path1" ... "pathn" |	Persist files or directories currently stored only in Alluxio to the underlying file system.
|pin	| pin "path"	| Pin the given file to avoid evicting it from memory. If the given path is a directory, it recursively pins all the files contained and any new files created within this directory.
|report	| report "path"	| Report to the master that a file is lost.
|rm	| rm "path"	| Remove a file. This command will fail if the given path is a directory rather than a file.
|setTtl	| setTtl "path" "time"	| Set the TTL (time to live) in milliseconds for a file.
|stat	| stat "path"	| Display information of the specified file or directory.
|tail	| tail "path"	| Print the last 1 KB of the specified file to the console.
|test	| test "path"	| Test a property of a path, returning 0 if the property is true, or 1 otherwise.
|touch	| touch "path"	| Create a 0-byte file at the specified location.
|unmount |	unmount "path"	| Unmount the underlying file system path mounted in the Alluxio namespace as "path". Alluxio objects under "path" are removed from Alluxio, but they still exist in the previously mounted under storage.
|unpin	| unpin "path"	| Unpin the given file to allow Alluxio to evict this file again. If the given path is a directory, it recursively unpins all files contained and any new files created within this directory.
|unsetTtl	|unsetTtl "path"	| Remove the TTL (time to live) setting from a file.

## cat

**Background**
The cat command prints the entire contents of a file in Alluxio to the console. This can be useful for verifying the file. Use the copyToLocal command to copy the file to your local file system.

**Operation example** 
When trying out a new computation job, cat can be used as a quick way to check the output:
```
$ ./bin/alluxio fs cat /output/part-00000
```

## checkConsistency
**Background**
The checkConsistency command compares Alluxio and under storage metadata for a given path. If the path is a directory, the entire subtree will be compared. The command returns a message listing each inconsistent file or directory. The system administrator should reconcile the differences of these files at their discretion. To avoid metadata inconsistencies between Alluxio and under storages, design your systems to modify files and directories through the Alluxio and avoid directly modifying state in the underlying storage.

If the -r option is used, the checkConsistency command will repair all inconsistent files and directories under the given path. If an inconsistent file or directory exists only in under storage, its metadata will be added to Alluxio. If an inconsistent file exists in Alluxio and its data is fully present in Alluxio, its metadata will be loaded to Alluxio again.

>!This command requires a read lock on the subtree being checked, meaning writes and updates to files or directories in the subtree cannot be completed until this command completes.

**Operation example**
checkConsistency can be used to periodically validate the integrity of the namespace.

List each inconsistent file or directory:

```
$ ./bin/alluxio fs checkConsistency /
```

Repair the inconsistent files or directories:

```
$ ./bin/alluxio fs checkConsistency -r /
```

## checksum

**Background**
The checksum command outputs the md5 value of a file in Alluxio.

**Operation example**
checksum can be used to verify the content of a file stored in Alluxio matches the content stored in an under file system or local file system.

```
$ ./bin/alluxio fs checksum /LICENSE
```

## chgrp

**Background**
The chgrp command changes the group of the file or directory in Alluxio. Alluxio supports file authorization with Posix file permission. Group is an authorizable entity in Posix file permission model. The file owner or super-user can execute this command to change the group of the file or directory.

Adding -R option also changes the group of child file and child directory recursively.

**Operation example**
chgrp can be used as a quick way to change the group of file:

```
$ ./bin/alluxio fs chgrp alluxio-group-new /input/file1
```

## chmod

**Background**
The chmod command changes the permission of file or directory in Alluxio. Currently, octal mode is supported: the numerical format accepts three octal digits which refer to permissions for the file owner, the group and other users. Here is the number-permission mapping table:

|Number	|Permission	| rwx |
|--|--|--|
|7	|read, write and execute	| rwx
|6	|read and write	| rw-
|5	|read and execute	|r-x
|4	|read only	|r--
|3	|write and execute	|-wx
|2	|write only	|-w-
|1	|execute only	|--x
|0	|none	|---

Adding -R option also changes the permission of child file and child directory recursively.

**Operation example**
chmod can be used as a quick way to change the permission of file:

```
$ ./bin/alluxio fs chmod 755 /input/file1
```

## chown

**Background**
The chown command changes the owner of the file or directory in Alluxio. For obvious security reasons, the ownership of a file can only be altered by a super-user.

Adding -R option also changes the owner of child file and child directory recursively.

**Sample**
chown can be used as a quick way to change the owner of file:

```
$ ./bin/alluxio fs chown alluxio-user /input/file1
```

## copyFromLocal

**Background**
The copyFromLocal command copies the contents of a file in your local file system into Alluxio. If the node you run the command from has an Alluxio worker, the data will be available on that worker. Otherwise, the data will be copied to a random remote node running an Alluxio worker. If a directory is specified, the directory and all its contents will be copied recursively.

**Operation example**
copyFromLocal can be used as a quick way to inject data into the system for processing:

```
$ ./bin/alluxio fs copyFromLocal /local/data /input
```

## copyToLocal

**Background**

The copyToLocal command copies the contents of a file in Alluxio to a file in your local file system. If a directory is specified, the directory and all its contents will be downloaded recursively.

**Operation example**
copyToLocal can be used as a quick way to download output data for additional investigation or debugging.

```
$ ./bin/alluxio fs copyToLocal /output/part-00000 part-00000
```

## count

**Background**
The count command outputs the number of files and folders matching a prefix as well as the total size of the files. count works recursively and accounts for any nested directories and files. count is best utilized when you have some predefined naming conventions for their files.

**Operation example**
If data files are stored by their date, count can be used to determine the number of data files and their total size for any date, month, or year.

```
$ ./bin/alluxio fs count /data/2014
```

## cp

**Background**
The cp command copies a file or directory in the Alluxio file system or between local file system and Alluxio file system.

Scheme file indicates the local file system and scheme alluxio or no scheme indicates the Alluxio file system.

If the -R option is used and the source designates a directory, cp copies the entire subtree at source to the destination.

**Operation example**

cp can be used to copy files between Under file systems.

```
$ ./bin/alluxio fs cp /hdfs/file1 /s3/
```

## du

**Background**
The du command outputs the size of a file. If a directory is specified, it will output the aggregate size of all files in the directory and its children directories.

**Operation example**
If the Alluxio space is unexpectedly over utilized, du can be used to detect which folders are taking up the most space.

```
$ ./bin/alluxio fs du /\\*
```

## fileInfo

**Background**
The fileInfo command is deprecated since Alluxio version 1.5. Please use the stat command instead.

The fileInfo command dumps the FileInfo representation of a file to the console. It is primarily intended to assist users in debugging their system. Generally, viewing the file information in the UI will be much easier to understand.

**Operation example**
fileInfo can be used to debug the block locations of a file. This is useful when trying to achieve locality for compute workloads.

```
$ ./bin/alluxio fs fileInfo /data/2015/logs-1.txt
```

## free

**Background**
The free command sends a request to the master to evict all blocks of a file from the Alluxio workers. If the argument to free is a directory, it will recursively free all files. This request is not guaranteed to take effect immediately, as readers may be currently by using the blocks of the file. free will return immediately after the request is acknowledged by the master. Note that, files must be persisted already in under storage before being freed, or the free command will fail; also any pinned files cannot be freed unless -f option is specified. The free command does not delete any data from the under storage system, but only removing the blocks of those files in Alluxio space to reclaim space. In addition, metadata will not be affected by this operation, meaning the freed file will still show up if an ls command is run.

**Operation example**
free can be used to manually manage Alluxio's data caching.

```
$ ./bin/alluxio fs free /unused/data
```

## getCapacityBytes

**Background**
The getCapacityBytes command returns the maximum number of bytes Alluxio is configured to store.

**Operation example**
getCapacityBytes can be used to verify if your cluster is set up as expected.

```
$ ./bin/alluxio fs getCapacityBytes
```

## getUsedBytes

**Background**
The getUsedBytes command returns the number of used bytes in Alluxio.

**Operation example**
getUsedBytes can be used to monitor the health of your cluster.

```
$ ./bin/alluxio fs getUsedBytes
```

## leader

**Background**
The leader command prints the current Alluxio leader master host name.

**Operation example**
```
$ ./bin/alluxio fs leader
```

## load

**Background**
The load command moves data from the under storage system into Alluxio storage. If there is an Alluxio worker on the machine this command is run from, the data will be loaded to that worker. Otherwise, a random worker will be selected to serve the data. If the data is already loaded into Alluxio, load is a no-op. If load is run on a directory, files in the directory will be recursively loaded.

**Operation example**
load can be used to prefetch data for analytics jobs.
```
$ ./bin/alluxio fs load /data/today
```

## loadMetadata

**Background**
The loadMetadata command queries the under storage system for any file or directory matching the given path and then creates a mirror of the file in Alluxio backed by that file. Only the metadata, such as the file name and size, are loaded this way and no data transfer occurs.

**Operation example**
loadMetadata can be used when other systems output to the under storage directly (bypassing Alluxio), and the application running on Alluxio needs to use the output of those systems.
```
$ ./bin/alluxio fs loadMetadata /hdfs/data/2015/logs-1.txt
```

## location

**Background**

The location command returns the addresses of all the Alluxio workers which contain blocks belonging to the given file.

**Operation example**
location can be used to debug data locality when running jobs by using a compute framework.

```
$ ./bin/alluxio fs location /data/2015/logs-1.txt
```

## ls

**Background**

The ls command lists all the immediate children in a directory and displays the file size, last modification time, and in memory status of the files. Using ls on a file will only display the information for that specific file. The ls command will also load the metadata for any file or immediate children of a directory from the under storage system to Alluxio namespace, if it does not exist in Alluxio yet. ls queries the under storage system for any file or directory matching the given path and then creates a mirror of the file in Alluxio backed by that file. Only the metadata, such as the file name and size are loaded this way and no data transfer occurs.

Options:

-d option lists the directories as plain files. For example, `ls -d /` shows the attributes of root directory.
f option forces loading metadata for immediate children in a directory. By default, it loads metadata only at the first time at which a directory is listed.
-h option displays file sizes in human-readable formats.
-p option lists all pinned files.
-R option also recursively lists child directories, displaying the entire subtree starting from the input path.

**Operation example**
ls can be used to browse the file system.
```
$ ./bin/alluxio fs mount /cos/data cosn://data-bucket/
```
Verify:
```
$ ./bin/alluxio fs ls /s3/data/
```

## masterInfo

**Background**
The masterInfo command prints information regarding master fault tolerance such as leader address, list of master addresses, and the configured Zookeeper address. If Alluxio is running in single master mode, masterInfo will print the master address. If Alluxio is running in fault tolerance mode, the leader address, list of master addresses and the configured Zookeeper address will be printed.

**Operation example**
masterInfo can be used to print information regarding master fault tolerance.

```
$ ./bin/alluxio fs masterInfo
```

## mkdir

**Background**
The mkdir command creates a new directory in Alluxio space. It is recursive and will create any nonexistent parent directories. Note that the created directory will not be created in the under storage system until a file in the directory is persisted to the underlying storage. Using mkdir on an invalid or already existing path will fail.

**Operation example**
mkdir can be used by an admin to set up the basic folder structures.

```
$ ./bin/alluxio fs mkdir /users
$ ./bin/alluxio fs mkdir /users/Alice
$ ./bin/alluxio fs mkdir /users/Bob
```

## mount

**Background**
The mount command links an under storage path to an Alluxio path, and files and folders created in Alluxio space under the path will be backed by a corresponding file or folder in the under storage path. For more details, please see Unified Namespace.

Options:
--readonly option sets the mount point to be readonly in Alluxio
--option `<key>=<val>` option passes a property to this mount point (e.g., S3 credential)

**Operation example**
mount can be used to make data in another storage system available in Alluxio.

```
$ ./bin/alluxio fs mount /mnt/hdfs hdfs://host1:9000/data/
```

## mv

**Background**
The mv command moves a file or directory to another path in Alluxio. The destination path must not exist or be a directory. If it is a directory, the file or directory will be placed as a child of the directory. mv is purely a metadata operation and does not affect the data blocks of the file. mv cannot be done between mount points of different under storage systems.

**Operation example**
mv can be used to move older data into a non working directory.

```
$ ./bin/alluxio fs mv /data/2014 /data/archives/2014
```

## persist

**Background**
The persist command persists data in Alluxio storage into the under storage system. This is a data operation and will take time depending on how large the file is. After persist is complete, the file in Alluxio will be backed by the file in the under storage, make it still valid if the Alluxio blocks are evicted or otherwise lost.
**Operation example**
persist can be used after filtering a series of temporary files for the ones containing useful data.

```
$ ./bin/alluxio fs persist /tmp/experimental-logs-2.txt
```

## pin

**Background**
The pin command marks a file or folder as pinned in Alluxio. This is a metadata operation and will not cause any data to be loaded into Alluxio. If a file is pinned, any blocks belonging to the file will never be evicted from an Alluxio worker. If there are too many pinned files, Alluxio workers may run low on storage space preventing other files from being cached.

**Operation example**
pin can be used to manually ensure performance if the administrator understands the workloads well.

```
$ ./bin/alluxio fs pin /data/today
```

## report

**Background**
The report command marks a file as lost to the Alluxio master. This command should only be used with files created by using the Lineage API. Marking a file as lost will cause the master to schedule a recomputation job to regenerate the file.

**Operation example**
report can be used to force recomputation of a file.

```
$ ./bin/alluxio fs report /tmp/lineage-file
```

## rm

**Background**
The rm command removes a file from Alluxio space and the under storage system. The file will be unavailable immediately after this command returns, but the actual data may be deleted a while later.

Add -R option will delete all contents of the directory and then the directory itself. Add -U option to not check whether the UFS contents being deleted are in-sync with Alluxio before attempting to delete persisted directories.

**Operation example**
rm can be used to remove temporary files which are no longer needed.

```
$ ./bin/alluxio fs rm /tmp/unused-file
```

## setTtl

**Background**
The setTtl command sets the time-to-live of a file or a directory, in milliseconds. If set ttl to a directory, all the children inside that directory will set too. So a directory's TTL expires, all the children inside that directory will also expire. Action parameter will indicate the action to perform once the current time is greater than the TTL + creation time of the file. Action delete (default) will delete file or directory from both Alluxio and the under storage system, whereas action free will just free the file from Alluxio even they are pinned.

**Operation example**
setTtl with action delete can be used to clean up files the administrator knows are unnecessary after a period of time, or with action free just remove the contents from Alluxio to make room for more space in Alluxio.

```
$ ./bin/alluxio fs setTtl -action free /data/good-for-one-day 86400000
```

## stat

**Background**
The stat command dumps the FileInfo representation of a file or a directory to the console. It is primarily intended to assist users in debugging their system. Generally, viewing the file information in the UI will be much easier to understand.

You can specify -f to display information in a given format:
- "%N": name of the file
- "%z": size of the file in bytes
- "%u": owner
- "%g": group name of the owner
- "%y" or "%Y": modification time, `%y shows ‘yyyy-MM-dd HH:mm:ss’ (the UTC date), %Y` shows milliseconds since January 1, 1970 UTC
- "%b": number of blocks allocated for the file

**Operation example**
stat can be used to debug the block locations of a file. This is useful when trying to achieve locality for compute workloads.
```
$ ./bin/alluxio fs stat /data/2015/logs-1.txt
$ ./bin/alluxio fs stat /data/2015
$ ./bin/alluxio fs stat -f %z /data/2015/logs-1.txt
```

## tail

**Background**
The tail command outputs the last 1 KB of data in a file to the console.

**Operation example**
tail can be used to verify the output of a job is in the expected format or contains expected values.
```
$ ./bin/alluxio fs tail /output/part-00000
```

## test

**Background**
The test command tests a property of a path, returning 0 if the property is true, or 1 otherwise.

Options:
-d option tests whether the path is a directory.
-e option tests whether the path exists.
-f option tests whether the path is a file.
-s option tests whether the directory is empty.
-z option tests whether the file is zero length.

**Operation example**
```
$ ./bin/alluxio fs test -d /someDir
```

## touch

**Background**
The touch command creates a 0-byte file. Files created with touch cannot be overwritten and are mostly useful as flags.

**Operation example**
touch can be used to create a file signifying the completion of analysis on a directory.

```
$ ./bin/alluxio fs touch /data/yesterday/_DONE_
```

## unmount

**Background**
The unmount command disassociates an Alluxio path with an under storage directory. Alluxio metadata for the mount point will be removed along with any data blocks, but the under storage system will retain all metadata and data. See Unified Namespace for more details.

**Operation example**
unmount can be used to remove an under storage system when you no longer need data from that system.

```
$ ./bin/alluxio fs unmount /s3/data
```

## unpin

**Background**
The unpin command unmarks a file or directory in Alluxio as pinned. This is a metadata operation and will not evict or delete any data blocks. Once a file is unpinned, its data blocks can be evicted from various Alluxio workers containing the block.

**Operation example**
unpin can be used when the administrator knows there is a change in the data access pattern.
```
$ ./bin/alluxio fs unpin /data/yesterday/join-table
```

## unsetTtl

**Background**
The unsetTtl command will remove the TTL of a file in Alluxio. This is a metadata operation and will not evict or store blocks in Alluxio. The TTL of a file can later be reset with setTtl.

**Operation example**
unsetTtl can be used if a regularly managed file requires manual management due to some special case.

```
$ ./bin/alluxio fs unsetTtl /data/yesterday/data-not-yet-analyzed
```
