The `rm` command is used to delete an object.

## Command Syntax

```plaintext
./coscli rm cos://<bucket-name>[/prefix/] [flag]
```


`rm` includes the following parameters:

| Parameter Format | Description | Example |
| --------- | ------------- | ------------------------ |
| cos://&lt;bucket-name&gt; | Specifies the target bucket, which is accessible by using the bucket alias or bucket name configured in the configuration file as detailed in [Download and Installation Configuration](https://intl.cloud.tencent.com/document/product/436/43265). If you use the bucket name for access, you also need to include the `endpoint` flag. | Access with the bucket alias: cos://example-alias <br>Access with the bucket name: cos://examplebucket-1250000000    |
| /prefix/          | Specifies a directory (optional). | /picture/ |

`rm` includes the following optional flags:

| Flag Abbreviation | Flag Name     | Description                         |
| --------- | ------------- | ------------------------------------ |
| -h |  --help |   Views the usage of this command. |
|     None      | --include     | Includes specific objects.                  |
|     None      | --exclude     | Excludes specific objects.                |
| -r        | --recursive | Specifies whether to traverse all objects in the directory recursively.  |
| -f        | --force       | Forces deletion (no prompt before the deletion). |

>?
> - `--include` and `--exclude` support standard regular expression syntax, so you can use them to filter out objects that meet specific criteria.
> - When using `zsh`, you may need to add double quotes at both ends of the `pattern` string.
```
./coscli rm cos://bucket1/example/ -r --include ".*.mp4"
```
>- For more general options for this command (such as switching buckets or user accounts), see [Common Options](https://www.tencentcloud.com/document/product/436/46273).


## Example

### Deleting an object

```plaintext
./coscli rm cos://bucket1/fig1.png
```

### Deleting all objects in the `picture` directory

```plaintext
./coscli rm cos://bucket1/pictrue/ -r
```
