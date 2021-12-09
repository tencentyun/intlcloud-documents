The `restore` command is used to retrieve archived files.

## Command Format


```plaintext
./coscli restore cos://<bucketAlias>[/prefix/] [flag]
```

>? For more information on `bucketAlias`, please see [Configuration](https://intl.cloud.tencent.com/document/product/436/43265).
>

The `restore` command contains the following optional flags:

| Flag Abbreviation | Flag Name     | Purpose                         |
| --------- | ------------- | --------------------------------- |
| -h        | --help        | Outputs help information                      |
| -c        | --config-path | Specifies the path of the configuration file to be used          |
|     None      | --include     | Includes files with a specific pattern                |
|     None      | --exclude     | Excludes files with a specific pattern                |
| -d        | --days        | Specifies the expiration time of temporary files, which is 3 days by default |
| -m        | --mode        | Specifies the restoration mode, which is `Standard` by default      |
| -r        | --recursive   | Traverses the folder recursively                  |

>?
> - `--include` and `--exclude` support standard regular expression syntax, so you can use them to filter files that meet specific criteria.
> - When using `zsh`, you may need to add double quotes at both ends of the `pattern` string.
```
./coscli restore cos://bucket1/example/ -r --include ".*.mp4"
```

## Example

### Retrieving archived files in `bucket1` bucket in Standard mode

```plaintext
./coscli restore cos://bucket1/picture.jpg
```

### Retrieving all archived files in `picture` folder in `bucket1` bucket in Expedited mode

```plaintext
./coscli restore cos://bucket1/picture/ -r --mode Expedited
```

>? Before running this command, you need to make sure that all files in the folder are of the same storage class (such as ARCHIVE). If there are files in different classes, use `--include` or `--exclude` to filter out files in the same class.
>

