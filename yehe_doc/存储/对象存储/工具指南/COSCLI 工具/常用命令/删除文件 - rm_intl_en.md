The `rm` command is used to delete an object.

## Command Syntax

```plaintext
./coscli rm cos://<bucketAlias>[/prefix/] [cos://<bucket-name>[/prefix/]...] [flag]
```

>? For more information about `bucketAlias`, please see [Configurations](https://intl.cloud.tencent.com/document/product/436/43265).
>

`rm` includes the following optional flags:

| Flag Abbreviation | Flag Full Name   | Description                     |
| --------- | ------------- | ------------------------------------ |
| -h        | --help      | Outputs help information.       |
| -c        | --config-path | Path of the configuration file to use |
|  None  | --include   | Includes specific objects.  |
|  None  | --exclude   | Excludes specific objects.    |
| -r        | --recursive | Whether to traverse all objects in the directory recursively  |
| -f        | --force       | Forces delete (no prompt before the deletion). |

>?
> - `--include` and `--exclude` support standard regular expressions. You can use regular expressions to filter objects that meet your requirements.
> - When using `zsh`, you may need to enclose the pattern string with double quotation marks.
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
