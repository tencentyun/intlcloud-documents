You can view the common options supported by COSCLI with the `./coscli --help` or `./coscli -h` command.

## Option Description
The following are common options for COSCLI, which can be used in all its commands:

>!
>- We recommend you use a temporary key as instructed in [Generating and Using Temporary Keys](https://intl.cloud.tencent.com/document/product/436/14048) to call the SDK for security purposes. When you apply for a temporary key, follow the [Notes on Principle of Least Privilege](https://intl.cloud.tencent.com/document/product/436/32972) to avoid leaking resources besides your buckets and objects.
>- If you must use a permanent key, we recommend you follow the [Notes on Principle of Least Privilege](https://intl.cloud.tencent.com/document/product/436/32972) to limit the scope of permission on the permanent key.


| Option | Description |
|  ----  | ----  |
|-h, --help| Outputs help information. You can view the help information and usage of the tool with the `-h` or `--help` command. You can also enter `-h` after each command (with no parameter appended) to see how to use the command. For example, to view the specific usage of the bucket creation command, enter `coscli mb -h`. |
|-c, --config-path| Configuration file path, which is `~/.cos.yaml` for COSCLI by default. You can also specify a custom configuration file by adding `-c` after a command. |
|-e, --endpoint   | In addition to configuring the region of a bucket in advance in the configuration file, you can also use `-e` in COSCLI to specify the bucket endpoint in the format of `cos.<region>.myqcloud.com`, where `<region>` represents the bucket region, such as `ap-guangzhou` and `ap-beijing`. For the list of regions supported by COS, see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). |
|-i, --secret-id  | Specifies the `SecretId` used to access COS. |
|-k, --secret-key  | Specifies the `SecretKey` used to access COS. |
|-t, --session-token | If you access COS with a temporary key, you can use `-t` to specify its token. |
|-v, --version | Displays the COSCLI version. |

## Examples

### Example 1: Switching bucket to upload an object


When you need to switch to a bucket in another region through COSCLI, you can use the `-e` option to specify the endpoint of the bucket.

For example, to upload the local file `test.txt` to the bucket `examplebucket-1250000000` in the Chengdu region with the endpoint `cos.ap-chengdu.myqcloud.com`, run the following command:
```
./coscli cp test.txt cos://examplebucket-1250000000/test.txt -e cos.ap-chengdu.myqcloud.com
```

### Example 2: Switching user account to view the file list

When you need to use the identity of another account, you can use the `-i` and `-k` options to specify the `SecretId` and `SecretKey` of your key respectively.

For example, to use the identity of another account to list the files in the bucket `examplebucket-1250000000` in the Chengdu region, run the following command:

```
./coscli ls cos://examplebucket-1250000000 -e cos.ap-chengdu.myqcloud.com -i AKIDYv3vWrwkHXVDfqkNjoc9PP8anjOm**** -k 4rNbYF1XmmVw67rKWTBernUu66u****
```
