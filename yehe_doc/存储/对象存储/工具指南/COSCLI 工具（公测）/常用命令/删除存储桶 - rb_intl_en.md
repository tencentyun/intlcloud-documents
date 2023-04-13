The `rb` command is used to delete a bucket.

## Command Syntax
```plaintext
./coscli rb cos://<bucket-name> [flag]
```

`rb` includes the following parameters:

| Parameter Format | Description | Example |
| --------- | ------------- | ------------------------ |
 cos://&lt;bucket-name&gt; | Specifies the target bucket, which is accessible by using the bucket alias or bucket name configured in the configuration file as detailed in [Download and Installation Configuration](https://intl.cloud.tencent.com/document/product/436/43265). If you use the bucket name for access, you also need to include the `endpoint` flag. | Access with the bucket alias: cos://example-alias <br>Access with the bucket name: cos://examplebucket-1250000000    |

`rb` includes the following optional flags:

| Flag Abbreviation | Flag Name     | Description                         |
| --------- | ------------- | ------------------------ |
| -h |  --help |   Views the usage of this command. |
| -r        | --region      | Indicates the region of the bucket.   |

>!
>- The `rb` command can only delete empty buckets. If there are files in your bucket, use the [rm](https://intl.cloud.tencent.com/document/product/436/43258) and [abort](https://intl.cloud.tencent.com/document/product/436/43261) commands to clear the files and incomplete multipart uploads in the bucket respectively and then delete the bucket.
>- After you run the `rb` command to delete the bucket successfully, we recommend that you delete the bucket information in the configuration file. For command usage, see the following example.
>- For more general options for this command (such as switching buckets or user accounts), see [Common Options](https://www.tencentcloud.com/document/product/436/46273).

## Example

```plaintext
// Delete the bucket3 bucket.
./coscli rb cos://bucket3-1250000000 -e cos.ap-chengdu.myqcloud.com
```

```plaintext
// Update the configuration file.
./coscli config delete -a bucket3
```
