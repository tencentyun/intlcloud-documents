The `abort` command is used to clear the generated incomplete multipart uploads.

## Command Syntax

```plaintext
./coscli abort cos://<bucketAlias>[/prefix/] [flag]
```

>? 
>- For more information on `bucketAlias`, see [Download and Installation Configuration](https://intl.cloud.tencent.com/document/product/436/43265).
>- For more general options for this command (such as switching buckets or user accounts), see [General Options](https://intl.cloud.tencent.com/document/product/436/46273).
>

The `abort` command contains the following optional flags:

| Flag Abbreviation | Flag Full Name     | Description                         |
| --------- | ------------- | ------------------------ |
|     None      | --include     | Includes specific objects.                |
|     None      | --exclude     | Excludes specific objects.                |

## Examples

### Clearing all incomplete multipart uploads in `bucket1` bucket

```plaintext
./coscli abort cos://bucket1
```

### Clearing all incomplete multipart uploads in `picture` folder in `bucket1` bucket

```plaintext
./coscli abort cos://bucket1/picture/
```
