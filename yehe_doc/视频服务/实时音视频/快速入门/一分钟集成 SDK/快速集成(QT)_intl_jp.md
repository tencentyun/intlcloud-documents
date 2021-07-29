ここでは、主にTencent Cloud TRTC SDK(QTのMacバージョンおよびWindowsバージョン) をプロジェクトに素早く統合する方法を紹介します。以下の手順に従って設定すれば、SDKの統合作業を素早く完了できます。

## Mac端末統合
### 開発環境要件

- オペレーティングシステム：Mac10.10以上のバージョン。
- 開発環境：Qt Creator 4.10.3以上のバージョン。Qt Creator 4.13.3以上のバージョンの使用を推奨。
- 開発フレームワーク：Based on Qt 5.10以上。

### 操作手順
ここではゼロからの簡単なQTTest項目の作成を例に、Qｔ CreatorプロジェクトでC++クロスプラットフォームSDKを統合する方法をご紹介します。

[](id:mac_step1)
### 手順1： C++クロスプラットフォームSDKのダウンロード
1. [SDK](https://liteavsdk-1252463788.cosgz.myqcloud.com/TXLiteAVSDK_TRTC_Mac_latest.tar.bz2)をダウンロードし、ファイルを解凍して開きます。
2. QTTestと同じクラスのディレクトリ下で空のSDKフォルダを作成し、手順1でダウンロードした`TXLiteAVSDKTRTCMacx.x.x/SDK/TXLiteAVSDKTRTC_Mac.framework` を、QTTest プロジェクトディレクトリと同じクラスのディレクトリにあるSDKフォルダにコピーします。

[](id:mac_step2)
#### 手順2：QTTest.proの設定
QTTest プロジェクトディレクトリを開き、任意のテキストエディタを使用して `QTTest.pro` ファイルを開いてから、SDK関連の引用を追加します。

```
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

[](id:mac_step3)
#### 手順3：カメラおよびマイクの使用権限の付与

SDKではカメラおよびマイクを使用しますので、対応する `Info.plist` に該当する権限申請説明を追加する必要があります。
```none
NSMicrophoneUsageDescription：マイクの使用申請
NSCameraUsageDescription：カメラの使用申請
```
下図に示すとおり：

[](id:mac_step4)
#### 手順4：TRTC SDKの引用
1.ヘッダーファイル `#include "ITRTCCloud.h"` によって直接引用することができます。
2. ネームスペースの利用：C++ のすべてのプラットフォームのインターフェースのメソッド、タイプなどはいずれも trtc ネームスペースで定義されています。コードをより簡潔にするため、trtc ネームスペースを直接使用することをお勧めします。

>? ここまでで統合作業はすでに完了していますので、プロジェクトをコンパイルして実行できます。 Demoを使用するためのクロスプラットフォームSDKのAPIの詳細については、[QTDemo](https://github.com/tencentyun/TRTCSDK/tree/master/Mac) をダウンロードして詳細をご参照ください。

## Windows端末の統合
### 開発環境要件
- OS：Windows 7以上のバージョン。
- 開発環境：Visual Studio 2015以上のバージョン、Visual Studio 2015の使用をお薦めします。VS関連のQT開発環境をすでに設定していることが前提になります。
>? VS 関連のQT開発環境の設定手順に詳しくない場合は、 [README](https://github.com/tencentyun/TRTCSDK/blob/master/Windows/QTDemo/README.md) の第2条の内容をご参照ください。

### 操作手順
ここでは、簡単なQTTestプロジェクトの新規作成を例に、 Visual StudioプロジェクトでC++クロスプラットフォームSDKを統合する方法をご紹介します。

[](id:win_step1)
### 手順1： C++クロスプラットフォームSDKのダウンロード
1. [SDK](https://liteavsdk-1252463788.cosgz.myqcloud.com/TXLiteAVSDK_TRTC_Win_latest.zip)をダウンロードし、ファイルを解凍して開きます。
2. QTTestと同じクラスのディレクトリ下で空のSDKフォルダを作成し、手順1でダウンロードした`TXLiteAVSDKTRTCWin_latest/SDK/CPlusPlus`を、QTTest プロジェクトディレクトリと同じクラスのディレクトリにあるSDKフォルダにコピーします。

[](id:win_step2)
#### 手順2：QTTestプロジェクトリクエスト環境の設定
##### シーン1：QtCreatorを使用したリクエスト環境の設定
QTTestプロジェクトディレクトリを開き、任意のテキストエディタ（[Sublime Text](http://www.sublimetext.com/3)を推奨）を使用して `QTTest.pro`（Qt Creatorを使用して作成）ファイルを開いてから、SDKに関連する引用を追加します。
```
INCLUDEPATH += $$PWD/.
               $$PWD/../SDK/CPlusPlus/Win32/include \
               $$PWD/../SDK/CPlusPlus/Win32/include/TRTC

DEPENDPATH += $$PWD/.
               $$PWD/../SDK/CPlusPlus/Win32/include \
               $$PWD/../SDK/CPlusPlus/Win32/include/TRTC

CONFIG += opengl
CONFIG += debug_and_release

debug {
	contains(QT_ARCH,i386) {
		LIBS += -L$$PWD/../SDK/CPlusPlus/Win32/lib -lliteav
	} else {
		LIBS += -L$$PWD/../SDK/CPlusPlus/Win64/lib -lliteav
	}
}

release {
	contains(QT_ARCH,i386) {
		LIBS += -L$$PWD/../SDK/CPlusPlus/Win32/lib -lliteav
	} else {
		LIBS += -L$$PWD/../SDK/CPlusPlus/Win64/lib -lliteav
	}
}
```
##### シーン2：VSを使用したリクエスト環境の設定
プロジェクトがすでに本格的なVSプロジェクトになっている場合は、VSのプロジェクト属性 `Properties->Linker->Input およびGeneral` でSDKライブラリパスのリクエスト情報を設定し、同時に `Properties -> C/C++ -> General` でSDK のヘッダーファイルパスのリクエスト情報を設定します。

[](id:win_step3)
#### 手順3：ファイルのコピー
VSを使用して`QTTest.pro`プロジェクトを開き、関連する `debug/release`フォルダを自動的に生成してから、`SDK/CPlusPlus/Win32/lib` 下のすべての`.dll`ファイルをプロジェクトディレクトリ下の `debug/release` フォルダにそれぞれコピーする必要があります。

[](id:win_step4)
#### 手順4：TRTC SDKの引用
1.ヘッダーファイル `#include "ITRTCCloud.h"` によって直接引用することができます。
2. ネームスペースの利用：C++ のすべてのプラットフォームのインターフェースのメソッド、タイプなどはいずれも trtc ネームスペースで定義されています。コードをより簡潔にするため、trtc ネームスペースを直接使用することをお勧めします。

>? ここまでで統合作業はすでに完了していますので、プロジェクトをコンパイルして実行できます。 Demoを使用するためのクロスプラットフォームSDKのAPIの詳細については、[QTDemo](https://github.com/tencentyun/TRTCSDK/tree/master/Windows) をダウンロードして詳細をご参照ください。
