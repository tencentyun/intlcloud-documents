

## Operation Scenarios
If your SCF service has a lot of dependent libraries or common code files, you can manage them by using the layers in SCF. With layer management, you can place dependencies in layers instead of the deployment package, ensuring that the deployment package remains small in size. For Node.js, Python, and PHP functions, as long as you keep the deployment package size below 10 MB, you can edit the function code online in the SCF Console.

## How It Works

### Creation and binding

Compressed files for layer creation are stored by layer version. Layers on specific versions can be bound to the functions on matched versions. A function can be bound to up to 5 specific layer versions in a certain sequence.

### Loading and access during runtime
When a function bound to a layer is triggered to run and start a concurrent instance, its runtime code will be decompressed to and loaded in the **/var/user/** directory, and the layer content will be decompressed to and loaded in the **/opt** directory.
If the **file** file that needs to be used or accessed is placed in the root directory of the compressed file during layer creation, you can directly access it in the **/opt/file** directory after the decompression and loading are completed. If it is compressed with its folder as **dir/file** during layer creation, you need to access it in **/opt/dir/file** during function execution.

If a function is bound to multiple layers, the decompression and loading sequence of the files in layers will be the same as the binding sequence. They will be sorted in ascending order by serial number. The lower the ranking, the later the loading time, but all files will be loaded before the concurrent instances of the function start. You can use the files in layers during function code initialization.



### Recommended usage

Layers are generally used to store static files or code dependent libraries that rarely change. When storing code dependent libraries, you can directly package available ones and upload the package to a layer. For example, in a Python environment, you can directly package the code package folder of the dependent libraries and create the package as a layer, and then it can be imported directly through `import` in the function code. In a Node.js environment, you can package the `node_modules` dependent library folder of the project and create the package as a layer, and then it can be imported directly through `require` in the function code.

You can use layers to separate function code, dependent libraries, and dependent static files, so as to keep the function code small in size. You can implement quick upload and update when editing a function in the command line tool, IDE plugin, or console.


## Notes

- The files in a layer will be added to the `/opt` directory, which is accessible during function execution.
- If your function is bound to multiple layers, these layers will be merged into the `/opt` directory in sequence. If the same file appears in multiple layers, SCF will retain the version in the highest-numbered layer.


## Directions
<span id="create"></span>
### Creating layer
1. Log in to the SCF Console and select **[Layer](https://console.cloud.tencent.com/scf/layer)** on the left sidebar to enter the "Layer" list page.
2. Select the target region at the top of the page and click **Create**.
3. On the "Create Layer" page, set the layer information based on your actual needs.
 - **Layer Name**: enter a custom layer name.
 - **Description**: enter descriptive information of the layer as needed.
 - **Submission Method**: **Local ZIP file**, **Local folder**, and **Upload a ZIP pack via COS** are supported. Please select an appropriate dependency package submission method based on your actual needs.
    After confirming the submission method, click **Upload**. On the pop-up page for dependency package selection, select the desired dependency package and click **OK**.
 - **Add Runtime Environment**: up to 5 runtime environments compatible with this layer can be set.
4. Click **OK** to create the layer.

### Binding function to layer<span id="bind"></span>
1. Log in to the SCF Console and select **[Function Service](https://console.cloud.tencent.com/scf/list)** on the left sidebar to enter the "Function Service" list page.
2. Select the function ID for layer management to enter the function management page.
3. Select the **Layer Management** tab and click **Bind**.
4. In the "Bind Layer" window that pops up, select the corresponding **Layer Name** and **Layer Version** .

5. Click **OK** to complete the binding.



### Using layer
This section uses Node.js as an example to describe how to create a layer, bind it to a locally uploaded function, and use it.

1. Upload `node_modules` to generate a layer as instructed in [Creating layer](#create). 

2. Package and upload the local function code as instructed in [Deploying Function](https://intl.cloud.tencent.com/document/product/583/32741). During the packaging, run the following command to exclude the `node_modules` folder:
```
zip -r package name.zip . -x "node_modules/*"
```

3. Bind the created layer to the deployed function as instructed in [Binding function to layer](#bind). 
4. You can use the layer in the function after completing the steps above.
Because the `NODE_PATH` environment variable contains the `/opt/node_modules` path, you can find the dependency in the layer when running the function. You can use the dependency in the same way as before with no code modification required. This document uses the `cos-nodejs-sdk-v5` dependency as an example.

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
2. <span id="Step2"></span>Create a layer as instructed in [Creating layer](#create). Set the parameters.
 - **Layer Name**: enter a custom name. This document uses `demo` as an example.
 - **Submission Method**: select "Local folder" and select and upload the `layer` folder in the folder obtained in [step 1](#Step1).
 - **Runtime Environment**: select "Nodejs12.16".
3. Go to the "[Function Service](https://console.cloud.tencent.com/scf/list)" page and click **Create** to enter the "Create Function" page.
4. Set the basic information of the function in "Basic Info" on the "Create Function" page and click **Next** .
 - **Function Name**: enter a custom name. This document uses `layerDemo` as an example.
 - **Runtime Environment**: select "Nodejs 12.16".
 - **Creation Method**: select **Blank function**.
5. In "Function Configuration", select "Local folder" as "Submission Method" and select and upload the `function` folder in the folder obtained in [step 1](#Step1).

6. Click **Advanced Settings** and add the function layer in "Layer Configuration".

	- **Layer Name**: select the layer `demo` created in [step 2](#Step2).
	- **Layer Version**: select v1.
7. Click **Complete** at the bottom to complete the function creation.
8. Select the **Function Code** tab on the "Function Management" page. You can click **Test** at the bottom to view the result.
