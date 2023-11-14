## Scenario

This document describes how to use the application-enabled authentication mode for the authentication management of your APIs in JavaScript.

## Operation Directions

1. In the [API Gateway console](https://console.cloud.tencent.com/apigateway/index?rid=1), create an API and select the authentication type as **App authentication**. To learn more about the authentication types, please find the documentation for different types of backends in [Creating API - Overview](https://intl.cloud.tencent.com/document/product/628/11795).
2. Release the service where the API resides to an environment. See [Service Release and Deactivation](https://intl.cloud.tencent.com/document/product/628/11809).
3. Create an application on the [Application](https://console.cloud.tencent.com/apigateway/app) page in the console.
4. Select the created application in the application list, click **Bind API**, select the service and API, and click **Submit** to bind the application to the API.
5. Generate signing information in JavaScript by referring to the [Sample Code](#Sample-Code).

## Environmental Dependencies

API Gateway provides sample codes with the request body in JSON format and form-data format. Please select as needed.

## Note

- For more information on operations such as application lifecycle management, authorizing an app to access the API, and binding an app with an API, please see [Application Management](https://intl.cloud.tencent.com/document/product/628/40306).
- For the application signature generation process, please see [Application Authentication](https://intl.cloud.tencent.com/document/product/628/40304).

## Sample Code[](id:Sample-Code)

### Sample codes with the request body in JSON format

<dx-codeblock>
:::  JavaScript
const https = require('https')
const crypto = require('crypto')

// Application's `ApiAppKey`
const apiAppKey = 'APIDLIA6tMfqsinsadaaaaaaaapHLkQ1z0kO5n5P'
// Application ApiAppSecret
const apiAppSecret = 'Dc44ACV2Da3Gm9JVaaaaaaaaumYRI4CZfVG8Qiuv'

const dateTime = new Date().toUTCString()
const body = {
  arg1: 'a',
  arg2: 'b',
}
const md5 = crypto.createHash('md5').update(JSON.stringify(body), 'utf8').digest('hex')
const contentMD5 = Buffer.from(md5).toString('base64')
const options = {
  hostname: 'service-xxxxxxxx-1234567890.gz.apigw.tencentcs.com',
  port: 443,
  path: '/data',
  method: 'POST',
  headers: {
    Accept: 'application/json',
    'Content-Type': 'application/json',
    'Content-MD5': contentMD5,
    'Content-Length': JSON.stringify(body).length,
    'x-date': dateTime,
  },
}

const signingStr = [
  `x-date: ${dateTime}`,
  options.method,
  options.headers.Accept,
  options.headers['Content-Type'],
  contentMD5,
  options.path,
].join('\n')
const signing = crypto.createHmac('sha1', apiAppSecret).update(signingStr, 'utf8').digest('base64')
const sign = `hmac id="${apiAppKey}", algorithm="hmac-sha1", headers="x-date", signature="${signing}"`
options.headers.Authorization = sign

const req = https.request(options, (res) => {
  console.log(`STATUS: ${res.statusCode}`)
  res.on('data', (chunk) => {
    console.log('BODY: ' + chunk)
  })
})
req.on('error', (error) => {
  console.error(error)
})
req.write(JSON.stringify(body))
req.end()
:::
</dx-codeblock>



### Sample code with the request body in form-data format

<dx-codeblock>
:::  JavaScript
const https = require('https')
const crypto = require('crypto')
const querystring = require('querystring')
const url = require('url')

// Application's `ApiAppKey`
const apiAppKey = 'APIDLIA6tMfqsinsadaaaaaaaapHLkQ1z0kO5n5P'
// Application ApiAppSecret
const apiAppSecret = 'Dc44ACV2Da3Gm9JVaaaaaaaaumYRI4CZfVG8Qiuv'

const dateTime = new Date().toUTCString()
const body = {
  arg1: 'a',
  arg2: 'b',
}
const contentMD5 = ''
const options = {
  hostname: 'service-xxxxxxxx-1234567890.gz.apigw.tencentcs.com',
  port: 443,
  path: '/data',
  method: 'POST',
  headers: {
    Accept: 'application/json',
    'Content-Type': 'application/x-www-form-urlencoded',
    'x-date': dateTime,
  },
}

// Splicing form parameter and query parameter and sort them according to the dictionary
const parsedPath = url.parse(options.path, true)
const sortedQueryParams = sortQueryParams({ ...body, ...parsedPath.query })
const signingStr = buildSignStr(sortedQueryParams)
const signing = crypto.createHmac('sha1', apiAppSecret).update(signingStr, 'utf8').digest('base64')
const sign = `hmac id="${apiAppKey}", algorithm="hmac-sha1", headers="x-date", signature="${signing}"`

options.headers.Authorization = sign

// Send the request
const req = https.request(options, (res) => {
  console.log(`STATUS: ${res.statusCode}`)
  res.on('data', (chunk) => {
    console.log('BODY: ' + chunk)
  })
})
req.on('error', (error) => {
  console.error(error)
})
req.write(querystring.stringify(body))
req.end()

function sortQueryParams(body) {
  const keys = Object.keys(body).sort()
  let signKeys = []
  for (let i = 0; i < keys.length; i++) {
    signKeys.push(keys[i])
  }
  // Sort in lexicographical order
  return signKeys.sort()
}

function buildSignStr(sorted_body) {
  const keyStr = sorted_body
    .map((item) => {
      return `${item}=${body[item]}`
    })
    .join('&')
  return [
    `x-date: ${dateTime}`,
    options.method,
    options.headers.Accept,
    options.headers['Content-Type'],
    contentMD5,
    `${parsedPath.pathname}${keyStr ? `?${keyStr}` : ''}`,
  ].join('\n')
}
:::
</dx-codeblock>

