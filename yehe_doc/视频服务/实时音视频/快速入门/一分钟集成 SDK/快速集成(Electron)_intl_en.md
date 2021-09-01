This document describes how to quickly integrate Tencent Cloud TRTC SDK for Electron into your project.

## Supported Platforms
-  Windows（PC）
-  macOS

## Integrating TRTC SDK for Electron

### Step 1. Install `Node.js`.
**Installing on Windows:**
1. Download the latest version of [Node.js](https://nodejs.org/en/download/) installer `Windows Installer (.msi) 64-bit`.
2. Open `Node.js command prompt` in the application list.
![](https://main.qcloudimg.com/raw/a29b4681c1ed6ce57d66b5a79bda5e94.png)

**Installing on macOS:**
1. Open the terminal window and run the following command to install Homebrew. If you have already installed it, skip this step.
```shell
$ ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```
2. Run the following command to install Node.js (version 10.0 or above).
```shell
$ brew install node
```
3. If Node.js is too slow to install via Homebrew’s default address, consider using a mirror address in your country or region.
```shell
$ cd `brew --repo`
$ git remote set-url origin https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/brew.git
$ brew update
```

### Step 2. Install Electron.
Run the following command in the command prompt to install Electron. Version 4.0.0 or above is recommended.
```shell
$ npm install electron@latest --save-dev
```

### Step 3. Install TRTC SDK for Electron.
1. Use the following nmp command in your Electron project to install the SDK.
```shell
$ npm install trtc-electron-sdk@latest --save
```

	>?You can view the information of the latest version of TRTC SDK for Electron [here](https://www.npmjs.com/package/trtc-electron-sdk).
2. Import the module into the project script and use the module.
```javascript
const TRTCCloud = require('trtc-electron-sdk').default;
// import TRTCCloud from 'trtc-electron-sdk';
this.rtcCloud = new TRTCCloud();
// Get the SDK version number
this.rtcCloud.getSDKVersion();
```
	Since version v7.9.348, TRTC SDK for Electron has integrated `trtc.d.ts` for developers using TypeScript.
```
import TRTCCloud from 'trtc-electron-sdk';
const rtcCloud: TRTCCloud = new TRTCCloud();
// Get the SDK version number.
rtcCloud.getSDKVersion();
```

## Packaging the Executable Program

### Step 1. Install a packaging tool.
1. We recommend that you use the packaging tool `electron-builder. You can run the following command to install it.
```bash
$ npm install electron-builder@latest --save-dev
```
2. To package TRTC SDK for Electron, i.e., the `trtc_electron_sdk.node` file correctly, you must also run the following command to install `native-ext-loader`.
```bash
$ npm install native-ext-loader@latest --save-dev
```

### Step 2. Modify `webpack.config.js`.
The `webpack.config.js` file contains the configuration information for project building. You can locate it in the following ways.
- Normally, `webpack.config.js` is in the root directory of the project.
- If you create your project with `create-react-app`, the configuration file will be `node_modules/react-scripts/config/webpack.config.js`.
- If you create your project with `vue-cli`, webpack configuration will be stored in the `configureWebpack` property of `vue.config.js`.
- If your project is customized, please locate webpack configuration by yourself.


1. First, `webpack.config.js` must receive the `--target_platform` command line parameter so that your project can be packaged correctly for its target platform. Add the following code before `module.exports`.
```js
const os = require('os');
const targetPlatform = (function(){
		let target = os.platform();
		for (let i=0; i<process.argv.length; i++) {
			if (process.argv[i].includes('--target_platform=')) {
				target = process.argv[i].replace('--target_platform=', '');
				break;
			}
		}
		if (!['win32', 'darwin'].includes) target = os.platform();
		return target;
})();
```
	>! In the result returned by `os.platform()`, "darwin" means macOS, and "win32" means Windows (64-bit or 32-bit).
2. Add the following configuration to the `rules` option. The `targetPlatform` variable allows `rewritePath` to switch configurations according to the target platform.
```js
rules: [
  { 
			test: /\.node$/, 
			loader: 'native-ext-loader', 
			options: { 
				rewritePath: targetPlatform === 'win32' ? './resources' : '../Resources' 
			} 
		},
]
```
	This above configuration means:
	- If you create an .exe file for Windows, `native-ext-loader` will load the TRTC SDK in `[application root directory]/resources`.
	- If you create a .dmg file for macOS, `native-ext-loader` will load the TRTC SDK in `[application directory]/Contents/Frameworsk/../Resources`.

You need to add the `--target_platform` parameter to the build script of `package.json` too. See step 3 for details.

### Step 3. Modify `package.json`.
The `package.json` file is in the root directory of the project and contains information needed for packaging. Normally, to successfully package your project, you need to modify the path in `package.json` as follows. 

1. Modify `main`.

```javascript
// In most cases, the name of the `main` file can be customized. For example, in TRTCSimpleDemo, `main` can be configured as:
"main": "main.electron.js",
  
// However, for projects created with the `create-react-app` scaffolding tool, `main` must be configured as:
"main": "public/electron.js",
```
2. Copy the following `build` configuration to your `package.json` file for `electron-builder` to read.

```json
"build": {
  "appId": "[Custom appId]",
  "directories": {
    "output": "./bin"
  },
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
  }
},
```

3. Add command scripts for building and packaging under `scripts`.
 The following command scripts are for projects created with `create-react-app` and `vue-cli`. They provide samples for projects created with other tools too.

```json
// Use this configuration for projects created with `create-react-app`.
"scripts": {
  "build:mac": "react-scripts build --target_platform=darwin",
  "build:win": "react-scripts build --target_platform=win32",
  "compile:mac": "node_modules/.bin/electron-builder --mac",
  "compile:win64": "node_modules/.bin/electron-builder --win --x64",
  "pack:mac": "npm run build:mac && npm run compile:mac",
  "pack:win64": "npm run build:win && npm run compile:win64"
}

// Use this configuration for projects created with `vue-cli`.
"scripts": {
  "build:mac": "vue-cli-service build --target_platform=darwin",
  "build:win": "vue-cli-service build --target_platform=win32",
  "compile:mac": "node_modules/.bin/electron-builder --mac",
  "compile:win64": "node_modules/.bin/electron-builder --win --x64",
  "pack:mac": "npm run build:mac && npm run compile:mac",
  "pack:win64": "npm run build:win && npm run compile:win64"
}
```

>? 
> -   `main`: entry point file for Electron, which can be customized in most cases. However, if your project is created with the `create-react-app` scaffolding tool, `main` must be set to `public/electron.js`.
> -   `build.win.extraFiles`: when packaging programs for Windows, `electron-builder` will copy all files in the directory specified by `from` to `bin/win-unpacked/resources` (all letters in lowercase).
> -   `build.mac.extraFiles`: when packaging programs for macOS, `electron-builder` will copy the `trtc_electron_sdk.node` file specified by `from` to `bin/mac/your-app-name.app/Contents/Resources` (first letters in uppercase).
> -   `build.directories.output`: output path of the packaged file. For example, if the above configuration is used, the packaged file will be generated in the `bin` directory. You can change the path as needed.
> -   `build.scripts.build:mac`: builds scripts for macOS.
> -   `build.scripts.build:win`: builds scripts for Windows.
> -   `build.scripts.compile:mac`: compiles the project into a .dmg file for macOS.
> -   `build.scripts.compile:win64`: compiles the project into an .exe file for Windows.
> -   `build.scripts.pack:mac`: calls `build:mac` first to build scripts and then `compile:mac` to package the project into a .dmg file.
> -   `build.scripts.pack:win64`: calls `build:win` first to build scripts and then `compile:win64` to package the project into an .exe file.

### Step 4. Run the packaging command.
- Packaging the project into a .dmg file for macOS:
```bash
$ cd [Project directory]
$ npm run pack:mac
```
	The packaging tool will generate an installation file named `bin/your-app-name-0.1.0.dmg`. Publish this file.
- Packaging the project into an .exe file for Windows:
```bash
$ cd [Project directory]
$ npm run pack:win64
```
	The packaging tool will generate an installation file named `bin/your-app-name Setup 0.1.0.exe`. Publish this file.


>!Currently, TRTC SDK for Electron does not support cross-platform packaging. This means you cannot package your project into an .exe file on macOS or a .dmg file on Windows, but we are working on this and may make it possible in the future.

## FAQ

### 1. What are firewall restrictions does the SDK face?

The SDK uses the UDP protocol for audio/video transmission and therefore cannot be used in office networks that block UDP. If you encounter such a problem, see [How to Deal with Firewall Restrictions](https://intl.cloud.tencent.com/document/product/647/35164).
