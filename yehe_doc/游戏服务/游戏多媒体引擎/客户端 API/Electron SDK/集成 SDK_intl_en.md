
This document describes how to configure an Electron project for the GME APIs for Electron.

## Supported Platforms

-  Windows

## Importing the SDK
### Step 1: Install Node.js
1. Download the latest version of the Node.js installation package `Windows Installer (.msi) 64-bit` for Windows.
2. Open `Node.js command prompt` in the application list and open a terminal window.

### Step 2. Install Electron
Run the following command in the terminal to install Electron. V4.0.0 or later is recommended.
```sh
$ npm install electron -g

```

### Step 3. Install the GME SDK for Electron

1. Use the following npm command in your Electron project to install the GME SDK:
```sh
$ npm install gme-electron-sdk@latest --save

```
2. In the project script, import and use the module:
```
const { GmeContext } = require('gme-electron-sdk');
// import gmesdk from 'gme-electron-sdk';
gmeContext = new GmeContext();
// Get the SDK version number
gmeContext.GetSDKVersion();

```

### Step 4. Create an executable program

Install the packaging tool. We recommend you use Electron Forge. You can run the following command:

1. Add Electron Forge to your application's development dependencies and run the `import` command to set the scaffold of Forge:
```sh
npm install --save-dev @electron-forge/cli
npx electron-forge import
```
2. Run the `make` command of Forge to create a distributable application:
```sh
npm run make
```
