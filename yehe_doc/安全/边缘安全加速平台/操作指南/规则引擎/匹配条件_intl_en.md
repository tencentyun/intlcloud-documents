## Notes

A condition defines the standard for identifying a request, including:<li>Matching type </li><li>Operator </li><li>Value</li>

## Matching Type

| Type            | Description                             | Value (Sample)                       |
| --------------- | -------------------------------- | -------------------------------- |
| HOST            | Request host                        | `www.example.com`                |
| URL Path        | Request URL path                    | `/example/foo/bar`               |
| URL Full        | Complete request URL                | `https://www.example.com/foo`    |
| Query string      | Query string in the request URL          | Parameter name: `key` <br/>Parameter value: `value`   |
| File extension        | File extension of the request content | jpg, png, css                      |
| Filename        | Filename of the request content               | foo.txt                             |
| HTTP request header     | HTTP request header                    | Header name: `name`<br/>Header value: `value` |
| Country/Region of the client | Country/Region of the client IP          | US                             |
| All            | Any site request                     | -                                |

## Operator

| Type     | Description                                                         |
| -------- | ------------------------------------------------------------ |
| Equal to     | The request is equal to a specified value (value of the matching type).                       |
| Not equal to   | The request is not equal to a specified value (value of the matching type).                     |
| Exist     | A specified value exists in the request (HTTP header name or query parameter name). |
| Not exist   | A specified value does not exist in the request (HTTP header name or query parameter name). |
| Find matching items via regex | It supports [Google RE2 ](https://github.com/google/re2/blob/main/doc/syntax.txt) regular expressions. |

## Value

It indicates the content of the selected matching type.

### Wildcard

You can enter content containing wildcards for certain matching types:

| Type | Description            | Value (Sample)                                                   |
| ---- | --------------- | ------------------------------------------------------------ |
| *    | Matches 0 or multiple characters | If the `URL Path` is `/foo/*/bar`, both `/foo/example/bar`and `/foo/demo/bar` are valid values. |

### Ignoring the case

You can modify the case sensitivity of certain matching types. By default, they are case sensitive. If you enable the **Ignore case** switch, they will be case insensitive.
