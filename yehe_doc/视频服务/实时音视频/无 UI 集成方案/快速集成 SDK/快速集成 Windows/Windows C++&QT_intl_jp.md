このドキュメントでは、Tencent Cloud TRTC SDK（Windows C++ 版）をQTプロジェクトに素早く統合する方法をご紹介します。

## 開発環境要件
- OS：Windows 7以降のバージョン。
- 開発環境：Visual Studio 2010以降のバージョンが必要です。Visual Studio 2015の使用を推奨します。
- [QT](https://download.qt.io/archive/qt/5.9/5.9.1/qt-opensource-windows-x86-5.9.1.exe)と[VS開発プラグイン](https://download.qt.io/archive/vsaddin/2.6.0/qt-vsaddin-msvc2015-2.6.0.vsix)の関連プラグイン環境が既にインストールされていることをご確認ください。

[](id:using_cpp)
## QTプロジェクトによるC++ SDKの統合
このセグメントでは、簡単なQTプロジェクトを作成することで、Visual Studioプロジェクトの中でC++ SDKを統合する方法を紹介します。

[](id:using_cpp_qt_step1)
### ステップ1： SDKのダウンロード
1. [SDKをダウンロード](https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_TRTC_Win_latest.zip)して、解凍して開きます。
本文の例の中で必要なものは、SDKディレクトリ下のC++バージョンのSDKファイルのみです。64bitを例とすると、そのSDKの位置は`./SDK/CPlusPlus/Win64/`下にあり、主に次の部分を含みます。
<table>
<thead>
<tr>
<th>ディレクトリ名</th>
<th>説明</th>
</tr>
</thead>
<tbody><tr>
<td>include</td>
<td>詳細なインターフェース注釈つきのAPIヘッダファイル</td>
</tr>
<tr>
<td>lib</td>
<td>コンパイル用の.libファイルと実行時にローディングされる.dllファイル</td>
</tr>
</tbody></table>

### 手順2：プロジェクトの新規作成[](id:using_cpp_qt_step2)
Visual Studio 2015 を例とすると、ローカル環境に[QT](https://download.qt.io/archive/qt/5.9/5.9.1/qt-opensource-windows-x86-5.9.1.exe)と[VS開発プラグイン](https://download.qt.io/archive/vsaddin/2.6.0/qt-vsaddin-msvc2015-2.6.0.vsix)がインストールされている前提で、Visual Studioを開きます。`TRTCDemo`という名前のQTアプリケーションプログラムを新規作成します。以下の図の通りです。
![](https://qcloudimg.tencent-cloud.cn/raw/fa665d6c78420db0da022ae81f2d7c68.png)
素早く統合する方法のご紹介のため、ナビゲーションから**Qt Widgets Application**タイプを選択し，**確定**をクリックします。その次のページで、プロジェクトの新規作成が完了するまで**Next**をクリックしてください。

### 手順3：**ファイルのコピー[](id:using_cpp_qt_step3)
解凍後のSDKフォルダをTRTCDemo.vcxprojが存在するディレクトリ下にコピーします。次の図のとおりです。
>?現在はC++ SDKがあれば、SDKパス下のCsharpディレクトリを削除できます。

![](https://qcloudimg.tencent-cloud.cn/raw/49681d526061bdef063e878879d471a8.png)

### 手順4：プロジェクト構成の変更[](id:using_cpp_qt_step4)
TRTCDemoの属性ページを開きます。**ソリューションのResource Manager** >**TRTCDemoプロジェクトのメニュー**>**属性**を右クリックして、次の手順にしたがって設定してください。
1. **Includeのディレクトリの追加：**
**C/C++** > **常規** > **添付ファイル付きディレクトリ**から、以下のSDKヘッダファイルディレクトリを追加します。なお、64bitの例： `$(ProjectDir)SDK\CPlusPlus\Win64\include`と`$(ProjectDir)SDK\CPlusPlus\Win64\include\TRTC`、下図の通りです。
>?32bitの場合、SDKヘッダファイルディレクトリを`$(ProjectDir)SDK\CPlusPlus\Win32\include` と `$(ProjectDir)SDK\CPlusPlus\Win32\include\TRTC`として設定してください。

![](https://qcloudimg.tencent-cloud.cn/raw/61a49b758ecb52ab6ee576421da5800d.png)
2. **ライブラリのディレクトリの追加：**
**リンカ** > **常規** > **添付ライブラリ付きディレクトリ**から、以下のSDKヘッダファイルディレクトリを追加します。なお、64bitの例： `$(ProjectDir)SDK\CPlusPlus\Win64\lib`、下図の通りです。
>?32bitの場合、SDKライブラリディレクトリを`$(ProjectDir)SDK\CPlusPlus\Win32\lib`として設定してください。

![](https://qcloudimg.tencent-cloud.cn/raw/89b465c893f456edacf3355dc59f0258.png)
3. **ライブラリファイルの追加：**
**リンカ** > **入力** > **依存項目の追加**からSDKライブラリファイル`liteav.lib`を追加します。下図の通りです。
![](https://qcloudimg.tencent-cloud.cn/raw/7eb6bbe2351dc4cd3e6c7ae817042fae.png)
4. **copyコマンドの追加：**
**イベントの生成** > **後続イベントの生成** > **コマンドライン**から、コピーコマンド`copy /Y $(ProjectDir)SDK\CPlusPlus\Win64\lib\*.dll  $(OutDir)`を追加します。コンパイルが完了すると、自動的にSDKの.dllファイルがプログラムの実行ディレクトリの下にコピーされます。下図のとおりです。
>?32bitの場合、コピーコマンド`copy /Y $(ProjectDir)SDK\CPlusPlus\Win32\lib\*.dll  $(OutDir)`を追加します。

![](https://qcloudimg.tencent-cloud.cn/raw/c6cb6d0dfd935be7a74313881a306c5f.png)

### 手順5： SDK バージョン番号のプリント[](id:using_cpp_qt_step5)
1. `TRTCDemo.cpp`ファイルのヘッドにヘッダファイルを追加してください。コードは以下のとおりです。
``` c++
#include "ITRTCCloud.h"
#include <QLabel>
```
2. `TRTCDemo.cpp` ファイルの`TRTCDemo::TRTCDemo`構造関数の中で、次のテストコードを追加します。
```C++
ITRTCCloud * pTRTCCloud = getTRTCShareInstance();
std::string version(pTRTCCloud->getSDKVersion());

QString sdk_version = QString("SDK Version: %1").arg(version.c_str());
QLabel* label_text = new QLabel(this);
label_text->setAlignment(Qt::AlignCenter);
label_text->resize(this->width(), this->height());
label_text->setText(sdk_version);
```
3. F5キーを押して実行すると、SDKのバージョン番号がプリントされます。次の図のとおりです。  
![](https://qcloudimg.tencent-cloud.cn/raw/bc1ddf818e5f0571c72d34ba212691c7.png)

## よくあるご質問
- 次のエラーが生じた場合は、前述のプロジェクト設定にしたがって、SDKヘッダーファイルのディレクトリが正しく追加されているかチェックしてください。
```
fatal error C1083: includeファイルを開くことができません:「TRTCCloud.h」: No such file or directory
```

- 次のエラーが生じた場合は、前述のプロジェクト設定にしたがって、SDKライブラリのディレクトリとライブラリファイルが正しく追加されているかチェックしてください。
```
error LNK2019: 解析できない外部シンボル"__declspec(dllimport) public: static class TXString __cdecl TRTCCloud::getSDKVersion(void)" (__imp_?getSDKVersion@TRTCCloud@@SA?AVTXString@@XZ)、この記号が関数"protected: virtual int __thiscall CTRTCDemoDlg::OnInitDialog(void)" (?OnInitDialog@CTRTCDemoDlg@@MAEHXZ)の中に引用されています
```
