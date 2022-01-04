The `lsparts` command is used to list the generated incomplete multipart uploads.

## Command Format

```plaintext
./coscli lsparts cos://<bucketAlias>[/prefix/] [flag]
```

>? For more information on `bucketAlias`, please see [Configuration](https://intl.cloud.tencent.com/document/product/436/43265).
>

The `lsparts` command contains the following optional flags:

| Flag Abbreviation | Flag Name     | Purpose                         |
| --------- | ------------- | ---------------------------- |
| -h        | --help        | Outputs help information                      |
| -c        | --config-path | Specifies the path of the configuration file to be used          |
|     None      | --include     | Includes files with a specific pattern                |
|     None      | --exclude     | Excludes files with a specific pattern                |
|     None      | --limit       | Specifies the maximum quantity (0–1000) to be listed  |

## Example

### Listing all incomplete multipart uploads in `bucket1` bucket

```plaintext
./coscli lsparts cos://bucket1
```

### Listing all incomplete multipart uploads in `picture` folder in `bucket1` bucket

```plaintext
./coscli lsparts cos://bucket1/picture/
```
