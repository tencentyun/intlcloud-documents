This document introduces the basic syntax and examples of URL functions.


## Syntax Format

URL functions can extract fields from standard HTTP URLs. The following is an example of a standard URL:

```
[protocol:][//host[:port]][path][?query][#fragment]
```

>! The extracted fields do not include URL delimiters `:` and `?`.
>


## Common URL Functions

| Function              | Description                                 | Example                              | Output                                |
| ---------------- | ---------------------------- | ------------------------- | --------------------------------- |
| url_extract_fragment(url)        | Extracts `fragment` from the URL. The result is of the varchar type.                   | `* | select url_extract_fragment('https://console.cloud.tencent.com/#/project/dashboard-demo/categoryList')` | `/project/dashboard-demo/categoryList`                       |
| url_extract_host(url)            | Extracts `host` from the URL. The result is of the varchar type.                       | `* | select url_extract_host('https://console.cloud.tencent.com/cls')` | `console.cloud.tencent.com`                                  |
| url_extract_parameter(url, name) | Extracts the value of `query` from the URL. The result is of the varchar type.    | `* | select url_extract_parameter('https://console.cloud.tencent.com/cls?region=ap-chongqing','region')` | `ap-chongqing`                                               |
| url_extract_path(url)            | Extracts `path` from the URL. The result is of the varchar type.                       | `* | select url_extract_path('https://console.cloud.tencent.com/cls?region=ap-chongqing')` | `cls`                                                        |
| url_extract_port(url)            | Extracts `port` from the URL. The result is of the bigint type.                        | `* | select url_extract_port('https://console.cloud.tencent.com:80/cls?region=ap-chongqing')` | `80`                                                         |
| url_extract_protocol(url)        | Extracts `protocol` from the URL. The result is of the varchar type.                       | `* | select url_extract_protocol('https://console.cloud.tencent.com:80/cls?region=ap-chongqing')` | `https`                                                      |
| url_extract_query(url)           | Extracts the key of `query` from the URL. The result is of the varchar type.                      | `* | select url_extract_query('https://console.cloud.tencent.com:80/cls?region=ap-chongqing')` | `region=ap-chongqing`                                        |
| url_encode(value)                | Escapes `value` so that it can be used in `URL_query`.<ul  style="margin: 0;"><li>Letters will not be decoded.</li><li>.-\*\_ will not be encoded. </li><li>Spaces are decoded as +.</li><li>Other characters are decoded into the UTF-8 format.</li></ul> | `* | select url_encode('https://console.cloud.tencent.com:80/cls?region=ap-chongqing')` | `https%3A%2F%2Fconsole.cloud.tencent.com%3A80%2Fcls%3Fregion%3Dap-chongqing` |
| url_decode(value)                | Decodes the URL.                                              | `* | select url_decode('https%3A%2F%2Fconsole.cloud.tencent.com%3A80%2Fcls%3Fregion%3Dap-chongqing')` | `https://console.cloud.tencent.com:80/cls?region=ap-chongqing` |




