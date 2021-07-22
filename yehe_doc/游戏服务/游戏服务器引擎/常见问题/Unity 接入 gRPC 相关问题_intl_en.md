

### The error `error: grpc_csharp_ext` pops up when I run the macOS server program package. How to fix it?

<img src="https://main.qcloudimg.com/raw/703dc0dd20342b4aff5d499f2ac1df85.png" style="width: 718px;"></img>

<b>Solution</b>: Open the path `Assert/Plugins/Grpc.Core/runtimes/osx/x64 `, rename the file `grpc_csharp_ext.bundle` to `grpc_csharp_ext`, and then copy the file to `YourUnityApp.app/Contents/Frameworks/MonoEmbedRuntime/osx`. Please create such directories if any parts of the path do not exist.

### The error `Unable to preload the following plugins: ScreenSelector.so` pops up when I run the packaged Linux server program. How to fix it?

<img src="https://main.qcloudimg.com/raw/f2926b2ac676f2e1e1ce85b8bae397f1.png" style="width: 718px;"></img>

<b>Solution</b>: In the Unity Editor, click **File** -> **Build Settings**, tick the **Server Build** option, and package it again.
<img src="https://main.qcloudimg.com/raw/3ffa6a320c4269669c411f32cf7597f0.png" style="width: 718px;"></img>

### When I run the packaged Windows server program using the image creation server of the Windows Server 2012 R2 Datacenter 64-bit English system provided by GSE, the error below pops up. How to fix it?
![](https://main.qcloudimg.com/raw/aeb980b1528b7796481f2e552a340c64.png)
<b>Solution</b>: In asset package creation, select the system of the Chinese version when you configure the **Upload Codes** item.
![](https://main.qcloudimg.com/raw/507d4226c74aa9ce30868be3e107d06c.png)


### After the file `grpc_unity_package.VERSION.zip` is downloaded and decompressed to Unity, an error as described in the [issue 22251](https://github.com/grpc/grpc/issues/22251) pops up in the Unity Editor. How to fix it?
**Solution**: Download and decompress the [grpc_unity_package.2.26.0-dev.zip](https://packages.grpc.io/archive/2019/12/a02d6b9be81cbadb60eed88b3b44498ba27bcba9-edd81ac6-e3d1-461a-a263-2b06ae913c3f/index.xml) v2.26.
