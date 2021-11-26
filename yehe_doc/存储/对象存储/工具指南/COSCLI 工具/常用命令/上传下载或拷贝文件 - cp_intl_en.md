
The `cp` command is used to upload, download, or copy objects.

## Command Syntax

```plaintext
./coscli cp <source_path> <destination_path> [flags]
```

>? For more information about `bucketAlias`, please see [Configuration Parameters](https://intl.cloud.tencent.com/document/product/436/43265).
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


>?
> - `cp` automatically uses concurrent upload/download for large objects.
> - If an object is larger than 32 MB, COSCLI will splice the object by 32 MB and uses 5 threads to concurrently upload/download the object.
> - If an object is uploaded/downloaded in parts, checkpoint restart will be enabled by default.
> - `--include` and `--exclude` support standard regular expressions. You can use regular expressions to filter objects that meet your requirements.
> - When using `zsh`, you may need to enclose the pattern string with double quotation marks.
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
