The `rm` command is used to delete an object.

## Command Syntax

```plaintext
./coscli rm cos://<bucketAlias>[/prefix/] [cos://<bucket-name>[/prefix/]...] [flag]
```

>? 
>- For more information on `bucketAlias`, see [Download and Installation Configuration](https://intl.cloud.tencent.com/document/product/436/43265).
>- For more general options for this command (such as switching buckets or user accounts), see [General Options](https://intl.cloud.tencent.com/document/product/436/46273).
>

`rm` includes the following optional flags:

| Flag Abbreviation | Flag Full Name     | Description                         |
| --------- | ------------- | ------------------------------------ |
|     None      | --include     | Includes specific objects.                  |
|     None      | --exclude     | Excludes specific objects.                |
| -r        | --recursive | Specifies whether to traverse all objects in the directory recursively.  |
| -f        | --force       | Forces deletion (no prompt before the deletion). |

>?
> - `--include` and `--exclude` support standard regular expression syntax, so you can use them to filter files that meet specific criteria.
> - When using `zsh`, you may need to add double quotes at both ends of the `pattern` string.
```
./coscli rm cos://bucket1/example/ -r --include ".*.mp4"
```

## Examples

### Deleting an object

```plaintext
./coscli rm cos://bucket1/fig1.png
```

### Deleting all objects in the `picture` directory

```plaintext
./coscli rm cos://bucket1/pictrue/ -r
```
