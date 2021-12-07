[](id:que1)
### Demo를 실행하면 정의되지 않은 널 포인터 오류 “cannot read property "dlopen" of undefined”가 발생합니다.
![](https://main.qcloudimg.com/raw/fa2ac368a07eefdc63901f3910a122f9.png)
Electron 12 버전 컨텍스트 격리는 기본적으로 활성화되어 있으며, contextIsolation은 false로 설정할 수 있습니다.

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
### vscode terminal에서 Electron Demo를 실행하여 방에 입장하면 빈 화면이 표시됩니다.
vscode는 카메라 권한이 필요하며 다음과 같은 방법으로 권한을 추가할 수 있습니다.

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
### Windows 32 시스템에서 32비트 trtc_electron_sdk.node가 필요하다는 오류가 보고됩니다.
![](https://main.qcloudimg.com/raw/4e0115819b868ee9a6d110f641096e01.png)
1. 프로젝트 디렉터리의 trtc-electron-sdk 디렉터리(xxx/node_modules/trtc-electron-sdk)로 이동하여 다음을 실행합니다.
```script
npm run install -- arch=ia32
```
2. 32비트 `trtc_electron_sdk.node` 다운로드 후, 프로젝트를 다시 패키징합니다.

[](id:que4)
### trtc-electron-sdk는 공식 Electron v12.0.1 버전과 호환됩니까?
호환됩니다. trtc-electron-sdk는 elecron 자체에 의존하는 sdk가 없으므로 관련 버전 종속성이 없습니다.

[](id:que5)
### Electron 방 재입장 문제가 반복해서 발생합니다.
구체적인 case 분석이 필요합니다. 일반적인 이유는 다음과 같습니다.
- 클라이언트의 네트워크 상태가 좋지 않은 경우(연결이 중단되면 방 재입장이 트리거됩니다).
- 방 입장 신호를 2회 연속으로 발송한 경우.
- 디바이스 과부하로 디코딩 실패가 발생한 경우.
- 동일 UID로 여러 단말에서 중복 로그인한 경우.

[](id:que6)
### .Node 모듈 로딩 문제가 발생하였습니다.
패키징 및 컴파일된 프로그램이 실행 중일 때 콘솔에서 다음과 같은 오류 메시지가 보고됩니다.
- `NodeRTCCloud is not a constructor`
![](https://main.qcloudimg.com/raw/f06737dc6be7d4eeed7573cd495c922f.png)
- `Cannot open xxx/trtc_electron_sdk.node`
![](https://main.qcloudimg.com/raw/a55c9ca2266bc6e591354e23da535e1d.png)
- `dlopen(xxx/trtc_electron_sdk.node, 1): image not found`
![](https://main.qcloudimg.com/raw/36c0e62fee13da96dc2136e10a07824b.png)
상기와 같은 오류 메시지는 trtc_electron_sdk.node 모듈이 프로그램에 올바르게 패키징되지 않았음을 뜻합니다.
