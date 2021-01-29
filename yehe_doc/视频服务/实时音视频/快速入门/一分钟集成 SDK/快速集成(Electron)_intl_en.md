This document describes how to quickly integrate the Tencent Cloud TRTC SDK for Electron into your project.

## Supported Platforms
-  Windows (PC)
-  macOS

## Integrating TRTC SDK for Electron

#### Step 1. Install Node.js
**Install on Windows:**
1. Download the latest version of the [Node.js](https://nodejs.org/en/download/) installation package `Windows Installer (.msi) 64-bit` for Windows.
2. Open the Node.js command prompt in the application list and launch the command line window for entering commands in subsequent steps.
![](https://main.qcloudimg.com/raw/a29b4681c1ed6ce57d66b5a79bda5e94.png)

**Install on macOS:**
1. Open the Terminal window and run the following command to install Homebrew. Skip this step if you have already installed it.
```shell
$ ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```
2. Run the following command to install Node.js, which must be higher than v10.0.
```shell
$ brew install node
```
3. If installing Node.js with the default address of Homebrew is slow, you can consider using a mirror address.
```shell
$ cd `brew --repo`
$ git remote set-url origin https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/brew.git
$ brew update
```

#### Step 2. Install Electron
1. Run the following command in the command line window to install Electron (v4.0.0 or above recommended).
```shell
$ npm install electron@latest --save-dev
```

#### Step 3. Install the TRTC SDK for Electron
1. Install the SDK package by using the npm command in your Electron project:
```shell
$ npm install trtc-electron-sdk@latest --save
```
>?The latest version of the TRTC SDK for Electron can be viewed in [trtc-electron-sdk](https://www.npmjs.com/package/trtc-electron-sdk).

2. Import the module into the project script and use:
```javascript
const TRTCCloud = require('trtc-electron-sdk');
this.rtcCloud = new TRTCCloud();
// Get the SDK version number
this.rtcCloud.getSDKVersion();
```
Starting from v7.0.149, the TRTC SDK for Electron has included the `trtc.d.ts` file for the convenience of developers with TypeScript:
```
// Enable ES Module interoperability mode (esModuleInterop=true)
import * as trtc_namespace from 'trtc-electron-sdk';
const TRTCCloud = require('trtc-electron-sdk');
const rtcCloud: trtc_namespace.TRTCCloud = new TRTCCloud();
// Get the SDK version number
rtcCloud.getSDKVersion();
```

## Packaging Executable Program

#### Step 1. Install a packaging tool
1. The packaging tool `electron-builder` is recommended. You can run the following command to install it:

```bash
$ npm install electron-builder@latest --save-dev
```

2. To correctly package the TRTC SDK for Electron (i.e., the `trtc_electron_sdk.node` file), you also need to run the following command to install the `native-ext-loader` tool:

```bash
$ npm install native-ext-loader@latest --save-dev
```

#### Step 2. Modify the webpack.config.js configuration
The `webpack.config.js` file contains the configuration information for project building. You can locate it in the following ways:
- Generally, `webpack.config.js` is in the root directory of the project.
- If you create the project with `create-react-app`, this configuration file will be `node_modules/react-scripts/config/webpack.config.js`.
- If you create the project with `vue-cli`, the webpack configuration will be stored in the `configureWebpack` attribute of the `vue.config.js` configuration file.
- If the project is customized, please locate the webpack configuration by yourself.


1. First, set `webpack.config.js` to receive the `--target_platform` command line parameter during the building so that the code can be correctly packaged for different target platforms in the code building process. Add the following code before `module.exports`:


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

>!
>In the result returned by `os.platform()`, "darwin" represents macOS, and "win32" represents Windows (regardless of 64-bit or 32-bit).


2. Add the following configuration to the `rules` option. The `targetPlatform` variable allows `rewritePath` to switch different configurations by different target platforms:

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

This configuration means:
- To package as an .exe file on Windows, it lets `native-ext-loader` load the TRTC SDK in the `[application root directory]/resources` directory.
- To package as a .dmg file on macOS, it lets `native-ext-loader` load the TRTC SDK in the `[application directory]/Contents/Frameworsk/../Resources` directory.

You also need to add the `--target_platform` parameter to the script in `package.json`, which will be performed in the next step.

#### Step 3. Modify the package.json configuration
The `package.json` file is in the root directory of the project and contains the information necessary for project packaging. By default, you need to modify the path in `package.json` as follows to successfully implement packaging: 

1. Modify the `main` configuration.

```javascript
// In most cases, the name of the `main` file can be configured arbitrarily. For example, in TRTCSimpleDemo, it can be configured as:
"main": "main.electron.js",
  
// However, for projects created with the `create-react-app` scaffolding tool, the `main` file must be configured as:
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

3. Add the following command script for building and packaging under the `scripts` node:

 This document uses the projects created with `create-react-app` and `vue-cli` as examples. For projects created with other tools, you can refer to this configuration:

```json
// Use this configuration for projects created with `create-react-app`
"scripts": {
  "build:mac": "react-scripts build --target_platform=darwin",
  "build:win": "react-scripts build --target_platform=win32",
  "compile:mac": "node_modules/.bin/electron-builder --mac",
  "compile:win64": "node_modules/.bin/electron-builder --win --x64",
  "pack:mac": "npm run build:mac && npm run compile:mac",
  "pack:win64": "npm run build:win && npm run compile:win64"
}

// Use this configuration for projects created with `vue-cli`
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
> -   `main`: entry file for Electron, which can generally be configured arbitrarily. However, if the project is created with the `create-react-app` scaffolding tool, it must be configured as `public/electron.js`.
> -   `build.win.extraFiles`: to package as a Windows program, `electron-builder` will copy all files in the directory specified by `from` to `bin/win-unpacked/resources` (all letters in lowercase).
> -   `build.mac.extraFiles`: to package as a macOS program, `electron-builder` will copy the `trtc_electron_sdk.node` file specified by `from` to `bin/mac/your-app-name.app/Contents/Resources` (first letter in uppercase).
> -   `build.directories.output`: output path of the packaged file. For example, the packaged file will be output to the `bin` directory according to this configuration. You can change it as needed.
> -   `build.scripts.build:mac`: builds scripts for macOS.
> -   `build.scripts.build:win`: builds scripts for Windows.
> -   `build.scripts.compile:mac`: compiles into a .dmg installation file for macOS.
> -   `build.scripts.compile:win64`: compiles into an .exe installation file for Windows.
> -   `build.scripts.pack:mac`: calls `build:mac` to build code and `compile:mac` to package it as a .dmg installation file.
> -   `build.scripts.pack:win64`: calls `build:win` to build code and `compile:win64` to package it as an .exe installation file.

#### Step 4. Run the packaging command
- Package as a .dmg installation file for macOS:

```bash
$ cd [Project directory]
$ npm run pack:mac
```
After successful execution, the packaging tool will generate the `bin/your-app-name-0.1.0.dmg` installation file. Please select this file to publish it.

- Package as an .exe installation file for Windows:

```bash
$ cd [Project directory]
$ npm run pack:win64
```
After successful execution, the packaging tool will generate the `bin/your-app-name Setup 0.1.0.exe` installation file. Please select this file to publish it.

>!Currently, the TRTC SDK for Electron does not support cross-platform packaging. For example, you cannot package a project as an .exe file on macOS or as a .dmg file on Windows. This feature will be available in the future.

## FAQs

### 1. What are the restrictions of the firewall?

As the SDK uses the UDP protocol for audio/video transmission, it cannot be used in office networks that block UDP. If you encounter such a problem, please see [How to Deal with Firewall Restrictions](https://intl.cloud.tencent.com/document/product/647/35164).





