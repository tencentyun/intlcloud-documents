## Operation Scenarios
If your SCF service has a lot of dependent libraries or common code files, you can manage them by using the layers in SCF. With layer management, you can place dependencies in layers instead of the deployment package, ensuring that the deployment package remains small in size. For Node.js, Python, and PHP functions, as long as you keep the deployment package size below 10 MB, you can edit the function code online in the SCF Console.




## Notes
- The files in a layer will be added to the `/opt` directory, which is accessible during function execution.
- If your function is bound to multiple layers, these layers will be merged into the `/opt` directory in sequence. If the same file appears in multiple layers, SCF will retain the version in the highest-numbered layer.
- Even after the layer version you are using is deleted, the functions bound to it will continue to run.


## Directions

<span id="create"></span>
### Creating layer
1. Log in to the SCF Console and select **[Layers](https://console.cloud.tencent.com/scf/layer)** on the left sidebar to enter the **Layers** list page.
2. Select the region to be used at the top of the page and click **Create**.
3. On the **Create Layer Version** page, set the layer information based on your actual needs as shown below:
![](https://main.qcloudimg.com/raw/5a04270aa7b74fb5572f6ffe51f03611.png)
 - **Layer Name**: enter a custom layer name.
 - **Description**: enter descriptive information of the layer as needed.
 - **Submission Method**: **local zip package upload** and **local folder upload** are supported. Please select an appropriate dependency package submission method based on your actual needs.
    After confirming the submission method, click **Upload**. On the pop-up page for dependent package selection, select the desired dependent package and click **OK**.
 - **Compatible Operating Environment**: up to 5 operating environment compatible with this layer can be set.
4. Click **OK** to complete the creation.

<span id="bind"></span>
### Binding function to layer
1. Log in to the SCF Console and select **[Functions](https://console.cloud.tencent.com/scf/list)** on the left sidebar to enter the **Functions** list page.
2. Select the function ID for layer management to enter the function configuration page.
3. Select the **Layer Management** tab and click **Bind Layer** as shown below:
![](https://main.qcloudimg.com/raw/24bf22fb1bea22d42452c53b08008ef1.png)
4. In the **Bind Layer** window that pops up, select the corresponding **Layer Name** and **Layer Version** as shown below:
![](https://main.qcloudimg.com/raw/54ee51aa030f4f1360ab050d6e2acb11.png)
5. Click **Submit** to complete the binding.



### Using layer
In this step, Node.js is used as an example to describe how to create a layer and bind it to a locally uploaded function for use.

1. Upload `node_modules` to generate a layer as instructed in [Creating layer](#create). The local function directory structure is as shown below:
![](https://main.qcloudimg.com/raw/88a8477d8668610dd150887b326628a4.png)
2. Package and upload the local function code as instructed in [Deploying Functions](https://intl.cloud.tencent.com/document/product/583/32741). Exclude the `node_modules` folder by running the following command when packaging:
```
zip -r package name.zip . -x "node_modules/*"
```
See below:
![](https://main.qcloudimg.com/raw/31c531fbc98d0a5cc5c542b7e3721c9d.png)
3. Bind the created layer to the deployed function as instructed in [Binding function](#bind). 
4. After completing the above steps, you can start using the layer in the function.
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


