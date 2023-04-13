The `restore` command is used to restore archived objects.
>! For more information on retrieving archived files, see [POST Object restore](https://intl.cloud.tencent.com/document/product/436/12633).

## Command Syntax

```plaintext
./coscli restore cos://<bucket-name>[/prefix/] [flag]
```


`restore` includes the following parameters:

| Parameter Format | Description | Example |
| --------- | ------------- | ------------------------ |
 cos://&lt;bucket-name&gt; | Specifies the target bucket, which is accessible by using the bucket alias or bucket name configured in the configuration file as detailed in [Download and Installation Configuration](https://intl.cloud.tencent.com/document/product/436/43265). If you use the bucket name for access, you also need to include the `endpoint` flag. | Access with the bucket alias: cos://example-alias <br>Access with the bucket name: cos://examplebucket-1250000000    |
| /prefix/          | Specifies a directory (optional). | /picture/ |

The `restore` command contains the following optional flags:

| Flag Abbreviation | Flag Name     | Description                         |
| --------- | ------------- | --------------------------------- |
| -h |  --help |   Views the usage of this command. |
|     None      | --include     | Includes specific objects.                  |
|     None      | --exclude     | Excludes specific objects.                |
| -d        | --days        | Specifies the expiration time of the temporary file generated during object restoration, which is 3 days by default. |
| -m        | --mode        | Specifies the restoration mode, which is `Standard` by default      |
| -r        | --recursive   | Traverses the folder recursively.                  |

>?
> - `--include` and `--exclude` support standard regular expression syntax, so you can use them to filter out objects that meet specific criteria.
> - When using `zsh`, you may need to add double quotes at both ends of the `pattern` string.
```
./coscli restore cos://bucket1/example/ -r --include ".*.mp4"
```
>- For more general options for this command (such as switching buckets or user accounts), see [Common Options](https://www.tencentcloud.com/document/product/436/46273).


## Examples

### Restoring archived objects in `bucket1` bucket in Standard mode

```plaintext
./coscli restore cos://bucket1/picture.jpg
```

### Restoring all archived objects in `picture` folder in `bucket1` bucket in Expedited mode

```plaintext
./coscli restore cos://bucket1/picture/ -r --mode Expedited
```

>? Before running this command, you need to make sure that all objects in the folder are of the same storage class (such as ARCHIVE). If there are objects in different classes, use `--include` or `--exclude` to filter out objects in the same class.
>

