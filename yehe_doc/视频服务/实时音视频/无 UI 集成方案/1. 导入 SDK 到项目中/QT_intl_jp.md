ここでは、主にTencent Cloud TRTC SDK(QTのWindowsバージョンおよびMacバージョン) をプロジェクトに素早く統合する方法を紹介します。以下の手順に従って設定すれば、SDKの統合作業を素早く完了できます。

![](https://qcloudimg.tencent-cloud.cn/raw/f85f7ee54d462d85290fc6f50e5ed96a.png)

## Windows端末の統合
### 開発環境要件
- OS：Windows 7以上のバージョン。
- 開発環境：Visual Studio 2015以上のバージョン、Visual Studio 2015の使用をお勧めします。VS関連のQT開発環境をすでに設定していることが前提になります。
>? VS関連のQT開発環境の設定手順に詳しくない場合は、[README](https://github.com/tencentyun/TRTCSDK/blob/master/Windows/QTDemo/README.md)の操作手順のステップ4の関連内容をご参照ください。

### 操作手順
このセグメントでは、簡単なQTプロジェクトを作成し、Visual Studioプログラムの中でC++ SDKを統合する方法を紹介します。

#### ステップ1： SDKのダウンロード
1. [SDKのダウンロード](https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_TRTC_Win_latest.zip)を行い、解凍して開きます。
ここの例では、 SDKディレクトリのC++バージョンのSDKファイルをインポートしさえすればOKです。64ビットの場合、SDKは`./SDK/CPlusPlus/Win64/`にあり、主に次のいくつかの部分が含まれます。
<table>
<thead>
<tr>
<th>ディレクトリ名</th>
<th>説明</th>
</tr>
</thead>
<tbody><tr>
<td>include</td>
<td>詳細なインターフェースの説明がついたAPIヘッダーファイル</td>
</tr>
<tr>
<td>lib</td>
<td>編集用の.libファイルおよび実行時にローディングする.dllファイル</td>
</tr>
</tbody></table>

#### ステップ2：プロジェクトの新規作成[](id:using_cpp_qt_step2)
Visual Studio 2015を例にとると、ローカルですでに[QT](https://download.qt.io/archive/qt/5.9/5.9.1/qt-opensource-windows-x86-5.9.1.exe)および[VS開発プラグイン](https://download.qt.io/archive/vsaddin/2.6.0/qt-vsaddin-msvc2015-2.6.0.vsix)をインストール済みという前提で、Visual Studioを開きます。下図のように、`TRTCDemo`という名前のQTアプリケーションを新規作成します。
![](https://qcloudimg.tencent-cloud.cn/raw/fa665d6c78420db0da022ae81f2d7c68.png)
クイックインテグレーションの方法を説明しやすくするため、ガイドの中で**Qt Widgets Application**タイプを選択し、**OK**をクリックします。次のページで**Next**をクリックし、プロジェクトを作成すれば完了です。

#### ステップ3：ファイルのコピー[](id:using_cpp_qt_step3)
下図のように、解凍後のSDKフォルダをTRTCDemo.vcxprojが存在するディレクトリ下にコピーします。
>? この時点ではC++ SDKだけが必要なため、 SDKパスのCSharpディレクトリを削除しても構いません。

![](https://qcloudimg.tencent-cloud.cn/raw/49681d526061bdef063e878879d471a8.png)

#### ステップ4：プロジェクト設定の修正[](id:using_cpp_qt_step4)
TRTCDemoの属性のページを開きます。**ソリューションのResource Manager** >**TRTCDemoプログラムの右クリックメニュー**>**属性**と進みます。次のステップにしたがって設定してください。
1. **Includeのディレクトリの追加：**
下図のように、**C/C++** > **通常** > **Includeディレクトリの追加**で、64ビットの場合は、SDKヘッダーファイルディレクトリ`$(ProjectDir)SDK\CPlusPlus\Win64\include`と`$(ProjectDir)SDK\CPlusPlus\Win64\include\TRTC`を追加します。
>?32ビットの場合は、SDKヘッダーファイルディレクトリを`$(ProjectDir)SDK\CPlusPlus\Win32\include`と`$(ProjectDir)SDK\CPlusPlus\Win32\include\TRTC`に設定する必要があります。

![](https://qcloudimg.tencent-cloud.cn/raw/61a49b758ecb52ab6ee576421da5800d.png)
2. **ライブラリのディレクトリの追加：**
下図のように、**リンカー**>**通常**>**ライブラリディレクトリの追加**で、64ビットの場合は、SDKライブラリディレクトリ `$(ProjectDir)SDK\CPlusPlus\Win64\lib`を追加します。
>?32ビットの場合は、SDKライブラリディレクトリを`$(ProjectDir)SDK\CPlusPlus\Win32\lib`に設定する必要があります。

![](https://qcloudimg.tencent-cloud.cn/raw/89b465c893f456edacf3355dc59f0258.png)
3. **ライブラリファイルの追加：**
下図のように、**リンカー**>**入力**>**依存プロジェクトの追加**で、 SDKライブラリファイル`liteav.lib`を追加します。
![](https://qcloudimg.tencent-cloud.cn/raw/7eb6bbe2351dc4cd3e6c7ae817042fae.png)
4. **copyコマンドの追加：**
下図のように、**イベントの生成**>**後続のイベントの生成**>**コマンドライン**で、コピーコマンド`copy /Y $(ProjectDir)SDK\CPlusPlus\Win64\lib\*.dll  $(OutDir)`を追加します。編集が完了すると、自動で SDKの.dll ファイルがプログラムの実行ディレクトリの下にコピーされます。
>?32ビットの場合は、追加するコピーコマンドは`copy /Y $(ProjectDir)SDK\CPlusPlus\Win32\lib\*.dll  $(OutDir)`となります。

![](https://qcloudimg.tencent-cloud.cn/raw/c6cb6d0dfd935be7a74313881a306c5f.png)

#### ステップ5： SDKバージョン番号の印刷[](id:using_cpp_qt_step5)
1. `TRTCDemo.cpp`ファイルのトップにヘッダーファイルをインポートして追加します。コードは次のとおりです。
``` c++
#include "ITRTCCloud.h"
#include <QLabel>
```
2. `TRTCDemo.cpp`ファイルの`TRTCDemo::TRTCDemo`コンストラクタの中に、以下のテストコードを追加します。
```C++
ITRTCCloud * pTRTCCloud = getTRTCShareInstance();
std::string version(pTRTCCloud->getSDKVersion());

QString sdk_version = QString("SDK Version: %1").arg(version.c_str());
QLabel* label_text = new QLabel(this);
label_text->setAlignment(Qt::AlignCenter);
label_text->resize(this->width(), this->height());
label_text->setText(sdk_version);
```
3. F5を押下して動作させ、下図のとおり、SKDのバージョン番号を印刷します。  
![](https://qcloudimg.tencent-cloud.cn/raw/bc1ddf818e5f0571c72d34ba212691c7.png)



## Mac端末統合
### 開発環境要件

- オペレーティングシステム：Mac10.10以上のバージョン。
- 開発環境：Qt Creator 4.10.3以上のバージョン。Qt Creator 4.13.3以上のバージョンの使用を推奨。
- 開発フレームワーク：Based on Qt 5.10以上。

### 操作手順
ここでは簡単なQTTest項目の作成を例に、Qｔ CreatorプロジェクトでC++クロスプラットフォームSDKを統合する方法をご紹介します。

[](id:mac_step1)
1. **C++クロスプラットフォームSDKのダウンロード**
	1. [SDK](https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_TRTC_Mac_latest.tar.bz2)をダウンロードし、ファイルを解凍して開きます。
	2. QTTestと同じクラスのディレクトリ下で空のSDKフォルダを作成し、SDK内の`TXLiteAVSDKTRTCMacx.x.x/SDK/TXLiteAVSDKTRTC_Mac.framework` を、QTTestプロジェクトディレクトリと同じクラスのディレクトリにあるSDKフォルダにコピーします。
2. **QTTest.proの設定**[](id:mac_step2)
QTTest プロジェクトディレクトリを開き、任意のテキストエディタを使用して `QTTest.pro` ファイルを開いてから、SDK関連の引用を追加します。
```MAC
INCLUDEPATH += $$PWD/.
DEPENDPATH += $$PWD/.

LIBS += "-F$$PWD/base/util/mac/usersig"
LIBS += "-F$$PWD/../SDK"
LIBS += -framework TXLiteAVSDK_TRTC_Mac
LIBS += -framework Accelerate
LIBS += -framework AudioUnit

INCLUDEPATH += $$PWD/../SDK/TXLiteAVSDK_TRTC_Mac.framework/Headers/cpp_interface

INCLUDEPATH += $$PWD/base/util/mac/usersig/include
DEPENDPATH += $$PWD/base/util/mac/usersig/include
```
3. **カメラおよびマイクの使用権限の承認**[](id:mac_step3)
SDKではカメラおよびマイクを使用しますので、対応する `Info.plist` に該当する権限申請説明を追加する必要があります。
```none
NSMicrophoneUsageDescription：マイクの使用申請
NSCameraUsageDescription：カメラの使用申請
```
下図に示すとおり：
![](https://qcloudimg.tencent-cloud.cn/raw/dc42db42bf51f14a8e22326edc3f0a16.png)

4. **TRTC SDKの引用**[](id:mac_step4)
	- ヘッダーファイル `#include "ITRTCCloud.h"` によって直接引用することができます。
	- ネームスペースの利用：C++のすべてのプラットフォームのインターフェースのメソッド、タイプなどはいずれもtrtcネームスペースで定義されています。コードをより簡潔にするため、trtcネームスペースを直接使用することをお勧めします。

>? ここまでで統合作業はすでに完了していますので、プロジェクトをコンパイルして実行できます。 Demoを使用するためのクロスプラットフォームSDKのAPIの詳細については、[QTDemo](https://github.com/tencentyun/TRTCSDK/tree/master/Mac)をダウンロードしてご参照ください。

## よくあるご質問
- 次のエラーが生じた場合は、前述のプログラム設定にしたがって、SDKヘッダーファイルのディレクトリが正しく追加されているかチェックしてください。
```
fatal error C1083: includeファイルを開くことができません: “TRTCCloud.h”: No such file or directory
```

- 次のエラーが生じた場合は、前述のプログラム設定にしたがって、SDKディレクトリとライブラリファイルが正しく追加されているかチェックしてください。
```
error LNK2019: 解析できない外部シンボル "__declspec(dllimport) public: static class TXString __cdecl TRTCCloud::getSDKVersion(void)" (__imp_?getSDKVersion@TRTCCloud@@SA?AVTXString@@XZ)、この記号が関数 "protected: virtual int __thiscall CTRTCDemoDlg::OnInitDialog(void)" (?OnInitDialog@CTRTCDemoDlg@@MAEHXZ) の中に引用されています
```
