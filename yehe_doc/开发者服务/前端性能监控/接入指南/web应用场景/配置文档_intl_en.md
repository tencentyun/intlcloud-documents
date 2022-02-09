## Configuration Description
The configuration items in the configuration file are as detailed below:

| Configuration Item             | Description                                                         |
| ---------------- | ------------------------------------------------------------ |
| id               | It is a required string and is empty by default. <br>It is the project ID assigned by RUM.          |
| uin              | It is a recommended string and is the UIN field in the cookie by default.<br>It is the unique ID of the current user. When a log is reported, it will be used to check whether the user is in the allowlist. Its value can contain only letters, digits, and `@=._-`, and its regular expression is `/^[@=.0-9a-zA-Z_-]{1,60}$/`. |
| reportApiSpeed   | It is an optional boolean value or <span id="jump">[object](#exp2)</span> and is `false` by default.<br>It specifies whether to enable API speed test. |
| reportAssetSpeed | It is an optional boolean value and is `false` by default.<br>It specifies whether to enable static resource speed test.          |
| pagePerformance  | It is an optional boolean value or <span id="jump">[object](#exp3)</span> and is `true` by default.<br>It specifies whether to enable page speed test. |
| webVitals        | It is an optional boolean value and is `true` by default.<br>It specifies whether to enable Web Vitals speed test.       |
| onError          | It is an optional boolean value and is `true` by default.<br>It specifies whether to enable error listening in the current instance to get error logs. |
| aid              | It is an optional boolean value and is `true` by default.<br>It specifies whether to generate `aid` in the current instance.            |
| random           | It is an optional number and is 1 by default.<br>It is the sample rate. Value range: 0–1.                         |
| spa              | It is an optional boolean value and is `false` by default.<br>It specifies whether the current page is an SPA page. If the value is `true`, `hashchange` and the history API will be listened on to report the PV during page redirect. |
|  version           |  It is an optional string and is the SDK version number by default.<br>It is the version of the currently reported content. If the page uses PWA or an offline package, it can be used to judge the version of the code where the currently reported content is from. Its value can contain up to 60 letters, digits, and `=._-`, and its regular expression is `/^[0-9a-zA-Z.,:_-]{1,60}$/`. |
| delay            | It is an optional number and is 1000 ms by default. <br>It is the time period for reducing reporting traffic, within which multiple reports will be merged into one reporting request. |
| repeat           | It is an optional number and is 5 by default. <br>It is the number of repeated reports. After it is exceeded, the same error will not be reported again. |
| env	| It is an optional enum and is `Aegis.environment.production` by default. <br>It is the current environment where the project runs. |
| offlineLog       | It is an optional boolean value and is `false` by default. <br>It specifies whether to use offline log.              |
| offlineLogExp    | It is an optional number and is 3 by default.<br>It is the offline log validity period.            |
| api              | It is an optional object and is `{}` by default. Fields:<br><li>apiDetail: it specifies whether to report the API request parameters and returned value if an API fails. It is an optional boolean value and is `false` by default.<br><li>retCodeHandler: <code>Function(data: String, url: String, xhr: Object):{isErr: boolean, code: string}</code>: it is the hook function for return code reporting and will pass in the API response data, request `url`, and `xhr` object. <code>resourceTypeHandler: Function</code>: it is the request resource type correction hook function and will pass in the API `url`. Its returned value is <code>static</code> or <code>fetch</code>. For more information, see [api.retCodeHandler](#exp1).<br><li>reportRequest: it is a boolean value and is `false` by default. After it is enabled, `aegis.info` will report the full data with no need to configure the allowlist, and information of all APIs will be reported (you need to enable `reportApiSpeed` in the reporting API). |
| speedSample      | It is an optional boolean value and is `true` by default.<br>It specifies whether to sample the speed test logs (that is, each URL reports only one speed test log). |
| hostUrl | It is optional and is <code>//aegis.qq.com</code> by default.<br>It is the host address that affects all reported data. After the following URL addresses are set, they will overwrite the original reporting addresses. |
| url | It is an optional string and is <code>//aegis.qq.com/collect</code> by default. <br>It is the log reporting address. <br>You can set it to an empty string to disable log reporting. |
| pvUrl | It is an optional string and is <code>//aegis.qq.com/collect/pv</code> by default. <br>It is the PV reporting address.<br>You can set it to an empty string to disable PV reporting. |
| whiteListUrl | It is an optional string and is <code>//aegis.qq.com/collect/whitelist</code> by default.<br>It is the allowlist confirming API.<br>You can set it to an empty string to disable allowlist API request. |
| offlineUrl | It is an optional string and is <code>//aegis.qq.com/collect/offline</code> by default.<br>It is the offline log reporting address.<br>You can set it to an empty string to disable offline log reporting. |
| eventUrl | It is an optional string and is <code>//aegis.qq.com/collect/events</code> by default.<br>It is the custom event reporting address.<br>You can set it to an empty string to disable custom event reporting. |
| speedUrl | It is an optional string and is <code>//aegis.qq.com/speed</code> by default. <br>It is the speed test log reporting address.<br>You can set it to an empty string to disable speed test data reporting. |
| customTimeUrl | It is an optional string and is <code>//aegis.qq.com/speed/custom</code> by default.<br>It is the custom speed test reporting address.<br>You can set it to an empty string to disable custom speed test reporting. |
| performanceUrl | It is an optional string and is <code>//aegis.qq.com/speed/performance</code> by default.<br>It is the page performance reporting address.<br>You can set it to an empty string to disable page performance reporting. |
| webVitalsUrl | It is an optional string and is <code>//aegis.qq.com/speed/webvitals</code> by default.<br>It is the Web Vitals reporting address.<br>You can set it to an empty string to disable Web Vitals reporting. |
|dbConfig| It is an optional object. |
| ext1 | It is the additional dimension in custom reporting, which can be overwritten during reporting. It is an optional string. |
| ext2 | It is the additional dimension in custom reporting, which can be overwritten during reporting. It is an optional string. |
| ext3 | It is the additional dimension in custom reporting, which can be overwritten during reporting. It is an optional string. |

## Sample Code

### api.retCodeHandler[](id:exp1)
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
}

```
If your business requires that if the `code` is not 200 or `retCode` is not 0, the request is incorrect. To meet this requirement, you can simply configure as follows:
```javascript
new Aegis({
    // xxx
    reportApiSpeed: true, // You need to enable two speed test APIs; otherwise, no return code will be reported
    reportAssetSpeed: true,
    api: {
        retCodeHandler(data, url, xhr) { 
            // `data` is a string. If you want to get an object, you need to manually parse it
            // `url` is the request URL
            // The complete backend `xhr` response can be obtained through `xhr.response`
            try {
                data = JSON.parse(data)
            } catch(e) {}
            return {
                isErr: data.body.code !== 200 || data.body.retCode !== 0,
                code:  data.body.code
            }
        }
    }
})
```

### api.resourceTypeHandler
If the API is `http://example.com/test-api` and the returned `Content-Type` is `text/html`, Aegis will consider that the content returned by the API is a static resource. In this case, you can correct the judgment as follows:
```javascript
new Aegis({
    reportApiSpeed: true, // You need to enable two speed test APIs; otherwise, no return code will be reported
    reportAssetSpeed: true,
    api: {
        resourceTypeHandler(url) {
            if (url?.indexOf('http://example.com/test-api') != -1) {
                return 'fetch';
            }
        }
    }
})
```

### reportApiSpeed.urlHandler[](id:exp2)
If your page has RESTful APIs such as:  
`www.example.com/user/1000`
`www.example.com/user/1001`

You need to aggregate the following APIs when reporting the speed test data:
```javascript
new Aegis({
    // xxx
    reportApiSpeed: {
        urlHandler(url, payload) {
            if ((/www\.example\.com\/user\/\d*/).test(url)) {
                return 'www.example.com/user/:id';
            }
            return url;
        }
    }
    // xxx
})
```

### pagePerformance.urlHandler[](id:exp3)
If your page has RESTful APIs such as:  
`www.example.com/user/1000`
`www.example.com/user/1001`

You need to aggregate the page addresses when reporting the page speed test data:
```javascript
new Aegis({
    // xxx
    pagePerformance: {
        urlHandler() {
            if ((/www\.example\.com\/user\/\d*/).test(window.location.href)) {
                return 'www.example.com/user/:id';
            }
        }
    }
    // xxx
})
```
