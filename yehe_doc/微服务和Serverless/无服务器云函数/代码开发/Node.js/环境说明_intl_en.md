## Node.js Version Selection

Currently, the following versions of Node.js programming language are supported:

- Node.js 16.13
- Node.js 14.18
- Node.js 12.16
- Node.js 10.15
- Node.js 8.9 (deactivating soon)
- Node.js 6.10 (deactivating soon)

You can choose a desired runtime environment when creating a function.

## Environment Variables

The environment variables built in the current Node.js runtime environment are as shown in the table below:

| Node.js Version | Environment Variable Key | Specific Value or Value Source |
| ------------- | ------------ | ------------------------------------------------------------ |
| Node.js 16.13 | `NODE_PATH`  | /var/user:/var/user/node_modules:/var/lang/node16/lib/node_modules:/opt:/opt/node_modules |
| Node.js 14.18 | `NODE_PATH`  | /var/user:/var/user/node_modules:/var/lang/node14/lib/node_modules:/opt:/opt/node_modules |
| Node.js 12.16 | `NODE_PATH`  | /var/user:/var/user/node_modules:/var/lang/node12/lib/node_modules:/opt:/opt/node_modules |
| Node.js 10.15 | `NODE_PATH`  | /var/user:/var/user/node_modules:/var/lang/node10/lib/node_modules:/opt:/opt/node_modules |
| Node.js 8.9   | `NODE_PATH`  | /var/user:/var/user/node_modules:/var/lang/node8/lib/node_modules:/opt:/opt/node_modules |
| Node.js 6.10  | `NODE_PATH`  | /var/user:/var/user/node_modules:/var/lang/node6/lib/node_modules:/opt:/opt/node_modules |

