## Command Syntax

The `sync` command is used to sync object upload, download, and copy. How `sync` differs from `cp` is that it will first compare the CRC64 value of an object whose name already exists, and if the value is the same, the object will not be transferred.

```plaintext
./coscli sync <source_path> <destination_path> [flag]
```

>? For more information on `bucketAlias`, please see [Configuration](https://intl.cloud.tencent.com/document/product/436/43265).
>

`sync` includes the following optional flags:

| Flag Abbreviation | Flag Name     | Purpose                         |
| --------- | ------------- | ------------------------------ |
| -h        | --help        | Outputs help information                      |
| -c        | --config-path | Specifies the path of the configuration file to be used          |
|  None  | --include   | Includes specific objects.  |
|  None  | --exclude   | Excludes specific objects.    |
| -r        | --recursive | Whether to traverse all objects in the directory recursively  |
|   None  | --storage-class | Specifies the storage class for the object to upload. Default value: `STANDARD` |
|   None       | --part-size     | Part size. Default value: `32 MB`; maximum value: `5 GB`     |
|   None       | --thread-num    | Number of concurrent threads. Default value: `5`      |
|   None       | --rate-limiting | Speed limit for a single URL. Value range: 0.1–100 MB/s       |


>?
> - `sync` automatically uses concurrent upload/download for large objects.
> - If an object is larger than `--part-size`, COSCLI will split the object into multiple parts according to `--part-size` and use `--thread-num` threads to concurrently upload/download the object.
> - Each thread maintains a URL. For each URL, you can use the `--rate-limiting` parameter to limit its speed. When concurrent upload/download is enabled, the total rate is `--thread-num * --rate-limiting`.
> - If an object is uploaded/downloaded in parts, checkpoint restart will be enabled by default.
> - `--include` and `--exclude` support standard regular expression syntax, so you can use them to filter files that meet specific criteria.
> - When using `zsh`, you may need to add double quotes at both ends of the `pattern` string.
```
./coscli sync ~/test/ cos://bucket1/example/ -r --include ".*.mp4"
```

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
