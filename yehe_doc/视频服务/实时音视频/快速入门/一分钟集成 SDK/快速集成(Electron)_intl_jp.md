このドキュメントでは、Tencent Cloud TRTC SDK for Electronをプロジェクトにすばやく統合する方法について説明します。

## サポートするプラットフォーム
- Windows (PC)
- Mac

## TRYC Electron SDK の統合

#### 手順1：Node.jsのインストール
**Windowsプラットフォームのインストールガイド**
1．Windows OSに従って、最新バージョンの[Node.js](https://nodejs.org/en/download/) インストールパッケージ `Windows Installer (.msi) 64-bit`をダウンロードします。
2．アプリケーションリストにあるNode.js command promptを開き、コマンドラインウィンドウを起動して、後続の手順でコマンドを入力します。
![](https://main.qcloudimg.com/raw/a29b4681c1ed6ce57d66b5a79bda5e94.png)

**Mac OS プラットフォームのインストールガイド：**
1．ターミナル（Terminal）ウィンドウを開き、以下のコマンドを実行してHomebrewをインストールします。インストール済みの場合は、この手順はスキップしてください。
```shell
$ ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```
2. 以下のコマンドを実行し、 Node.jsをインストールします。 10.0 バージョンより大きい必要があります。
```shell
$ brew install node
```

#### 手順2： Electronのインストール
1．コマンドラインウィンドウで以下のコマンドを実行し、Electronをインストールします。バージョンは>=4.0.0を推奨します。
```shell
$ npm install electron@latest --save-dev
```

#### 手順3： TRTC Electron SDKのインストール
1. Electronプロジェクトでnpm コマンドを使用して SDKパッケージをインストールします：
```shell
$ npm install trtc-electron-sdk@latest --save
```
>?TRTC Electron SDKの最新バージョンは、 [trtc-electron-sdk](https://www.npmjs.com/package/trtc-electron-sdk) でクエリができます。

2．プロジェクトスクリプトにモジュールをインポートして使用します。
```javascript
const TRTCCloud = require('trtc-electron-sdk');
this.rtcCloud = new TRTCCloud();
// SDKバージョン番号の取得
this.rtcCloud.getSDKVersion();
```
v7.0.149から、TRTC Electron SDKは trtc.d.ts ファイルを増加しており、 TypeScript を使用する開発者には便利になりました：
```
// Enable ES Module interoperability mode (esModuleInterop=true)
import * as trtc_namespace from 'trtc-electron-sdk';
const TRTCCloud = require('trtc-electron-sdk');
const rtcCloud: trtc_namespace.TRTCCloud = new TRTCCloud();
// SDKバージョン番号の取得
rtcCloud.getSDKVersion();
```

## 実行可能プログラムのパッケージ化

#### 手順1：インストールパッケージツール
1．パッケージ化ツール`electron-builder` を使用してパッケージングすることを推奨します。以下のコマンドを実行して`electron-builder`をインストールできます。

```bash
$ npm install electron-builder@latest --save-dev
```

2． TRTC SDK for Electron（すなわち`trtc_electron_sdk.node` ファイル）を正しくパッケージ化するには、以下のコマンドを実行して `native-ext-loader` ツールもインストールする必要があります。

```bash
$ npm install native-ext-loader@latest --save-dev
```

#### 手順2：webpack.config.js 設定の変更
`webpack.config.js` ファイルには、プロジェクト構築の設定情報が含まれています。`webpack.config.js` ファイルの位置は以下のとおりです。
- 通常、`webpack.config.js` はプロジェクトのルートディレクトリにあります。
-  `create-react-app` を使用してプロジェクトを作成する場合、この設定ファイルは `node_modules/react-scripts/config/webpack.config.js`です。
-  `vue-cli` を使用してプロジェクトを作成する場合、webpack の設定は `vue.config.js` 設定ファイルの `configureWebpack` プロパティに保存されます。
- プロジェクトファイルがカスタマイズされている場合は、ご自身でwebpack設定を探してください。


1. 初めに `webpack.config.js`を構築するときは、`--target_platform`という名前のコマンドラインパラメータを受信できるようにします。コードの構築プロセスで異なる目標プラットフォームの特徴に応じてコードを正しくパッケージ化できるようにします。 `module.exports` の前に次のコードを追加します。


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
>os.platform() によって返される結果では、"darwin" は macOSを表します。64 ビットまたは 32ビットに関わらず、"win32" はWindowsを表します。


2. その後 `rules` オプションに以下の設定を追加します。`targetPlatform`変数を使用すると、 `rewritePath` はさまざまなターゲットプラットフォームに応じてさまざまな設定を切り替えることができます。

```js
rules: [
  { 
    test: /⧵.node$/, 
    loader: 'native-ext-loader', 
    options: { 
      rewritePath: targetPlatform === 'win32' ? './resources' : '../Resources' 
    } 
  },
]
```

この設定の意味は以下のとおりです。
-  Windows の.exe ファイルをパッケージ化するには、 `native-ext-loader`が `[アプリケーションルートディレクトリ]/resources` ディレクトリに TRTC SDKをロードします。
-  Mac の .dmgをパッケージ化するには、`native-ext-loader` が`[アプリケーションディレクトリ]/Contents/Frameworsk/../Resources` ディレクトリにTRTC SDKをロードします。

 `package.json`のスクリプトに`--target_platform`パラメーターを追加する必要があります。

#### 手順3：package.json設定の変更
`package.json` ファイルはプロジェクトのルートディレクトリにあり、プロジェクトのパッケージ化に必要な情報が含まれています。しかし、デフォルトでは、パッケージ化を正常に実装するには、`package.json`  のパスを次のように変更する必要があります。 

1．`main`設定の変更

```javascript
// 多くの状況では、main ファイル名は任意に設定できます。例えば、 TRTCSimpleDemo のものは次のように設定できます。
"main": "main.electron.js",
  
// しかし、 create-react-appスキャフォールディングツールで作成されたプロジェクトの場合、main ファイルは次のように設定する必要があります：
"main": "public/electron.js",
```
2. 以下の `build` 設定をコピーし、`package.json` ファイルに追加します。これは `electron-builder` が読み取る必要のある設定情報です。

```json
"build": {
   "appId": "[Custom appId]"
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

3． `scripts`ノードにおいて以下のコマンドスクリプトを追加します。

 このドキュメントでは、`create-react-app` および `vue-cli` で作成されたプロジェクトを例として使用します。他のツールで作成されたプロジェクトについては、次の設定を参照できます。

```json
// create-react-app で作成されたプロジェクトにはこの設定を使用してください
"scripts": {
  "build:mac": "react-scripts build --target_platform=darwin",
  "build:win": "react-scripts build --target_platform=win32",
  "compile:mac": "node_modules/.bin/electron-builder --mac",
  "compile:win64": "node_modules/.bin/electron-builder --win --x64",
  "pack:mac": "npm run build:mac && npm run compile:mac",
  "pack:win64": "npm run build:win && npm run compile:win64"
}

// vue-cli で作成されたプロジェクトにはこの設定を使用してください
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
> -   `main` ：Electron のエントリーファイルは、一般には自由に設定できます。しかし、プロジェクトが`create-react-app` スキャフォールディングツールを使用して作成されている場合は、エントリーファイルは `public/electron.js` に設定する必要があります。　
> -   `build.win.extraFiles` ： Windows プログラムをパッケージ化する場合は、`electron-builder` は `from` が示すディレクトリ下のすべてのファイルを bin/win-unpacked/resources（すべて小文字表記）にコピーします。
> -   `build.mac.extraFiles` ：macOSプログラムをパッケージ化する場合は、`electron-builder` は `from` で指定された `trtc_electron_sdk.node` ファイルを bin/mac/your-app-name.app/Contents/Resources（頭文字は大文字表記）にコピーします。
> -   `build.directories.output` ：パッケージ化されたファイルの出力パス。たとえば、パッケージ化されたファイルは、この設定に従って`bin`ディレクトリに出力されます。必要に応じて変更できます。
> -   `build.scripts.build:mac` ： Mac プラットフォームを目標にスクリプトを構築します。
> -   `build.scripts.build:win` ： Windows プラットフォームを目標にスクリプトを構築します。
> -   `build.scripts.compile:mac` ：macOS用の .dmgインストールファイルにコンパイルします。
> -   `build.scripts.compile:win64` ：Windows用の.exeインストールファイルにコンパイルします。
> -   `build.scripts.pack:mac` ： build:macを呼び出してコードをビルドし、compile:macを呼び出して.dmgインストールファイルとしてパッケージ化します。
> -   `build.scripts.pack:win64` ：build:winを呼び出してコードをビルドし、pack:win64を呼び出して.exeインストールファイルとしてパッケージ化します

#### 手順4：パッケージ化のためのコマンドの実行
-  Mac .dmg インストールファイルをパッケージ化します：

```bash
$ cd [Project directory]
$ npm run pack:mac
```
実行が上手くいけば、パッケージツールは `bin/your-app-name-0.1.0.dmg` インストールファイルを新規作成しますので、このファイルのリリースを選択してください。

-  Windows .exe インストールファイルのパッケージ：

```bash
$ cd [項目ディレクトリ]
$ npm run pack:win64
```
正常に実行されると、パッケージ化ツールは `bin/your-app-name Setup 0.1.0.exe` インストールファイルを生成しますので、このファイルを選択して公開してください。

>!TRTC Electron SDK は、クロスプラットフォームパッケージングを一時的にサポートしません。現在クロスプラットフォームパッケージング方法を検討中ですのでご期待ください。

## よくあるご質問

### 1．ファイアウォールにどのような制限がありますか？

SDKがUDP プロトコルを使用してオーディオ/ビデオ送信を行っていることから、 UDPをブロックするオフィスネットワークでは使用できません。このような問題が発生した場合は、 [ファイアウォールの制限に対処する方法](https://intl.cloud.tencent.com/document/product/647/35164)をご参照ください。





