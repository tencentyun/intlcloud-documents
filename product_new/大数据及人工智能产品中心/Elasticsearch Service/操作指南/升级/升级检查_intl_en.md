Different versions of Elasticsearch have certain incompatible configuration items, and if you have set such items, an upgrade may affect the use of your cluster. You can use the upgrade check feature to check whether there are any incompatible configuration items and adjust them accordingly. The following describes the check to be performed when upgrading the Elasticsearch version.

> On the details page in the [console](https://console.cloud.tencent.com/es), click **Upgrade** in the top-right corner. For detailed directions, see [Upgrading ES Clusters](https://intl.cloud.tencent.com/document/product/845/32600).

## Configuration check for Elasticsearch upgrade from 5.6.4 to 6.4.3

### Checklist of configuration items

| No. | Configuration Level | Configuration Information | Compatibility | Description |
| ---- | ---------- | --------------------------------------------------- | -------- | ------------------------------------------ |
| 1 | Cluster | Snapshot settings | CRITICAL | The `cluster.routing.allocation.snapshot.relocation_enabled` setting has been disused since 6.0. For more information, see [Breaking changes in 6.0](https://www.elastic.co/guide/en/elasticsearch/reference/6.0/breaking_60_settings_changes.html#_store_settings) |
| 2 | Cluster | Store throttling settings | CRITICAL | The `indices.store.throttle.type` and `indices.store.throttle.max_bytes_per_sec` settings have been disused since 6.0. For more information, see [Breaking changes in 6.0](https://www.elastic.co/guide/en/elasticsearch/reference/6.0/breaking_60_settings_changes.html#_store_throttling_settings) |
| 3 | Index | Similarity settings | WARNING | The `index.similarity.base` setting has been disused since 6.0. For more information, see [Breaking changes in 6.0](https://www.elastic.co/guide/en/elasticsearch/reference/6.0/breaking_60_settings_changes.html#_similarity_settings) |
| 4 | Index | Shadow replicas settings | CRITICAL | The `index.shared_filesystem` and `index.shadow_replicas` settings have been disused since 6.0. For more information, see [Breaking changes in 6.0](https://www.elastic.co/guide/en/elasticsearch/reference/6.0/breaking_60_indices_changes.html#_shadow_replicas_have_been_removed) |
| 5 | Index | Index store settings | CRITICAL | The `default` `index.store.type` has been disused since 6.0. For more information, see [Breaking changes in 6.0](https://www.elastic.co/guide/en/elasticsearch/reference/6.0/breaking_60_settings_changes.html#_store_settings) |
| 6 | Index | Index store throttling settings | CRITICAL | The `index.store.throttle.type` and `index.store.throttle.max_bytes_per_sec` settings have been disused since 6.0. For more information, see [Breaking changes in 6.0](https://www.elastic.co/guide/en/elasticsearch/reference/6.0/breaking_60_settings_changes.html#_store_throttling_settings) |
| 7 | Index | `include_in_all` index mapping parameter | WARNING | The `include_in_all` mapping parameter cannot be used in indices on version 6.0 or above (indices created by 5.x which contain this setting will be compatible after upgrade to 6.x). For more information, see [Breaking changes in 6.0](https://www.elastic.co/guide/en/elasticsearch/reference/6.0/breaking_60_mappings_changes.html#_the_literal_include_in_all_literal_mapping_parameter_is_now_disallowed) |

>
  > - WARNING: Upgrade can still be performed even if the check fails. The settings for this type of check items will be ignored after the upgrade.
  > - CRITICAL: Upgrade cannot be performed if the check fails. The settings for this type of check items are incompatible in the target version.

### How to adjust incompatible configuration items

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

- Similarity settings
  These settings will be ignored after upgrade to 6.x, which will not affect the upgrade though. To cancel them, follow the steps below:
 1. The index needs to be closed before you modify these settings, and the closed index cannot be read or written. Close the index:
```
POST my_index/_close
```
 2. Cancel these settings through the ES index settings update API:
```
PUT my_index/_settings
{
       "index.similarity.base.*": null
}
```
 3. Then, open the index:
```
POST my_index/_open
```
4. Shadow replicas settings
 1. The index needs to be closed before you modify these settings, and the closed index cannot be read or written. Close the index:
```
POST my_index/_close
```
 2. Cancel these settings through the ES index settings update API:
```
PUT my_index/_settings
{
        "index.shared_filesystem": null,
        "index.shadow_replicas": null
}
```
 3. Then, open the index:
```
POST my_index/_open
```

- Index store settings
 1. The index needs to be closed before you modify these settings, and the closed index cannot be read or written. Close the index:
```
POST my_index/_close
```
 2. Cancel these settings through the ES index settings update API:
```
PUT my_index/_settings
{
       "index.store.type": null
}
```
 3. Then, open the index:
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

