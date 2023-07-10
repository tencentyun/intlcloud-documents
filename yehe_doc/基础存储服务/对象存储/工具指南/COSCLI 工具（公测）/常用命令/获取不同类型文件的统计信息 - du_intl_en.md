
The `du` command is used to list the statistics (total number and size) of files of each storage class in a bucket or a directory.

## Command Syntax
```plaintext
./coscli du cos://<bucket-name>[/prefix/] [flag]
```


`du` includes the following parameters:

| Parameter Format | Description | Example |
| ----------------- | -------------- | -------------------- |
| cos://&lt;bucket-name&gt; | Specifies the target bucket, which is accessible by using the bucket alias or bucket name configured in the configuration file as detailed in [Download and Installation Configuration](https://intl.cloud.tencent.com/document/product/436/43265). If you use the bucket name for access, you also need to include the `endpoint` flag. | Access with the bucket alias: cos://example-alias <br>Access with the bucket name: cos://examplebucket-1250000000    |
| /prefix/          | Specifies a directory (optional). | /picture/ |


`du` includes the following optional flags:

| Flag Abbreviation | Flag Name     | Description                         |
| --------- | ------------- | ------------------------ |
| -h |  --help |   Views the usage of this command. |
|  None  | --include   | Includes specific objects.  |
|  None  | --exclude   | Excludes specific objects.    |

>? 
>- `--include` and `--exclude` support standard regular expression syntax, so you can use them to filter out objects that meet specific criteria.
> - When using `zsh`, you may need to enclose the pattern string with double quotation marks.
```plaintext
./coscli du cos://bucket1/picture/ --include ".*.mp4"
```
>- For more general options for this command (such as switching buckets or user accounts), see [Common Options](https://www.tencentcloud.com/document/product/436/46273).



## Examples

### Listing statistics on objects in the `bucket1` bucket

```plaintext
./coscli du cos://bucket1
```

The returned information includes the number and size of objects in different storage classes, total number of objects, and total object size in the bucket. Below is an example:

```plaintext
       STORAGE CLASS      | OBJECTS COUNT | TOTAL SIZE
--------------------------+---------------+-------------
                 STANDARD |             2 |     164  B
              STANDARD_IA |             0 |       0  B
      INTELLIGENT_TIERING |             0 |       0  B
                  ARCHIVE |             0 |       0  B
             DEEP_ARCHIVE |             0 |       0  B
             MAZ_STANDARD |             0 |       0  B
          MAZ_STANDARD_IA |             0 |       0  B
  MAZ_INTELLIGENT_TIERING |             0 |       0  B
              MAZ_ARCHIVE |             0 |       0  B
--------------------------+---------------+-------------
INFO[2022-12-14 17:35:41] Total Objects Count: 2
INFO[2022-12-14 17:35:41] Total Objects Size:  164  B
```

### Listing statistics on objects in the `picture` directory in the `bucket1` bucket

```plaintext
./coscli du cos://bucket1/picture/
```

### Listing statistics on all MP4 objects in the `picture` directory in the `bucket1` bucket

```plaintext
./coscli du cos://bucket1/picture/ --include .*.mp4
```

### Listing statistics on all non-MD objects in the `picture` directory in the `bucket1` bucket

```plaintext
./coscli du cos://bucket1/picture/ --exclude .*.md
```
