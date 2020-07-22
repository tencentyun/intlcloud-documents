## Overview
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


## Relevant Operations
For more information on how to use layers in the SCF Console, please see [Layer Management Operations](https://intl.cloud.tencent.com/document/product/583/34878).

