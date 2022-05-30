このドキュメントでは、主にTencent Cloud TRTC SDK（QTのWindowsバージョンおよびMacバージョン）をプロジェクトに素早く統合する方法をご紹介します。以下の手順に従って設定すれば、SDKの統合作業を素早く完了できます。

## Windows端末の統合
### 開発環境要件
- OS：Windows 7以降のバージョン。
- 開発環境：Visual Studio 2015以降のバージョンが必要です。VS関連のQT開発環境をすでに設定している前提で、Visual Studio 2015の使用をお勧めします。
>? VS関連のQT開発環境の設定手順に詳しくない場合は、[README](https://github.com/tencentyun/TRTCSDK/blob/master/Windows/QTDemo/README.md)の手順4に関連する内容をご参照ください。

### 操作手順
このセグメントでは、簡単なQTTestプロジェクトの新規作成を例に、Visual StudioプロジェクトでC++クロスプラットフォームSDKを統合する方法をご紹介します。

1. **C++ クロスプラットフォームSDKのダウンロード**[](id:win_step1)
	1. [SDK](https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_TRTC_Win_latest.zip)をダウンロードして、解凍して開きます。
	2. QTTestと同じクラスのディレクトリ下で空のSDKフォルダを作成し、SDKの中の`TXLiteAVSDKTRTCWin_latest/SDK/CPlusPlus`を、QTTestプロジェクトディレクトリと同じクラスのディレクトリにあるSDKフォルダにコピーします。
2. **QTTestプロジェクト依存環境の設定**[](id:win_step2)
<dx-tabs>
::: シーン1：QtCreatorを使用した依存環境の設定
QTTestプロジェクトディレクトリを開き、任意のテキストエディタ（[Sublime Text](http://www.sublimetext.com/3)を推奨）を使用して`QTTest.pro`（Qt Creatorを使用して作成）ファイルを開いてから、SDKに関連する引用を追加します。
<dx-codeblock>
::: Windows
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
	}else{
		LIBS += -L$$PWD/../SDK/CPlusPlus/Win64/lib -lliteav
	}
}

release {
	contains(QT_ARCH,i386) {
		LIBS += -L$$PWD/../SDK/CPlusPlus/Win32/lib -lliteav
	}else{
		LIBS += -L$$PWD/../SDK/CPlusPlus/Win64/lib -lliteav
	}
}
:::
</dx-codeblock>
:::
::: シーン2：VSを使用した依存環境の設定
既に本格的なプロジェクトになっている場合：
1．VSの中のプロジェクトプロパティから**リンカ** > **入力** > **依存項目の追加**からSDKライブラリファイル`liteav.lib`を追加できます。
2．**リンカ** > **常規** > **ライブラリディレクトリの追加**からSDKライブラリパスを設定します。64bitの場合：`$(ProjectDir)SDK\CPlusPlus\Win64\lib`。
3. 同時に、**C/C++** > **常規** > **添付ファイル付きディレクトリ**から、SDKのヘッダファイルパス`$(ProjectDir)SDK\CPlusPlus\Win64\include` と `$(ProjectDir)SDK\CPlusPlus\Win64\include\TRTC`を設定します。

<dx-alert infotype="explain">32bitの場合、パスの中のWin64をWin32に変更してください。</dx-alert>
:::
</dx-tabs>

3. **ファイルのコピー**[](id:win_step3)
	- QtCreatorで`QTTest.pro`プロジェクトを開き、プログラムをデバッグする場合、関連する`debug/release`フォルダが自動的に生成されます。`SDK/CPlusPlus/Win64/lib`（32bitの場合、`SDK/CPlusPlus/Win32/lib`）下のすべての`.dll`ファイルをそれぞれプロジェクトディレクトリ下の`debug/release`フォルダにコピーする必要があります。
	- VSを使用してデバッグを行う際、手動で`SDK/CPlusPlus/Win64/lib`下のすべての`.dll`ファイルをプログラムの出力実行ディレクトリ下にコピーします。あるいは、**イベントの生成** > **後続イベントの生成** > **コマンドライン**にて、コピーコマンド`copy /Y "$(ProjectDir)LiteAVSDK\lib\\\*.dll$(OutDir)`を追加することもできます。コンパイルが完了するとSDKのdllファイルがプログラムの実行ディレクトリ下に自動的にコピーされます。
>?32bitの場合、コピーコマンド`copy /Y $(ProjectDir)SDK\CPlusPlus\Win32\lib\*.dll $(OutDir)`を追加します。
4. **TRTC SDKの引用**[](id:win_step4)
	- ヘッダーファイル`#include "ITRTCCloud.h"`によって直接引用することができます。
	- ネームスペースの利用：C++の全プラットフォームインターフェースのメソッド、タイプなどはいずれもtrtcネームスペースで定義されています。コードをより簡潔にするために、trtcネームスペースを直接使用することをお勧めします。

>? ここまで統合作業はすでに完了していますので、プロジェクトをコンパイルして実行できます。Demoを使用するためのクロスプラットフォームSDKのAPIの詳細については、[QTDemo](https://github.com/tencentyun/TRTCSDK/tree/master/Windows)をダウンロードして詳細をご参照ください。

## Mac端末統合
### 開発環境要件

- OS：Mac10.10以降のバージョン。
- 開発環境：Qt Creator 4.10.3以降のバージョンが必要です。Qt Creator 4.13.3以降のバージョンの使用を推奨します。
- 開発フレームワーク：Based on Qt 5.10以降。

### 操作手順
このセグメントではゼロからの簡単なQTTest項目の作成を例に、Qｔ CreatorプロジェクトでC++クロスプラットフォームSDKを統合する方法をご紹介します。

[](id:mac_step1)
1. **C++クロスプラットフォームSDKのダウンロード**
	1. [SDK](https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_TRTC_Mac_latest.tar.bz2)をダウンロードして、解凍して開きます。
	2. QTTestと同じクラスのディレクトリ下で空のSDKフォルダを作成し、SDKの中の`TXLiteAVSDKTRTCMacx.x.x/SDK/TXLiteAVSDKTRTC_Mac.framework`を、QTTestプロジェクトディレクトリと同じクラスのディレクトリにあるSDKフォルダにコピーします。
2. **QTTest.proの構成**[](id:mac_step2)
QTTestプロジェクトディレクトリを開き、任意のテキストエディタを使用して`QTTest.pro`ファイルを開いてから、SDK関連の引用を追加します。
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

3. **カメラとマイクの使用権限の許可**[](id:mac_step3)
SDKではカメラおよびマイクを使用しますので、対応する`Info.plist`に該当する権限申請説明を追加する必要があります。
```none
NSMicrophoneUsageDescription：マイクの使用申請
NSCameraUsageDescription：カメラの使用申請
```
以下の図の通りです。
![](https://qcloudimg.tencent-cloud.cn/raw/dc42db42bf51f14a8e22326edc3f0a16.png)
4. **TRTC SDKの引用**[](id:mac_step4)
	- ヘッダーファイル`#include "ITRTCCloud.h"`によって直接引用することができます。
	- ネームスペースの利用：C++の全プラットフォームインターフェースのメソッド、タイプなどはいずれもtrtcネームスペースで定義されています。コードをより簡潔にするために、trtcネームスペースを直接使用することをお勧めします。

>? ここまで統合作業はすでに完了していますので、プロジェクトをコンパイルして実行できます。Demoを使用するためのクロスプラットフォームSDKのAPIの詳細については、[QTDemo](https://github.com/tencentyun/TRTCSDK/tree/master/Mac)をダウンロードして詳細をご参照ください。
