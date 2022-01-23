## Overview

This document describes how to create, bind, and use a layer in the SCF console.


## Directions

### Creating layer[](id:create)

1. Log in to the SCF console and select **[Layer](https://console.cloud.tencent.com/scf/layer)** on the left sidebar to enter the **Layers** list page.
2. Select the target region at the top of the page and click **Create**.
3. On the **Create Layer** page, set the layer information based on your actual needs as shown below:
	![](https://qcloudimg.tencent-cloud.cn/raw/bebed68def459d70c2781776c0071b1c.png)
	 - **Layer Name**: enter a custom layer name.
	 - **Description**: enter descriptive information of the layer as needed.
	 - **Submission Method**: **Local ZIP file**, **Local folder**, and **Upload a ZIP pack via COS** are supported. Please select an appropriate layer file submission method based on your actual needs.
		 After confirming the submission method, click **Upload**, select the desired file, and click **OK**.
	 - **Add Runtime Environment**: up to 5 runtime environments compatible with this layer can be set.
4. Click **OK**.

### Binding function to layer[](id:bind)

1. Log in to the SCF console and select **[Function Service](https://console.cloud.tencent.com/scf/list)** on the left sidebar to enter the **Function Service** list page.
2. Select the function ID for layer management to enter the function management page.
3. Select the **Layer Management** tab and click **Bind** as shown below:
   ![](https://qcloudimg.tencent-cloud.cn/raw/f9004c1b7fb01e36d0dc10685da3266c.png)
4. In the **Bind Layer** window that pops up, select the corresponding **Layer Name** and **Layer Version** as shown below:
   ![](https://qcloudimg.tencent-cloud.cn/raw/bb13a5413a502c90687a94b1f893f1eb.png)
5. Click **OK**.



### Using layer

Files in the layer are all under the `/opt/` directory, which can be accessed through their absolute paths in the function code. In addition, the built-in environment variables of each runtime also include layer paths, so files can be uploaded according to such paths, and then they can be imported through their relative paths in the code.

For the environment variables in Python, Java, and Node.js, see the table below:

<table>
	<tr>
	<th>Environment Variable</th>
	<th>Path</th>
	</tr>
	<tr>
	<td>PYTHONPATH</td>
	<td><code>/var/user:/opt </code></td>
	</tr>
	<tr>
	<td>CLASSPATH</td>
	<td><code> /var/runtime/java8:/var/runtime/java8/lib/*:/opt   </code></td>
	</tr>
	<tr>
	<td>NODE_PATH</td>
	<td><code>/var/user:/var/user/node_modules:/var/lang/node6/lib/node_modules:/opt:/opt/node_modules</code></td>
	</tr>
</table>



The following takes importing the `cos-nodejs-sdk-v5` dependency from `node_modules` in a layer in the code in the Node.js runtime environment as an example:

1. Upload `node_modules` to generate a layer as instructed in [Creating layer](#create). The local function directory structure is as shown below:
   ![](https://main.qcloudimg.com/raw/88a8477d8668610dd150887b326628a4.png)
2. Package and upload the local function code as instructed in [Deploying Function](https://intl.cloud.tencent.com/document/product/583/32741). During the packaging, run the following command to exclude the `node_modules` folder:
   ``` shell
   zip -r package name.zip . -x "node_modules/*"
   ```
   See the figure below:
   ![](https://main.qcloudimg.com/raw/31c531fbc98d0a5cc5c542b7e3721c9d.png)
3. Bind the created layer to the deployed function as instructed in [Binding function to layer](#bind). 
4. You can import files at the layer in the function after completing the steps above.
 ``` js
 'use strict'
 var COS = require('cos-nodejs-sdk-v5')
 ```
> !
> - As the `NODE_PATH` environment variable already includes the `/opt/node_modules` path, there is no need to specify the absolute path of the dependency. SCF will load the file according to the path specified in the environment variable during execution.
> - If the file path in the layer and the path included in the environment variable are different, you need to use the absolute path when importing the file.


The following takes importing the `cos-python-sdk-v5` dependency from a layer in the code in the Python runtime environment as an example:

1. Upload `cos-python-sdk-v5` to generate a layer as instructed in [Creating layer](#create).
2. Package and upload the local function code as instructed in [Deploying Function](https://intl.cloud.tencent.com/document/product/583/32741). Files that have already been uploaded to the layer don't need to be uploaded again together with the function code.
3. Bind the created layer to the deployed function as instructed in [Binding function to layer](#bind). 
4. You can import files at the layer in the function after completing the steps above.
 ``` python
 # -*- coding: utf8 -*-
 import cos-python-sdk-v5
 ```
> !
> - As the `PYTHONPATH` environment variable already includes the `/opt` path, there is no need to specify the absolute path of the dependency. SCF will load the file according to the path specified in the environment variable during execution.
> - If the file path in the layer and the path included in the environment variable are different, you need to use the absolute path when importing the file.



## Sample

### Using layer and testing function

1. [](id:Step1)Go to [scf_layer_demo](https://github.com/tencentyun/scf_layer_demo) and select **Clone or download** > **Download ZIP** to download the demo and decompress it.
2. [](id:Step2)Create a layer as instructed in [Creating layer](#create). Set the parameters as shown below:
   ![](https://qcloudimg.tencent-cloud.cn/raw/496aea68b0381b750d63e22ff7f5612b.png)
 - **Layer Name**: enter a custom name. This document uses `demo` as an example.
 - **Submission Method**: select **Local folder** and select and upload the `layer` folder in the folder obtained in [step 1](#Step1).
 - **Runtime Environment**: select **Nodejs12.16**.
3. Go to the **[Function Service](https://console.cloud.tencent.com/scf/list)** page and click **Create** to enter the **Create Function** page.
4. Set the basic information of the function in **Basic Info** on the **Create Function** page and click **Next** as shown below:
   ![](https://qcloudimg.tencent-cloud.cn/raw/e35920d158c7ae4cd43fbc1b6ed8c254.png)
 - **Function Name**: enter a custom name. This document uses `layerDemo` as an example.
 - **Runtime Environment**: select **Nodejs 12.16**.
 - **Creation Method**: select **Blank function**.
5. In **Function Configuration**, select **Local folder** as **Submission Method** and select and upload the `function` folder in the folder obtained in [step 1](#Step1).
   ![](https://qcloudimg.tencent-cloud.cn/raw/54df95485ba11ff3af2db16a2095c313.png)
6. Click **Advanced Settings** and add the function layer in **Layer Configuration** as shown below:
   ![](https://qcloudimg.tencent-cloud.cn/raw/5b8b091443e6091ee09bf85ee161a37e.png)
   - **Layer Name**: select the layer `demo` created in [step 2](#Step2).
   - **Layer Version**: select v1.
7. Click **Complete** at the bottom to complete the function creation.
8. Select the **Function Code** tab on the **Function Management** page. You can click **Test** at the bottom to view the result as shown below:
   ![](https://qcloudimg.tencent-cloud.cn/raw/362472571ebff79d11340db03d54164e.png)
