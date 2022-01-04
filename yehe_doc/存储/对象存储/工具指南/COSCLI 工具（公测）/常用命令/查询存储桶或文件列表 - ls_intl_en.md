The `ls` command is used to query the list of buckets, objects in a bucket, and objects in a directory.

## Command Syntax

```plaintext
./coscli ls [cos://bucketAlias[/prefix/]] [flag]
```

>? For more information about `bucketAlias`, please see [Configuration Parameters](https://intl.cloud.tencent.com/document/product/436/43265).
>

`ls` includes the following optional parameters:

| Parameter Format | Description | Example |
| ----------------- | -------------- | -------------------- |
| cos://bucketAlias | Specifies a bucket. | cos://bucket1          |
| /prefix/          | Specifies a directory. | /picture/ |

`ls` includes the following optional flags:

| Flag Abbreviation | Flag Full Name   | Description                     |
| --------- | ----------- | ------------------------------------ |
| -h        | --help      | Outputs help information.       |
|  None  | --include   | Includes specific objects.  |
|  None  | --exclude   | Excludes specific objects.    |
| -r        | --recursive | Whether to traverse directories recursively and list all objects. |

>? 
> - `--include` and `--exclude` support standard regular expressions. You can use regular expressions to filter objects that meet your requirements.
> - When using `zsh`, you may need to enclose the pattern string with double quotation marks.
```plaintext
./coscli ls cos://bucket1 -r --include ".*.mp4"
```

## Examples


### Listing all buckets of the current account

```plaintext
./coscli ls
```

### Listing objects

#### Listing all objects in the `bucket1` bucket

```plaintext
./coscli ls cos://bucket1
```

#### Listing all objects and subdirectories in the `picture` directory in the `bucket1` bucket

```plaintext
./coscli ls cos://bucket1/picture/
```

#### Listing all objects in the `picture` directory in the `bucket1` bucket recursively

```plaintext
./coscli ls cos://bucket1/picture/ -r
```

#### Listing all MP4 objects in the `bucket1` bucket recursively

```plaintext
./coscli ls cos://bucket1 -r --include .*.mp4
```



#### Listing all non-MP4 objects in the `bucket1` bucket recursively

```plaintext
./coscli ls cos://bucket1 -r --exclude .*.mp4
```

#### Listing all non-JPG objects prefixed with `test` in the `picture` directory in the `bucket1` bucket

```plaintext
./coscli ls cos://bucket1/picture -r --include ^picture/test.* --exclude .*.jpg
```
