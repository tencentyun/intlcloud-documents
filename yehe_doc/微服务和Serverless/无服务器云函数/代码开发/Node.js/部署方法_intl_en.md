
## Deployment Methods

Tencent Cloud SCF provides the following function deployment methods. For more information about how to create and update a function, see [Create and Update a Function](https://intl.cloud.tencent.com/document/product/583/19806).

- Uploading and deploying a zip package, as instructed in [Installing and Deploying Dependencies](#install)
- Editing and deploying functions via the console, as instructed in [Deployment Through Console](https://intl.cloud.tencent.com/document/product/583/32741).
- Using the command line, as instructed in [Deployment Through Serverless Cloud Framework](https://intl.cloud.tencent.com/document/product/583/32741).

## Installing and Deploying Dependencies[](id:install)

Currently, the SCF standard Node.js Runtime only supports writing to the `/tmp` directory, and other directories are read-only. Therefore, you need to install, package and upload the local dependent library for use. The Node.js dependency package can be uploaded with function codes to the cloud, or uploaded to the layer that will be bound to the required function.

### Online dependency installation

Node.js provides an online dependency installation feature as detailed in [Online Dependency Installation](https://intl.cloud.tencent.com/document/product/583/38105).

### Local dependency installation


#### Dependency manager

In Node.js, dependencies can be managed with the npm package manager.

#### Directions

Run the `npm install xxx` command in the code directory to install dependencies.


>!
>- Because the function is running on CentOS 7, install the dependency package in the same environment to avoid errors. For detailed directions, see [Using Container Image](https://intl.cloud.tencent.com/document/product/583/39009).
>- If some dependencies require dynamic link library, please manually copy these dependencies to the installation directory, and then package them for uploading. For more information, see [Installing Dependency with Docker](https://intl.cloud.tencent.com/document/product/583/38127).

#### Sample
1. Use the `index.js` code file shown below to install the `requests` dependency locally.
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

2. Run the `npm install request` command to install the requests dependency under the current directory of the project. 


### Packaging and uploading

You can upload dependencies together with the project, and use them through the `require` statement in function codes. You can also package and deploy dependencies to a layer, and bind the layer to a function being created to reuse them.

The zip package for deploying functions or layers can be generated automatically by a local folder via the console or manually. All the packaging should be under the project directory to place codes and dependencies in the root directory of the zip package. For more information, see [Packaging requirements](https://intl.cloud.tencent.com/document/product/583/32741).

