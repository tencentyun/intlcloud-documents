The `lsparts` command is used to list the generated incomplete multipart uploads.

## Command Syntax

```plaintext
./coscli lsparts cos://<bucketAlias>[/prefix/] [flag]
```

>? 
>- For more information on `bucketAlias`, see [Download and Installation Configuration](https://intl.cloud.tencent.com/document/product/436/43265).
>- For more general options for this command (such as switching buckets or user accounts), see [General Options](https://intl.cloud.tencent.com/document/product/436/46273).
>

The `lsparts` command contains the following optional flags:

| Flag Abbreviation | Flag Name     | Purpose                         |
| --------- | ------------- | ---------------------------- |
|     None      | --include     | Includes files with a specific pattern                |
|     None      | --exclude     | Excludes files with a specific pattern                |
|     None      | --limit       | Specifies the maximum quantity (0–1000) to be listed  |

## Examples

### Listing all incomplete multipart uploads in `bucket1` bucket

```plaintext
./coscli lsparts cos://bucket1
```

### Listing all incomplete multipart uploads in `picture` folder in `bucket1` bucket

```plaintext
./coscli lsparts cos://bucket1/picture/
```
