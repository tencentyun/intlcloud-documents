
The `cp` command is used to upload, download, or copy objects.

## Command Syntax

```plaintext
./coscli cp <source_path> <destination_path> [flags]
```

`cp` includes the following parameters:


| Parameter Format | Description | Example |
| --------- | ------------- | ------------------------ |
| source_path | Source file path, which can be a local path or a COS file path. The COS path is accessible by using the bucket alias or bucket name configured in the configuration file as detailed in [Download and Installation Configuration](https://intl.cloud.tencent.com/document/product/436/43265). If you use the bucket name for access, you also need to include the `endpoint` flag. | Local path: ~/example.txt <br>COS file path specified with the bucket alias: cos://bucketalias/example.txt <br>COS file path specified with the bucket name: cos://examplebucket-1250000000/example.txt |
| destination_path | Destination file path, which can be a local path or a COS file path. The COS path is accessible by using the bucket alias or bucket name configured in the configuration file as detailed in [Download and Installation Configuration](https://intl.cloud.tencent.com/document/product/436/43265). If you use the bucket name for access, you also need to include the `endpoint` flag. | Local path: ~/example.txt <br>COS file path specified with the bucket alias: cos://bucketalias/example.txt <br>COS file path specified with the bucket name: cos://examplebucket-1250000000/example.txt |

`cp` includes the following optional flags:

| Flag Abbreviation | Flag Name   | Description                     |
| --------- | --------------- | ------------------------------------ |
|  None  | --include   | Includes specific objects.  |
|  None  | --exclude   | Excludes specific objects.    |
| -r        | --recursive | Specifies whether to traverse all objects in the directory recursively.  |
|   None       | --storage-class | Specifies the storage class of the uploaded file. Default value: `STANDARD`. For more information, see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925). |
|   None       | --part-size     | Part size in MB. Default value: 32 MB     |
|   None       | --thread-num    | Number of concurrent threads. Default value: 5      |
|   None       | --rate-limiting | Speed limit for a single URL in MB/s. Value range: 0.1–100 MB/s       |
| None | --meta | Metadata of the uploaded file, including certain HTTP standard attributes (HTTP Header) and custom metadata prefixed with `x-cos-meta-` (User Meta). The file metadata is in the format of `header:value#header:value`, such as `Expires:2022-10-12T00:00:00.000Z#Cache-Control:no-cache#Content-Encoding:gzip#x-cos-meta-x:x`. |


>?
> - `cp` automatically uses concurrent upload/download for large objects.
> - If an object is larger than `--part-size`, COSCLI will split the object into multiple parts according to `--part-size` and use `--thread-num` threads to concurrently upload/download the object.
> - Each thread maintains a URL. For each URL, you can use the `--rate-limiting` parameter to limit the speed of a single URL. When concurrent upload/download is enabled, the total rate is `--thread-num * --rate-limiting`.
> - If an object is uploaded/downloaded in parts, checkpoint restart will be enabled by default.
> - `--include` and `--exclude` support standard regular expression syntax, so you can use them to filter out objects that meet specific criteria.
> - When using `zsh`, you may need to add double quotes at both ends of the `pattern` string.
```plaintext
./coscli cp ~/test/ cos://bucket1/example/ -r --include ".*.txt" --meta=x-cos-meta-a:a#ContentType:text#Expires:2022-10-12T00:00:00.000Z
```
> - For other common options of this command (such as switching bucket and user account), see [Common Options](https://intl.cloud.tencent.com/document/product/436/46273).


## Examples

### Upload

#### Uploading a single object

```plaintext
./coscli cp ~/example.txt cos://bucket1/example.txt
```

#### Uploading all objects in the local directory `test` to the `example` directory in the `bucket1` bucket

```plaintext
./coscli cp ~/test/ cos://bucket1/example/ -r
```

#### Uploading all MP4 objects in the local directory `test` to the `example` directory in the `bucket1` bucket

```plaintext
./coscli cp ~/test/ cos://bucket1/example/ -r --include .*.mp4
```

#### Uploading all non-MD objects in the local directory `test` to the `example` directory in the `bucket1` bucket

```plaintext
./coscli cp ~/test/ cos://bucket1/example/ -r --exclude .*.md
```

#### Uploading all objects in the `dir` directory (containing the `dirA`, `dirB`, `dirC`, and `dirD` subdirectories) except the `dirD` directory

```plaintext
./coscli cp dir/ cos://bucket1/example/ -r --exclude dirD/.*
```

#### Uploading all objects in the local directory `test` to the `example` directory in the `bucket1` bucket using the ARCHIVE storage class

```plaintext
./coscli cp ~/test/ cos://bucket1/example/ -r --storage-class ARCHIVE
```

#### Uploading the local `file.txt` file to the `bucket1` bucket and setting the single-URL speed limit to 1.3 MB/s

```plaintext
./coscli cp ~/file.txt cos://bucket1/file.txt --rate-limiting 1.3
```


### Download

#### Downloading a single object

```plaintext
./coscli cp cos://bucket1/example.txt ~/example.txt
```

#### Downloading all objects in the `example` directory in the `bucket1` bucket to the `test` directory

```plaintext
./coscli cp cos://bucket1/example/ ~/test/ -r
```

#### Downloading all MP4 objects in the `example` directory in the `bucket1` bucket to the `test` directory

```plaintext
./coscli cp cos://bucket1/example/ ~/test/ -r --include .*.mp4
```

#### Downloading all non-MD objects in the `example` directory in the `bucket1` bucket to the `test` directory

```plaintext
./coscli cp cos://bucket1/example/ ~/test/ -r --exclude .*.md
```

### Copy

#### Copying a single object within a bucket

```plaintext
./coscli cp cos://bucket1/example.txt cos://bucket1/example_copy.txt
```

#### Copying a single object across buckets

```plaintext
./coscli cp cos://bucket1/example.txt cos://bucket2/example_copy.txt
```

#### Copying all objects in the `example1` directory in `bucket1` to the `example2` directory in `bucket2`

```plaintext
./coscli cp cos://bucket1/example1/ cos://bucket2/example2/ -r
```

#### Copying all MP4 objects in the `example1` directory in `bucket1` to the `example2` directory in `bucket2`

```plaintext
./coscli cp cos://bucket1/example1/ cos://bucket2/example2/ -r --include .*.mp4
```

#### Copying all non-MD objects in the `example1` directory in `bucket1` to the `example2` directory in `bucket2`

```plaintext
./coscli cp cos://bucket1/example1/ cos://bucket2/example2/ -r --exclude .*.md
```
