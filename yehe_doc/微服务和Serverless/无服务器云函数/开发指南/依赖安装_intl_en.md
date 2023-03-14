## Built-in Dependencies

SCF runtime environments have provided some dependent libraries, which can be queried in the corresponding runtime development guide:

- [Node.js](https://intl.cloud.tencent.com/document/product/583/11060)
- [Python](https://intl.cloud.tencent.com/document/product/583/40323) 
- [PHP](https://intl.cloud.tencent.com/document/product/583/17531)
- [Golang](https://intl.cloud.tencent.com/document/product/583/18032)

## Installing Dependent Libraries

You can save the dependent libraries of the SCF code in the code package and upload it to the cloud for use by SCF. SCF supports the following runtimes and usage methods:


### Node.js runtime

The Node.js runtime supports installing dependent libraries in the following three ways:

<dx-tabs>
::: Upload from local
You can use a dependency manager (such as npm) to locally install the dependent library, package and upload it with the function code.
<dx-alert infotype="notice" title="">
Place the entry point file of the function in the root directory of the `zip` package. If you package and upload the entire folder as a `zip` package, the function creation will fail because the entry point file cannot be found in the unzipped root directory.
</dx-alert>
This document takes installing the `lodash` library as an example.

1. Run the `mkdir test-package` command on your local computer to create a directory to store the function code and the dependent library.
2. Run the following commands to install the `lodash` dependent library in the directory.

```bash
cd test-package
npm install lodash
```

3. Create the `index.js` entry point file of the function in the directory and import the `lodash` library in codes.

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

4. Compress the function code and dependent library to a zip package. Upload the zip package and create a function via the [SCF console](https://console.cloud.tencent.com/scf).
   1. Log in to the [SCF console](https://console.cloud.tencent.com/scf) and click **Functions** on the left sidebar.
   2. Choose a region at the top of the **Functions** page and click **Create**.
   3. Enter the basic information of the function on the **Create** page. 
      ![](https://staticintl.cloudcachetci.com/yehe/backend-news/6uYd173_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221230165310.png)
      - **Creation method**: Select **From scratch**.
      - **Runtime environment**: Choose **Node.js12.16**.
      - **Submitting method**: Choose **Local ZIP file**.
   4. Click **Complete**.

:::
::: Install online
The Node.js runtime supports online dependency installation. You can install the dependent library online according to the configuration in `package.json`. For details, see [Online Dependency Installation](https://intl.cloud.tencent.com/document/product/583/38105)
:::
::: Using a dependency manager
The SCF online editor [Serverless Web IDE](https://intl.cloud.tencent.com/document/product/583/39962) supports Terminal capability that has a built-in `npm` package management tool. 
<dx-alert infotype="notice" title="">
 Serverless Web IDE has a delay in supporting newer versions of runtime environments. If the console does not open up the Serverless Web IDE for the corresponding runtime environment, package and upload the dependency library together with the code for dependency installation or install the dependency online.
</dx-alert>
This document takes installing the `lodash` library in the terminal as an example:

1. Log in to the [SCF console](https://console.cloud.tencent.com/scf/index?rid=1) and click **Functions** on the left sidebar.
2. In the function list, click a function name to enter the function details page.
3. On the **Function management** page, select **Function Code** > **Edit codes** to view and edit the function.
4. Select **Terminal** > **New Terminal** on the topbar of the IDE to open the terminal window.
5. Run the following commands in the terminal window to install the `lodash` dependent library.
```bash
cd src  # Install the dependent library in the same level of directory as the function’s entry point file, namely, enter the `src` directory and install it.
npm install lodash # You can view the npm version through the terminal
```
6. After the installation is complete, check `package.json` and `node_modules` in the file tree on the left side of the IDE.
7. Click **Deploy** to package the dependency library and upload it to the cloud together with the function code. 
   ![](https://staticintl.cloudcachetci.com/yehe/backend-news/I7SN275_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221230165842.png)
   :::
   </dx-tabs>

### Python runtime

The Python runtime supports installing dependent libraries in the following two ways.

<dx-tabs>
::: Upload from local
You can use a dependency manager (such as pip) to locally install the dependent library, package and upload it with the function code.
<dx-alert infotype="notice" title="">

- Place the function’s entry point file in the root directory of the `zip` package. If you package and upload the entire folder as a `zip` package, the function creation will fail because the entry point file cannot be found in the unzipped root directory.
- Due to runtime environment differences, confirm that the installed dependency version is adapted to the function runtime environment.
- The function runtime environment is CentOS 7, and you need to install the dependencies in the same environment. If not, an error where the dependencies cannot be found may occur while running the function after upload.
- For dependencies requiring dynamic link library, you need to manually copy these dependencies to the installation directory, and then compress and upload them. You can [install dependency with Docker](https://intl.cloud.tencent.com/document/product/583/38127) or online IDE.
  </dx-alert>
  This document takes installing the `numpy` library as an example:

1. Run the `mkdir test-package` command on your local computer to create a directory to store the function code and the dependent library.
2. Run the following commands to install the `numpy` dependent library in the directory.
```bash
cd test-package
pip install numpy -t . # Check whether the pip version you are using is adapted to the function runtime environment
```
3. Create the `index.py` entry point file of the function in the directory and import the `numpy` library in codes.
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
4. Compress the function code and dependent library to a zip package. Upload the zip package and create a function via the [SCF console](https://console.cloud.tencent.com/scf).
   1. Log in to the [SCF console](https://console.cloud.tencent.com/scf) and click **Functions** on the left sidebar.
   2. Choose a region at the top of the **Functions** page and click **Create**.
   3. Enter the basic information of the function on the **Create** page. 
      ![](https://staticintl.cloudcachetci.com/yehe/backend-news/edQX579_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221230165944.png)
      - **Creation method**: Select **From scratch**.
      - **Runtime environment**: Select **Python 3.6**.
      - **Submitting method**: Choose **Local ZIP file**.
   4. Click **Complete**.

:::
::: Using a dependency manager
The SCF online editor [Serverless Web IDE](https://intl.cloud.tencent.com/document/product/583/39962) supports Terminal capability that has a built-in `pip` package management tool. 
<dx-alert infotype="notice" title="">
 Serverless Web IDE has a delay in supporting newer versions of runtime environments. If the console does not open up the Serverless Web IDE for the corresponding runtime environment, package and upload the dependency library together with the code for dependency installation or install the dependency online.
</dx-alert>
This document takes installing the `numpy` library in the terminal as an example:

1. Log in to the [SCF console](https://console.cloud.tencent.com/scf/index?rid=1) and click **Functions** on the left sidebar.
2. In the function list, click a function name to enter the function details page.
3. On the **Function management** page, select **Function Code** > **Edit codes** to view and edit the function.
4. Select **Terminal** > **New Terminal** on the topbar of the IDE to open the terminal window.
5. Run the following commands in the terminal to install the `numpy` dependent library.
```bash
cd src  # Install the dependent library in the same level of directory as the function’s entry point file, namely, enter the `src` directory and install it.
pip install numpy -t . # You can view the pip version through the terminal to check whether it is adapted to the function runtime environment
```
6. After the installation is complete, check the installed dependent library in the file tree on the left side of the IDE.
7. Click **Deploy** to package and upload the dependent library with function codes to the cloud.
   <dx-alert infotype="notice" title="">
- Use the `pip freeze > requirements.txt` command to generate a `requirements.txt` file that contains all dependencies of the local environment.
- Run the `pip install -r requirements.txt -t .` command in the IDE Terminal to install the dependency package according to the `requirements.txt` configurations.
  </dx-alert>
  :::
  </dx-tabs>


### PHP runtime

>! The PHP versions supported by SCF are 5.6, 7.2, 7.4 and 8.0. Different minor versions of PHP may be incompatible. Please check the version number first before installing dependencies.

<dx-tabs>
::: Install custom libraries
You can use a dependency manager (such as “composer”) to locally install the dependent library, package and upload it with the function code.
<dx-alert infotype="notice" title="">
Place the entry point file of the function in the root directory of the `zip` package. If you package and upload the entire folder as a `zip` package, the function creation will fail because the entry point file cannot be found in the unzipped root directory.
</dx-alert>
This document takes installing the `requests` library for PHP 7.2 as an example:

1. Run the `mkdir test-package` command on your local computer to create a directory to store the function code and the dependent library.
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

5. Compress the function code and dependent library to a zip package. Upload the zip package and create a function via the [SCF console](https://console.cloud.tencent.com/scf).
   1. Log in to the [SCF console](https://console.cloud.tencent.com/scf) and click **Functions** on the left sidebar.
   2. Choose a region at the top of the **Functions** page and click **Create**.
   3. Enter the basic information of the function on the **Create** page. 
      ![](https://staticintl.cloudcachetci.com/yehe/backend-news/TRF5230_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221230170044.png)
    - **Creation method**: Select **From scratch**.
    - **Runtime environment**: Select **Php7.2**.
    - **Submitting method**: Choose **Local ZIP file**.
   4. Click **Complete**.
   :::
   ::: Install custom extensions
   Create the extension folder `php_extension` in a directory at the same level as the function entry file, add the custom extension file `.so` and configuration file `php.ini`, and package and upload them together with the function code.

This document uses installing the custom extension `swoole.so` for PHP 7.2 as an example.

1. Run the `mkdir test-package` command on your local computer to create a directory to store the function code and the dependent library.
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

3. Custom extensions can be loaded from the code or layers. If an extension is uploaded as a layer, please make sure that the unzipped directory structure of the uploaded zip file is as follows:

```plaintext
|____php_extension
| |____swoole.so
```

4. `php.ini` writing method:
     - Set in the code directory:
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

6. Compress the function code and dependent library to a zip package. Upload the zip package and create a function via the [SCF console](https://console.cloud.tencent.com/scf).
  - Log in to the [SCF console](https://console.cloud.tencent.com/scf) and click **Functions** on the left sidebar.
  - Choose a region at the top of the **Functions** page and click **Create**.
  - Enter the basic information of the function on the **Create** page. 
![](https://staticintl.cloudcachetci.com/yehe/backend-news/TRF5230_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221230170044.png)
      - **Creation method**: Select **From scratch**.
      - **Runtime environment**: Select **Php7.2**.
      - **Submitting method**: Choose **Local ZIP file**.
  - Click **Complete**.
   :::
   </dx-tabs>



### Java runtime

You can use a dependency manager (such as maven) to locally install the dependent library, package and upload it with the function code.

1. Run the `mkdir test-package` command on your local computer to create a directory to store the function code and the dependent library.
2. Create a `pom.xml file in the directory and configure dependency in the file.
3. Run the `mvn package` command in the root directory of the project folder, and the compilation output should be as follows:
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
4. Compress the function code and dependent library to a jar package. Upload the jar package and create a function via the [SCF console](https://console.cloud.tencent.com/scf).
   1. Log in to the [SCF console](https://console.cloud.tencent.com/scf) and click **Functions** on the left sidebar.
   
   2. Choose a region at the top of the **Functions** page and click **Create**.
   
   3. Enter the basic information of the function on the **Create** page. 
      ![](https://staticintl.cloudcachetci.com/yehe/backend-news/shvj772_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221230170239.png)
      
      - **Creation method**: Select **From scratch**.
      - **Runtime environment**: Choose **Java8**.
      - **Submitting method**: Choose **Local ZIP file**.
      
   4. Click **Complete**.
   

### Go runtime

**Instructions**: upload the final binary file when packaging.

Compile the dependent library of the Go runtime with codes to generate a binary file. Upload the binary file and create a function via the [SCF console](https://console.cloud.tencent.com/scf).

1. Log in to the [SCF console](https://console.cloud.tencent.com/scf) and click **Functions** on the left sidebar.
2. Choose a region at the top of the **Functions** page and click **Create**.
3. Enter the basic information of the function on the **Create** page. 
   ![](https://staticintl.cloudcachetci.com/yehe/backend-news/URgr420_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221230170355.png)
   - **Creation method**: Select **From scratch**.
   - **Runtime environment**: select **Go 1**.
   - **Submitting method**: Choose **Local ZIP file**.
4. Click **Complete**.
