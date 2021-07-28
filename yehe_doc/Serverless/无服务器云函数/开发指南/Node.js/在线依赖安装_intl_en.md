## Overview

Tencent Cloud SCF supports online dependency installation during function deployment.

## Features

>?Currently, online dependency installation is supported only for Node.js.

If "Online install dependency" is enabled in the function configuration, each time the code is uploaded, the SCF backend will check the `package.json` file in the root directory of the code package and try using `npm install` to install the dependencies based on the dependencies in `package.json`.

For example, if the `package.json` file in the project lists the following dependency:

```
{
      "dependencies": {
      "lodash": "4.17.15"
    }
}
```



Then this dependency will be imported into the function during the deployment:

```
const _ = require('lodash');
exports.handle = (event, context, callback) => {
    _.chunk(['a', 'b', 'c', 'd'], 2);
    // => [['a', 'b'], ['c', 'd']]
};
```

## Directions

You can implement the dependency installation feature of SCF in either of the following ways:

#### Enabling automatic dependency installation

1. Log in to the [SCF console](https://console.cloud.tencent.com/scf/index) and select the **Guangzhou** region.
2. Select **Function Service** on the left sidebar and select the function name on the **Function Service** list page.
3. Select the **Function code** tab and modify the function code as needed.
4. In the top-right corner of the IDE code editing window, click **<img src="https://main.qcloudimg.com/raw/2b9a01a346ba19c9050c6c160ec54f48.jpg" width="2%"></img>** and select **Automatic dependency installation: disable** in the drop-down list to enable automatic dependency installation as shown below:
![](https://main.qcloudimg.com/raw/a6e558badfef96cbbcc85bbe31a11b16.png)
5. Click **Deploy**, and the SCF backend will automatically install dependencies according to `package.json`.

#### Using npm to directly install Node.js dependencies
1. Select the **Terminal** tab on the menu bar at the top of the IDE code editing window and select **New Terminal** in the drop-down list.
2. Run the following command in the opened terminal to enter the function root directory `/src`.
``` plaintext
  cd src
```
10. Run the `npm` command to install the Node.js dependency package. For example, run the following command to add the `lodash` dependency package:
``` plaintext
  npm install lodash
```
![](https://main.qcloudimg.com/raw/530d6878c6d9711045a4cac6c9000071.png)
11. Click **Deploy** to package and sync the successfully installed dependency package and function together to the cloud.

