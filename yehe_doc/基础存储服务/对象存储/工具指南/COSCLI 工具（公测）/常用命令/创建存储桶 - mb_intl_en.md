The `mb` command is used to create a bucket.

## Command Syntax

```plaintext
./coscli mb cos://<BucketName-APPID> -e <endpoint> [flag]
```

>! To create a bucket with the `mb` command, you need to add the global flag `-e` or `--endpoint` to specify the region where the bucket resides.

`mb` includes the following parameters:

| Parameter Format | Description | Example |
| --------- | ------------- | ------------------------ |
| cos://&lt;BucketName-APPID&gt; | Customizes the bucket name |cos://examplebucket-1250000000  |


`mb` includes the following optional flags:

| Flag Abbreviation | Flag Name     | Description                         |
| --------- | ------------- | ------------------------ |
| -h |  --help |   Views the usage of this command. |
| -r        | --region      | Indicates the region of the bucket   |

>! 
>- After you run the `mb` command to successfully create a bucket, we recommend that you add information about the bucket in the configuration file, so that you can use the bucket alias for quick operations. For command usage, see the following example.
>- For more general options for this command (such as switching buckets or user accounts), see [Common Options](https://www.tencentcloud.com/document/product/436/46273).
>

## Examples

```plaintext
// Create the bucket3 bucket.
./coscli mb cos://bucket3-1250000000 -e cos.ap-chengdu.myqcloud.com
```

If you want to configure an alias for the bucket you just created, update the configuration file with the following command:

```plaintext
// Update the configuration file.
./coscli config add -b bucket3-1250000000 -e cos.ap-chengdu.myqcloud.com -a bucket3
// After the update, you can access the bucket at cos://bucket3.
```
