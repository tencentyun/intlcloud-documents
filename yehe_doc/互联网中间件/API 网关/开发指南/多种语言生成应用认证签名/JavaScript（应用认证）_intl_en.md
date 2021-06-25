## Overview

This document describes how to use the application-enabled authentication mode for the authentication management of your APIs in JavaScript.

## Directions

1. Create an API in the [API Gateway console](https://console.cloud.tencent.com/apigateway/index?rid=1), and select “Application-Enabled” as the authentication type. For details, see [API Creation Overview](https://intl.cloud.tencent.com/document/product/628/11795).
2. Publish the service to which the API belongs to the release environment. For details, see [Service Release and Deactivation](https://intl.cloud.tencent.com/document/product/628/11809).
3. Create an application on the [Application](https://console.cloud.tencent.com/apigateway/app) page.
4. Select the application you created in the application list and click **Bind API**. In the pop-up window, select a service and an API, and click **Submit**. Then you can bind the selected API to the application.
5. Generate signing information in JavaScript by referring to the [Sample Code](#sample-code).

## Environmental Dependencies

API Gateway provides sample codes with the request body in JSON format and form-data format. Please select as needed.

## Notes

- For information on application lifecycle management, API authorization, and how to bind an API to an application, please see [Application Management](https://intl.cloud.tencent.com/document/product/628/40306).
- For information on signature generation, please see [Application-Enabled Authentication](https://intl.cloud.tencent.com/document/product/628/40304).

<span id="sample code"></span>
## Sample Code

### Sample codes with the request body in JSON format

<dx-codeblock>
:::  JavaScript
const https = require('https')
const crypto = require('crypto')

// Application ApiAppKey
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



### Sample codes with the request body in form-data format

<dx-codeblock>
:::  JavaScript
const https = require('https')
const crypto = require('crypto')
const querystring = require('querystring')

// Application ApiAppKey
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

const sorted_body = sortBody(body)
const signingStr = buildSignStr(sorted_body)
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

function sortBody(body) {
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
    options.path + '?' + keyStr,
  ].join('\n')
}
:::
</dx-codeblock>

