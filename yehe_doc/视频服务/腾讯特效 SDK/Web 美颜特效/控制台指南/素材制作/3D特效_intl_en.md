The SDK has supported 3D effects since v0.3.0. Please check your SDK version before using this capability.

Based on our standard head model, you can create more realistic 3D models using software such as Blender or 3ds Max and upload them to the console.

## Limits

To produce more applicable and realistic effects, we recommend you make 3D models based on our [standard head model](https://webar-static.tencent-cloud.com/assets/model/3D-temp.glb).

| Type | Limit |
|---------|---------|
| Format | GLB file or GLTF folder |
| Size | Keep the size of a model within 5 MB; otherwise it may take a long time to load. |
| Polygons | Keep the polygon count of a model within 100,000; otherwise the output file may be too large.  |
| Texture maps | Use square textures in PNG format and keep the size of each map within 1024 x 1024. Commonly used dimensions include 256, 512, and 1024. <br>Keep the size as small as possible without compromising the quality. |
| Materials | Make sure you use Principled BSDF materials for the surfaces; otherwise a rendering error will occur. |

## Directions

### Step 1. Create a material

1. Download our standard head model and import it into your software (Blender is used as an example in this document). Create a material based on the model and export it in GLB or GLTF format.

>!
>- To ensure that the materials created fit the user’s view, please do not modify the model’s transform options such as location and scale.
>- To keep the size of the output file small and the loading time short, we recommend you generate your model in GLB format.

### Step 2. Import the model into the console

1. Go to the material customization page of the console. A built-in 2D effect model is displayed by default. Click **3D effects** at the top to switch to a 3D model, which is the same as the standard head model mentioned above.
2. Click **Import model** on the right and select a model format (GLB is selected in this example).

>!
>- You can edit only one 3D effect scenario at a time. To import multiple 3D models, click **+** on the left.
>- During editing, you can switch among different models by clicking them in the list on the left.

### Step 3. Modify parameters
Normally, because your 3D model is already built based on our standard head model, it should be ready to use after being imported into the console. If you need to modify the parameters of your model, select an editing mode at the top and drag elements in the editing area to change the settings or directly modify the parameters on the right.

>! If your model is not created based on our standard head model, you can adjust the tracking points to better track your model. For example, you can set nose bridge as the tracking point for a glass model and set philtrum as the tracking point for a mustache model.

### Step 4. Preview the material
You can preview your material on the built-in model. You can also switch to camera to view the effect in videos captured by the camera.

### Step 5. Export the material
Click **Export** in the top right corner. In the pop-up window, select a thumbnail and enter information such as the effect name, and click **Publish**. You can view published materials on the **Manage materials** page.