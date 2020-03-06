## Operation Scenarios
If your SCF service has a lot of dependent libraries or common code files, you can manage them by using the layers in SCF. With layer management, you can place dependencies in layers instead of the deployment package, ensuring that the deployment package remains small in size. For Node.js, Python, and PHP functions, as long as you keep the deployment package size below 10 MB, you can edit the function code online in the SCF Console.
>SCF's layer management feature is currently in beta test and may be updated at any time. To use this feature, please fill out and submit the application.



## Notes
- The files in a layer will be added to the `/opt` directory, which is accessible during function execution.
- If your function is bound to multiple layers, these layers will be merged into the `/opt` directory in sequence. If the same file appears in multiple layers, SCF will retain the version in the highest-numbered layer.
- Even after the layer version you are using is deleted, the functions bound to it will continue to run.


## Directions

### Creating layers
1. Log in to the SCF Console and select **[Layers](https://console.cloud.tencent.com/scf/layer)** on the left sidebar to enter the **Layers** list page.
2. Select the region to be used at the top of the page and click **Create**.
3. On the **Create Layer Version** page, set the layer information based on your actual needs.
 - **Layer Name**: enter a custom layer name.
 - **Description**: enter descriptive information of the layer as needed.
 - **Submission Method**: **local zip package upload** and **local folder upload** are supported. Please select an appropriate dependency package submission method based on your actual needs.
    After confirming the submission method, click **Upload**. On the pop-up page for dependent package selection, select the desired dependent package and click **OK**.
 - **Compatible Operating Environment**: up to 5 operating environment compatible with this layer can be set.
4. Click **OK**.

### Binding functions to layers
1. Log in to the SCF Console and select **[Functions](https://console.cloud.tencent.com/scf/list)** on the left sidebar to enter the **Functions** list page.
2. Select the function ID for layer management to enter the function configuration page.
3. Select the **Layer Management** tab and click **Bind Layer**.
4. In the **Bind Layer** window that pops up, select the corresponding **Layer Name** and **Layer Version**.
5. Click **Submit**.





