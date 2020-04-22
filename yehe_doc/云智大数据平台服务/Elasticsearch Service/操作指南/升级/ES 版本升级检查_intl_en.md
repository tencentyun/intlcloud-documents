Different versions of Elasticsearch have certain incompatible configuration items, and if you have set such items, an upgrade may affect the use of your cluster. You can use the upgrade check feature to check whether there are any incompatible configuration items and adjust them accordingly. The following describes the check to be performed when upgrading the Elasticsearch version.

> On the details page in the [console](https://console.cloud.tencent.com/es), click **Upgrade** in the top-right corner. For detailed directions, please see [Upgrading ES Clusters](https://intl.cloud.tencent.com/document/product/845/32600).

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

### How to adjust incompatible configuration items
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
- The `include_in_all` index mapping parameter
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

