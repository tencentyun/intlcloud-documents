
The `du` command is used to obtain statistics on each storage class for a bucket or a directory, including the size and number of objects in each storage class.

## Command Syntax

```plaintext
./coscli du cos://<bucketAlias>[/prefix/] [flag]
```

>? For more information about `bucketAlias`, please see [Configuration Parameters](https://intl.cloud.tencent.com/document/product/436/43265).
>

`ls` includes the following optional parameters:

| Parameter Format | Description | Example |
| -------- | -------------- | -------------------- |
| /prefix/ | Specifies a directory. | cos://bucket1/picture/ |

`du` includes the following optional flags:

| Flag Abbreviation | Flag Full Name   | Description                     |
| --------- | ------------- | ------------------------ |
| -h        | --help      | Outputs help information.       |
| -c        | --config-path | Path of the configuration file to use |
|  None  | --include   | Includes specific objects.  |
|  None  | --exclude   | Excludes specific objects.    |

>? 
> - `--include` supports standard regular expressions. You can use regular expressions to filter objects that meet your requirements.
> - When using `zsh`, you may need to enclose the pattern string with double quotation marks.
```plaintext
./coscli du cos://bucket1/picture/ --include ".*.mp4"
```

## Examples

### Listing statistics on objects in the `bucket1` bucket

```plaintext
./coscli du cos://bucket1
```

### Listing statistics on objects in the `picture` directory in the `bucket1` bucket

```plaintext
./coscli du cos://bucket1/picture/
```

### Listing statistics on all MP4 objects in the `picture` directory in the `bucket1` bucket

```plaintext
./coscli du cos://bucket1/picture/ --include .*.mp4
```

### Listing statistics on all non-MD objects in the `picture` directory in the `bucket1` bucket

```plaintext
./coscli du cos://bucket1/picture/ --exclude .*.md
```
