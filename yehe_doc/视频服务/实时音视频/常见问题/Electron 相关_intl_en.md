[](id:install)
## Installation
[](id:install_q1)
### Is `trtc-electron-sdk` compatible with Electron v12.0.1?

Yes, it is. `trtc-electron-sdk` does not rely on the SDK of Electron and therefore does not have version requirements.


[](id:install_q3)
### What should I do if a 404 error occurs when I download Electron?
![](https://qcloudimg.tencent-cloud.cn/raw/a1855dc24d83db2f0fabe03fcdbce916.png)

Type the following command in the terminal
```
$ npm config set electron_custom_dir 8.1.1 # Determined by the actual version number
```

[](id:run)
## Running
[](id:run_q1)

### When I ran the SDK on 32-bit Windows, the error “Error：resource\trtc_electron_sdk.node is not a valid Win32 application” occurred and the system said I should use 32-bit trtc_electron_sdk.node. What should I do?

![](https://main.qcloudimg.com/raw/4e0115819b868ee9a6d110f641096e01.png)
**Solution:**
1. Go to the directory of `trtc-electron-sdk` (xxx/node_modules/trtc-electron-sdk) in your project and run the following command:
```script
npm run install -- arch=ia32
```
2. Download the 32-bit `trtc_electron_sdk.node` and build your project again.


[](id:run_q2)
### I launched the Electron demo on the VS Code terminal, and a blank screen was displayed after room entry. What should I do?

You need to request access to the camera from VS Code. Use the code below:

```script
    cd ~/Library/Application\ Support/com.apple.TCC/
    cp TCC.db TCC.db.bak
    sqlite3 TCC.db    # sqlite> prompt appears.

    # for Mojave, Catalina
    INSERT into access VALUES('kTCCServiceCamera',"com.microsoft.VSCode",0,1,1,NULL,NULL,NULL,'UNUSED',NULL,0,1541440109);

    # for BigSur
    INSERT into access VALUES('kTCCServiceCamera',"com.microsoft.VSCode",0,1,1,1,NULL,NULL,NULL,'UNUSED',NULL,0,1541440109);
```

[](id:run_q3)

### What should I do if an undefined null pointer error “cannot read property 'dlopen' of undefined” occurs when I run the demo?

![](https://main.qcloudimg.com/raw/fa2ac368a07eefdc63901f3910a122f9.png)
**Solution:**
Context isolation is enabled by default in Electron 12. Disable it by setting `contextIsolation` to `false`.

```javascript
let win = new BrowserWindow({
	width: 1366,
	height: 1024,
	minWidth: 800,
	minHeight: 600,
	webPreferences: {
	nodeIntegration: true,
	contextIsolation: false
		},
});
```


[](id:run_q4)
### What should I do with the frequent reentry issue in the SDK for Electron?

This issue should be dealt with case by case. Possible causes include:

- The client has bad network conditions (network disconnection triggers reentry).
- The room entry signaling message is sent twice consecutively.
- The device is overloaded, which results in decoding failure.
- The same UID is used to log in on different devices.


[](id:run_q5)
### What should I do if the error “Electron failed to install correctly” occurs in the terminal?
After download, when you run your project, the following error may occur in the terminal:
```
Error: Electron failed to install correctly, please delete node_modules/electron and try installing again
```
Follow the steps below to **manually download** Electron:
1. Run `npm config get cache` to view the cache path.
2. Manually download Electron to the cache folder.
3. Run `npm install` again.

[](id:run_q6)

### What should I do if VS Code crashes on macOS when the SDK starts the camera and mic?

If you launch your project using the VS Code terminal, the process may crash when the SDK starts the camera and mic:


- **Solution A**: Use an authorized terminal to run your project.
- **Solution B**: Go to **System Preferences** > **Security & Privacy** and allow VS Code to load.
- **Solution C**: Follow the steps below to disable SIP:
	1. Restart your computer, **holding down** Command + R **until** it enters the recovery mode.
	2. Open the terminal and enter `csrutil disable`.
	3. Restart your computer in the normal mode. You can now use the VS Code terminal to start your project.
	4. To switch SIP back on, enter `csrutil enable` in step 2.


[](id:run_q7)
### What should I do if Electron reports the error “xx is not defined” in the console?
When you run your project, Electron may report the error “xx is not defined” in the console (`xx` is the node module):
```
	Uncaught ReferenceError: require is not defined
```
Set `nodeIntegration` to `true` in the `main.js` file of Electron:
```
	let win = new BrowserWindow({
        width: 1366,
        height: 1024,
        webPreferences: {
     		nodeIntegration: true,  // Set it to `true`
    	},
	  });
```


[](id:pack)
## Packaging
[](id:pack_q1)
### What should I do with a .node module loading issue?
#### Errors
You may see one of the following error messages when running your project after compilation:

- `NodeRTCCloud is not a constructor`
	![](https://main.qcloudimg.com/raw/f06737dc6be7d4eeed7573cd495c922f.png)
- `Cannot open xxx/trtc_electron_sdk.node` or `The specified module could not be found`
	![](https://main.qcloudimg.com/raw/a55c9ca2266bc6e591354e23da535e1d.png)
- `dlopen(xxx/trtc_electron_sdk.node, 1): image not found`
	![](https://main.qcloudimg.com/raw/36c0e62fee13da96dc2136e10a07824b.png)

#### Solution
The errors indicate that the `trtc_electron_sdk.node` module hasn’t been built into your project successfully. To fix the problem, follow these steps:

1. Install `native-ext-loader`.
```
	 $ npm i native-ext-loader -D
```
2. Modify webpack configuration.
	1. Add the following code before `module.exports` to pass the `--target_platform` command line parameter to `webpack.config.js` so that your project can be packaged correctly for its target platform.
```
const os = require('os');
// If you don’t pass `target_platform`, your project will be packaged for the current platform.
const targetPlatform = (function(){
	let target = os.platform();
	for (let i=0; i<process.argv.length; i++) {
		if (process.argv[i].includes('--target_platform=')) {
			target = process.argv[i].replace('--target_platform=', '');
			break;
		}
	}
	// `win32` indicates Windows, including 32-bit and 64-bit. `darwin` indicates macOS.
	if (!['win32', 'darwin'].includes) target = os.platform();
		return target;
})();
```
	2. Add rules:
```
module: {
	rules: [
		{ 
			test: /\.node$/, 
			loader: 'native-ext-loader', 
			options: { 
				rewritePath: targetPlatform === 'win32' ? './resources' : '../Resources' 
			} 
		},
	]
}
```
> !
> - If you create your project with `vue-cli`, webpack configuration can be found in the `configureWebpack` option of `vue.config.js`.
> - If you create your project with `create-react-app`, the path to the webpack configuration file is `[Project directory]/node_modules/react-scripts/config/webpack.config.js`.
3. Add packaging and building scripts to `packages.json`.
	1. Add packaging configuration for `electron-builder` (case sensitive):
```
"build": {
	"Omit": "...",
	"win": {
		"extraFiles": [
			{
			"from": "node_modules/trtc-electron-sdk/build/Release/",
			"to": "./resources",
			"filter": ["**/*"]
			}
		]
	},
	"mac": {
		"extraFiles": [
			{ 
			"from": "node_modules/trtc-electron-sdk/build/Release/trtc_electron_sdk.node", 
			"to": "./Resources" 
			}
		]
	},
	"directories": {
		"output": "./bin"
	}
},
```
	2. For projects created with `create-react-app`, add building and packaging scripts as follows:
```
"scripts": {
	"build:mac": "react-scripts build --target_platform=darwin",
	"build:win": "react-scripts build --target_platform=win32",
	"compile:mac": "node_modules/.bin/electron-builder --mac",
	"compile:win64": "node_modules/.bin/electron-builder --win --x64",
	"pack:mac": "npm run build:mac && npm run compile:mac",
	"pack:win64": "npm run build:win && npm run compile:win64"
}
```
	3. For projects created with `vue-cli`, add building and packaging scripts as follows:
```
"scripts": {
	"build:mac": "vue-cli-service build --target_platform=darwin",
	"build:win": "vue-cli-service build --target_platform=win32",
	"compile:mac": "node_modules/.bin/electron-builder --mac",
	"compile:win64": "node_modules/.bin/electron-builder --win --x64",
	"pack:mac": "npm run build:mac && npm run compile:mac",
	"pack:win64": "npm run build:win && npm run compile:win64"
}
```


[](id:pack_q2)
### What should I do if I cannot find the entry point file?
When you use `electron-builder` to build a project created with `create-react-app`, the following error may occur:
```
    $ node_modules\.bin\electron-builder.cmd
      • electron-builder  version=22.6.0 os=6.1.7601
      • loaded configuration  file=package.json ("build" field)
      • public/electron.js not found. Please see https://medium.com/@kitze/%EF%B8%8F-from-react-to-an-electron-app-ready-for-production-a0468ecb1da3
      • loaded parent configuration  preset=react-cra
```
`public/electron.js not found` indicates that the entry point file was not found.

#### Solution
1. Move and rename the entry point file:
```
$ cd [Project directory]
$ mv main.electron.js ./public/electron.js
```
2. Modify the `pacakge.json` file:
```
{
	"main": "public/electron.js",
	"Omit": "..."
}
```

[](id:pack_q3)
### What should I do if a syntax error of the `fs-extra` module occurs during packaging?
```
[Project directory]\node_modules\electron-builder\node_modules\fs-extra\lib\empty\index.js:33
	} catch {
            ^

SyntaxError: Unexpected token {
	at new Script (vm.js:51:7)
```
Update to the [latest version of Node](https://nodejs.org/en/download/).
