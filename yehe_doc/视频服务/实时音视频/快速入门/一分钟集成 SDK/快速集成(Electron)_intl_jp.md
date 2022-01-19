ここでは、主にTencent Cloud TRTC Electron SDK をプロジェクトに素早く統合する方法を紹介します。

## サポートするプラットフォーム
-  Windows(PC)
-  Mac

## TRYC Electron SDKの統合

### 手順1：Node.jsのインストール
<dx-tabs>
::: Windowsプラットフォームのインストールガイド
1．WindowsOSに従って、最新バージョンの[Node.js](https://nodejs.org/en/download/) インストールパック`Windows Installer (.msi) 64-bit`を選択、ダウンロードします。
2．アプリケーションプログラムリストにあるNode.js command promptを開き、コマンドラインのポートを起動し、その後の手順における各コマンドの入力に使用します。
![](https://main.qcloudimg.com/raw/a29b4681c1ed6ce57d66b5a79bda5e94.png)
:::
::: MacOSプラットフォームのインストールガイド
1．ターミナル（Terminal）ポートを開き、以下のコマンドを実行してHomebrewをインストールします。すでにインストールされている場合は、この手順はスキップしてください。
<dx-codeblock>
::: shell shell
$ ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
:::
</dx-codeblock>

2. 以下のコマンドを実行し、 Node.jsをインストールします。 10.0 バージョンより大きい必要があります。
```shell
$ brew install node
```

:::
</dx-tabs>

### 手順2： Electronのインストール
コマンドラインポートで以下のコマンドを実行し、Electronをインストールします。バージョンは>=4.0.0を推奨します。
```shell
$ npm install electron@latest --save-dev
```


### 手順3： Electronバージョン TRTC SDKのインストール
1. Electron項目でnpmコマンドを使用してSDKパッケージをインストールします：
```shell
$ npm install trtc-electron-sdk@latest --save
```
>?TRTC Electron SDK最新版では、 [trtc-electron-sdk](https://www.npmjs.com/package/trtc-electron-sdk) でクエリーできます。
2．プロジェクトのスクリプトでモジュールを導入して、使用します。
```javascript
const TRTCCloud = require('trtc-electron-sdk').default;
// import TRTCCloud from 'trtc-electron-sdk';
this.rtcCloud = new TRTCCloud();
// SDKバージョン番号の取得
this.rtcCloud.getSDKVersion();
```
v7.9.348から、TRTC Electron SDKはtrtc.d.tsファイルを増加しており、 TypeScriptを使用する開発者には便利になりました：
```
import TRTCCloud from 'trtc-electron-sdk';
const rtcCloud: TRTCCloud = new TRTCCloud();
// SDKバージョン番号の取得
rtcCloud.getSDKVersion();
```

## パッケージで実行可能なプログラム

### 手順1：パッケージングツールのインストール
1．パッケージングツール`electron-builder` を使用してパッケージングすることを推奨します。以下のコマンドを実行して`electron-builder`をインストールできます。
```bash
$ npm install electron-builder@latest --save-dev
```
2． Electronバージョンの TRTC SDK（すなわち`trtc_electron_sdk.node` ファイル）を正しくパッケージするために、以下のコマンドを実行して `native-ext-loader` ツールもインストールする必要があります。
```bash
$ npm install native-ext-loader@latest --save-dev
```

### 手順2：webpack.config.js設定の修正
`webpack.config.js` は、項目アーキテクチャの設定情報を含んでいます。`webpack.config.js` ファイルの位置は以下のとおりです。
- 通常、`webpack.config.js` は項目のルートディレクトリにあります。
- `create-react-app` 使用して項目を新規作成する状況では、この設定ファイルは `node_modules/react-scripts/config/webpack.config.js`です。
- `vue-cli` を使用して項目を新規作成する状況では、webpack の設定は `vue.config.js` 設定の `configureWebpack` のプロパティにあります。
- プロジェクトファイルがカスタマイズされている場合は、ご自身でwebpack設定を検索してください。


1. 初めに `webpack.config.js` を構築するときは、 受信名を`--target_platform` のコマンドラインパラメータにできるため、コードの構築プロセスで異なる目標プラットフォームの特徴に応じて正しくパッケージできます。 `module.exports` の前に以下のコードを追加します。
``` js
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
>! `os.platform()` によって返される結果では、"darwin" は Macのプラットフォームを表します。64ビットまたは 32ビットに関わらず、"win32" は Windowsプラットフォームを表します。
2. その後 `rules` オプションでは以下の設定を追加します。`targetPlatform` 変数は `rewritePath` を使って、異なる目標プラットフォームに従って違う設定に切り替えることができます。
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
	この設定の意味は以下のとおりです。
	-  Windowsの`.exe` ファイルをパッケージにするときは、 `native-ext-loader` に `[アプリケーションプログラムルートディレクトリ]/resources` ディレクトリでTRTC SDKをアップロードします。
	-  Macの `.dmg` をパッケージするときは、 `native-ext-loader` に`[アプリケーションディレクトリ]/Contents/Frameworsk/../Resources` ディレクトリでTRTC SDKをロードします。

`package.json` のスクリプト構築で、 `--target_platform`パラメータを追加するには、以下を実行します。

### 手順3：package.json設定の修正
`package.json` は項目のルートディレクトリにあり、そのうち項目のパッケージに必要な情報を含みます。しかし、デフォルトの状況では、`package.json`  の中のパスを修正しなければ順調にパッケージできません。以下の手順に従ってこのファイルを修正できます。 

1．`main`設定の修正。
<dx-codeblock>
::: javascript javascript
// 多くの状況では、mainファイル名は任意に設定できます。例えば、 TRTCSimpleDemoのものは次のように設定できます。
"main": "main.electron.js",

// しかし、 create-react-app のスキャフォールディングを使用して新規作成した項目、mainファイルは次のように設定する必要があります：
"main": "public/electron.js",
:::
</dx-codeblock>
2. 以下の `build` 設定をコピーし、`package.json` ファイルに追加します。これは `electron-builder` が読み取る必要のある設定情報です。
<dx-codeblock>
::: json json
"build": {
    "appId": "[appId はご自身で定義してください]",
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
:::
</dx-codeblock>
3． `scripts`ノードにおいて以下のアーキテクチャおよびパッケージしたコマンドスクリプトを追加します。
 ここでは 、`create-react-app` および `vue-cli` 項目を例に、その他のツールで作成した項目もこの設定を参考にすることができます。
<dx-codeblock>
::: json json
// create-react-app項目にはこの設定を使用してください
"scripts": {
    "build:mac": "react-scripts build --target_platform=darwin",
    "build:win": "react-scripts build --target_platform=win32",
    "compile:mac": "node_modules/.bin/electron-builder --mac",
    "compile:win64": "node_modules/.bin/electron-builder --win --x64",
    "pack:mac": "npm run build:mac && npm run compile:mac",
    "pack:win64": "npm run build:win && npm run compile:win64"
}

// vue-cli項目にはこの設定を使用してください
"scripts": {
  "build:mac": "vue-cli-service build --target_platform=darwin",
  "build:win": "vue-cli-service build --target_platform=win32",
  "compile:mac": "node_modules/.bin/electron-builder --mac",
  "compile:win64": "node_modules/.bin/electron-builder --win --x64",
  "pack:mac": "npm run build:mac && npm run compile:mac",
  "pack:win64": "npm run build:win && npm run compile:win64"
}
:::
</dx-codeblock>
<table>
<tr><th>パラメータ</th><th>説明</th></tr>
<tr>
<td>main</td>
<td>Electron のエントリーファイルは、一般には自由に設定できます。しかし、項目を<code>create-react-app</code> のスキャフォールディングを使用して作成した場合は、エントリーファイルは <code>public/electron.js</code>に設定する必要があります</td>
</tr><tr>
<td>build.win.extraFiles</td>
<td>Windowsプログラムをパッケージする場合は、<code>electron-builder</code>は<code>from</code>が示すディレクトリ下のすべてのファイルをbin/win-unpacked/resources（すべて小文字表記）にコピーします</td>
</tr><tr>
<td>build.mac.extraFiles</td>
<td>Macプログラムをパッケージする場合は、<code>electron-builder</code>は<code>from</code>が示す<code>trtc_electron_sdk.node</code>ファイルをbin/mac/your-app-name.app/Contents/Resources（頭文字は大文字表記）にコピーします</td>
</tr><tr>
<td>build.directories.output</td>
<td>パッケージファイルの出力パス。例えば、この設定を<code>bin</code>ディレクトリに出力する場合は、実際のニーズに従って修正します</td>
</tr><tr>
<td>build.scripts.build:mac</td>
<td>Macプラットフォームを目標にスクリプトを構築します</td>
</tr><tr>
<td>build.scripts.build:win</td>
<td>Windowsプラットフォームを目標にスクリプトを構築します</td>
</tr><tr>
<td>build.scripts.compile:mac</td>
<td>Macの .dmgインストールファイルをコンパイルします</td>
</tr><tr>
<td>build.scripts.compile:win64</td>
<td>Windowsの .exeインストールファイルをコンパイルします</td>
</tr><tr>
<td>build.scripts.pack:mac</td>
<td>まず build:macアーキテクチャコードをコールしてからcompile:macをコールして .dmgインストールファイルをパッケージします</td>
</tr><tr>
<td>build.scripts.pack:win64</td>
<td>まず build:winアーキテクチャコードをコールしてからcompile:win64をコールして .exeインストールファイルをパッケージします</td>
</tr></table>




### 手順4：パッケージコマンドの実行
-  Mac .dmgインストールファイルのパッケージ：
```bash
$ cd [項目ディレクトリ]
$ npm run pack:mac
```
	実行に成功すると、パッケージツールは`bin/your-app-name-0.1.0.dmg`インストールファイルを新規作成しますので、このファイルのリリースを選択してください。
-  Windows .exeインストールファイルのパッケージ：
```bash
$ cd [項目ディレクトリ]
$ npm run pack:win64
```
	実行に成功すると、パッケージツールは`bin/your-app-name Setup 0.1.0.exe`インストールファイルを新規作成しますので、このファイルのリリースを選択してください。


>!TRTC Electron SDK は、プラットフォームパッケージ（Mac下でWindowsをパッケージする.exe ファイル、またはWindowsプラットフォーム下でMacをパッケージする .dmgファイルなど）を一時的にサポートしません。現在プラットフォームを跨がるパッケージ方法を検討中ですのでご期待ください。

## よくあるご質問

### 1. ファイアウォールにはどのような制限がありますか。

SDKがUDPプロトコルを使用してオーディオ・ビデオ伝送を行っているため、UDPをブロックするオフィスネットワークでは使用できません。類似した問題がおありの際は、[企業ファイアウォール制限の対応](https://intl.cloud.tencent.com/document/product/647/35164)をご参照の上、問題及び原因解決にお役立てください。

### 2. Electronのインストールまたはパッケージ化のトラブル
- Electron統合中にトラブルが生じた場合、例えばインストールのタイムアウトまたは失敗、パッケージ後にtrtc_electron_sdk.nodeファイルのロード失敗などの状況が生じた場合は、[お問い合わせ](https://intl.cloud.tencent.com/contact-us)までご連絡いただければご質問にお答えします。



## 参考ドキュメント

- [SDK APIマニュアル](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/index.html)
- [SDK更新ログ](https://intl.cloud.tencent.com/document/product/647/38702)
- [Simple Demoソースコード](https://github.com/tencentyun/TRTCSDK/tree/master/Electron/TRTCSimpleDemo)
- [API Exampleソースコード](https://github.com/tencentyun/TRTCSDK/tree/master/Electron/TRTC-API-Example)
- [Electronについてのよくあるご質問](https://intl.cloud.tencent.com/document/product/647/43093)
