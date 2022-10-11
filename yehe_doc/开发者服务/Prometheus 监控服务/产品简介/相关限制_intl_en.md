## Instance limits
Each instance can have up to 4.5 million series. If you need to adjust it, [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category) for application.
>? A series consists of a metric name and label. The same metric name and labels form a unique series.

## Custom reporting limits
If you use TMP's [custom monitoring](https://intl.cloud.tencent.com/document/product/1116/43215) feature to monitor data, there will be the following limits on metrics (series with a unique `__name__`).
- Data reporting must carry a metric name, i.e., the ` __name__` label, which can contain only ASCII letter, characters, digits, underscores, and colons and must start with a letter and match the regex `[a-zA-Z_:][a-zA-Z0-9_:]*`. For more information, see [Metric names and labels](https://prometheus.io/docs/concepts/data_model/#metric-names-and-labels).
- Each metric can have up to 32 labels.
- The label name can contain only ASCII letters, digits, and underscores. It must match the regex `[a-Za-Z_][a-Za-Z0-9_]*`. Labels beginning with `__` are reserved for internal use.
- The label name and label value can contain up to 1,024 and 2,048 characters respectively.
- Under the same metric, the dimension combinations of labels cannot exceed 100,000. When the histogram has many buckets, the histogram-type metrics cannot be adjusted.

>?The role of labels: In Prometheus, data is stored as time series, which are uniquely identified by the metric name and a series of labels (key-value pairs). Different labels represent different time series, so you can query the specified data by label. The more labels you add, the finer the query dimension.


## Prometheus query limits

To ensure the query efficiency and better user experience, Prometheus query has the following limits (which don't apply to metadata such as queries about labels and don't affect the Grafana metrics browser feature).
- The number of time series involved in a single query cannot exceed 100,000.
- The amount of data involved in a single query cannot exceed 100 MB.
- There is no limit on the query frequency, but if the concurrency exceeds 15, there may be a certain queuing delay in slower large queries (the probability is low though). Large queries with a time span of more than two weeks will have a higher delay.

The above limits also apply to alarm rules and recording rules. We recommend you limit the query scope based on your business scenario or appropriately split large queries in other ways. You can also use the method of splitting first and then aggregating, such as aggregating recorded results again.

## Other configuration limits
Configuration limits:
- Up to 150 alarm rules can be configured for each instance.
- Up to 150 recording rules can be configured for each instance.
