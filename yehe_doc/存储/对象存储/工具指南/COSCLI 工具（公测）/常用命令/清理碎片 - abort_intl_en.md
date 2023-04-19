The `abort` command is used to clear the generated incomplete multipart uploads.

## Command Syntax

```plaintext
./coscli abort cos://<bucket-name>[/prefix/] [flag]
```

`abort` includes the following parameters:

| Parameter Format | Description | Example |
| --------- | ------------- | ------------------------ |
|  cos://&lt;bucket-name&gt;/&lt;key&gt;  | Specifies the target object in the bucket, which is accessible by using the bucket alias or bucket name configured in the configuration file as detailed in [Download and Installation Configuration](https://intl.cloud.tencent.com/document/product/436/43265). If you use the bucket name for access, you also need to include the `endpoint` flag. | Access with the bucket alias: cos://example-alias <br>Access with the bucket name: cos://examplebucket-1250000000    |
| /prefix/          | Specifies a directory (optional). | /picture/ |


The `abort` command contains the following optional flags:

| Flag Abbreviation | Flag Name     | Description                         |
| --------- | ------------- | ------------------------ |
| -h |  --help |   Views the usage of this command. |
|     None      | --include     | Includes specific objects                  |
|     None      | --exclude     | Excludes files with a specific pattern                |

>? For other common options of this command (such as switching bucket and user account), see [Common Options](https://www.tencentcloud.com/document/product/436/46273).
>

## Examples

### Clearing all incomplete multipart uploads in `bucket1` bucket

```plaintext
./coscli abort cos://bucket1
```

### Clearing all incomplete multipart uploads in `picture` folder in `bucket1` bucket

```plaintext
./coscli abort cos://bucket1/picture/
```

