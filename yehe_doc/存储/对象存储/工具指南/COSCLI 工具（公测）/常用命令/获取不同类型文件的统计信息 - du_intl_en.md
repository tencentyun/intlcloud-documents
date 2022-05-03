
The `du` command is used to list the statistics (total number and size) of files of each storage class in a bucket or a directory.

## Command Syntax

```plaintext
./coscli du cos://<bucketAlias>[/prefix/] [flag]
```

>? 
>- For more information on `bucketAlias`, see [Download and Installation Configuration](https://intl.cloud.tencent.com/document/product/436/43265).
>- For other common options of this command (such as switching bucket and user account), see [Common Options](https://intl.cloud.tencent.com/document/product/436/46273).
>

`du` includes the following optional parameters:

| Parameter Format | Description | Example |
| -------- | -------------- | -------------------- |
| /prefix/ | Specifies a directory. | cos://bucket1/picture/ |

`du` includes the following optional flags:

| Flag Abbreviation | Flag Full Name     | Description                         |
| --------- | ------------- | ------------------------ |
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
