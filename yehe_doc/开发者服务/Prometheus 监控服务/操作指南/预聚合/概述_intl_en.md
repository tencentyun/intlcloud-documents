A recording rule allows you to calculate some commonly used or complex metrics in advance and then store the calculated data in new data metrics. In this way, querying the calculated data will be faster and easier than querying the original data. This is very suitable for dashboard scenarios and can solve the problems of complicated user configuration and slow query.

Recording rules exist in the form of rule group, and rules in the same group are executed sequentially at a certain interval. Rule names must conform to the [corresponding Prometheus specification](https://prometheus.io/docs/concepts/data_model/#metric-names-and-labels).

Generally, a rule file is as follows:

```plaintext
groups:
  [ - <rule_group> ]
```

Below is a simple example of recording rule:

```plaintext
groups:
  - name: example
    rules:
    - record: job:http_inprogress_requests:sum
      expr: sum by (job) (http_inprogress_requests)
```


## Rule Group

```plaintext
# A rule group name must be unique in the same file
name: <string>

# Rule detection interval
[ interval: <duration> | default = global.evaluation_interval ]

rules:
  [ - <rule> ... ]
```

## Rule

The recording rule syntax is as follows:

```plaintext
# The generated new metric name, which must be valid
record: <string>

# PromQL expression. Each calculated data entry will be stored in the new metric name `record`
expr: <string>

# The label to be added or overwritten in the data to be stored
labels:
  [ <labelname>: <labelvalue> ]
```

## Recommended Name Format

The recommended format for naming recording rules is `level:metric:operations`.

- level: indicates the recording level and the output label of the rule.
- metric: indicates the metric name.
- operations: indicates the list of operations applied to the metric.

Example:
```plaintext
- record: instance_path:requests:rate5m
  expr: rate(requests_total{job="myjob"}[5m])

- record: path:requests:rate5m
  expr: sum without (instance)(instance_path:requests:rate5m{job="myjob"})
```
