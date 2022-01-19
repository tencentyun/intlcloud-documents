[](id:install)
## インストール関連
[](id:install_q1)
### trtc-electron-sdkは公式のElectron v12.0.1バージョンと互換性がありますか。

互換性があります。trtc-electron-sdkは特にelecron自体のSDKに依存しないので、それに関するバージョンの依存関係はありません。


[](id:install_q3)
### Electronのダウンロードの際に404エラーが表示されます。
![](https://qcloudimg.tencent-cloud.cn/raw/a1855dc24d83db2f0fabe03fcdbce916.png)

端末に次のコマンドを入力します。
```
$ npm config set electron_custom_dir 8.1.1 # バージョン番号によって決定
```

[](id:run)
## 実行関連
[](id:run_q1)

###  Windows 32システムの実行時に`Error：resource\trtc_electron_sdk.node is not a valid Win32 application`というエラーが表示されます。32ビットのtrtc_electron_sdk.nodeが必要ということでしょうか。

![](https://main.qcloudimg.com/raw/4e0115819b868ee9a6d110f641096e01.png)
**解決方法**：
1. プロジェクトディレクトリ下のtrtc-electron-sdkのライブラリディレクトリ（xxx/node_modules/trtc-electron-sdk）に入り、次を実行します。
```script
npm run install -- arch=ia32
```
2. 32ビットの`trtc_electron_sdk.node`のダウンロードを完了後、項目を再度パッケージ化します。


[](id:run_q2)
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

[](id:run_q3)

###  Demoの実行時にNULLポインタの未定義のエラー`“cannot read property 'dlopen' of undefined”`がスローされてしまいます。

![](https://main.qcloudimg.com/raw/fa2ac368a07eefdc63901f3910a122f9.png)
**解決方法**：
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


[](id:run_q4)
### Electronで再入室の問題が何度も発生します。

具体的なcaseを分析する必要がありますが、おおよその原因は次のとおりです。

- クライアントのネットワーク状態不良（ネットワークが切断されると再入室がトリガーされます）。
- 連続して2回入室シグナルを送信した場合も、再入室となる場合があります。
- デバイスの負荷が高すぎたことで、デコードに失敗し再入室となる場合があります。
- 同一のUIDでの複数端末ログインが互いにキックアウトされ、再入室となる場合があります。


[](id:run_q5)
### 端末に「Electron failed to install correctly」と表示されました。
インストールが完了したように見えて、実行中のプログラムがある場合、端末に次のエラーが表示されます。
```
Error: Electron failed to install correctly, please delete node_modules/electron and try installing again
```
次の3つの手順によって**手動でのダウンロード**を行ってください。
1. `npm config get cache`を実行し、キャッシュディレクトリを確認します。
2. Electronを手動でダウンロードし、キャッシュディレクトリに保存します。
3. 再び`npm install`を実行します。

[](id:run_q6)

### カメラまたはマイクを呼び出すとそのままクラッシュしました。

vscodeの端末起動プログラムを使用し、trtc-electron-sdkがカメラとマイクを起動した場合、プログラムがそのままクラッシュします。


- **対処方法A**：権限が承認されている端末実行プログラムを使用します。
- **対処方法B**：vscodeの権限承認を行います。**システム環境設定 > セキュリティとプライバシー**からvscodeの権限を承認します。
- **対処方法C**：次の手順で保護メカニズムを無効化します。
	1. システムを再起動し、 command + rキーを**押したまま**、システムが保護モードに入るまで**押し続けます**。
	2. terminal を開いて`csrutil disable`と入力し、保護メカニズムを無効化します。
	3. 再起動し、正常にシステムに入ります。この時点で vscode の端末起動プログラムは使用できるようになっています。
	4. 保護メカニズムを再度有効にしたい場合は、ステップ2で`csrutil enable`を実行します。


[](id:run_q7)
### Electronのコンソールで「xx is not defined」というエラーが表示されました。
プログラムの実行時に、Electron のコンソールで `xx is not defined` と表示されます。この `xx` には node モジュールが入ります。例えば次のようになります。
```
	Uncaught ReferenceError: require is not defined
```
Electron の `main.js` ファイルで `nodeIntegration` 設定項目を true に変更します。
```
	let win = new BrowserWindow({
        width: 1366,
        height: 1024,
        webPreferences: {
     		nodeIntegration: true,  // この項目をtrueに設定してください
    	},
	  });
```


[](id:pack)
## パッケージ化関連
[](id:pack_q1)
### .nodeモジュールのロードに問題があります。
#### エラーメッセージ
パッケージ化してコンパイルしたプログラムを実行する際、コンソールにこのようなエラーメッセージがみられます。

- `NodeRTCCloud is not a constructor`
	![](https://main.qcloudimg.com/raw/f06737dc6be7d4eeed7573cd495c922f.png)
- `Cannot open xxx/trtc_electron_sdk.node`または`The specified module could not be found`
	![](https://main.qcloudimg.com/raw/a55c9ca2266bc6e591354e23da535e1d.png)
- `dlopen(xxx/trtc_electron_sdk.node, 1): image not found`
	![](https://main.qcloudimg.com/raw/36c0e62fee13da96dc2136e10a07824b.png)

#### ソリューション
上のようなメッセージが表示された場合は、 trtc_electron_sdk.nodeモジュールがプログラムに正しくパッケージ化されていないことを意味します。次の手順に従って処理することができます。

1. `native-ext-loader`をインストールします。
```
	 $ npm i native-ext-loader -D
```
2. webpack の設定を変更します。
	1. `webpack.config.js`を構築する際、 受信名を`--target_platform`のコマンドラインパラメータにできるため、コードの構築プロセスで異なる目標プラットフォームの特徴に応じて正しくパッケージできます。 `module.exports`の前に以下のコードを追加します。
```
const os = require('os');
// target_platformパラメータが渡されない場合、プログラムはデフォルトで現在のプラットフォームタイプに応じてパッケージします
const targetPlatform = (function(){
	let target = os.platform();
	for (let i=0; i<process.argv.length; i++) {
		if (process.argv[i].includes('--target_platform=')) {
			target = process.argv[i].replace('--target_platform=', '');
			break;
		}
	}
	// win32 は統一してWindowsプラットフォームを表し、32ビットと64ビットのどちらも含まれます。darwinはMacプラットフォームを表します
	if (!['win32', 'darwin'].includes) target = os.platform();
		return target;
})();
```
	2. 次のrules設定を追加します。
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
> - `vue-cli`を使用して作成した項目については、webpack設定は`vue.config.js`ファイルの`configureWebpack`オプションに保存されます。
> - `create-react-app`を使用して作成した項目については、webpack設定ファイルは`[プロジェクトディレクトリ]/node_modules/react-scripts/config/webpack.config.js`となります。
3. packages.jsonファイルを設定し、パッケージ設定と構築したスクリプトを追加します。
	1. `electron-builder`パッケージ設定を追加します（大文字と小文字の区別に注意）。
```
"build": {
	"省略": "...",
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
	2. scripts構築、パッケージスクリプト`create-react-app`項目の追加については次の設定をご参照ください。
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
	3. `vue-cli`項目については次の設定をご参照ください。
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
### エントリーファイルが見つかりません。
`create-react-app`を使用して作成した項目を、`electron-builder`でパッケージ化する際にこの問題が起きることがあります。
```
    $ node_modules\.bin\electron-builder.cmd
      • electron-builder  version=22.6.0 os=6.1.7601
      • loaded configuration  file=package.json ("build" field)
      • public/electron.js not found. Please see https://medium.com/@kitze/%EF%B8%8F-from-react-to-an-electron-app-ready-for-production-a0468ecb1da3
      • loaded parent configuration  preset=react-cra
```
このうち、`public/electron.js not found`が、エントリーファイルが見つからないことを意味しています。

#### ソリューション
1. エントリーファイルを移動してリネームします。
```
$ cd [項目ディレクトリ]
$ mv main.electron.js ./public/electron.js
```
2. pacakge.jsonファイルを修正します。
```
{
	"main": "public/electron.js",
	"省略": "..."
}
```

[](id:pack_q3)
### パッケージ化を実行した際、fs-extraモジュールの構文エラーが表示されました。
```
[プロジェクトディレクトリ]\node_modules\electron-builder\node_modules\fs-extra\lib\empty\index.js:33
	} catch {
            ^

SyntaxError: Unexpected token {
	at new Script (vm.js:51:7)
```
最新のnodeにアップグレードできます。具体的には[Node.js公式サイト](https://nodejs.org/en/download/)をご参照ください。
