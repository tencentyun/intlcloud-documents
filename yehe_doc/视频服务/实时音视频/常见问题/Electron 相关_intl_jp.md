[](id:que1)
###  Demoの実行時にNULLポインタの未定義のエラー「cannot read property "dlopen" of undefined」がスローされてしまいます。
![](https://main.qcloudimg.com/raw/fa2ac368a07eefdc63901f3910a122f9.png)
Electron 12バージョンではコンテキスト分離がデフォルトでオンになっています。contextIsolationをfalseに設定できます。

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
###  vscode terminalでElectron Demoを起動すると、入室後にディスプレイが白くなります。
vscodeにカメラの権限が必要です。次の方法で権限を追加することができます。

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
###  Windowsシステム32の実行がエラーとなり、32ビットのtrtc_electron_sdk.nodeが必要と表示されました。
![](https://main.qcloudimg.com/raw/4e0115819b868ee9a6d110f641096e01.png)
1. プロジェクトディレクトリ下のtrtc-electron-sdkのライブラリディレクトリ（xxx/node_modules/trtc-electron-sdk）に入り、次を実行します。
```script
npm run install -- arch=ia32
```
2. 32ビットの`trtc_electron_sdk.node`のダウンロードを完了後、項目を再度パッケージ化します。

[](id:que4)
### trtc-electron-sdkは公式のElectron v12.0.1バージョンと互換性がありますか。
互換性があります。trtc-electron-sdkは特にelecron自体のsdkに依存しないので、それに関するバージョンの依存関係はありません。

[](id:que5)
### Electronで再入室の問題が何度も発生します。
具体的なcaseを分析する必要がありますが、おおよその原因は次のとおりです。
- クライアントのネットワーク状態不良（ネットワークが切断されると再入室がトリガーされます）。
- 連続して2回入室シグナルを送信した場合も、再入室となる場合があります。
- デバイスの負荷が高すぎたことで、デコードに失敗し再入室となる場合があります。
- 同一のUIDでの複数端末ログインが互いにキックアウトされ、再入室となる場合があります。

[](id:que6)
### .nodeモジュールのロードに問題があります。
パッケージ化してコンパイルしたプログラムを実行する際、コンソールにこのようなエラーメッセージがみられます。
- `NodeRTCCloud is not a constructor`
![](https://main.qcloudimg.com/raw/f06737dc6be7d4eeed7573cd495c922f.png)
- `Cannot open xxx/trtc_electron_sdk.node`
![](https://main.qcloudimg.com/raw/a55c9ca2266bc6e591354e23da535e1d.png)
- `dlopen(xxx/trtc_electron_sdk.node, 1): image not found`
![](https://main.qcloudimg.com/raw/36c0e62fee13da96dc2136e10a07824b.png)
上のようなメッセージが表示された場合は、trtc_electron_sdk.nodeモジュールがプログラムに正しくパッケージ化されていないことを意味します。
