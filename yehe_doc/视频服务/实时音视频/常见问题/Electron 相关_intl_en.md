[](id:que1)
### An undefined null pointer error “cannot read property "dlopen" of undefined” occurred when I ran the demo. What should I do?
![](https://main.qcloudimg.com/raw/fa2ac368a07eefdc63901f3910a122f9.png)
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

[](id:que2)
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

[](id:que3)
### When I ran the SDK on 32-bit Windows, an error occurred saying that I need to use 32-bit `trtc_electron_sdk.node`. What should I do?
![](https://main.qcloudimg.com/raw/4e0115819b868ee9a6d110f641096e01.png)
1. Go to the directory of `trtc-electron-sdk` (xxx/node_modules/trtc-electron-sdk) in your project and run the following command:
```script
npm run install -- arch=ia32
```
2. Download the 32-bit `trtc_electron_sdk.node` and build your project again.

[](id:que4)
### Is `trtc-electron-sdk` compatible with Electron v12.0.1?
Yes, it is. `trtc-electron-sdk` does not rely on the SDK of Electron and therefore does not have version requirements.

[](id:que5)
### What should I do with the frequent reentry issue in the SDK for Electron?
This issue should be dealt with case by case. Possible causes include:
- The client has bad network conditions (network disconnection triggers reentry).
- The room entry signaling message is sent twice consecutively.
- The device is overloaded, which results in decoding failure.
- The same UID is used to log in from different devices.

[](id:que6)
### How do I know if there is a .node module loading issue?
You may see the error message below when running your project after compilation:
- `NodeRTCCloud is not a constructor`
![](https://main.qcloudimg.com/raw/f06737dc6be7d4eeed7573cd495c922f.png)
- `Cannot open xxx/trtc_electron_sdk.node`
![](https://main.qcloudimg.com/raw/a55c9ca2266bc6e591354e23da535e1d.png)
- `dlopen(xxx/trtc_electron_sdk.node, 1): image not found`
![](https://main.qcloudimg.com/raw/36c0e62fee13da96dc2136e10a07824b.png)
It indicates that the `trtc_electron_sdk.node` module hasn’t been built into your project successfully.
