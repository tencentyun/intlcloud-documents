The `abort` command is used to clear the generated incomplete multipart uploads.

## Command Format

```plaintext
./coscli abort cos://<bucketAlias>[/prefix/] [flag]
```

>? For more information on `bucketAlias`, please see [Configuration](https://intl.cloud.tencent.com/document/product/436/43265).
>

The `abort` command contains the following optional flags:

| Flag Abbreviation | Flag Name     | Purpose                         |
| --------- | ------------- | ------------------------ |
| -h        | --help        | Outputs help information                      |
| -c        | --config-path | Specifies the path of the configuration file to be used          |
|     None      | --include     | Includes files with a specific pattern                |
|     None      | --exclude     | Excludes files with a specific pattern                |

## Example

### Clearing all incomplete multipart uploads in `bucket1` bucket

```plaintext
./coscli abort cos://bucket1
```

### Clearing all incomplete multipart uploads in `picture` folder in `bucket1` bucket

```plaintext
./coscli abort cos://bucket1/picture/
```
