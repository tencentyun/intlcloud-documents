Curator is Elasticsearch's official tool for managing indices. It can perform a wide variety of index lifecycle management tasks, such as clearing indices created 7 days ago, backing up specified indices regularly every day, and migrating indices from a hot node to a cold node regularly. For more information on operations in Curator, see [here](https://www.elastic.co/guide/en/elasticsearch/client/curator/current/actions.html).

Curator provides a CLI which allows you to configure the tasks to be executed using parameters. It also comes with a complete set of Python APIs that can be used together with SCF.SCF has a pre-defined template for Curator, which can be run after simple parameter configuration. For more information on how to use SCF, see [here](https://intl.cloud.tencent.com/document/product/583).

## Curator Usage Example
The following describes how to configure and run Curator to delete expired indices regularly.

### Installation
Purchase a CVM instance in the VPC where your Elasticsearch cluster resides and install the Curator package via pip.
```
pip install elasticsearch-curator
```

### Running as command line parameters
The following command filters out the indices named in the format of `logstash-20xx-xx-xx` and created 7 days ago and then deletes them.

>The sample code performs a deletion operation to clear your data. Make sure that the above statement has been tested in a non-production environment. You can add the ```--dry-run``` parameter for testing purpose to avoid actually deleting data.

```
curator_cli --host 10.0.0.2:9200 --http_auth user:passwd delete_indices --filter_list '[{"filtertype": "pattern", "kind": "prefix", "value": "logstash-"}, {"filtertype": "age", "source": "name", "direction": "older", "timestring": "%Y.%m.%d", "unit": "days", unit_count: 7}]'
```

### Running as configuration files

If your operations are complex, there are a lot of parameters, or you don't want to use command line parameters, you can place the parameter in configuration files.
In the specified `config` directory, you need to edit the [config.yml](https://www.elastic.co/guide/en/elasticsearch/client/curator/5.6/configfile.html) and [action.yml](https://www.elastic.co/guide/en/elasticsearch/client/curator/current/actionfile.html?spm=a2c4g.11186623.2.15.246a2001E6EWcE) configuration files.
```
curator_cli --config PATH
```
### Scheduled run

If you need a scheduled run, you can configure the command to a crontab on Linux, or directly use the timer trigger feature of SCF mentioned above.

### Using the API
For more information on how to use the Python APIs, see [here](https://curator.readthedocs.io/en/latest/).
