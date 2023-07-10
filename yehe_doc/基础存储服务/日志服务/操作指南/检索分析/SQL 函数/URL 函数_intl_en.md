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
| url_extract_fragment(url) [](id:url_extract_fragment)       | Extracts `fragment` from the URL. The result is of the varchar type.                   | `* \| select url_extract_fragment('https://console.cloud.tencent.com/#/project/dashboard-demo/categoryList')` | `/project/dashboard-demo/categoryList`                       |
| url_extract_host(url) [](id:url_extract_host)           | Extracts `host` from the URL. The result is of the varchar type.                       | `* \| select url_extract_host('https://console.cloud.tencent.com/cls')` | `console.cloud.tencent.com`                                  |
| url_extract_parameter(url, name)[](id:url_extract_parameter) | Extracts the value of `query` from the URL. The result is of the varchar type.    | `* \| select url_extract_parameter('https://console.cloud.tencent.com/cls?region=ap-chongqing','region')` | `ap-chongqing`                                               |
| url_extract_path(url) [](id:url_extract_path)           | Extracts `path` from the URL. The result is of the varchar type.                       | `* \| select url_extract_path('https://console.cloud.tencent.com/cls?region=ap-chongqing')` | `/cls`                                                        |
| url_extract_port(url)  [](id:url_extract_port)          | Extracts `port` from the URL. The result is of the bigint type.                        | `* \| select url_extract_port('https://console.cloud.tencent.com:80/cls?region=ap-chongqing')` | `80`                                                         |
| url_extract_protocol(url)[](id:url_extract_protocol)        | Extracts `protocol` from the URL. The result is of the varchar type.                       | `* \| select url_extract_protocol('https://console.cloud.tencent.com:80/cls?region=ap-chongqing')` | `https`                                                      |
| url_extract_query(url)  [](id:url_extract_query)         | Extracts the key of `query` from the URL. The result is of the varchar type.                      | `* \| select url_extract_query('https://console.cloud.tencent.com:80/cls?region=ap-chongqing')` | `region=ap-chongqing`                                        |
| url_encode(value)  [](id:url_encode)              | Escapes `value` so that it can be used in `URL_query`.<ul  style="margin: 0;"><li>Letters will not be decoded.</li><li>.-\*\_ will not be encoded. </li><li>Spaces are decoded as +.</li><li>Other characters are decoded into the UTF-8 format.</li></ul> | `* \| select url_encode('https://console.cloud.tencent.com:80/cls?region=ap-chongqing')` | `https%3A%2F%2Fconsole.cloud.tencent.com%3A80%2Fcls%3Fregion%3Dap-chongqing` |
| url_decode(value)   [](id:url_decode)             | Decodes the URL.                                              | `* \| select url_decode('https%3A%2F%2Fconsole.cloud.tencent.com%3A80%2Fcls%3Fregion%3Dap-chongqing')` | `https://console.cloud.tencent.com:80/cls?region=ap-chongqing` |


