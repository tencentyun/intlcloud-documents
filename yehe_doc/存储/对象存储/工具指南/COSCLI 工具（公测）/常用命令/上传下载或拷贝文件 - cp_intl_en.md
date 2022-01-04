
The `cp` command is used to upload, download, or copy objects.

## Command Syntax

```plaintext
./coscli cp <source_path> <destination_path> [flags]
```

>? For more information on `bucketAlias`, please see [Configuration](https://intl.cloud.tencent.com/document/product/436/43265).
>

`cp` includes the following optional flags:

| Flag Abbreviation | Flag Full Name   | Description                     |
| --------- | --------------- | ------------------------------------ |
| -h        | --help      | Outputs help information.       |
| -c        | --config-path | Path of the configuration file to use |
|  None  | --include   | Includes specific objects.  |
|  None  | --exclude   | Excludes specific objects.    |
| -r        | --recursive | Whether to traverse all objects in the directory recursively  |
|   None  | --storage-class | Specifies the storage class for the object to upload. Default value: `STANDARD` |
|   None       | --part-size     | Part size. Default value: `32 MB`      |
|   None       | --thread-num    | Number of concurrent threads. Default value: `5`      |
|   None       | --rate-limiting | Speed limit for a single URL. Value range: 0.1-100 MB/s       |


>?
> - `cp` automatically uses concurrent upload/download for large objects.
> - If an object is larger than `--part-size`, COSCLI will split the object into multiple parts according to `--part-size` and use `--thread-num` threads to concurrently upload/download the object.
> - Each thread maintains a URL. For each URL, you can use the `--rate-limiting` parameter to limit its speed. When concurrent upload/download is enabled, the total rate is `--thread-num * --rate-limiting`.
> - If an object is uploaded/downloaded in parts, checkpoint restart will be enabled by default.
> - `--include` and `--exclude` support standard regular expression syntax, so you can use them to filter files that meet specific criteria.
> - When using `zsh`, you may need to add double quotes at both ends of the `pattern` string.
```
./coscli cp ~/test/ cos://bucket1/example/ -r --include ".*.mp4"
```

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

#### Uploading all MP4 objects in the `example1` directory in `bucket1` to the `example2` directory in `bucket2`

```plaintext
./coscli cp cos://bucket1/example1/ cos://bucket2/example2/ -r --include .*.mp4
```

#### Copying all non-MD objects in the `example1` directory in `bucket1` to the `example2` directory in `bucket2`

```plaintext
./coscli cp cos://bucket1/example1/ cos://bucket2/example2/ -r --exclude .*.md
```
