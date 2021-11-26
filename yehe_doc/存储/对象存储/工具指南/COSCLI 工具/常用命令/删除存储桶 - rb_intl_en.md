The `rb` command is used to delete a bucket.

## Command Syntax

```plaintext
./coscli rb cos://<BucketName-APPID> -r <Region> [flag]
```

`rb` includes the following optional flags:

| Flag Abbreviation | Flag Full Name   | Description                     |
| --------- | ------------- | ------------------------ |
| -h        | --help      | Outputs help information.       |
| -c        | --config-path | Path of the configuration file to use |
| -r        | --region      | Region of the bucket   |

## Examples

```plaintext
// Delete the bucket3 bucket.
./coscli rb cos://bucket3-1250000000 -r ap-chengdu
// Update the configuration file.
./coscli config delete -a bucket3
```