For more information on environment variables, see [Environment Variables](https://intl.cloud.tencent.com/document/product/583/32748).

## Included Library and Usage

> !   For Node.js 14.18 and later, the platform no longer has additional built-in dependency libraries. For more information on the dependencies required by code execution, see [Dependency Installation](https://intl.cloud.tencent.com/document/product/583/34879) and [Online Dependency Installation](https://intl.cloud.tencent.com/document/product/583/38105).

### COS SDK

SCF's runtime environment for Node.js 12.16 or earlier already contains the [COS SDK for Node.js](https://intl.cloud.tencent.com/document/product/436/8629), and the specific version is `cos-nodejs-sdk-v5`.

The COS SDK can be referenced and used within the code as follows:
```
var COS = require('cos-nodejs-sdk-v5');
```

For more information on how to use the COS SDK, see [COS SDK for Node.js](https://intl.cloud.tencent.com/document/product/436/8629).

### Built-in library in environment

 The following libraries are supported in Node.js runtime:


<dx-tabs>
::: Node.js 12.16
<table><thead>
<tr><th width="60%">Library Name</th><th width="40%">Version</th></tr>
</thead>
<tbody><tr>
<td align="left">cos-nodejs-sdk-v5</td>
<td align="left">2.5.20</td>
</tr>
<tr>
<td align="left">base64-js</td>
<td align="left">1.3.1</td>
</tr>
<tr>
<td align="left">buffer</td>
<td align="left">5.5.0</td>
</tr>
<tr>
<td align="left">crypto-browserify</td>
<td align="left">3.12.0</td>
</tr>
<tr>
<td align="left">ieee754</td>
<td align="left">1.1.13</td>
</tr>
<tr>
<td align="left">imagemagick</td>
<td align="left">0.1.3</td>
</tr>
<tr>
<td align="left">isarray</td>
<td align="left">2.0.5</td>
</tr>
<tr>
<td align="left">jmespath</td>
<td align="left">0.15.0</td>
</tr>
<tr>
<td align="left">lodash</td>
<td align="left">4.17.15</td>
</tr>
<tr>
<td align="left">microtime</td>
<td align="left">3.0.0</td>
</tr>
<tr>
<td align="left">npm</td>
<td align="left">6.13.4</td>
</tr>
<tr>
<td align="left">punycode</td>
<td align="left">2.1.1</td>
</tr>
<tr>
<td align="left">puppeteer</td>
<td align="left">2.1.1</td>
</tr>
<tr>
<td align="left">qcloudapi-sdk</td>
<td align="left">0.2.1</td>
</tr>
<tr>
<td align="left">querystring</td>
<td align="left">0.2.0</td>
</tr>
<tr>
<td align="left">request</td>
<td align="left">2.88.2</td>
</tr>
<tr>
<td align="left">sax</td>
<td align="left">1.2.4</td>
</tr>
<tr>
<td align="left">scf-nodejs-serverlessdb-sdk</td>
<td align="left">1.1.0</td>
</tr>
<tr>
<td align="left">tencentcloud-sdk-nodejs</td>
<td align="left">3.0.147</td>
</tr>
<tr>
<td align="left">url</td>
<td align="left">0.11.0</td>
</tr>
<tr>
<td align="left">uuid</td>
<td align="left">7.0.3</td>
</tr>
<tr>
<td align="left">xml2js</td>
<td align="left">0.4.23</td>
</tr>
<tr>
<td align="left">xmlbuilder</td>
<td align="left">15.1.0</td>
</tr>
</tbody></table>
:::
::: Node.js 10.15
<table>
<thead>
<tr><th width="60%">Library Name</th><th width="40%">Version</th></tr>
</thead>
<tbody><tr>
<td align="left">cos-nodejs-sdk-v5</td>
<td align="left">2.5.14</td>
</tr>
<tr>
<td align="left">base64-js</td>
<td align="left">1.3.1</td>
</tr>
<tr>
<td align="left">buffer</td>
<td align="left">5.4.3</td>
</tr>
<tr>
<td align="left">crypto-browserify</td>
<td align="left">3.12.0</td>
</tr>
<tr>
<td align="left">ieee754</td>
<td align="left">1.1.13</td>
</tr>
<tr>
<td align="left">imagemagick</td>
<td align="left">0.1.3</td>
</tr>
<tr>
<td align="left">isarray</td>
<td align="left">2.0.5</td>
</tr>
<tr>
<td align="left">jmespath</td>
<td align="left">0.15.0</td>
</tr>
<tr>
<td align="left">lodash</td>
<td align="left">4.17.15</td>
</tr>
<tr>
<td align="left">microtime</td>
<td align="left">3.0.0</td>
</tr>
<tr>
<td align="left">npm</td>
<td align="left">6.4.1</td>
</tr>
<tr>
<td align="left">punycode</td>
<td align="left">2.1.1</td>
</tr>
<tr>
<td align="left">puppeteer</td>
<td align="left">2.0.0</td>
</tr>
<tr>
<td align="left">qcloudapi-sdk</td>
<td align="left">0.2.1</td>
</tr>
<tr>
<td align="left">querystring</td>
<td align="left">0.2.0</td>
</tr>
<tr>
<td align="left">request</td>
<td align="left">2.88.0</td>
</tr>
<tr>
<td align="left">sax</td>
<td align="left">1.2.4</td>
</tr>
<tr>
<td align="left">scf-nodejs-serverlessdb-sdk</td>
<td align="left">1.0.1</td>
</tr>
<tr>
<td align="left">tencentcloud-sdk-nodejs</td>
<td align="left">3.0.104</td>
</tr>
<tr>
<td align="left">url</td>
<td align="left">0.11.0</td>
</tr>
<tr>
<td align="left">uuid</td>
<td align="left">3.3.3</td>
</tr>
<tr>
<td align="left">xml2js</td>
<td align="left">0.4.22</td>
</tr>
<tr>
<td align="left">xmlbuilder</td>
<td align="left">13.0.2</td>
</tr>
</tbody></table>

:::
::: Node.js 8.9
<table>
<thead>
<tr><th width="60%">Library Name</th><th width="40%">Version</th></tr>
</thead>
<tbody><tr>
<td align="left">cos-nodejs-sdk-v5</td>
<td align="left">2.5.8</td>
</tr>
<tr>
<td align="left">base64-js</td>
<td align="left">1.2.1</td>
</tr>
<tr>
<td align="left">buffer</td>
<td align="left">5.0.7</td>
</tr>
<tr>
<td align="left">crypto-browserify</td>
<td align="left">3.11.1</td>
</tr>
<tr>
<td align="left">ieee754</td>
<td align="left">1.1.8</td>
</tr>
<tr>
<td align="left">imagemagick</td>
<td align="left">0.1.3</td>
</tr>
<tr>
<td align="left">isarray</td>
<td align="left">2.0.2</td>
</tr>
<tr>
<td align="left">jmespath</td>
<td align="left">0.15.0</td>
</tr>
<tr>
<td align="left">lodash</td>
<td align="left">4.17.4</td>
</tr>
<tr>
<td align="left">npm</td>
<td align="left">5.6.0</td>
</tr>
<tr>
<td align="left">punycode</td>
<td align="left">2.1.0</td>
</tr>
<tr>
<td align="left">puppeteer</td>
<td align="left">1.14.0</td>
</tr>
<tr>
<td align="left">qcloudapi-sdk</td>
<td align="left">0.1.5</td>
</tr>
<tr>
<td align="left">querystring</td>
<td align="left">0.2.0</td>
</tr>
<tr>
<td align="left">request</td>
<td align="left">2.87.0</td>
</tr>
<tr>
<td align="left">sax</td>
<td align="left">1.2.4</td>
</tr>
<tr>
<td align="left">tencentcloud-sdk-nodejs</td>
<td align="left">3.0.56</td>
</tr>
<tr>
<td align="left">url</td>
<td align="left">0.11.0</td>
</tr>
<tr>
<td align="left">uuid</td>
<td align="left">3.1.0</td>
</tr>
<tr>
<td align="left">xml2js</td>
<td align="left">0.4.17</td>
</tr>
<tr>
<td align="left">xmlbuilder</td>
<td align="left">9.0.1</td>
</tr>
</tbody></table>
:::
::: Node.js 6.10
<table>
<thead>
<tr><th width="60%">Library Name</th><th width="40%">Version</th></tr>
</thead>
<tbody><tr>
<td align="left">base64-js</td>
<td align="left">1.2.1</td>
</tr>
<tr>
<td align="left">buffer</td>
<td align="left">5.0.7</td>
</tr>
<tr>
<td align="left">cos-nodejs-sdk-v5</td>
<td align="left">2.0.7</td>
</tr>
<tr>
<td align="left">crypto-browserify</td>
<td align="left">3.11.1</td>
</tr>
<tr>
<td align="left">ieee754</td>
<td align="left">1.1.8</td>
</tr>
<tr>
<td align="left">imagemagick</td>
<td align="left">0.1.3</td>
</tr>
<tr>
<td align="left">isarray</td>
<td align="left">2.0.2</td>
</tr>
<tr>
<td align="left">jmespath</td>
<td align="left">0.15.0</td>
</tr>
<tr>
<td align="left">lodash</td>
<td align="left">4.17.4</td>
</tr>
<tr>
<td align="left">npm</td>
<td align="left">3.10.10</td>
</tr>
<tr>
<td align="left">punycode</td>
<td align="left">2.1.0</td>
</tr>
<tr>
<td align="left">qcloudapi-sdk</td>
<td align="left">0.1.5</td>
</tr>
<tr>
<td align="left">querystring</td>
<td align="left">0.2.0</td>
</tr>
<tr>
<td align="left">request</td>
<td align="left">2.87.0</td>
</tr>
<tr>
<td align="left">sax</td>
<td align="left">1.2.4</td>
</tr>
<tr>
<td align="left">tencentcloud-sdk-nodejs</td>
<td align="left">3.0.10</td>
</tr>
<tr>
<td align="left">url</td>
<td align="left">0.11.0</td>
</tr>
<tr>
<td align="left">uuid</td>
<td align="left">3.1.0</td>
</tr>
<tr>
<td align="left">xml2js</td>
<td align="left">0.4.17</td>
</tr>
<tr>
<td align="left">xmlbuilder</td>
<td align="left">9.0.1</td>
</tr>
</tbody></table>


:::
</dx-tabs>
