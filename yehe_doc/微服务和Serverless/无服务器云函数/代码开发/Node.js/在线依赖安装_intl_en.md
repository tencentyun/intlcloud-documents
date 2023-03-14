## Overview

Tencent Cloud SCF supports online dependency installation during function deployment.

## Features

>?Online dependency installation is supported only for Node.js.

If **Online install dependency** is enabled in the function configuration, each time the code is uploaded, the SCF backend will check the `package.json` file in the root directory of the code package and try using `npm install` to install the dependencies based on the dependencies in `package.json`.

For example, if the `package.json` file in the project lists the following dependency:

```json
{
      "dependencies": {
      "lodash": "4.17.15"
    }
}
```



Then this dependency will be imported into the function during the deployment:

```js
const _ = require('lodash');
exports.handle = (event, context, callback) => {
    _.chunk(['a', 'b', 'c', 'd'], 2);
    // => [['a', 'b'], ['c', 'd']]
};
```

## Directions

1. Log in to the [SCF console](https://console.cloud.tencent.com/scf) and select **Guangzhou** as the region.
2. Select **Functions** on the left sidebar and locate the target function.
3. Select the **Function codes** tab and modify the function code as needed.
4. In the top-right corner of the IDE code editing window, click **<img src="https://main.qcloudimg.com/raw/2b9a01a346ba19c9050c6c160ec54f48.jpg" width="2%"></img>** and select **Automatic dependency installation: disable** in the drop-down list to enable automatic dependency installation as shown below: 
	 ![](https://main.qcloudimg.com/raw/a6e558badfef96cbbcc85bbe31a11b16.png)
   After enabling online installation, refresh the page. In the bottom right corner of the code editing page, click **Switch to Old Editor**. In **Upload method**, select **Online install dependency**.
	 ![](https://qcloudimg.tencent-cloud.cn/raw/d268d8687df5e420ba7f296678d0933a.png)
5. Click **Deploy**, and SCF will automatically install dependencies according to `package.json`.
