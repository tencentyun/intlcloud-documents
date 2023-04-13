## Command Syntax

The `sync` command is used to sync object upload, download, and copy. The difference between `sync` and `cp` is that `sync` first compares the CRC64 value of an object with the same name that already exists, and if the value is the same, the object will not be transferred.

```plaintext
./coscli sync <source_path> <destination_path> [flag]
```


`cp` includes the following parameters:

| Parameter Format | Description | Example |
| --------- | ------------- | ------------------------ |
|  source_path | Source file path, which can be a local path or a COS file path. The COS path is accessible by using the bucket alias or bucket name configured in the configuration file as detailed in [Download and Installation Configuration](https://intl.cloud.tencent.com/document/product/436/43265). If you use the bucket name for access, you also need to include the `endpoint` flag. | Local path: ~/example.txt <br>COS file path specified with the bucket alias: cos://bucketalias/example.txt <br>COS file path specified with the bucket name: cos://examplebucket-1250000000/example.txt |
|   destination_path | Destination file path, which can be a local path or a COS file path. The COS path is accessible by using the bucket alias or bucket name configured in the configuration file as detailed in [Download and Installation Configuration](https://intl.cloud.tencent.com/document/product/436/43265). If you use the bucket name for access, you also need to include the `endpoint` flag. | Local path: ~/example.txt <br>COS file path specified with the bucket alias: cos://bucketalias/example.txt <br>COS file path specified with the bucket name: cos://examplebucket-1250000000/example.txt |

`sync` includes the following optional flags:

| Flag Abbreviation | Flag Name     | Description                         |
| --------- | ------------- | ------------------------------ |
|  None  | --include   | Includes specific objects.  |
|  None  | --exclude   | Excludes specific objects.    |
| -r        | --recursive | Specifies whether to traverse all objects in the directory recursively.  |
|   None       | --storage-class | Specifies the storage class of the uploaded file. Default value: `STANDARD`. For more information, see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925). |
|   None       | --part-size     | Part size. Default value: 32 MB; maximum value: 5 GB     |
|   None       | --thread-num    | Number of concurrent threads. Default value: 5      |
|   None       | --rate-limiting | Speed limit for a single URL. Value range: 0.1–100 MB/s       |
| None | --snapshot-path | Specifies the directory where the snapshot information is stored when the uploaded or downloaded file is saved. During the next file upload or download, COSCLI will read the snapshot information in the specified directory for incremental upload or download. This option is used to speed up directory file sync. |
| None | --meta | Metadata of the uploaded file, including certain HTTP standard attributes (HTTP Header) and custom metadata prefixed with `x-cos-meta-` (User Meta). The file metadata is in the format of `header:value#header:value`, such as `Expires:2022-10-12T00:00:00.000Z#Cache-Control:no-cache#Content-Encoding:gzip#x-cos-meta-x:x`. |


>?
> - `sync` automatically uses concurrent upload/download for large objects.
> - If an object is larger than `--part-size`, COSCLI will split the object into multiple parts according to `--part-size` and use `--thread-num` threads to concurrently upload/download the object.
> - Each thread maintains a URL. For each URL, you can use the `--rate-limiting` parameter to limit the speed of a single URL. When concurrent upload/download is enabled, the total rate is `--thread-num * --rate-limiting`.
> - If an object is uploaded/downloaded in parts, checkpoint restart will be enabled by default.
> - `--include` and `--exclude` support standard regular expression syntax, so you can use them to filter out objects that meet specific criteria.
> - When using `zsh`, you may need to add double quotes at both ends of the `pattern` string.
> - Do not set `snapshot-path` to the directory to be migrated or its subdirectories. COSCLI will not actively delete the snapshot information in the `snapshot-path` folder. Therefore, to avoid excessive snapshot information, delete unnecessary snapshots in this folder regularly.
```
./coscli sync ~/test/ cos://bucket1/example/ -r --include ".*.txt" --snapshot-path=/path/snapshot-path  --meta=x-cos-meta-a:a#ContentType:text#Expires:2022-10-12T00:00:00.000Z
```
> - For other common options of this command (such as switching bucket and user account), see [Common Options](https://intl.cloud.tencent.com/document/product/436/46273).


## Examples

### Syncing object upload

```plaintext
./coscli sync ~/example.txt cos://bucket1/example.txt
```

### Syncing object download

```plaintext
./coscli sync cos://bucket1/example.txt ~/example.txt
```

### Syncing intra-bucket replication

```plaintext
./coscli sync cos://bucket1/example.txt cos://bucket1/example_copy.txt
```

### Syncing cross-bucket replication

```plaintext
./coscli sync cos://bucket1/example.txt cos://bucket2/example_copy.txt
```
