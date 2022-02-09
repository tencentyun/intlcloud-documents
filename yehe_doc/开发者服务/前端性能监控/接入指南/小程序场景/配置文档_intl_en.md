## Configuration Description
The configuration items in the configuration file are as detailed below:

| Configuration Item       | Description                             |
| -------------- | ------------------------------------------------------------ |
| id       | It is a required number and is empty by default. <br>It is the project key assigned by your platform.        |
| uin      | It is a recommended string and is the UIN field in the cookie by default.<br>It is the unique ID of the current user. When a log is reported, it will be used to check whether the user is in the allowlist. Its value can contain only letters, digits, and `@=._-`, and its regular expression is `/^[@=.0-9a-zA-Z_-]{1,60}$/`. |
| reportApiSpeed | It is an optional boolean value and is `false` by default. <br>It specifies whether to enable API speed test.         |
| version    | It is an optional string and is the SDK version number by default.<br>It is the version of the currently reported content. If the page uses PWA or an offline package, it can be used to judge the version of the code where the currently reported content is from. Its value can contain up to 60 letters, digits, and `.,:_-`, and its regular expression is `/^[0-9a-zA-Z.,:_-]{1,60}$/`. |
| delay      | It is an optional number and is 1000 ms by default. <br>It is the time period for reducing reporting traffic, within which multiple reports will be merged into one reporting request. |
| repeat     | It is an optional number and is 5 by default. <br>It is the number of repeated reports. After it is exceeded, the same error will not be reported again. |
| env        | It is an optional enum and is `Aegis.environment.production` by default. <br>It is the current environment where the project runs. |
| spa        | It is an optional boolean value and is `false` by default. <br>It specifies whether to report the PV during page redirect in the mini program. |
| offlineLog   | It is an optional boolean value and is `false` by default. <br>It specifies whether to use offline log.        |
| offlineLogExp  | It is an optional number and is 3 by default.<br>It is the offline log validity period.            |
| url      | It is an optional string and is `//aegis.qq.com/collect` by default. <br>It is the log reporting address. <br>You can set it to an empty string to disable log reporting.  |
| pvUrl | It is an optional string and is `//aegis.qq.com/collect/pv` by default. <br>It is the PV reporting address.<br>You can set it to an empty string to disable PV reporting. |
| whiteListUrl | It is an optional string and is `//aegis.qq.com/collect/whitelist` by default.<br>It is the allowlist confirming API.<br>You can set it to an empty string to disable allowlist API request. |
| offlineUrl | It is an optional string and is `//aegis.qq.com/collect/offline` by default.<br>It is the offline log reporting address.<br>You can set it to an empty string to disable offline log reporting. |
| eventUrl | It is an optional string and is `//aegis.qq.com/collect/events` by default.<br>It is the custom event reporting address.<br>You can set it to an empty string to disable custom event reporting. |
| speedUrl | It is an optional string and is `//aegis.qq.com/speed` by default. <br>It is the speed test log reporting address.<br>You can set it to an empty string to disable speed test data reporting. |
| customTimeUrl | It is an optional string and is `//aegis.qq.com/speed/custom` by default.<br>It is the custom speed test reporting address.<br>You can set it to an empty string to disable custom speed test reporting.|
| performanceUrl | It is an optional string and is `//aegis.qq.com/speed/performance` by default.<br>It is the page performance reporting address.<br>You can set it to an empty string to disable page performance reporting. |
| setDataReportConfig | It is an optional object and is `{}` by default. Fields:<br>disabled: it specifies whether to disable `setData` data reporting. It is an optional boolean value and is `false` by default.<br>timeThreshold: it is the reporting duration threshold. It is an optional number and is 30 by default. Only data whose update duration exceeds this threshold will be reported.<br>withDataPaths: it specifies whether to report the field information updated currently. It is an optional boolean value and is `true` by default.|
| api | It is an optional object and is `{}` by default. Fields:<br><li>apiDetail: it specifies whether to report the API request parameters and returned value if an API fails. It is an optional boolean value and is `false` by default.<br><li>retCodeHandler: it is the hook function for return code reporting and will pass in the API response data. The returned value is <code>{isErr: boolean, code: string}</code>. For more information, see [api.retCodeHandler](#exp1).<br><li>reportRequest: it is a boolean value and is `false` by default. After it is enabled, `aegis.info` will report the full data with no need to configure the allowlist, and information of all APIs will be reported (you need to enable `reportApiSpeed` in the reporting API). |
| ext1       | It is the additional dimension in custom reporting, which can be overwritten during reporting. It is an optional string. |
| ext2       | It is the additional dimension in custom reporting, which can be overwritten during reporting. It is an optional string. |
| ext3       | It is the additional dimension in custom reporting, which can be overwritten during reporting. It is an optional string. |

## Sample Code

#### api.retCodeHandler[](id:exp1)
If the backend returns the following data:
```json
{
  body: {
    code: 200,
    retCode: 0,
    data: {
        // xxx
  }
}

```
If your business requires that if the `code` is not 200 or `retCode` is not 0, the request is incorrect. To meet this requirement, you can simply configure as follows:
```javascript
new Aegis({
// xxx
  reportApiSpeed: true, // You need to enable two speed test APIs; otherwise, no return code will be reported
  reportAssetSpeed: true,
  api: {
    retCodeHandler(data) {
// Note that the obtained `data` is a string. If you want to get an object, you need to manually parse it
      try {
        data = JSON.parse(data)
      } catch (e) {
      }
      return {
        isErr: data.body.code !== 200 || data.body.retCode !== 0,
        code: data.body.code
      }
    }
  }
})
```
