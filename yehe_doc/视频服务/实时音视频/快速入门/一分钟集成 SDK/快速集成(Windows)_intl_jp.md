このドキュメントでは、Tencent Cloud TRTC SDK（Windows C#およびC++ 版をプロジェクトに迅速に統合する方法を紹介します。

## 開発環境要件

- OS：Windows 7およびそれ以上のバージョン。
- 開発環境：Visual Studio 2010およびそれ以上のバージョン、Visual Studio 2015の使用を推奨します。
- 開発アーキテクチャ：.Net Framework 4.0およびそれ以上のバージョン。

## TRTC C# SDKの統合

このセグメントでは、例として簡単な Winformのプロジェクトを作成し、Visual Studioのプログラムの中でC# SDKを統合する方法を紹介します。

[](id:step1)
### ステップ1： Windows SDKのダウンロード  
[SDKをダウンロード ](https://liteavsdk-1252463788.cosgz.myqcloud.com/TXLiteAVSDK_TRTC_Win_latest.zip)し、ファイルを解凍して開きます。これには次の部分が含まれています。

| ディレクトリ名  | 説明                                   |
| ------- | -------------------------------------- |
| xxxDemo | C++ Demo ソースコードおよびC# Demo ソースコード |
| CPlusPlus | C++版32ビット/64ビットの依存する SDK ライブラリファイル |
| CSharp | C#版32ビット/64ビットの依存するSDK ライブラリファイル |

ここの例では、SDK ディレクトリの下のC# 版のSDK ファイルを引用するだけで済みます。

[](id:step2)
### ステップ2：プログラムの新規作成
Visual Studioを開き、`TRTCCSharpDemo`という名前の Winform アプリケーションプログラムを新規作成します。

[](id:step3)
### ステップ3：ファイルのコピー
解凍後のSDK ファイルフォルダを `TRTCCSharpDemo.csproj`が存在するディレクトリにコピーします。
>?C# SDKのみが必要な場合は、SDKのパスの下の CPlusPlus ディレクトリを削除して構いません。



[](id:step4)
### ステップ4：プログラム設定の修正
#### ステップ4.1：追加および引用
1. Visual Studio の【生成】ディレクトリの下から【Configuration Manager】を見つけて開きます。[](id:step4_1_2)
2. 【イベントソリューションプラットフォーム】のプルダウン・リストから【新規作成】を選択すると、【ソリューションプラットフォームの新規作成】のダイアログボックスがポップアップします。[](id:step4_1_3)
3. 新しいプラットフォームを入力または選択し、【確定】をクリックします。

4. 実際のニーズにもとづき、[ステップ2](#step4_1_2) - [ステップ3](#step4_1_3)を繰り返して、サポートする必要があるソリューションプラットフォームを新規作成します。

5. TRTCCSharpDemo プロジェクトが存在するファイルフォルダを開き、テキストエディタを使って`TRTCCSharpDemo.csproj`ファイルを編集します。
6. `TRTCCSharpDemo.csproj`のファイルの中のタグ `<itemGroup>`の下に次の内容を追加します。
```
  //それぞれのプラットフォームの下に引用を追加します
  <Reference Include="ManageLiteAV" Condition="'$(Platform)' == 'x64'">
		<HintPath>SDK\CSharp\Win64\lib\ManageLiteAV.dll</HintPath>
  </Reference>
  <Reference Include="ManageLiteAV" Condition="'$(Platform)' == 'AnyCPU'">
		<HintPath>SDK\CSharp\Win64\lib\ManageLiteAV.dll</HintPath>
  </Reference>
  <Reference Include="ManageLiteAV" Condition="'$(Platform)' == 'x86'">
		<HintPath>SDK\CSharp\Win32\lib\ManageLiteAV.dll</HintPath>
  </Reference>
```


#### ステップ4.2：copy コマンドの追加
1. TRTCCSharpDemoの属性のページを開きます。【ソリューションのResource Manager】>【TRTCCSharpDemo プログラムの右クリックメニュー】>【属性】を選択します。
2. 【イベントの生成】>【後続のイベント生成コマンドライン】の中に次のコマンドを追加し、編集完了後に、様々なプラットフォーム下の SDKの .dll ファイルが自動的にプログラムの実行ディレクトリの下にコピーされるようにします。次の図のとおりです。
```
set Platform=Win64
SETLOCAL ENABLEDELAYEDEXPANSION
if $(PlatformName)==x86 ( 
  set Platform=Win32
)
copy /Y "$(ProjectDir)SDK\CSharp\!Platform!\lib\*.dll" "$(ProjectDir)$(OutDir)"
ENDLOCAL
```


#### ステップ4.3：デバッグ環境の修正
TRTCDemoの属性のページを開き、【生成】を選択して、【プラットフォーム(M)】とトップメニューバーの中のソリューションプラットフォームの設定を一致させます。次の図のとおりです。


[](id:step5)
### ステップ5： SDK バージョンナンバーのプリント
1. Form1.csの設計ツールの中にlabelコントロールを追加します。次の図のとおりです。
2. Form1.csのコードファイルを開き、次のコードを追加します。
```c#
	using System.Windows.Forms;
	using ManageLiteAV;   // 1..ネームスペースの引用を追加します

	namespace TRTCCSharpDemo
	{
			public partial class Form1 : Form
			{
					public Form1()
					{
							InitializeComponent();
							// 2.ITRTCCloud インスタンスを取得し、SDK バージョンナンバーをプリントします
							ITRTCCloud lTRTCCloud = ITRTCCloud.getTRTCShareInstance(); 
							this.label1.Text = "SDK version : " + lTRTCCloud.getSDKVersion();
							// 3.使用終了時に、ITRTCCloud インスタンスを手動で破棄する必要があります
							ITRTCCloud.destroyTRTCShareInstance();
					}
			}
	}
```
3.  F5を押して実行し、SDKのバージョンナンバーをプリントします。次の図のとおりです。
 ![](https://main.qcloudimg.com/raw/9bfebaac4fa339af6b7c74b0413cde1d.png)


[](id:using_cpp)
## TRTC C++ SDKの統合

このセグメントでは、簡単なMFC プロジェクトを作成し、Visual Studio プログラムの中で C++ SDKを統合する方法を紹介します。

[](id:using_cpp_step1)
### ステップ1： SDKのダウンロード
[SDKをダウンロード](https://liteavsdk-1252463788.cosgz.myqcloud.com/TXLiteAVSDK_TRTC_Win_latest.zip)し、解凍して開きます。これには次の部分が含まれています。

| ディレクトリ名  | 説明                                   |
| ------- | -------------------------------------- |
| include | 詳細なインターフェースの説明がついたAPI ヘッダーファイル          |
| lib     | 編集用の.lib ファイルおよび実行時にローディングする.dll ファイル |


[](id:using_cpp_step2)
### ステップ2： プログラムの新規作成
Visual Studioを開き、TRTCDemoという名前のMFC アプリケーションプログラムを作成します。次の図のとおりです。


迅速に統合する方法を紹介しやすいように、ガイドの**アプリケーションプログラムのタイプ**の画面では、比較的簡単な**ダイアログベース**のタイプを選択しています。次の図のとおりです。


その他のガイドの設定は、デフォルトの設定を選択してください。


[](id:using_cpp_step3)
### ステップ3：ファイルのコピー
解凍後のLiteAVSDK ファイルフォルダを TRTCDemo.vcxprojが存在するディレクトリの下にコピーします。次の図のとおりです。



[](id:using_cpp_step4)
### ステップ4：プログラム設定の修正
TRTCDemoの属性のページを開きます。【ソリューションのResource Manager】 >【TRTCDemo プログラムの右クリックメニュー】>【属性】と進みます。次のステップにしたがって設定してください。

1.  **Includeのディレクトリの追加：**
【C/C++】>【Genaral】>【Include ディレクトリの追加】で、SDK ヘッダーファイルディレクトリ `$(ProjectDir)LiteAVSDK\include` と `$(ProjectDir)LiteAVSDK\include\TRTC`を追加します。次の図のとおりです。

2. **ライブラリのディレクトリの追加：**
【リンケージ】>【通常】>【ライブラリディレクトリの追加】で、SDKライブラリディレクトリ `$(ProjectDir)LiteAVSDK\lib`を追加します。次の図のとおりです。

3. **ライブラリファイルの追加：**
【リンケージ】>【入力】>【依存項目の追加】で、 SDK ライブラリファイル `liteav.lib`を追加します。次の図のとおりです。

4. **copy コマンドの追加：**
【イベントの生成】>【後続のイベントの生成】>【コマンドライン】で、コマンド `copy /Y "$(ProjectDir)LiteAVSDK\lib\\\*.dll" "\$(OutDir)"`のコピーを追加します。編集が完了すると、自動で SDKの.dll ファイルがプログラムの実行ディレクトリの下にコピーされます。次の図のとおりです。



[](id:using_cpp_step5)
### ステップ5：SDK バージョンナンバーのプリント
- `CTRTCDemoDlg::OnInitDialog`関数の中に、以下のテストコードを追加します。
<dx-codeblock>
:::  c++  c++
ITRTCCloud * pTRTCCloud = getTRTCShareInstance();
std::string version(pTRTCCloud->getSDKVersion());
CString szText;
szText.Format(L"SDK version: %hs", version.c_str());

CWnd *pStatic = GetDlgItem(IDC_STATIC);
pStatic->SetWindowTextW(szText);
:::
</dx-codeblock>
- F5キーを押して実行すると、SDKのバージョンナンバーがプリントされます。次の図のとおりです。  
![](https://main.qcloudimg.com/raw/6851ab7f24d95ae8115fdf5f69e36a3b.png)


## よくあるご質問
- 次のエラーが出現した場合は、 [プログラム設定の修正](#step4)にしたがって、SDKの引用がプログラムの中に引用されているかチェックしてください。
```
エラー CS0246は、タイプまたはネームスペース“ManageLiteAV”が見つからない場合です(using のコマンドまたはプログラムセットの引用が欠如していませんか?)
```

- 次のエラーが生じた場合は、 [プログラム設定の修正](#step4)にしたがって、プログラムの動作プラットフォーム環境がソリューションの現在のターゲットプラットフォームに修正されているかチェックしてください 。
```
System.BadImageFormatException:“ファイルまたはプログラムセット“ManageLiteAV, Version=2.0.7152.18518, Culture=neutral, PublicKeyToken=null”またはそれの或る依存項目がローディングできません。形式が正しくないプログラムをローディングしようとしています。”
```

- 次のエラーが生じた場合は、 [プログラム設定の修正](#step4)にしたがって、生成したイベントが実行ディレクトリの中に正しく追加されているかチェックしてください。
```
System.IO.FileNotFoundException:“ファイルまたはプログラムセット“ManageLiteAV.dll”またはそれの或る依存項目がローディングできません。指定したコンポーネントが見つかりません。”
```

- Windows のバージョンの違いにより互換性の問題が存在している可能性があります。現在 C# SDK の中には互換性の問題を解決する dll ファイルを新規追加しています。ファイルリストは次の図のとおりです。

- 次のエラーが生じた場合は、前述のプログラム設定にしたがって、 SDKヘッダーファイルのディレクトリが正しく追加されているかチェックしてください。
```
fatal error C1083: include ファイルを開くことができません: “TRTCCloud.h”: No such file or directory
```

- 次のエラーが生じた場合は、前述のプログラム設定にしたがって、SDKライブラリのディレクトリとライブラリファイルが正しく追加されているかチェックしてください。
```
error LNK2019: 解析できない外部シンボル "__declspec(dllimport) public: static class TXString __cdecl TRTCCloud::getSDKVersion(void)" (__imp_?getSDKVersion@TRTCCloud@@SA?AVTXString@@XZ)、この記号が関数 "protected: virtual int __thiscall CTRTCDemoDlg::OnInitDialog(void)" (?OnInitDialog@CTRTCDemoDlg@@MAEHXZ) の中に引用されています
```
