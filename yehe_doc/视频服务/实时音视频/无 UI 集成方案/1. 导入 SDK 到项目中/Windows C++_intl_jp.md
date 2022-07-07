このドキュメントでは、Tencent Cloud TRTC SDK（Windows C++ 版）をMFCプロジェクトに素早く統合する方法を紹介します。

![](https://qcloudimg.tencent-cloud.cn/raw/956dded61564c3a29ea8e93238d9a4e1.png)

## 開発環境要件

- OS：Windows 7以上のバージョン。
- 開発環境：Visual Studio 2010およびそれ以上のバージョン、Visual Studio 2015の使用を推奨します。

[](id:using_cpp)
### MFCプロジェクトによるC++ SDKの統合
このセグメントでは、簡単なMFC プロジェクトを作成し、Visual Studio プログラムの中で C++ SDKを統合する方法を紹介します。

### 手順1：SDKのダウンロード[](id:using_cpp_step1)
[SDKダウンロード](https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_TRTC_Win_latest.zip)し、解凍して開きます。この例では、SDKディレクトリ下のC++バージョンのSDKファイルを参照するだけで済みます。64ビットを例にとると、SDKの場所は`./SDK/CPlusPlus/Win64/`です。これには主に次の部分が含まれます：
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

### 手順2：プロジェクトの新規作成[](id:using_cpp_step2)
Visual Studioを開き、TRTCDemoという名前のMFC アプリケーションプログラムを作成します。
迅速に統合する方法を紹介しやすいように、ガイドの**アプリケーションプログラムのタイプ**の画面では、比較的簡単な**ダイアログベース**のタイプを選択しています。
その他のガイドの設定は、デフォルトの設定を選択してください。

### 手順3：**ファイルのコピー[](id:using_cpp_step3)
解凍後のSDKフォルダを`TRTCDemo.vcxproj`が存在するディレクトリ下にコピーします。下図のとおりです：
>?現在はC++ SDKがあれば、SDKパス下のCsharpディレクトリを削除できます。

![](https://qcloudimg.tencent-cloud.cn/raw/49681d526061bdef063e878879d471a8.png)

### 手順4：プロジェクト構成の変更[](id:using_cpp_step4)
TRTCDemoの属性ページを開きます。**ソリューションのResource Manager** >**TRTCDemoプロジェクトのメニュー**>**属性**を右クリックして、次の手順にしたがって設定してください：
1.  **Includeのディレクトリの追加：**
**C/C++** > **常規** > **添付ファイル付きディレクトリ**から、以下のSDKヘッダファイルディレクトリを追加します。なお、64bitの例： `$(ProjectDir)SDK\CPlusPlus\Win64\include` 和 `$(ProjectDir)SDK\CPlusPlus\Win64\include\TRTC`、下図のとおりです：
>?32bitの場合、SDKヘッダファイルディレクトリを`$(ProjectDir)SDK\CPlusPlus\Win32\include` と `$(ProjectDir)SDK\CPlusPlus\Win32\include\TRTC`として設定してください。

![](https://qcloudimg.tencent-cloud.cn/raw/61a49b758ecb52ab6ee576421da5800d.png)
2. **ライブラリのディレクトリの追加：**
**リンカ** > **常規** > **添付ライブラリ付きディレクトリ**から、以下のSDKヘッダファイルディレクトリを追加します。なお、64bitの例： `$(ProjectDir)SDK\CPlusPlus\Win64\lib`、下図のとおりです：
>?32bitの場合、SDKライブラリディレクトリを`$(ProjectDir)SDK\CPlusPlus\Win32\lib`として設定してください。

![](https://qcloudimg.tencent-cloud.cn/raw/89b465c893f456edacf3355dc59f0258.png)
3. **ライブラリファイルの追加：**
**リンカ** > **入力** > **依存項目の追加**からSDKライブラリファイル`liteav.lib`を追加します。下図のとおりです：
![](https://qcloudimg.tencent-cloud.cn/raw/7eb6bbe2351dc4cd3e6c7ae817042fae.png)
4. **copy コマンドの追加：**
**イベントの生成** > **後続イベントの生成** > **コマンドライン**から、コピーコマンド`copy /Y $(ProjectDir)SDK\CPlusPlus\Win64\lib\*.dll  $(OutDir)`を追加します。コンパイルが完了すると、自動的にSDKの.dllファイルがプログラムの実行ディレクトリの下にコピーされます。下図のとおりです。
>?32bitの場合、コピーコマンド`copy /Y $(ProjectDir)SDK\CPlusPlus\Win32\lib\*.dll $(OutDir)`を追加します。

![](https://qcloudimg.tencent-cloud.cn/raw/c6cb6d0dfd935be7a74313881a306c5f.png)

### 手順5： SDKバージョン番号のプリント[](id:using_cpp_step5)
1. TRTCDemoDlg.cppファイルのヘッドにヘッダファイルを追加してください。コードは以下のとおりです：
``` c++
#include "ITRTCCloud.h"
```
2. `CTRTCDemoDlg::OnInitDialog`関数の中に、以下のテストコードを追加します：
```c++
ITRTCCloud * pTRTCCloud = getTRTCShareInstance();
CString szText;
szText.Format(L"SDK version: %hs", pTRTCCloud->getSDKVersion());

CWnd *pStatic = GetDlgItem(IDC_STATIC);
pStatic->SetWindowTextW(szText);
```
3. F5キーを押して実行すると、SDKのバージョン番号がプリントされます。下図のとおりです：  
![](https://qcloudimg.tencent-cloud.cn/raw/bc1ddf818e5f0571c72d34ba212691c7.png)


## よくあるご質問
- 次のエラーが生じた場合は、前述のプログラム設定にしたがって、 SDKヘッダーファイルのディレクトリが正しく追加されているかチェックしてください。
```
fatal error C1083: include ファイルを開くことができません: “TRTCCloud.h”: No such file or directory
```

- 次のエラーが生じた場合は、前述のプログラム設定にしたがって、SDKライブラリのディレクトリとライブラリファイルが正しく追加されているかチェックしてください。
```
error LNK2019: 解析できない外部シンボル "__declspec(dllimport) public: static class TXString __cdecl TRTCCloud::getSDKVersion(void)" (__imp_?getSDKVersion@TRTCCloud@@SA?AVTXString@@XZ)、この記号が関数 "protected: virtual int __thiscall CTRTCDemoDlg::OnInitDialog(void)" (?OnInitDialog@CTRTCDemoDlg@@MAEHXZ) の中に引用されています
```
