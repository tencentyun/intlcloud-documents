## Default template description

An index template is a predefined template that is automatically applied when a new index is created. It typically contains configuration items for index settings, mapping, and template priority. ES offers a default index template for cluster creation, which can be viewed by running the `GET _template/default@template` command in **Dev Tools** on the Kibana page. The following describes the default template and its configuration items, which can be adjusted based on your actual needs.

```
{
  "default@template": {
    "order": 1, // Priority of the template. The greater the value, the higher the priority
    "index_patterns": [ // Index to which the template is applied
      "*"
    ],
    "settings": {
      "index": {
        "max_result_window": "65536", // Maximum query result window. If the result quantity exceeds this value, error message "Result window is too large" will be displayed, and you will need to increase this value
        "routing": {
          "allocation": {
            "include": {
              "temperature": "hot"
            }
          }
        },
        "refresh_interval": "30s", // Index refresh interval. The indexed document can only be queried after the interval elapses. If you have high requirement for real-time query, you can properly reduce this value, but a too small value will compromise the write performance
        "unassigned": {
          "node_left": {
            "delayed_timeout": "5m"
          }
        },
        "translog": {
          "sync_interval": "5s", // translog flush interval. A too small value will compromise the write performance
          "durability": "async" 
        },
        "number_of_replicas": "1" // Number of replica shards
      }
    },
    "mappings": {
      "_default_": {
        "_all": {
          "enabled": false // It is recommended to set this parameter to disabled. The `_all` field contains all other fields to form a large string, which will take up a lot of disk space and compromise the write performance
        },
        "dynamic_templates": [ // Dynamic template
          {
            "message_full": { // Dynamically map the field named `message_full` to `text` and `keyword` types
              "match": "message_full",
              "mapping": {
                "type": "text",
                "fields": {
                  "keyword": {
                    "type": "keyword",
                    "ignore_above": 2048
                  }
                }
              }
            }
          },
          {
            "message": { // Dynamically map the field named `message` to `text` type
              "match": "message",
              "mapping": {
                "type": "text"
              }
            }
          },
          {
            "strings": { // Dynamically map a field of `string` type to `keyword` type
              "match_mapping_type": "string",
              "mapping": {
                "type": "keyword"
              }
            }
          }
        ]
      }
    },
    "aliases": {}
  }
}
```

## Template adjustment

You can create your own custom index template by running the `PUT _template/my_template` command in **Dev Tools** on the Kibana page. Then, you can overwrite the configurations in the default index template by setting the `order` parameter of your own template to be greater than that of the default template.

>The index template is only applied when an index is created; therefore, template adjustment will not affect existing indices.

### Adjusting the number of primary shards

In Elasticsearch 5.6.4 and 6.4.3, an index has 5 primary shards by default. For scenarios with a small data size and a large number of indices, you are recommended to lower the number of primary shards so as to reduce the pressure of index metadata on the heap memory. You can do so by referring to the following template:

```
{
  "index_patterns" : ["*"],
    "order" : 2, // Make sure that the value of the `order` field in the template is greater than 1
    "settings" : {
        "index": {
            "number_of_shards" : 1
        }
    }
}
```

### Adjusting field type

In the default template, fields of `string` type are dynamically mapped to `keyword` type in order to prevent full-text indexing of all the data of `text` type. You can modify the specified fields of `string` type to `text` based on your business needs to allow full-text indexing:

```
{
  "index_patterns" : ["*"],
    "order" : 2, // Make sure that the value of the `order` field in the template is greater than 1
    "mappings": {
      "properties": {
        "Field name": {
          "type":  "text"
        }
    }
  }
}
```

### Other business scenarios

For example, if you want that a document can be searched for 10 seconds after being indexed by any ` search-*` index, you can create a template as shown below:

```
{
    "index_patterns" : ["search-*"],
    "order" : 2, // Make sure that the value of the `order` field in the template is greater than 1
    "settings" : {
        "index": {
            "refresh_interval": "10s"
        }
    }
}
```

