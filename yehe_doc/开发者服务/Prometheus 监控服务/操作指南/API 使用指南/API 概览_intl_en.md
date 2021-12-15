## HTTP API

All stable HTTP APIs of Prometheus are under the path `/api/v1`. When you need to query monitoring data, you can request data through query APIs. To submit data, you can use the [remote write](https://prometheus.io/docs/practices/remote_write/) protocol or [Pushgateway](https://prometheus.io/docs/practices/pushing/).

## Supported APIs

| API | Description | Authentication Required | Method |
| --------------------------------- | :-------------------: | -------- | ------------ |
| /api/v1/query | Query | Yes | GET/POST |
| /api/v1/query_range | Range query | Yes | GET/POST |
| /api/v1/series | Series query | Yes | GET/POST |
| /api/v1/labels | Labels query | Yes | GET/POST |
| /api/v1/label/&lt;label_name>/values | Label value query | Yes | GET |
| /api/v1/prom/write | Data submission through remote write | Yes | remote write |
| Pushgateway | Data submission through Pushgateway | Yes | SDK |

## Authentication Method

Authentication is enabled by default, so all APIs require authentication, and all authentication methods support bearer token and basic authentication.

### Bearer token

A bearer token is generated as an instance is generated and can be queried in the console. For more information on bearer token, please see [Bearer Authentication](https://swagger.io/docs/specification/authentication/bearer-authentication/).

### Basic auth

Basic auth is compatible with the native Prometheus query authentication method. The username is your `APPID`, and the password is the bearer token (generated when the instance is generated), which can be queried in the console. For more information on basic auth, please see [Basic Authentication](https://swagger.io/docs/specification/authentication/basic-authentication/).   


## Data Return Format

The response data of all APIs is in JSON format. Every successful request will return a status code of `2xx`.

An invalid request will return a piece of JSON data containing an error object and a status code as described below:

| Status Code | Description |
| ------ | -------------------------------------------- |
| 401 | Authentication failed |
| 400 | A parameter was missing or incorrect |
| 422 | An invalid expression couldn't be specified (RFC4918) |
| 503 | The query was unavailable or canceled |

Below is a response template for invalid requests:

```
{
  "status": "success" | "error",
  "data": <data>,

  // When the `status` is `error`, the following data will be returned
  "errorType": "<string>",
  "error": "<string>",

  // When there is a warning message during request execution, this field will be filled and returned
  "warnings": ["<string>"]
}
```
