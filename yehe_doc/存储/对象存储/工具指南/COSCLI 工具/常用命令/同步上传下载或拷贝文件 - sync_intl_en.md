## Command Syntax

The `sync` command is used to sync object upload, download, and copy. How `sync` differs from `cp` is that it will first compare the CRC64 value of an object whose name already exists, and if the value is the same, the object will not be transferred.

```plaintext
./coscli sync <source_path> <destination_path> [flag]
```

>? For more information about `bucketAlias`, please see [Configuration Parameters](https://intl.cloud.tencent.com/document/product/436/43265).

`sync` includes the following optional flags:

| Flag Abbreviation | Flag Full Name   | Description                     |
| --------- | ------------- | ------------------------------ |
| -h        | --help      | Outputs help information.       |
| -c        | --config-path | Path of the configuration file to use |
|  None  | --include   | Includes specific objects.  |
|  None  | --exclude   | Excludes specific objects.    |
| -r        | --recursive | Whether to traverse all objects in the directory recursively  |


>?
> - `--include` and `--exclude` support standard regular expressions. You can use regular expressions to filter objects that meet your requirements.
> - When using `zsh`, you may need to enclose the pattern string with double quotation marks.
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
