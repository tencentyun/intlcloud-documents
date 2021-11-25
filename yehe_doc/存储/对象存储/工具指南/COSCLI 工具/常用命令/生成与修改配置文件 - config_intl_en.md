
## Command Syntax

The `config` command is used to generate and modify the configuration file.

```
./coscli config [command] [flag]
```

>? If you have set the configuration items correctly, you can run `./coscli config show` to view the configurations.
>

<span id="config"></span>

`config` includes the following sub-commands:

| Command | Description |
| ------------ | ------------------------------------------ |
| add          | Adds a new bucket configuration.      |
| delete       | Deletes an existing bucket configuration.       |
| init         | Generates the configuration file interactively.     |
| set          | Modifies one or more configuration items in the base group of the configuration file. |
| show         | Prints information in a specific configuration file.  |

`config` and its sub-commands include the following optional flags:

| Flag Abbreviation | Flag Full Name   | Description                     |
| --------- | ------------- | -------------------------- |
| -h        | --help      | Outputs help information.       |
| -c        | --config-path | Path of the configuration file to use |

The `config add` sub-command includes the following optional flags:

| Flag Abbreviation | Flag Full Name   | Description                     |
| --------- | --------- | ------------ |
| -a        | --alias   | Bucket alias |
| -b        | --bucket  | Bucket name |
| -r        | --region      | Region of the bucket   |

The `config delete` sub-command includes the following optional flags:

| Flag Abbreviation | Flag Full Name   | Description                     |
| --------- | --------- | ------------ |
| -a        | --alias   | Bucket alias |

The `config set` sub-command includes the following optional flags:

| Flag Abbreviation | Flag Full Name   | Description                     |
| --------- | ------------ | ----------------- |
| -i        | --secret_id  | Secret ID  |
| -k        | --secret_key | Secret key |
| -t        | --token      | Token     |

## Examples

### Adding a new bucket configuration

```
./coscli config add -b examplebucket3-1250000000 -r ap-chengdu -a bucket3
```

### Deleting an existing bucket configuration

```
./coscli config delete -a bucket3
```

### Modifying `session-token` in the default configuration file

```
./coscli config set -t test-token123
```

### Printing information in a specific configuration file

```
./coscli config show -c /your/config/path.yaml
```
