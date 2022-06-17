## Built-In Dependencies

Some common dependency libraries have been built in various runtimes of SCF, which can be queried in the corresponding runtime code development guide:

- [Node.js](https://intl.cloud.tencent.com/document/product/583/11060)
- [Python](https://intl.cloud.tencent.com/document/product/583/40323) 
- [PHP](https://intl.cloud.tencent.com/document/product/583/17531)
- [Go](https://intl.cloud.tencent.com/document/product/583/18032)

## Installing Dependency Libraries

You can save all the dependency libraries of the SCF code in the code package and upload it to the cloud for use by SCF. SCF supports the following runtimes and usage methods:


### Node.js runtime

The Node.js runtime supports the following three dependency library installation methods:

<dx-tabs>
::: Package the dependency libraries and code together for upload
Use a dependency management tool such as npm to install the dependencies locally and upload them together with the function code.
<dx-alert infotype="notice" title="">
When you package them, the function entry file needs to be put in the root directory of the `zip` package. If you package the entire folder as the `zip` package and upload it, function creation will fail because the entry file cannot be found in the root directory after decompression.
</dx-alert>
This document takes installing the `lodash` library as an example:

1. Run the `mkdir test-package` command in the local terminal to create a directory for storing the function code and dependency libraries.
2. Run the following command to install the `lodash` dependency library in this directory.

```bash
cd test-package
npm install lodash
```

3. Create the function entry file `index.js` in this directory and import the `lodash` library in the code.

```js
'use strict';
const _ = require('lodash');
exports.main_handler = async (event, context) => {
     console.log("Hello World")
     console.log(event)
     console.log(event["non-exist"])
     console.log(context)
     return event
};
```

4. Compress the function code and dependency libraries into a zip package, upload the package in the [SCF console](https://console.cloud.tencent.com/scf), and create a function in the following steps:
   1. Log in to the [SCF console](https://console.cloud.tencent.com/scf) and click **Functions** on the left sidebar.
   2. Select the region where to create a function at the top of the page and click **Create** to enter the function creation process.
   3. Enter the basic information of the function on the **Create function** page as shown below:
      ![](https://main.qcloudimg.com/raw/e3b4a740329a13d7058a2d5e6a1665f4.png)
      - **Creation method**: Select **Custom**.
      - **Runtime environment**: Select **Node.js 12.16**.
      - **Submitting method**: Select **Local ZIP file**.
   4. Click **Complete**.

:::
::: Install dependencies online
The Node.js runtime provides an online dependency installation feature, which can install dependencies online according to the dependency information configured in `package.json`. For more information, see [Online Dependency Installation](https://intl.cloud.tencent.com/document/product/583/38105).
:::
::: Use dependency management tools
[Serverless Web IDE](https://intl.cloud.tencent.com/document/product/583/39962), SCF's online editor, provides a terminal feature and builds the package management tool `npm` in the terminal.

>! Serverless Web IDE has a delay in supporting newer versions of runtime environments. If the console does not open up the Serverless Web IDE for the corresponding runtime environment, package and upload the dependency library together with the code for dependency installation or install the dependency online.

This document takes installing the `lodash` library in the terminal as an example:

1. Log in to the [SCF console](https://console.cloud.tencent.com/scf/index?rid=1) and select **Functions** on the left sidebar.
2. In the function list, click a function name to enter the function details page.
3. On the **Function management** page, select **Function codes** > **Edit codes** to view and edit the function.
4. Select **Terminal** > **New terminal** on the topbar of the IDE to open the terminal window.
5. Run the following command in the terminal to install the `lodash` dependency library:
```bash
cd src  # The dependency library needs to be installed in a directory at the same level as the function entry file, that is, you need to enter the `src` directory before installing the dependency.
npm install lodash # You can view the npm version through the terminal
```
6. After the installation is completed, view `package.json` and `node_modules` in the file tree on the left side of the IDE.
7. After you click **Deploy**, the dependency library can be packaged and uploaded to the cloud together with the function code.
   :::
   </dx-tabs>






### Python runtime

The Python runtime supports the following two dependency library installation methods:

<dx-tabs>
::: Package the dependency libraries and code together for upload
Use a dependency management tool such as pip to install the dependencies locally and upload them together with the function code.
<dx-alert infotype="notice" title="">

- When you package them, the function entry file needs to be put in the root directory of the `zip` package. If you package the entire folder as the `zip` package and upload it, function creation will fail because the entry file cannot be found in the root directory after decompression.
- Due to runtime environment differences, confirm that the installed dependency version is adapted to the function runtime environment.
- The function runtime environment is CentOS 7, and you need to install the dependencies in the same environment. If not, an error where the dependencies cannot be found may occur while running the function after upload.
- If some dependencies involve a dynamic link library, such as Pandas in Python 3.6, you need to manually copy the relevant dependency package to the dependency installation directory before packaging and uploading them. For more information, see [Installing Dependency with Docker](https://intl.cloud.tencent.com/document/product/583/38127). You can also use the online IDE for installation.
  </dx-alert>
  This document takes installing the `numpy` library as an example:

1. Run the `mkdir test-package` command in the local terminal to create a directory for storing the function code and dependency libraries.
2. Run the following command to install the `numpy` dependency library in this directory.
```bash
cd test-package
pip install numpy -t . # Check whether the pip version you are using is adapted to the function runtime environment
```
3. Create the function entry file `index.py` in this directory and import the `numpy` library in the code.
```python
# -*- coding: utf8 -*-
import json
import numpy
def main_handler(event, context):
     print("Received event: " + json.dumps(event, indent = 2)) 
     print("Received context: " + str(context))
     print("Hello world")
     return("Hello World")
```
4. Compress the function code and dependency libraries into a zip package, upload the package in the [SCF console](https://console.cloud.tencent.com/scf), and create a function in the following steps:
   1. Log in to the [SCF console](https://console.cloud.tencent.com/scf) and click **Functions** on the left sidebar.
   2. Select the region where to create a function at the top of the page and click **Create** to enter the function creation process.
   3. Enter the basic information of the function on the **Create function** page as shown below:
      ![](https://main.qcloudimg.com/raw/e3b4a740329a13d7058a2d5e6a1665f4.png)
      - **Creation method**: Select **Custom**.
      - **Runtime environment**: Select **Python 3.6**.
      - **Submitting method**: Select **Local ZIP file**.
   4. Click **Complete**.

:::
::: Use dependency management tools
[Serverless Web IDE](https://intl.cloud.tencent.com/document/product/583/39962), SCF's online editor, provides a terminal feature and builds the package management tool `pip` in the terminal.

>! Serverless Web IDE has a delay in supporting newer versions of runtime environments. If the console does not open up the Serverless Web IDE for the corresponding runtime environment, package and upload the dependency library together with the code for dependency installation or install the dependency online.

This document takes installing the `numpy` library in the terminal as an example:

1. Log in to the [SCF console](https://console.cloud.tencent.com/scf/index?rid=1) and select **Functions** on the left sidebar.
2. In the function list, click a function name to enter the function details page.
3. On the **Function management** page, select **Function codes** > **Edit codes** to view and edit the function.
4. Select **Terminal** > **New terminal** on the topbar of the IDE to open the terminal window.
5. Run the following command in the terminal to install the `numpy` dependency library:
```bash
cd src  # The dependency library needs to be installed in a directory at the same level as the function entry file, that is, you need to enter the `src` directory before installing the dependency.
pip install numpy -t . # You can view the pip version through the terminal to check whether it is adapted to the function runtime environment
```
6. After the installation is completed, view the installed dependency libraries in the file tree on the left side of the IDE.
7. After you click **Deploy**, the dependency library can be packaged and uploaded to the cloud together with the function code.
   <dx-alert infotype="notice" title="">
- You can run `pip freeze > requirements.txt` to generate the `requirements.txt` files for all dependencies in the local environment.
- Run `pip install -r requirements.txt -t .` in the terminal of the IDE to install the dependency package according to the configuration in `requirements.txt`.
  </dx-alert>
  :::
  </dx-tabs>


### PHP runtime



>! The PHP versions supported by SCF are 5.6 and 7.2. Different minor versions of PHP may be incompatible. Check the version number first before installing dependencies.


<dx-tabs>
::: Install custom libraries
Use a dependency management tool such as Composer to install the dependencies locally and upload them together with the function code.
<dx-alert infotype="notice" title="">
When you package them, the function entry file needs to be put in the root directory of the `zip` package. If you package the entire folder as the `zip` package and upload it, function creation will fail because the entry file cannot be found in the root directory after decompression.
</dx-alert>
This document takes installing the `requests` library for PHP 7 as an example:

1. Run the `mkdir test-package` command in the local terminal to create a directory for storing the function code and dependency libraries.
2. Create `Composer.json` under `test-package` and specify the dependency library and version to be installed.
```json
{
"require": {
 "requests": ">=1.0"
	}
}
```
3. Run the following command to install the `requests` dependency library in this directory.
```bash
cd test-package
composer install
```
4. Create the function entry file `index.php` in this directory and import the `requests` library in the code.
```php
<?php
require 'vendor/autoload.php';
function main_handler($event, $context) {
    return "hello world";
}
?> 
```

5. Compress the function code and dependency libraries into a zip package, upload the package in the [SCF console](https://console.cloud.tencent.com/scf), and create a function in the following steps:
   1. Log in to the [SCF console](https://console.cloud.tencent.com/scf) and click **Functions** on the left sidebar.
   2. Select the region where to create a function at the top of the page and click **Create** to enter the function creation process.
   3. Enter the basic information of the function on the **Create function** page as shown below:
      ![](https://main.qcloudimg.com/raw/5112f6d762b1e90a3b62ad7446da0a79.png)
    - **Creation method**: Select **Custom**.
    - **Runtime environment**: Select **PHP 7**.
    - **Submitting method**: Select **Local ZIP file**.
   4. Click **Complete**.
   :::
   ::: Install custom extensions
   Create the extension folder `php_extension` in a directory at the same level as the function entry file, add the custom extension file `.so` and configuration file `php.ini`, and package and upload them together with the function code.

This document uses installing the custom extension `swoole.so` for PHP 7 as an example.

1. Run the `mkdir test-package` command in the local terminal to create a directory for storing the function code and dependency libraries.
2. Run the following command to create the folder `php_extension` in `test-package` and place the configuration file `php.ini` and extension file `.so` corresponding to the extension in this directory. The directory structure is as follows:
   <dx-alert infotype="explain" title="">

- The extension folder `php_extension` and configuration file `php.ini` are given fixed names. If other names are used, the extension may fail to load.
- The extension folder `php_extension`, the configuration file `php.ini`, and the custom extension file `.so` need to have executable permissions.
  </dx-alert>

```plaintext
|____php_extension
| |____php.ini
| |____swoole.so
|____index.php  
```

3. Custom extensions can be loaded from the code or layers. If an extension is uploaded as a layer, make sure that the unzipped directory structure of the uploaded zip file is as follows:

```plaintext
|____php_extension
| |____swoole.so
```

4. `php.ini` writing method:
     - The extension is in the code directory:
     ```ini
     extension=/var/user/php_extension/swoole.so
  ```
     - This extension is in the layer directory:
     ```ini
extension=/opt/php_extension/swoole.so
  ```

5. Create the function entry file `index.php` in this directory. Check whether the extension is loaded successfully through the `extension_loaded( )` function, and if so, `true` will be returned; otherwise, `false` will be returned.

```php
<?php
function main_handler($event, $context) {
  	var_dump(extension_loaded('swoole'));
    return "hello world";
}
?> 
```

6. Compress the function code and dependency libraries into a zip package, upload the package in the [SCF console](https://console.cloud.tencent.com/scf), and create a function in the following steps:
    	 1. Log in to the [SCF console](https://console.cloud.tencent.com/scf) and click **Functions** on the left sidebar.
     2. Select the region where to create a function at the top of the page and click **Create** to enter the function creation process.
     3. Enter the basic information of the function on the **Create function** page as shown below:
      ![](https://main.qcloudimg.com/raw/4fe183a20d4f5ce9b0db9c897a7df095.png)
          - **Creation method**: Select **Custom**.
          - **Runtime environment**: Select **PHP 7**.
          - **Submitting method**: Select **Local ZIP file**.
     4. Click **Complete**.
   :::
   </dx-tabs>



### Java runtime

Use a dependency management tool such as Maven to install the dependencies locally and upload them together with the function code.

1. Run the `mkdir test-package` command in the local terminal to create a directory for storing the function code and dependency libraries.
2. Create `pom.xml` in this directory and configure the dependency information in `pom.xml`.
3. Run the `mvn package` command in the root directory of the project folder, and the compilation output is as follows:
```bash
[INFO] Scanning for projects...
[INFO]
[INFO] ------------------------------------------------------------------------
[INFO] Building java-example 1.0-SNAPSHOT
[INFO] ------------------------------------------------------------------------
[INFO]
...
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time: 1.785 s
[INFO] Finished at: 2017-08-25T10:53:54+08:00
[INFO] Final Memory: 17M/214M
[INFO] ------------------------------------------------------------------------
```
4. Compress the function code and dependency libraries into a JAR package, upload the package in the [SCF console](https://console.cloud.tencent.com/scf), and create a function in the following steps:
   1. Log in to the [SCF console](https://console.cloud.tencent.com/scf) and click **Functions** on the left sidebar.
   2. Select the region where to create a function at the top of the page and click **Create** to enter the function creation process.
   3. Enter the basic information of the function on the **Create function** page as shown below:
      ![](https://main.qcloudimg.com/raw/e3b4a740329a13d7058a2d5e6a1665f4.png)
      - **Creation method**: Select **Custom**.
      - **Runtime environment**: Select **Java 8**.
      - **Submitting method**: Select **Local ZIP file**.
   4. Click **Complete**.












### Go runtime

**Instructions**: Upload the final binary file when packaging.

Compile the dependency libraries of the Go runtime with the code to get a binary file, upload the packaged binary file in the [SCF console](https://console.cloud.tencent.com/scf), and create a function in the following steps:

1. Log in to the [SCF console](https://console.cloud.tencent.com/scf) and click **Functions** on the left sidebar.
2. Select the region where to create a function at the top of the page and click **Create** to enter the function creation process.
3. Enter the basic information of the function on the **Create function** page as shown below:
   ![](https://main.qcloudimg.com/raw/e3b4a740329a13d7058a2d5e6a1665f4.png)
   - **Creation method**: Select **Custom**.
   - **Runtime environment**: Select **Go 1**.
   - **Submitting method**: Select **Local ZIP file**.
4. Click **Complete**.
