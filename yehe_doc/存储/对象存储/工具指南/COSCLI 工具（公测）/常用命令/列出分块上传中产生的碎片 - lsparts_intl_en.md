The `lsparts` command is used to list the generated incomplete multipart uploads.
>! For more information, see [Multipart Upload](https://intl.cloud.tencent.com/document/product/436/14112).

## Command Syntax
```plaintext
./coscli lsparts cos://<bucket-name>[/prefix/] [flag]
```

`lsparts` includes the following parameters:

| Parameter Format | Description | Example |
| --------- | ------------- | ------------------------ |
 cos://&lt;bucket-name&gt; | Specifies the target bucket, which is accessible by using the bucket alias or bucket name configured in the configuration file as detailed in [Download and Installation Configuration](https://intl.cloud.tencent.com/document/product/436/43265). If you use the bucket name for access, you also need to include the `endpoint` flag. | Access with the bucket alias: cos://example-alias <br>Access with the bucket name: cos://examplebucket-1250000000    |
| /prefix/          | Specifies a directory (optional). | /picture/ |

The `lsparts` command contains the following optional flags:

| Flag Abbreviation | Flag Name     | Description                         |
| --------- | ------------- | ---------------------------- |
| -h |  --help |   Views the usage of this command. |
|     None      | --include     | Includes specific objects.                  |
|     None      | --exclude     | Excludes files with a specific pattern                |
|     None      | --limit       | Specifies the maximum quantity (0–1000) to be listed.  |

>? For other common options of this command (such as switching bucket and user account), see [Common Options](https://www.tencentcloud.com/document/product/436/46273).
>

## Examples

### Listing all incomplete multipart uploads in `bucket1` bucket

```plaintext
./coscli lsparts cos://bucket1
```

The returned information includes the object key (the unique identifier of the object in the bucket), multipart upload ID, multipart upload start time, and total number of incomplete multipart uploads in the bucket. Below is an example:

```plaintext
      KEY      |              UPLOAD ID              |      INITIATE TIME
---------------+-------------------------------------+----------------------------
    test.txt   | 1671191183635d2b71b1d68a0********** | 2022-01-01T00:00:00.000Z
---------------+-------------------------------------+----------------------------
                                                                TOTAL: 1
                                                      ----------------------------
```

### Listing all incomplete multipart uploads in `picture` folder in `bucket1` bucket

```plaintext
./coscli lsparts cos://bucket1/picture/
```
