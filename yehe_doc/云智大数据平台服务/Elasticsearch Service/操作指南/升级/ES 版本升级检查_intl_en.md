Different versions of Elasticsearch have certain incompatible configuration items, and if you have set such items, an upgrade may affect the use of your cluster. You can use the upgrade check feature to check whether there are any incompatible configuration items and change them accordingly. The following describes the check to be performed when upgrading the Elasticsearch version.

On the details page in the [console](https://console.cloud.tencent.com/es), click **Upgrade** in the top-right corner. For detailed directions, please see [Upgrading ES Clusters](https://intl.cloud.tencent.com/document/product/845/32600).

>= You should pay special attention to the configuration items that need to be checked manually (they cannot be checked automatically) in this document and complete compatibility transformation for your code before the upgrade to ensure that clusters can be accessed normally after the upgrade. For example, after v6.8 is upgraded to v7.5, indices containing `type` cannot be created. For more information, please see [Incompatible configuration items to be checked manually](#jump1).


## Configuration Check for Elasticsearch Upgrade from 5.x to 6.x
### Checklist of configuration items

| No. | Configuration Level | Configuration Information | Compatibility | Description |
| ---- | ---------- | --------------------------------------------------- | -------- | ------------------------------------------ |
| 1 | Cluster | Snapshot settings | CRITICAL | The `cluster.routing.allocation.snapshot.relocation_enabled` setting has been disused since v6.0. For more information, please see [Breaking changes in 6.0](https://www.elastic.co/guide/en/elasticsearch/reference/6.0/breaking_60_settings_changes.html#_store_settings) |
| 2 | Cluster | Store throttling settings | CRITICAL | The `indices.store.throttle.type` and `indices.store.throttle.max_bytes_per_sec` settings have been disused since v6.0. For more information, please see [Breaking changes in 6.0](https://www.elastic.co/guide/en/elasticsearch/reference/6.0/breaking_60_settings_changes.html#_store_throttling_settings) |
| 3 | Index | Similarity settings | WARNING | The `index.similarity.base` setting has been disused since v6.0. For more information, please see [Breaking changes in 6.0](https://www.elastic.co/guide/en/elasticsearch/reference/6.0/breaking_60_settings_changes.html#_similarity_settings) |
| 4 | Index | Shadow replicas settings | CRITICAL | The `index.shared_filesystem` and `index.shadow_replicas` settings have been disused since v6.0. For more information, please see [Breaking changes in 6.0](https://www.elastic.co/guide/en/elasticsearch/reference/6.0/breaking_60_indices_changes.html#_shadow_replicas_have_been_removed) |
| 5 | Index | Index store settings | CRITICAL | The `default` `index.store.type` has been disused since v6.0. For more information, please see [Breaking changes in 6.0](https://www.elastic.co/guide/en/elasticsearch/reference/6.0/breaking_60_settings_changes.html#_store_settings) |
| 6 | Index | Index store throttling settings | CRITICAL | The `index.store.throttle.type` and `index.store.throttle.max_bytes_per_sec` settings have been disused since v6.0. For more information, please see [Breaking changes in 6.0](https://www.elastic.co/guide/en/elasticsearch/reference/6.0/breaking_60_settings_changes.html#_store_throttling_settings) |
| 7 | Index | `include_in_all` index mapping parameter | WARNING | The `include_in_all` mapping parameter cannot be used in indices on v6.0 or above (indices created by v5.x which contain this setting will be compatible after upgrade to v6.x). For more information, please see [Breaking changes in 6.0](https://www.elastic.co/guide/en/elasticsearch/reference/6.0/breaking_60_mappings_changes.html#_the_literal_include_in_all_literal_mapping_parameter_is_now_disallowed) |
| 8 | Index | `index.version.created` | CRITICAL | `index.version.created` cannot be used across major Elasticsearch versions. For example, you cannot directly upgrade indices created on v5.x to v7.x; instead, you have to [reindex](https://www.elastic.co/guide/en/elasticsearch/reference/6.4/docs-reindex.html) the failed indices to new ones and delete them before upgrading |
| 9 | Index template | Similarity settings | CRITICAL | The `index.similarity.base` setting has been disused since v6.0. For more information, please see [Breaking changes in 6.0](https://www.elastic.co/guide/en/elasticsearch/reference/6.0/breaking_60_settings_changes.html#_similarity_settings). If this item is in the template, the template cannot be used to create indices after the upgrade |
| 10 | Index template | Shadow replicas settings | CRITICAL | The `index.shared_filesystem` and `index.shadow_replicas` settings have been disused since v6.0. For more information, please see [Breaking changes in 6.0](https://www.elastic.co/guide/en/elasticsearch/reference/6.0/breaking_60_indices_changes.html#_shadow_replicas_have_been_removed). If this item is in the template, the template cannot be used to create indices after the upgrade |
| 11 | Index template | Index store settings | CRITICAL | The `default` `index.store.type` has been disused since v6.0. For more information, please see [Breaking changes in 6.0](https://www.elastic.co/guide/en/elasticsearch/reference/6.0/breaking_60_settings_changes.html#_store_settings). If this item is in the template, the template cannot be used to create indices after the upgrade |
| 12 | Index template | Index store throttling settings | CRITICAL | The `index.store.throttle.type` and `index.store.throttle.max_bytes_per_sec` settings have been disused since v6.0. For more information, please see [Breaking changes in 6.0](https://www.elastic.co/guide/en/elasticsearch/reference/6.0/breaking_60_settings_changes.html#_store_throttling_settings). If this item is in the template, the template cannot be used to create indices after the upgrade |
| 13 | Index template | `include_in_all` mapping parameter | CRITICAL | The `include_in_all` mapping parameter has been disused since v6.0. For more information, please see [Breaking changes in 6.0](https://www.elastic.co/guide/en/elasticsearch/reference/6.0/breaking_60_mappings_changes.html#_the_literal_include_in_all_literal_mapping_parameter_is_now_disallowed). If this item is in the template, the template cannot be used to create indices after the upgrade |
| 14 | Index template | `_all` mapping metafield | CRITICAL | The `_all` mapping metafield has been disused since v6.0. For more information, please see [Breaking changes in 6.0](https://www.elastic.co/guide/en/elasticsearch/reference/6.0/breaking_60_mappings_changes.html#_the_literal__all_literal_meta_field_is_now_disabled_by_default). If this item is in the template, the template cannot be used to create indices after the upgrade |
| 15 | Index template | Mapping types | CRITICAL | Multiple mapping types have been disused since v6.0. For more information, please see [Removal of mapping types](https://www.elastic.co/guide/en/elasticsearch/reference/6.0/removal-of-types.html#removal-of-types). If this item is in the template, the template cannot be used to create indices after the upgrade |

>
> - WARNING: upgrade can still be performed even if the check fails. The settings for this type of check items will be ignored after the upgrade.
> - CRITICAL: upgrade cannot be performed if the check fails. The settings for this type of check items are incompatible in the target version.

### How to change incompatible configuration items
#### Cluster level
- Snapshot settings
You can cancel these settings (including persistent and transient) through the ES cluster settings update API (`PUT _cluster/settings`):
```
PUT _cluster/settings
{
    "persistent": {
      "cluster.routing.allocation.snapshot.relocation_enabled": null
    },
    "transient": {
      "cluster.routing.allocation.snapshot.relocation_enabled": null
    }
}
```
- Store throttling settings
You can cancel these settings (including persistent and transient) through the ES cluster settings update API (`PUT _cluster/settings`):
```
PUT _cluster/settings
{
    "persistent": {
      "indices.store.throttle.type": null,
      "indices.store.throttle.max_bytes_per_sec": null
    },
    "transient": {
      "indices.store.throttle.type": null,
      "indices.store.throttle.max_bytes_per_sec": null
    }
}
```

#### Index level
- Similarity settings 
These settings will be ignored after upgrade to 6.x, which will not affect the upgrade though. To cancel them, follow the steps below:
 - The index needs to be closed before you modify these settings, and the closed index cannot be read or written. Close the index:
```
POST my_index/_close
```
 - Cancel these settings through the ES index settings update API:
```
PUT my_index/_settings
{
       "index.similarity.base.*": null
}
```
 - Then, open the index by running the following command:
```
POST my_index/_open
```
- Shadow replicas settings
 - The index needs to be closed before you modify these settings, and the closed index cannot be read or written. Close the index:
```
POST my_index/_close
```
 - Cancel these settings through the ES index settings update API:
```
PUT my_index/_settings
{
        "index.shared_filesystem": null,
        "index.shadow_replicas": null
}
```
 - Then, open the index by running the following command:
```
POST my_index/_open
```
- Index store settings
 - The index needs to be closed before you modify these settings, and the closed index cannot be read or written. Close the index:
```
POST my_index/_close
```
 - Cancel these settings through the ES index settings update API:
```
PUT my_index/_settings
{
       "index.store.type": null
}
```
 - Then, open the index by running the following command:
```
POST my_index/_open
```
- Index store throttling settings
  Cancel these settings through the ES index settings update API:
```
PUT my_index/_settings
{
    "settings": {
      "index.store.throttle.type": null,
      "index.store.throttle.max_bytes_per_sec": null
    }
}
```
- `include_in_all` index mapping parameter
A previously created index containing this parameter is compatible after the upgrade and does not need to be repaired.


#### **Index template level**
1. Use the `GET _template/my_template` API to get the incompatible template `my_template`. There are three incompatible items: index store settings, index template mapping parameter (`include_in_all`), and index template mapping metafield (`_all`).
```
  {
    "my_template": {
      "order": 0,
      "template": "my_*",
      "settings": {
        "index": {
          "store": {
            "throttle": {
              "max_bytes_per_sec": "10m"
            }
          }
        }
      },
      "mappings": {
        "my_type": {
          "_all": {
            "enabled": true
          },
          "properties": {
            "my_field": {
              "type": "text",
              "include_in_all": true
            }
          }
        }
      },
      "aliases": {}
    }
  }
```
2. After copying and removing incompatible configuration items from the template, use the `PUT _template/my_template` API to update the template.
```
  PUT _template/my_template
  {
      "order": 0,
      "template": "my_*",
      "settings": {
      },
      "mappings": {
        "my_type": {
          "properties": {
            "my_field": {
              "type": "text"
            }
          }
        }
      },
      "aliases": {}
  }
```


## Configuration Check for Elasticsearch Upgrade from 6.8 to 7.x
### <span id="jump1">Incompatible configuration items to be checked manually</span>

- For indices containing more than 1,024 fields, performance costs will be high if no fields are specified during query. You are recommended to set the default query field `index.query.default_field`. If you still want to query all fields, you can increase the "maximum number of clauses in boolean query" by setting `indices.query.bool.max_clause_count`.
- `include_type_name` is `false` by default. Indices containing `type` cannot be created by default after the upgrade. You need to explicitly specify the parameter `include_type_name`:
>= You should check whether your clusters have this incompatible configuration item so as to ensure that clusters can be accessed normally after the upgrade.
> 
```
   PUT my_index?include_type_name
   {
     "mappings": {
       "type1": {
         "properties": {
           "name": {
             "type": "text"
           }
         }
       }
     }
   }
```

### Checklist of automatically checked configuration items

| No. | Configuration Level | Configuration Information | Compatibility | Description |
| ---- | -------- | -------------------------------------------- | -------- | ------------------------------------------------------------ |
| 1 | Cluster | User agent processor settings | WARNING | The default value of the user agent processor format has been changed to`ecs`. For more information, please see [Breaking changes in 7.0](https://www.elastic.co/guide/en/elasticsearch/reference/7.0/breaking-changes-7.0.html#ingest-user-agent-ecs-always) |
| 2 | Cluster | cluster.max_shards_per_node | WARNING | The default value of the maximum number of shards of each node (`cluster.max_shards_per_node`) is 1,000. If this value is exceeded, new shards cannot be created after the upgrade. For more information, please see [Breaking changes in 7.0](https://www.elastic.co/guide/en/elasticsearch/reference/7.0/breaking-changes-7.0.html#_enforce_cluster_wide_shard_limit) |
| 3 | Cluster | discovery.zen.no_master_block | WARNING | The cluster setting `discovery.zen.no_master_block` has been renamed to `cluster.no_master_block`. For more information, please see [Breaking changes in 7.0](https://www.elastic.co/guide/en/elasticsearch/reference/7.0/breaking-changes-7.0.html#new-name-no-master-block-setting) |
| 4 | Cluster | Date format of ingest pipeline | WARNING | The date format used by the `date` or `date_index_name` processor of the ingest pipeline has been disused. For more information, please see [Breaking changes in 7.0](https://www.elastic.co/guide/en/elasticsearch/reference/7.0/breaking-changes-7.0.html#breaking_70_java_time_changes) |
| 5 | Index | Index creation version | CRITICAL | Indices created on versions below v6.0 cannot be upgraded to v7.x. For more information, please see [Breaking changes in 7.0](https://www.elastic.co/guide/en/elasticsearch/reference/7.0/breaking-changes-7.0.html#_indices_created_before_7_0) |
| 6 | Index | Delimited payload token filter setting | WARNING | The delimited payload token filter `delimited_payload_filter` has been renamed to `delimited_payload`. For more information, please see [Breaking changes in 7.0](https://www.elastic.co/guide/en/elasticsearch/reference/7.0/breaking-changes-7.0.html#delimited-payload-filter-renaming) |
| 7 | Index | index.percolator.map_unmapped_fields_as_string | CRITICAL | The `index.percolator.map_unmapped_fields_as_string` setting has been renamed to `index.percolator.map_unmapped_fields_as_text`. For more information, please see [Breaking changes in 7.0](https://www.elastic.co/guide/en/elasticsearch/reference/7.0/breaking-changes-7.0.html#_percolator) |
| 8 | Index | Index name | WARNING | An index name cannot contain ":". For more information, please see [Breaking changes in 7.0](https://www.elastic.co/guide/en/elasticsearch/reference/7.0/breaking-changes-7.0.html#_literal_literal_is_no_longer_allowed_in_cluster_name) |
| 9 | Index | index.unassigned.node_left.delayed_timeout | CRITICAL | Negative values of the `index.unassigned.node_left.delayed_timeout` setting have been disused. For more information, please see [Breaking changes in 7.0](https://www.elastic.co/guide/en/elasticsearch/reference/7.0/breaking-changes-7.0.html#index-unassigned-node-left-delayed-timeout-no-longer-negative) |
| 10 | Index | index.shard.check_on_startup | CRITICAL | The value `fix` of the `index.shard.check_on_startup` setting has been disused. For more information, please see [Breaking changes in 7.0](https://www.elastic.co/guide/en/elasticsearch/reference/7.0/breaking-changes-7.0.html#fix-value-for-index-shard-check-on-startup-removed) |
| 11 | Index | Classic similarity mapping parameter | WARNING | The classic similarity mapping parameter has been disused. For more information, please see [Breaking changes in 7.0](https://www.elastic.co/guide/en/elasticsearch/reference/7.0/breaking-changes-7.0.html#classic-similarity-removed) |
| 12 | Index | Classic similarity setting | WARNING | The classic similarity setting has been disused. For more information, please see [Breaking changes in 7.0](https://www.elastic.co/guide/en/elasticsearch/reference/7.0/breaking-changes-7.0.html#classic-similarity-removed) |
| 13 | Index level | Number of fields | WARNING | For indices containing more than 1,024 fields, you are recommended to set the default query field `index.query.default_field` or increase the maximum number of fields by setting `indices.query.bool.max_clause_count`; otherwise, query without specified fields cannot be normally used after the upgrade. For more information, please see [Breaking changes in 7.0](https://www.elastic.co/guide/en/elasticsearch/reference/7.0/breaking-changes-7.0.html#_limiting_the_number_of_auto_expanded_fields) |
| 14 | Index | Mapping date format | WARNING | The `Joda-Time` format has been changed to `Java Time`. For more information, please see [Breaking changes in 7.0](https://www.elastic.co/guide/en/elasticsearch/reference/7.0/breaking-changes-7.0.html#_joda_based_date_formatters_are_replaced_with_java_ones) |
| 15 | Index template | Delimited payload token filter setting | WARNING | The delimited payload token filter `delimited_payload_filter` has been renamed to `delimited_payload`，For more information, please see [Breaking changes in 7.0](https://www.elastic.co/guide/en/elasticsearch/reference/7.0/breaking-changes-7.0.html#delimited-payload-filter-renaming) |
| 16 | Index template | index.percolator.map_unmapped_fields_as_string | CRITICAL | The `index.percolator.map_unmapped_fields_as_string` setting has been renamed to `index.percolator.map_unmapped_fields_as_text` and becomes incompatible after the upgrade. For more information, please see [Breaking changes in 7.0](https://www.elastic.co/guide/en/elasticsearch/reference/7.0/breaking-changes-7.0.html#_percolator) |
| 17 | Index template | index.unassigned.node_left.delayed_timeout | CRITICAL | Negative values of the `index.unassigned.node_left.delayed_timeout` setting have been disused and become incompatible after the upgrade. For more information, please see [Breaking changes in 7.0](https://www.elastic.co/guide/en/elasticsearch/reference/7.0/breaking-changes-7.0.html#index-unassigned-node-left-delayed-timeout-no-longer-negative) |
| 18 | Index template | index.shard.check_on_startup | CRITICAL | The `fix` value of the `index.shard.check_on_startup` setting has been disused and becomes incompatible after the upgrade. For more information, please see [Breaking changes in 7.0](https://www.elastic.co/guide/en/elasticsearch/reference/7.0/breaking-changes-7.0.html#fix-value-for-index-shard-check-on-startup-removed) |
| 19 | Index template | Classic similarity mapping parameter | CRITICAL | The classic similarity mapping parameter has been disused and becomes incompatible after the upgrade. For more information, please see [Breaking changes in 7.0](https://www.elastic.co/guide/en/elasticsearch/reference/7.0/breaking-changes-7.0.html#classic-similarity-removed) |
| 20 | Index template | Classic similarity setting  | CRITICAL | The classic similarity setting has been disused and becomes incompatible after the upgrade. For more information, please see [Breaking changes in 7.0](https://www.elastic.co/guide/en/elasticsearch/reference/7.0/breaking-changes-7.0.html#classic-similarity-removed) |
| 21 | Index template | Number of fields | CRITICAL | For index templates containing more than 1,024 fields, you are recommended to set the default query field `index.query.default_field` or increase the maximum number of fields by setting `indices.query.bool.max_clause_count`; otherwise, query without specified fields cannot be normally used after the upgrade. For more information, please see [Breaking changes in 7.0](https://www.elastic.co/guide/en/elasticsearch/reference/7.0/breaking-changes-7.0.html#_limiting_the_number_of_auto_expanded_fields) |
| 22 | Index template | Mapping date format | WARNING | The `Joda-Time` format has been changed to `Java Time`. For more information, please see [Breaking changes in 7.0](https://www.elastic.co/guide/en/elasticsearch/reference/7.0/breaking-changes-7.0.html#_joda_based_date_formatters_are_replaced_with_java_ones) |

### How to change incompatible configuration items

#### Cluster level
- User agent processor settings
User agents not in the `ecs` format will be disused and should be changed to:
```
PUT _ingest/pipeline/my_pipeline1
{
  "processors" : [
    {
      "user_agent" : {
        "field" : "agent",
        "ecs": true
      }
    }
  ]
}
```
- Number of cluster shards
Clusters where shard quantity exceeds the limit can be changed in the following ways:
 - Reduce the number of cluster shards by means such as clearing expired indices or [shrinking indices](https://www.elastic.co/guide/en/elasticsearch/reference/6.8/indices-shrink-index.html).
 - Modify the cluster settings to increase the number limit of shards.
```
PUT _cluster/settings
{
  "persistent": {
    "cluster.max_shards_per_node": 5000
  }
}
```
- Cluster setting (discovery.zen.no_master_block)
For clusters using the `discovery.zen.no_master_block` setting, change it to `cluster.no_master_block` **after the upgrade**; for example:
```
PUT _cluster/settings
{
  "persistent": {
    "cluster.no_master_block": "write"
  }
}
```
- Ingest pipeline data format
For more information on how to change it, please see [Joda based date formatters are replaced with java ones](https://www.elastic.co/guide/en/elasticsearch/reference/7.0/breaking-changes-7.0.html#_joda_based_date_formatters_are_replaced_with_java_ones).

#### <span id="jump">Index level</span>

- Index creation version
Indices created on versions below v6.0 cannot be upgraded to v7.x. For indices that need to be reserved, call [Reindex](https://www.elastic.co/guide/en/elasticsearch/reference/6.8/docs-reindex.html) before the upgrade; for example:
```
POST _reindex
{
  "source": {
    "index": "my_index"
  },
  "dest": {
    "index": "new_my_index"
  }
}
```
- Delimited payload token filter index template setting
Change `delimited_payload_filter` in index settings to `delimited_payload`. For example, the original index:
```
PUT my_index
{
  "settings": {
    "analysis": {
      "analyzer": {
        "whitespace_plus_delimited": {
          "tokenizer": "whitespace",
          "filter": [ "plus_delimited" ]
        }
      },
      "filter": {
        "plus_delimited": {
          "type": "delimited_payload_filter",
          "delimiter": "+",
          "encoding": "int"
        }
      }
    }
  }
}
```
Should be modified to:
```
PUT my_index
{
  "settings": {
    "analysis": {
      "analyzer": {
        "whitespace_plus_delimited": {
          "tokenizer": "whitespace",
          "filter": [ "plus_delimited" ]
        }
      },
      "filter": {
        "plus_delimited": {
          "type": "delimited_payload",
          "delimiter": "+",
          "encoding": "int"
        }
      }
    }
  }
}
```
- Index setting (index.percolator.map_unmapped_fields_as_string)
Change the index setting `index.percolator.map_unmapped_fields_as_string` to `index.percolator.map_unmapped_fields_as_text` (before the change, you need to [close](https://www.elastic.co/guide/en/elasticsearch/reference/6.8/indices-open-close.html) the index).
```
PUT my_index/_settings
{
  "index.percolator.map_unmapped_fields_as_text": true
}
```
- Index name
For indices containing ":", you need to call [Reindex](https://www.elastic.co/guide/en/elasticsearch/reference/6.8/docs-reindex.html); for example:
```
POST _reindex
{
  "source": {
    "index": "my_index"
  },
  "dest": {
    "index": "new_my_index"
  }
}
```
- Index setting (index.unassigned.node_left.delayed_timeout)
Change the index setting `index.unassigned.node_left.delayed_timeout` to a positive integer:
```
PUT my_index/_settings
{
  "index.unassigned.node_left.delayed_timeout": 0
}
```
- Index setting (index.shard.check_on_startup)
Change the `fix` value of the index setting `index.shard.check_on_startup` to another value; for example:
```
PUT my_index/_settings
{
  "index.shard.check_on_startup": true
}
```
- Classic similarity index mapping parameter and classic similarity index setting
Change the classic similarity index setting or mapping parameter to another type. For example, the original index:
```
PUT my_index
{
  "mappings": {
    "doc": {
      "properties": {
        "field1": {
          "properties": {
            "field4": {
              "type": "text",
              "similarity": "classic"
            }
          }
        }
      }
    }
  }
}
```
Should be modified to:
```
PUT my_index
{
  "mappings": {
    "doc": {
      "properties": {
        "field1": {
          "properties": {
            "field4": {
              "type": "text",
              "similarity": "BM25"
            }
          }
        }
      }
    }
  }
}
```
- Number of index fields
Indices with over 1,024 fields can be changed in the following methods:
 - Set the default query field `index.query.default_field`.
```
PUT my_index/_settings
{
  "index.query.default_field": "field1"
}
```
 - Modify the ES YML configuration file to set `indices.query.bool.max_clause_count` in order to increase the maximum number of fields (this method will be supported in the future).
- Index mapping date format
For more information on how to change it, please see [Joda based date formatters are replaced with java ones](https://www.elastic.co/guide/en/elasticsearch/reference/7.0/breaking-changes-7.0.html#_joda_based_date_formatters_are_replaced_with_java_ones).


#### Index template level
For more information on how to change the incompatible settings of index templates, please see [Index level](#jump).

