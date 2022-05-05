The `rb` command is used to delete a bucket.

## Command Syntax

```plaintext
./coscli rb cos://<BucketName-APPID> -r <Region> [flag]
```

`rb` includes the following optional flags:

| Flag Abbreviation | Flag Full Name     | Description           |
| --------- | ------------- | ------------------------ |
| None | BucketName-APPID | Specifies the name of the bucket to be deleted, such as `examplebucket-1250000000` |
| -r        | --region      | Region of the bucket   |

>? For other common options of this command (such as switching bucket and user account), see [Common Options](https://intl.cloud.tencent.com/document/product/436/46273).
>
## Examples

```plaintext
// Delete the bucket3 bucket.
./coscli rb cos://bucket3-1250000000 -r ap-chengdu
// Update the configuration file.
./coscli config delete -a bucket3
```
