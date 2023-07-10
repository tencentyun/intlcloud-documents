
## Command Syntax

The `config` command is used to generate and modify the configuration file.

```
./coscli config [command] [flag]
```

>? 
>- After setting the configuration items correctly, you can run `./coscli config show` to view the configuration.
>- For more general options for this command (such as switching buckets or user accounts), see [Common Options](https://www.tencentcloud.com/document/product/436/46273).
>- The generated configuration file uses the HTTPS protocol by default. If you want to change it to HTTP, directly modify it in the configuration file.

<span id="config"></span>

`config` includes the following sub-commands:

| Command | Description |
| ------------ | ------------------------------------------ |
| add          | Adds a new bucket configuration.      |
| delete       | Deletes an existing bucket configuration.       |
| init         | Generates the configuration file interactively.     |
| set          | Modifies one or more configuration items in the base group of the configuration file, which contains `secretid`, `secretkey`, and `sessiontoken`. |
| show         | Prints information in a specific configuration file.  | 

`config` and its sub-commands include the following optional flags:

| Flag Abbreviation | Flag Name     | Description                         |
| --------- | ------------- | -------------------------- |
| -h |  --help |   Views the usage of this command. |
| -c        | --config-path | Path of the configuration file to use |

The `config add` sub-command includes the following optional flags:

| Flag Abbreviation | Flag Name   | Description                     |
| --------- | --------- | ------------ |
| -h |  --help |   Views the usage of this command. |
| -a        | --alias   | Bucket alias |
| -b        | --bucket  | Bucket name |
| -r        | --region      | Region of the bucket   |
| -o |  --ofs |   Metadata acceleration bucket flag. For more information, see [Metadata Acceleration Overview](https://intl.cloud.tencent.com/document/product/436/43305).  |

>! If you want to specify the endpoint of the bucket, use the common flag `-e` or `--endpoint`. For more information, see [Common Options](https://intl.cloud.tencent.com/document/product/436/46273).

The `config delete` sub-command includes the following optional flags:

| Flag Abbreviation | Flag Name   | Description                     |
| --------- | --------- | ------------ |
| -h |  --help |   Views the usage of this command. |
| -a        | --alias   | Bucket alias |

The `config set` sub-command includes the following optional flags:

| Flag Abbreviation | Flag Name   | Description                     |
| --------- | ------------ | ----------------- |
| -h |  --help |   Views the usage of this command. |
| None      | --secret_id  | Sets the secret ID, which can be created and obtained from the [CAM console](https://console.cloud.tencent.com/cam/capi).   |
| None       | --secret_key | Sets the secret key, which can be created and obtained from the [CAM console](https://console.cloud.tencent.com/cam/capi).   |
| -t        | --session_token      | Sets the temporary key token. For more information on temporary key, see [Accessing COS Using a Temporary Key](https://intl.cloud.tencent.com/document/product/436/45242).  |

## Examples

### Adding a new bucket configuration

```
./coscli config add -b examplebucket3-1250000000 -r ap-chengdu -e cos.ap-chengdu.myqcloud.com -a bucket3
```

### Deleting an existing bucket configuration

```
./coscli config delete -a bucket3
```

### Modifying `session-token` in the default configuration file

```
./coscli config set --session_token test-token123
```

### Printing information in a specific configuration file

```
./coscli config show -c /your/config/path.yaml
```
