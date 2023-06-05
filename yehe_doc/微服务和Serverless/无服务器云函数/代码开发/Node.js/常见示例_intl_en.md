These examples provide code snippets based on Node.js 12.16 for your reference.

You can click [scf-nodejs-code-snippet](https://github.com/awesome-scf/scf-nodejs-code-snippet) to obtain the relevant code snippets and directly use them for deployment.

## Obtaining Environment Variables

This example shows you how to obtain all or a single environment variable.

```js
'use strict';
exports.main_handler = async (event, context) => {
		console.log(process.env)
    console.log(process.env.SCF_RUNTIME)
    return "Hello world"
};
```

## Formatting Local Time

This example uses the `moment` library to obtain the local time, and provides a time formatted output method to output date and time in the specified format.

The SCF environment uses the UTC format by default. To output in Beijing time, you can add the `TZ=Asia/Shanghai` environment variable to the function.

```js
'use strict';
const moment = require('moment')
exports.main_handler = async (event, context) => {
    let currentTime = moment(Date.now()).format('YYYY-MM-DD HH:mm:ss')
    console.log(currentTime)
    return "hello world"
};
```

## Initiating Network Connection in Function

This example shows you how to use the requests library to initiate network connections in a function and obtain page information. You can run the `npm install request` command under the project directory to install this dependent library.

```js
'use strict';
var request = require('request');
exports.main_handler = async (event, context) => {
    request('https://cloud.tencent.com/', function (error, response, body) {
        if (!error && response.statusCode == 200) {
            console.log(body) // Processing logic for successful request
        }
    })
    return "success"
};
```

