## Background

Alluxio provides access to data through a filesystem interface. Files in Alluxio offer write-once semantics: they become immutable after they have been written in their entirety and cannot be read before being completed. Alluxio provides two different Filesystem APIs, the Alluxio API and a Hadoop compatible API. The Alluxio API provides additional functionality, while the Hadoop compatible API gives you the flexibility of leveraging Alluxio without having to modify existing code written using Hadoop's API.

All resources with the Alluxio Java API are specified through an AlluxioURI which represents the path to the resource.

## Getting a Filesystem Client

To obtain an Alluxio filesystem client in Java code, use:

`FileSystem fs = FileSystem.Factory.get();`

## Creating a File
All metadata operations as well as opening a file for reading or creating a file for writing are executed through the FileSystem object. Since Alluxio files are immutable once written, the idiomatic way to create files is to use FileSystem#createFile(AlluxioURI), which returns a stream object that can be used to write the file. For example:

```
FileSystem fs = FileSystem.Factory.get();
AlluxioURI path = new AlluxioURI("/myFile");
// Create a file and get its output stream
FileOutStream out = fs.createFile(path);
// Write data
out.write(...);
// Close and complete file
out.close();
```

## Specifying Operation Options

For all FileSystem operations, an additional options field may be specified, which allows you to specify non-default settings for the operation. For example:

```
FileSystem fs = FileSystem.Factory.get();
AlluxioURI path = new AlluxioURI("/myFile");
// Generate options to set a custom blocksize of 128 MB
CreateFileOptions options = CreateFileOptions.defaults().setBlockSize(128 * Constants.MB);
FileOutStream out = fs.createFile(path, options);
```

## IO Options

Alluxio uses two different storage types: Alluxio managed storage and under storage. Alluxio managed storage is the memory, SSD, and/or HDD allocated to Alluxio workers. Under storage is the storage resource managed by the underlying storage system, such as S3, Swift, or HDFS. You can specify the interaction with Alluxio managed storage through ReadType and WriteType. ReadType specifies the data read behavior when reading a file. WriteType specifies the data write behavior when writing a new file, e.g., whether the data should be written in Alluxio storage.

Below is a table of the expected behaviors of ReadType. Reads will always prefer Alluxio storage over the under storage system.

|Read Type |	Behavior |
|--|--|
|CACHE_PROMOTE |	Data is moved to the highest tier in the worker where the data was read. If the data was not in the Alluxio storage of the local worker, a replica will be added to the local Alluxio worker. <br>If `alluxio.user.file.cache.partially.read.block` is set to true, data blocks that are not completely read will also be `entirely` stored in Alluxio. In contrast, a data block can be cached only when it is completely read.|
| CACHE	| If the data was not in the Alluxio storage of the local worker, a replica will be added to the local Alluxio worker. <br>If `alluxio.user.file.cache.partially.read.block` is set to true, data blocks that are not completely read will also be `entirely` stored in Alluxio. In contrast, a data block can be cached only when it is completely read.|
| NO_CACHE |	Data is read without storing a replica in Alluxio.|

Below is a table of the expected behaviors of WriteType.

| Write Type |	Behavior |
|--|--|
|CACHE_THROUGH|	Data is written synchronously to an Alluxio worker and the under storage system.|
|MUST_CACHE |	Data is written synchronously to an Alluxio worker. No data will be written to the under storage. This is the default write type.|
|THROUGH |	Data is written synchronously to the under storage. No data will be written to Alluxio.|
|ASYNC_THROUGH |	Data is written synchronously to an Alluxio worker and asynchronously to the under storage system. This is experimental.|

## Location Policy

Alluxio provides location policy to choose which workers to store the blocks of a file.
Using Alluxio's Java API, you can set the policy in CreateFileOptions for writing files into Alluxio and OpenFileOptions for reading files from Alluxio.
You can simply override the default policy class in the configuration file at property `alluxio.user.file.write.location.policy.class. The built-in policies include:
- LocalFirstPolicy (alluxio.client.file.policy.LocalFirstPolicy) 
It returns the local host first, and if the local worker doesn't have enough capacity of a block, it randomly picks a worker from the active workers list. This is the default policy.
- MostAvailableFirstPolicy (alluxio.client.file.policy.MostAvailableFirstPolicy)
It returns the worker with the most available bytes.
- RoundRobinPolicy (alluxio.client.file.policy.RoundRobinPolicy)
It chooses the worker for the next block in a round-robin manner and skips workers that do not have enough capacity.
- SpecificHostPolicy (alluxio.client.file.policy.SpecificHostPolicy)
It returns a worker with the specified host name. This policy cannot be set as default policy.

Alluxio supports custom policies, so you can also develop your own policy appropriate for your workload by implementing interface alluxio.client.file.policyFileWriteLocationPolicy.
>The default policy must have an empty constructor. To use the ASYNC_THROUGH write type, all the blocks of a file must be written to the same worker.

Alluxio allows a client to select a tier preference when writing blocks to a local worker. Currently, this policy preference exists only for local workers but not remote workers; remote workers will write blocks to the highest tier.
By default, data is written to the top tier. You can modify the default setting through the alluxio.user.file.write.tier.default configuration property or override it through an option to the FileSystem#createFile(AlluxioURI) API call.
All operations on existing files or directories require you to specify the AlluxioURI. With the AlluxioURI, you may use any of the methods of FileSystem to access the resource.
An AlluxioURI can be used to perform Alluxio FileSystem operations, such as modifying the file metadata, ttl, or pin state, or getting an input stream to read the file.
For example, to read a file:
```
FileSystem fs = FileSystem.Factory.get();
AlluxioURI path = new AlluxioURI("/myFile");
// Open the file for reading
FileInStream in = fs.openFile(path);
// Read data
in.read(...);
// Close file relinquishing the lock
in.close();
```
