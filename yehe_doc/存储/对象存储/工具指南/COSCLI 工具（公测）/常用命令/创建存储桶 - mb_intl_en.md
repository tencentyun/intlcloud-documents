The `mb` command is used to create a bucket.

## Command Syntax

```plaintext
./coscli mb cos://<BucketName-APPID> -r <Region> [flag]
```

`mb` includes the following optional flags:

| Flag Abbreviation | Flag Name     | Purpose                         |
| --------- | ------------- | ------------------------ |
| None | BucketName-APPID | Customizes the bucket name, such as `examplebucket-1250000000` |
| -r        | --region      | Region of the bucket   |

>! 
>- To use the `mb` command to create a bucket in COSCLI, you need to run the `config add` command to update the bucket configuration in the configuration file after running the `mb` command successfully.
>- For other common options of this command (such as switching bucket and user account), see [Common Options](https://intl.cloud.tencent.com/document/product/436/46273).
>

## Examples

```plaintext
// Create the bucket3 bucket.
./coscli mb cos://bucket3-1250000000 -r ap-chengdu
// Update the configuration file.
./coscli config add -b bucket3-1250000000 -r ap-chengdu -a bucket3
// After the update, you can access the bucket at cos://bucket3.
```
