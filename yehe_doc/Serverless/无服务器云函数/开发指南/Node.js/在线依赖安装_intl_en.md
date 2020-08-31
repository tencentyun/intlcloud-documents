## Overview
Tencent Cloud SCF supports online dependency installation during function deployment.

## Features
>?Currently, online dependency installation is supported only for Node.js.
>

If "Online install dependency" is enabled in the function configuration, each time the code is uploaded, the SCF backend will check the `package.json` file in the root directory of the code package and try using npm to install the dependencies based on the dependencies in `package.json`.

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

### Enabling in console when creating function
1. Log in to the [SCF Console](https://console.cloud.tencent.com/scf/index) and select **Guangzhou**.
2. Select **Function Service** on the left sidebar and click **Create** on the "Function Service" list page.
3. On the "Create Function" page, enter the function information as needed and click **Next**.
4. On the "Function Configuration" page, configure the function as needed and select "Online install dependency" as the upload method at the bottom of the page.

>?Every time the code is uploaded, the SCF backend will automatically install the dependencies.
5. Click **Complete**.

### Enabling in the console when updating function
1. Log in to the [SCF Console](https://console.cloud.tencent.com/scf/index) and select **Guangzhou**.
2. Select **Function Service** on the left sidebar and select the function name on the "Function Service" list page.
3. Select the "Function code" tab, modify the function code as needed, and select "Online install dependency" as the upload method at the bottom of the page.

>?Every time the code is updated, the SCF backend will automatically install the dependencies.
5. Click **Save**.

### Using npm to directly install Node.js dependencies
>!You need to install the dependencies locally and upload the code package to the SCF platform in "Upload All" mode.
>
You can use the [SCF CLI](https://intl.cloud.tencent.com/document/product/583/32753) to directly run the relevant command to install the dependencies in the function folder; for example, run the following command to add the `lodash` dependency:
```
npm install lodash
```




