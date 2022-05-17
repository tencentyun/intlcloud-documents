## Overview

When using the data access and distribution services in DataHub, you may encounter the following issues:

- You need to parse certain fields in messages to get the relevant information.
- You need to process a field in messages multiple times in an iterative manner.
- You need to convert messages to unstructured raw messages before you can use them.
- You need to process messages in a multi-level nested format.

Based on the long-term experience of technical experts in the CKafka team, the brand new data processing component v2.0 is launched. It has the following new features while remaining fully compatible with v1.0:

- Diverse plugins: Data processing supports various preconfigured processing plugins to help you quickly generate data in desired consumption formats.
- Chain processing: Data processing supports chain message processing; that is, the previous processing result can be used as the input parameters in the current processing. This greatly facilitates processing complex data structures.
- Visual preview: Data processing supports real-time structured JSON preview to help you quickly locate and troubleshoot problems.
- Type conversion: Data processing can convert data between different types to make data format check easier.

## How It Works

The overall data processing flow is as shown below, with each component structure detailed as follows:
![](https://qcloudimg.tencent-cloud.cn/raw/fb205375b1f11cdfdcfc47e7e92f5bd4.svg)

- In the data processing component cluster, multiple workers form a consumer group to batch read messages from the source topic and process each message in sequence.
- In each message, the nested structure of message fields is expanded according to the processing chain sequence configured in the console, and operations such as replacement, extraction, data conversion, and time formatting are performed.
- The current processing chain reads the result of the previous processing chain, preforms chain processing, and ships the processing result to the next chain.
- The result of the last processing chain is shipped to the configured target topic. At this time, the data processing of a message is completed.

## Prerequisites

- The CKafka service has been activated.
- The message format is JSON or string. Currently, other encoding protocols are not supported.

## Actual Application

### Processing string-type log

Below is a log in the default Nginx format (aka `combined` format), from which you can parse information such as requester, packet, and request status for further analysis.
<dx-codeblock>
:::  properties
66.249.65.159 - - [06/Nov/2014:19:10:38 +0600] "GET /news/53f8d72920ba2744fe873ebc.html HTTP/1.1" 404 177 "-" "Mozilla/5.0 (iPhone; CPU iPhone OS 6_0 like Mac OS X) AppleWebKit/536.26 (KHTML, like Gecko) Version/6.0 Mobile/10A5376e Safari/8536.25 (compatible; Googlebot/2.1; +http://www.google.com/bot.html)"
:::
</dx-codeblock>


As the `combined` format of Nginx uses spaces and `-` to separate data, design the parsing process in the following steps:

1. First, use the `"` **separator** to initially parse the data. At this time, data processing automatically converts the log to the JSON structure.
<dx-codeblock>
:::  JSON
{
  "0": "66.249.65.159 - - [06/Nov/2014:19:10:38 +0600] ",
  "1": "GET /news/53f8d72920ba2744fe873ebc.html HTTP/1.1",
  "2": " 404 177 ",
  "5": "Mozilla/5.0 (iPhone; CPU iPhone OS 6_0 like Mac OS X) AppleWebKit/536.26 (KHTML, like Gecko) Version/6.0 Mobile/10A5376e Safari/8536.25 (compatible; Googlebot/2.1; +http://www.google.com/bot.html)"
}
:::
</dx-codeblock>
2. As shown in the above JSON structure, there are still concatenated coupled data records in the fields of keys `0` and `2` as affected by `-` and spaces. Therefore, split the fields of the two keys with the space and `-` **separators**. The JSON result after splitting is as follows:
<dx-codeblock>
:::  JSON
{
  "1": "GET /news/53f8d72920ba2744fe873ebc.html HTTP/1.1",
  "5": "Mozilla/5.0 (iPhone; CPU iPhone OS 6_0 like Mac OS X) AppleWebKit/536.26 (KHTML, like Gecko) Version/6.0 Mobile/10A5376e Safari/8536.25 (compatible; Googlebot/2.1; +http://www.google.com/bot.html)",
  "0.0": "66.249.65.159 ",
  "0.2": " [06/Nov/2014:19:10:38 +0600] ",
  "2.1": "404",
  "2.2": "177"
}   
:::
</dx-codeblock>
3. As the time format is enclosed by square brackets “[ ]”, use a **separator** again to extract the time information. The JSON structure after extraction is as follows:
<dx-codeblock>
:::  JSON
{
  "1": "GET /news/53f8d72920ba2744fe873ebc.html HTTP/1.1",
  "5": "Mozilla/5.0 (iPhone; CPU iPhone OS 6_0 like Mac OS X) AppleWebKit/536.26 (KHTML, like Gecko) Version/6.0 Mobile/10A5376e Safari/8536.25 (compatible; Googlebot/2.1; +http://www.google.com/bot.html)",
  "0.0": "66.249.65.159 ",
  "0.2": "06/Nov/2014:19:10:38 +0600",
  "2.1": "404",
  "2.2": "177"
}
:::
</dx-codeblock>
4. At this point, all fields have been split appropriately. Name the `keys` of the corresponding mapped fields based on the field attribute. The eventual modification result is as follows:
<dx-codeblock>
:::  JSON
{
  "request": "GET /news/53f8d72920ba2744fe873ebc.html HTTP/1.1",
  "http_user_agent": "Mozilla/5.0 (iPhone; CPU iPhone OS 6_0 like Mac OS X) AppleWebKit/536.26 (KHTML, like Gecko) Version/6.0 Mobile/10A5376e Safari/8536.25 (compatible; Googlebot/2.1; +http://www.google.com/bot.html)",
  "remote_addr": "66.249.65.159 ",
  "dateTime": "06/Nov/2014:19:10:38 +0600",
  "status": "404",
  "body_bytes_sent ": "177"
}
:::
</dx-codeblock>


### Processing nested log

Below is a sample TKE collection format. The TKE collector will place the metadata into the `kubernetes` field in the JSON structure and place the collected log into the `log` field. The overall structure is as follows:
<dx-codeblock>
:::  JSON
{
  "@timestamp": 1648803500.63659,
  "@filepath": "/var/log/tke-log-agent/test7/c816991f-adfe-4617-8cf3-9997aea90ded/c_tke-es-687995d557-n29jr_default_nginx-add90ccf49626ef42d5615a636aae74d6380996043cf6f6560d8131f21a4d8ba/jgw_INFO_2022-02-10_15_4.log",
  "log": "15:00:00.000[4349811564226374227] [http-nio-8081-exec-64] INFO  com.qcloud.jgw.gateway.server.topic.TopicService",
  "kubernetes": {
    "pod_name": "tke-es-687995d557-n29jr",
    "namespace_name": "default",
    "pod_id": "c816991f-adfe-4617-8cf3-9997aea90ded",
    "labels": {
      "k8s-app": "tke-es",
      "pod-template-hash": "687995d557",
      "qcloud-app": "tke-es"
    },
    "annotations": {
      "qcloud-redeploy-timestamp": "1648016531476",
      "tke.cloud.tencent.com/networks-status": "[{\n    \"name\": \"tke-bridge\",\n    \"interface\": \"eth0\",\n    \"ips\": [\n        \"172.16.0.31\"\n    ],\n    \"mac\": \"ae:61:12:4a:c2:ba\",\n    \"default\": true,\n    \"dns\": {}\n}]"
    },
    "host": "10.0.96.47",
    "container_name": "nginx",
    "docker_id": "add90ccf49626ef42d5615a636aae74d6380996043cf6f6560d8131f21a4d8ba",
    "container_hash": "nginx@sha256:e1211ac17b29b585ed1aee166a17fad63d344bc973bc63849d74c6452d549b3e",
    "container_image": "nginx"
  }
}
:::
</dx-codeblock>


When collected logs are shipped to Elasticsearch, as the nested JSON format is supported, you don't need to make major changes on the data. However, when logs are shipped to a database, you need to convert the data to an identifiable single-level JSON format. In this case, design the parsing process in the following steps:

1. Use the **JSONPATH** statement to process the `$.kubernetes` JSON structure at the first nested level and select `JSON` as the parsing mode. This converts the nested JSON structure to a single-level JSON structure. The tested result is as follows:
<dx-codeblock>
:::  JSON
{
  "@timestamp": 1.64880350063659E9,
  "@filepath": "/var/log/tke-log-agent/test7/c816991f-adfe-4617-8cf3-9997aea90ded/c_tke-es-687995d557-n29jr_default_nginx-add90ccf49626ef42d5615a636aae74d6380996043cf6f6560d8131f21a4d8ba/jgw_INFO_2022-02-10_15_4.log",
  "log": "15:00:00.000[4349811564226374227] [http-nio-8081-exec-64] INFO  com.qcloud.jgw.gateway.server.topic.TopicService",
  "$.kubernetes.pod_name": "tke-es-687995d557-n29jr",
  "$.kubernetes.namespace_name": "default",
  "$.kubernetes.pod_id": "c816991f-adfe-4617-8cf3-9997aea90ded",
  "$.kubernetes.labels": {
    "k8s-app": "tke-es",
    "pod-template-hash": "687995d557",
    "qcloud-app": "tke-es"
  },
  "$.kubernetes.annotations": {
    "qcloud-redeploy-timestamp": "1648016531476",
    "tke.cloud.tencent.com/networks-status": "[{\n    \"name\": \"tke-bridge\",\n    \"interface\": \"eth0\",\n    \"ips\": [\n        \"172.16.0.31\"\n    ],\n    \"mac\": \"ae:61:12:4a:c2:ba\",\n    \"default\": true,\n    \"dns\": {}\n}]"
  },
  "$.kubernetes.host": "10.0.96.47",
  "$.kubernetes.container_name": "nginx",
  "$.kubernetes.docker_id": "add90ccf49626ef42d5615a636aae74d6380996043cf6f6560d8131f21a4d8ba",
  "$.kubernetes.container_hash": "nginx@sha256:e1211ac17b29b585ed1aee166a17fad63d344bc973bc63849d74c6452d549b3e",
  "$.kubernetes.container_image": "nginx"
}
:::
</dx-codeblock>
2. Process the `$.kubernetes.annotations` and `$.kubernetes.labels` nested structures at the second level. Use `Map` to select the two names in the processing chain to convert the nested format into a single-level JSON format. The processing result is as follows:
<dx-codeblock>
:::  JSON
{
  "@timestamp": 1648803500.63659,
  "@filepath": "/var/log/tke-log-agent/test7/c816991f-adfe-4617-8cf3-9997aea90ded/c_tke-es-687995d557-n29jr_default_nginx-add90ccf49626ef42d5615a636aae74d6380996043cf6f6560d8131f21a4d8ba/jgw_INFO_2022-02-10_15_4.log",
  "log": "15:00:00.000[4349811564226374227] [http-nio-8081-exec-64] INFO  com.qcloud.jgw.gateway.server.topic.TopicService",
  "$.kubernetes.pod_name": "tke-es-687995d557-n29jr",
  "$.kubernetes.namespace_name": "default",
  "$.kubernetes.pod_id": "c816991f-adfe-4617-8cf3-9997aea90ded",
  "$.kubernetes.host": "10.0.96.47",
  "$.kubernetes.container_name": "nginx",
  "$.kubernetes.docker_id": "add90ccf49626ef42d5615a636aae74d6380996043cf6f6560d8131f21a4d8ba",
  "$.kubernetes.container_hash": "nginx@sha256:e1211ac17b29b585ed1aee166a17fad63d344bc973bc63849d74c6452d549b3e",
  "$.kubernetes.container_image": "nginx",
  "$.kubernetes.labels.k8s-app": "tke-es",
  "$.kubernetes.labels.pod-template-hash": "687995d557",
  "$.kubernetes.labels.qcloud-app": "tke-es",
  "$.kubernetes.annotations.qcloud-redeploy-timestamp": "1648016531476",
  "$.kubernetes.annotations.tke.cloud.tencent.com/networks-status": "[{\n    \"name\": \"tke-bridge\",\n    \"interface\": \"eth0\",\n    \"ips\": [\n        \"172.16.0.31\"\n    ],\n    \"mac\": \"ae:61:12:4a:c2:ba\",\n    \"default\": true,\n    \"dns\": {}\n}]"
}
:::
</dx-codeblock>
3. Rename the `keys` of the corresponding mapped fields and delete unnecessary fields. Click **Add Processing Chain** and **Process All Upper-Level Results**. Below is a sample result after organization and optimization:
<dx-codeblock>
:::  JSON
{
  "@timestamp": 1.64880350063659E9,
  "@filepath": "/var/log/tke-log-agent/test7/c816991f-adfe-4617-8cf3-9997aea90ded/c_tke-es-687995d557-n29jr_default_nginx-add90ccf49626ef42d5615a636aae74d6380996043cf6f6560d8131f21a4d8ba/jgw_INFO_2022-02-10_15_4.log",
  "log": "15:00:00.000[4349811564226374227] [http-nio-8081-exec-64] INFO  com.qcloud.jgw.gateway.server.topic.TopicService",
  "pod_name": "tke-es-687995d557-n29jr",
  "namespace_name": "default",
  "pod_id": "c816991f-adfe-4617-8cf3-9997aea90ded",
  "host": "10.0.96.47",
  "container_name": "nginx",
  "docker_id": "add90ccf49626ef42d5615a636aae74d6380996043cf6f6560d8131f21a4d8ba"
}
:::
</dx-codeblock>


> ?If the `key` contains a period (.) when you use **JSONPath** to process a parameter, you need to add square brackets and single quotation marks to the path for isolation.
>
> For example, to get the desired fields from `{"key1.key2":"value1"}`, you need to use `$.['key1.key2']` to get the corresponding key values.
>

### Processing serialized JSON string-type log

Sometimes, the JSON format needs to be escaped to the string format during data transfer in order to meet the format or performance requirements. This string format is called **raw JSON**, which must be deserialized to the JSON format in data processing. The following uses the raw JSON format in MongoDB as an example, and the overall structure is as shown below:
<dx-codeblock>
:::  JSON
{
  "key": "  {\n    \"categories\": [\"dev\"],\n    \"created_at\": \"2020-01-05 13:42:19.324003\",\n    \"icon_url\": \"https://assets.chucknorris.host/img/avatar/chuck-norris.png\",\n    \"id\": \"elgv2wkvt8ioag6xywykbq\",\n    \"updated_at\": \"2020-01-05 13:42:19.324003\",\n    \"url\": \"https://api.chucknorris.io/jokes/elgv2wkvt8ioag6xywykbq\",\n    \"value\": \"Chuck Norris's keyboard doesn't have a Ctrl key because nothing controls Chuck Norris.\"\n  }\n"
}
:::
</dx-codeblock>


After the raw JSON format is converted to the general JSON format during data processing, the message can be directly shipped to the target downstream service without changing the field format. The overall processing process is as follows:

1. Set **Parsing Mode** to JSON to preread the message into the internal MAP format. The parsing result is as follows:
<dx-codeblock>
:::  JSON
{
  "key": "  {\n    \"categories\": [\"dev\"],\n    \"created_at\": \"2020-01-05 13:42:19.324003\",\n    \"icon_url\": \"https://assets.chucknorris.host/img/avatar/chuck-norris.png\",\n    \"id\": \"elgv2wkvt8ioag6xywykbq\",\n    \"updated_at\": \"2020-01-05 13:42:19.324003\",\n    \"url\": \"https://api.chucknorris.io/jokes/elgv2wkvt8ioag6xywykbq\",\n    \"value\": \"Chuck Norris's keyboard doesn't have a Ctrl key because nothing controls Chuck Norris.\"\n  }\n"
}
:::
</dx-codeblock>
2. Click **Add Processing Chain**, use MAP to select the `key`, and select `JSON` as the parsing mode. Then, data processing can automatically convert the raw JSON format to the JSON format. The parsing result is as follows:
<dx-codeblock>
:::  JSON
{
  "key.categories": [
    "dev"
  ],
  "key.created_at": "2020-01-05 13:42:19.324003",
  "key.icon_url": "https://assets.chucknorris.host/img/avatar/chuck-norris.png",
  "key.id": "elgv2wkvt8ioag6xywykbq",
  "key.updated_at": "2020-01-05 13:42:19.324003",
  "key.url": "https://api.chucknorris.io/jokes/elgv2wkvt8ioag6xywykbq",
  "key.value": "Chuck Norris's keyboard doesn't have a Ctrl key because nothing controls Chuck Norris."
}
:::
</dx-codeblock>
3. Click **Add Processing Chain** and **Process All Upper-Level Results**, rename the `keys` of the corresponding mapped fields, and delete unnecessary fields. Below is a sample result after organization and optimization:
<dx-codeblock>
:::  JSON
{
  "categories": [
    "dev"
  ],
  "created_at": "2020-01-05 13:42:19.324003",
  "icon_url": "https://assets.chucknorris.host/img/avatar/chuck-norris.png",
  "id": "elgv2wkvt8ioag6xywykbq",
  "updated_at": "2020-01-05 13:42:19.324003",
  "url": "https://api.chucknorris.io/jokes/elgv2wkvt8ioag6xywykbq",
  "value": "Chuck Norris's keyboard doesn't have a Ctrl key because nothing controls Chuck Norris."
}
:::
</dx-codeblock>


> ?Currently, only MAP-type data in the raw JSON format can be parsed. If the first level is in List type, such as `"[\"test1\",\"test2\"]"` or `"[{\"key\":\"value\"}]"`, as it cannot be parsed into appropriate key values, a parsing failure will be reported.
>
