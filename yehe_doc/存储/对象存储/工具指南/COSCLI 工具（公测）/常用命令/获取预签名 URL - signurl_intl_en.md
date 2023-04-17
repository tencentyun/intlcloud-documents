The `signurl` command is used to get the pre-signed URL of an object, through which the object can be accessed anonymously.

## Command Syntax

```plaintext
./coscli signurl cos://<bucket-name>/<key> [flag]
```


`signurl` includes the following parameters:

| Parameter Format | Description | Example |
| ----------------- | -------------- | -------------------- |
|  cos://&lt;bucket-name&gt;/&lt;key&gt;  | Specifies the target object in the bucket, which is accessible by using the bucket alias or bucket name configured in the configuration file as detailed in [Download and Installation Configuration](https://intl.cloud.tencent.com/document/product/436/43265). If you use the bucket name for access, you also need to include the `endpoint` flag. | Access with the bucket alias: cos://example-alias/test.txt <br>Access with the bucket name: cos://examplebucket-1250000000/test.txt  |


The `signurl` command contains the following optional flags:

| Flag Abbreviation | Flag Name     | Description                         |
| --------- | ------------- | ---------------------------- |
| -h |  --help |   Views the usage of this command. |
| -t        | --time        | Sets the URL expiration time, which is 1000s by default |

>? For other common options of this command (such as switching bucket and user account), see [Common Options](https://www.tencentcloud.com/document/product/436/46273).
>

## Examples

### Getting the pre-signed URL of `picture.jpg` in `bucket1` bucket

```plaintext
./coscli signurl cos://bucket1/picture.jpg
```

### Getting the pre-signed URL of `picture.jpg` in `bucket2` bucket and setting the URL expiration time to 1314s

```plaintext
./coscli signurl cos://bucket2/picture.jpg --time 1314
```

