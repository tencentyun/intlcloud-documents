ES is capable of automatic backup, which involves automatically creating a snapshot of the primary index shards in a cluster and backing it up to COS. The snapshot can be restored to the cluster as needed.

## Notes on backup

- ES automatically performs snapshot backup and only retains the snapshot data for the past 7 days.
- Data generated from automatic snapshot backup can only be restored to the source cluster. For more information on how to restore to other regions, see [Manual Snapshot](https://intl.cloud.tencent.com/document/product/845/19549).
- By default, automatic snapshot backup is performed at midnight, and you are recommended to select a time when the number of access requests to your cluster is small based on your business needs.
- The first snapshot of a cluster is a complete copy of all cluster data, and the time it takes to complete depends on the amount of data. Subsequent backups only retain the incremental difference between the saved snapshots and new data.
- When the health status of your cluster is RED, the automatic snapshot service will be suspended, so you are recommended to pay close attention to the health status of your cluster.

## Directions

### Enabling automatic snapshot backup

1. Log in to the [ES Console](https://console.cloud.tencent.com/es) and click a cluster name in the cluster list to enter the cluster details page.
2. On the "Advanced Configuration" page, enable automatic snapshot backup and configure the start time for automatic snapshot backup.
![Automatic snapshot backup](https://main.qcloudimg.com/raw/93132de5410a2a87d18d14594dd63250.png)
![Automatic snapshot backup](https://main.qcloudimg.com/raw/7020262c8e2e17ed2e0cdbc4a6e89581.png)
### Viewing snapshot repository

Click **Kibana** on the cluster details page to enter the Kibana console where you can view the repository of all cluster snapshots using ES API on the "Dev Tools" page.
- View the cluster snapshot repository.

```
GET _snapshot?pretty
```

If only automatic snapshot is performed, the following message will be returned:

```
{
  "ES_AUTO_BACKUP": {
    "type": "cos",
    "settings": {
      "bucket": "es-ap-guangzhou",
      "base_path": "/es_backup/es-2s8x1b9u",
      "chunk_size": "500mb",
      "region": "ap-guangzhou",
      "compress": "true"
    }
  }
}
```

- View the snapshot information in the automatic snapshot repository.  

```
GET _snapshot/ES_AUTO_BACKUP/_all?pretty
```
The returned result is as follows:

```
If there are no snapshots, the list will be empty.
{
  "snapshots": []
}

{
  "snapshots": [
    {
      "snapshot": "es-2s8x1b9u_20181220",
      "uuid": "gsXPyWb1SNOlTuj3eNs2gA",
      "version_id": 5060499,
      "version": "5.6.4",
      "indices": [
        ".kibana"
      ],
      "state": "SUCCESS",
      "start_time": "2018-12-20T08:00:12.336Z",
      "start_time_in_millis": 1545292812336,
      "end_time": "2018-12-20T08:00:12.945Z",
      "end_time_in_millis": 1545292812945,
      "duration_in_millis": 609,
      "failures": [],
      "shards": {
        "total": 1,
        "failed": 0,
        "successful": 1
      }
    }
  ]
}
```

### Restoring data

```
POST _snapshot/ES_AUTO_BACKUP/es-2s8x1b9u_20181220/_restore
```

