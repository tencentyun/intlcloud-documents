## Operation Scenarios
This document describes how to create, bind, and use a layer in the SCF Console.


## Directions

### Creating layer<span id="create"></span>
1. Log in to the SCF Console and select **[Layer](https://console.cloud.tencent.com/scf/layer)** on the left sidebar to enter the "Layer" list page.
2. Select the target region at the top of the page and click **Create**.
3. On the "Create Layer" page, set the layer information based on your actual needs as shown below:
![](https://main.qcloudimg.com/raw/011aafa792556171838e7bce56e86348.png)
 - **Layer Name**: enter a custom layer name.
 - **Description**: enter descriptive information of the layer as needed.
 - **Submission Method**: **Local ZIP file**, **Local folder**, and **Upload a ZIP pack via COS** are supported. Please select an appropriate dependency package submission method based on your actual needs.
    After confirming the submission method, click **Upload**. On the pop-up page for dependency package selection, select the desired dependency package and click **OK**.
 - **Add Runtime Environment**: up to 5 runtime environments compatible with this layer can be set.
4. Click **OK** to create the layer.

### Binding function to layer<span id="bind"></span>
1. Log in to the SCF Console and select **[Function Service](https://console.cloud.tencent.com/scf/list)** on the left sidebar to enter the "Function Service" list page.
2. Select the function ID for layer management to enter the function management page.
3. Select the **Layer Management** tab and click **Bind** as shown below:
![](https://main.qcloudimg.com/raw/335653f2ded6ab62f41b0fa6b45d5857.png)
4. In the "Bind Layer" window that pops up, select the corresponding **Layer Name** and **Layer Version** as shown below:
![](https://main.qcloudimg.com/raw/1a42cca458210446496598127c1525ab.png)
5. Click **OK** to complete the binding.



### Using layer
This section uses Node.js as an example to describe how to create a layer, bind it to a locally uploaded function, and use it.

1. Upload `node_modules` to generate a layer as instructed in [Creating layer](#create). The local function directory structure is as shown below:
![](https://main.qcloudimg.com/raw/88a8477d8668610dd150887b326628a4.png)
2. Package and upload the local function code as instructed in [Deploying Function](https://intl.cloud.tencent.com/document/product/583/32741). During the packaging, run the following command to exclude the `node_modules` folder:
```
zip -r package name.zip . -x "node_modules/*"
```
See the figure below:
![](https://main.qcloudimg.com/raw/31c531fbc98d0a5cc5c542b7e3721c9d.png)
3. Bind the created layer to the deployed function as instructed in [Binding function to layer](#bind). 
4. You can use the layer in the function after completing the steps above.
Because the `NODE_PATH` environment variable contains the `/opt/node_modules` path, you can find the dependency in the layer when running the function. You can use the dependency in the same way as before with no code modification required. This document uses the `cos-nodejs-sdk-v5` dependency as an example as shown below:
![](https://main.qcloudimg.com/raw/6167eb686aeeadacd646beb998e19136.png)
For the environment variables in Python, Java, and Node.js, please see the table below:
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




## Example
### Using layer and testing function
1. <span id="Step1"></span>Go to [scf_layer_demo](https://github.com/tencentyun/scf_layer_demo) and select **Clone or download** > **Download ZIP** to download the demo and decompress it.
2. <span id="Step2"></span>Create a layer as instructed in [Creating layer](#create). Set the parameters as shown below:
![](https://main.qcloudimg.com/raw/7bf2839302ba35e8dbc39a65cfb33c60.png)
 - **Layer Name**: enter a custom name. This document uses `demo` as an example.
 - **Submission Method**: select "Local folder" and select and upload the `layer` folder in the folder obtained in [step 1](#Step1).
 - **Runtime Environment**: select "Nodejs12.16".
3. Go to the "[Function Service](https://console.cloud.tencent.com/scf/list)" page and click **Create** to enter the "Create Function" page.
4. Set the basic information of the function in "Basic Info" on the "Create Function" page and click **Next** as shown below:
 ![](https://main.qcloudimg.com/raw/325bdd76e4f02560bc2093a2daae6451.png)
 - **Function Name**: enter a custom name. This document uses `layerDemo` as an example.
 - **Runtime Environment**: select "Nodejs 12.16".
 - **Creation Method**: select **Blank function**.
5. In "Function Configuration", select "Local folder" as "Submission Method" and select and upload the `function` folder in the folder obtained in [step 1](#Step1).
![](https://main.qcloudimg.com/raw/9314878a908e9a75997e42d286d6b70f.png)
6. Click **Advanced Settings** and add the function layer in "Layer Configuration" as shown below:
![](https://main.qcloudimg.com/raw/2fd92c6713bbe6951811ab9163135b27.png)
	- **Layer Name**: select the layer `demo` created in [step 2](#Step2).
	- **Layer Version**: select v1.
7. Click **Complete** at the bottom to complete the function creation.
8. Select the **Function Code** tab on the "Function Management" page. You can click **Test** at the bottom to view the result as shown below:
![](https://main.qcloudimg.com/raw/a772a3dce7890469290053271c3a54d0.png)
