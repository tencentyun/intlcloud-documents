This document describes how to quickly integrate the Tencent Cloud TRTC SDK for Electron into your project.

## Supported Platforms
-  Windows (PC)
-  macOS

## Integrating the TRTC SDK for Electron

#### Step 1. Install Node.js
**Installation guide for Windows:**
1. Download the latest [Node.js](https://nodejs.org/en/download/) installer `Windows Installer (.msi) 64-bit` for Windows.
2. Open Node.js command prompt in the application list. Commands in subsequent steps will be entered in this window.
![](https://main.qcloudimg.com/raw/a29b4681c1ed6ce57d66b5a79bda5e94.png)

**Installation guide for macOS:**
1. Open the terminal window and run the following command to install Homebrew. If you have installed it, skip this step.
```shell
$ ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```
2. Run the following command to install Node.js (whose version number should be larger than 10.0).
```shell
$ brew install node
```

#### Step 2. Install Electron
1. Run the following command in the command prompt window to install Electron (v4.0.0 or above).
```shell
$ npm install electron@latest --save-dev
```


#### Step 3. Install the TRTC SDK for Electron
1. Install the SDK package by using the `npm` command in your Electron project:
```shell
$ npm install trtc-electron-sdk@latest --save
```
>The latest version of the TRTC SDK for Electron can be viewed in [trtc-electron-sdk](https://www.npmjs.com/package/trtc-electron-sdk).

2. Import the module into the project script and use:
```javascript
const TRTCCloud = require('trtc-electron-sdk');
this.rtcCloud = new TRTCCloud();
// Get the SDK version number
this.rtcCloud.getSDKVersion();
```
Since v7.0.149, the TRTC SDK for Electron has added the `trtc.d.ts` file to facilitate developers to use TypeScript:
```
// Enable ES Module interoperability (esModuleInterop=true)
import * as trtc_namespace from 'trtc-electron-sdk';
const TRTCCloud = require('trtc-electron-sdk');
const rtcCloud: trtc_namespace.TRTCCloud = new TRTCCloud();
// Get the SDK version number
rtcCloud.getSDKVersion();
```

## Packaging as Executable Programs

#### Step 1. Install the packaging tool
1. The packaging tool `electron-builder` is recommended. Run the following command to install it:

```bash
$ npm install electron-builder@latest --save-dev
```

2. To package the project integrated with the TRTC SDK for Electron (i.e., the `trtc_electron_sdk.node` file), you still need to run the following command to install `native-ext-loader`:

```bash
$ npm install native-ext-loader@latest --save-dev
```

#### Step 2. Modify webpack.config.js configurations
The `webpack.config.js` file contains configurations for project building. You can locate it in the following ways:
- Generally, `webpack.config.js` is in the root directory of the project.
- If you create the project with `create-react-app`, the configuration file is `node_modules/react-scripts/config/webpack.config.js`.
- If you create the project with `vue-cli`, the webpack configurations are stored in the `configureWebpack` property of the `vue.config.js` configuration file.
- If the project is customized, please locate the webpack configurations yourself.




1. During the building, the `webpack.config.js` file should receive the `--target_platform` command line parameter to generate code to package for different platforms. For this purpose, add the following code before `module.exports` in the `webpack.config.js` file:


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

>
>In the results returned by `os.platform()`, "darwin" refers to a macOS platform, and "win32" a 64-bit or 32-bit Windows platform.


2. Add the following configuration to the `rules` option. The `targetPlatform` variable enables `rewritePath` to have different values (different configurations) depending on the platforms.

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

The configuration is described as follows:
- To package as an .exe file on Windows, `native-ext-loader` loads the TRTC SDK in the `[application root directory]/resources` directory.
- To package as a .dmg file on macOS, `native-ext-loader` loads the TRTC SDK in the `[application root directory]/Contents/Frameworsk/../Resources` directory.

You still need to add the `--target_platform` parameter to the script in `package.json`, which will be detailed in the next step.

#### Step 3. Modify package.json configurations
The `package.json` file is in the root directory of the project, which contains the information necessary for packaging. By default, you need to modify the path in `package.json` in the following steps to package successfully: 

1. Modify the `main` configuration. We recommend that you use `public/electron.js`.

```json
"main": "public/electron.js",
```
2. Copy the following `build` configuration to the `package.json` file for `electron-builder` to read.

```json
"build": {
  "appId": "[Customize appId]",
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

3. Add the following building and packaging script under the `scripts` node:

 This document takes the projects created by `create-react-app` and `vue-cli` as examples. For projects created by other tools, you can also refer to this configuration:

```json
// Configuration for projects created by create-react-app
"scripts": {
  "build:mac": "react-scripts build --target_platform=darwin",
  "build:win": "react-scripts build --target_platform=win32",
  "compile:mac": "node_modules/.bin/electron-builder --mac",
  "compile:win64": "node_modules/.bin/electron-builder --win --x64",
  "pack:mac": "npm run build:mac && npm run compile:mac",
  "pack:win64": "npm run build:win && npm run compile:win64"
}

// Configuration for projects created by vue-cli project
"scripts": {
  "build:mac": "vue-cli-service build --target_platform=darwin",
  "build:win": "vue-cli-service build --target_platform=win32",
  "compile:mac": "node_modules/.bin/electron-builder --mac",
  "compile:win64": "node_modules/.bin/electron-builder --win --x64",
  "pack:mac": "npm run build:mac && npm run compile:mac",
  "pack:win64": "npm run build:win && npm run compile:win64"
}
```

> 
> -   `main`: Electron entry file. In general, you can configure it as needed. However, if the project is created using the `create-react-app` scaffolding tool, the entry file must be configured as `public/electron.js`.
> -   `build.win.extraFiles`: to package as a Windows program, `electron-builder` copies all files in the directory specified by `from` to `bin/win-unpacked/resources` (case sensitive).
> -   `build.mac.extraFiles`: to package a macOS program, `electron-builder` copies the `trtc_electron_sdk.node` file in the directory specified by `from` to `bin/mac/your-app-name.app/Contents/Resources` (case sensitive).
> -   `build.directories.output`: refers to the output path of the packaged file. For example, the packaged file will be output to the `bin` directory according to the configuration in this document. You can modify it as needed.
> -   `build.scripts.build:mac`: builds scripts for macOS.
> -   `build.scripts.build:win`: builds scripts for Windows.
> -   `build.scripts.compile:mac`: compiles as .dmg installation files on macOS.
> -   `build.scripts.compile:win64`: compiles as .exe installation files on Windows.
> -   `build.scripts.pack:mac`: invokes `build:mac` to generate code, and `compile:mac` to package as .dmg installation files.
> -   `build.scripts.pack:win64`: invokes `compile:win64` to generate code, and `pack:win64` to package as .exe installation files.

#### Step 4. Run the packaging command
- Package as .dmg installation files on macOS:

```bash
$ cd [Project directory]
$ npm run pack:mac
```
After successful execution, the packaging tool will generate the `bin/your-app-name-0.1.0.dmg` installation file. Please publish it.

- Package as .exe installation files on Windows:

```bash
$ cd [Project directory]
$ npm run pack:win64
```
After successful execution, the packaging tool will generate the `bin/your-app-name Setup 0.1.0.exe` installation file. Please publish it.

>
>Currently, the TRTC SDK for Electron does not support cross-platform packaging. For example, you cannot package as an .exe file on macOS, or as a .dmg file on Windows. This feature is under development and will be available in the future.

## FAQs

### 1. What are the restrictions of the firewall?

As the SDK uses the UDP protocol for audio/video transmission, it cannot be used in office networks that block UDP. If you encounter such a problem, please see [How to Deal with Firewall Restrictions](https://intl.cloud.tencent.com/document/product/647/35164).




