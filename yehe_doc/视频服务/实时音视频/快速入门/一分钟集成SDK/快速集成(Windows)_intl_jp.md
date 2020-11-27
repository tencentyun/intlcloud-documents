このドキュメントでは、主にTencent Cloud　TRTC SDK（Windows C#バージョン）をプロジェクトにすばやく統合する方法について説明します。

## 開発環境要件

- OS：Windows 7以降。
- 開発環境：Visual Studio 2010以上のバージョン、 Visual Studio 2015の使用をお薦めします。
- 開発フレームワーク：.Net Framework 4.0以上のバージョン。

## TRTC SDKの統合

ここでは、簡単なWinformプロジェクトの新規作成を例に、 Visual Studio プロジェクトで C# SDKを統合する方法を紹介します。

### 手順1： Windows SDKのダウンロード

[ SDKをダウンロード](http://liteavsdk-1252463788.cosgz.myqcloud.com/TXLiteAVSDK_TRTC_Win_latest.zip)して解凍し、次のようなファイルを開きます。

| ディレクトリ名  | 説明
| ------- | -------------------------------------- |
| xxxDemo | C++ Demo ソースコードおよび C# Demo ソースコード |
| CPlusPlus | C++バージョン32ビット/64ビットに依存するSDKライブラリファイル|
| CSharp | C#バージョン32ビット/64ビットに依存するSDKライブラリファイル |

ここの例では、SDKファイルのC＃バージョンをSDKディレクトリにインポートするだけで済みます。

### 手順2：プロジェクトの新規作成

Visual Studioを開き、新規作成名を`TRTCCSharpDemo`の Winformアプリケーションプログラムとします。

### 手順3：ファイルのコピー

解凍後の SDKフォルダーを`TRTCCSharpDemo.csproj`が所在するディレクトリにコピーします。
>? C# SDKだけを必要とする場合は、SDKパスの下のCPlusPlus ディレクトリを削除できます。


<span id="Step4"></span>
### 手順4：プロジェクト設定の変更
**手順4.1：参照の追加**
1. Visual Studio の【ビルド】ディレクトリで【構成マネージャー】を探して開きます。
<span id="step4_1_2"></span>
2. 【アクティブソリューションプラットフォーム】のドロップダウン・リストから【新規作成】を選択し、【新しいソリューション プラットフォーム】ダイアログボックスをポップアップします。
<span id="step4_1_3"></span>
3．新しいプラットフォームを入力または選択し、【OK】をクリックします。

4．実際のニーズに応じて [手順2](#step4_1_2) - [手順3](#step4_1_3) を繰り返して、サポートが必要なソリューションプラットフォームを新規作成します。

5.  TRTCCSharpDemoプロジェクトが配置されているフォルダーを開き、テキストエディタで`TRTCCSharpDemo.csproj`ファイルを編集します。
6. `TRTCCSharpDemo.csproj`ファイルのタグ `<itemGroup>`の下に以下の内容を追加します。
  ```
  // Add references to different platforms
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


**手順4.2： copy コマンドの追加**
1.  TRTCCSharpDemo プロパティページを開き、【ソリューション エクスプローラー】>【TRTCCSharpDemo プロジェクトの右キーメニュー】>【プロパティ】を選択します。
2. 【ビルド イベント】>【ビルド後に実行するコマンド ライン】に以下のコマンドを追加します。コンパイルが完了したら、下図に示すとおり、異なるプラットフォームの SDKの .dll ファイルをプログラムの実行ディレクトリに自動的にコピーします。
```
set Platform=Win64
SETLOCAL ENABLEDELAYEDEXPANSION
if $(PlatformName)==x86 ( 
  set Platform=Win32
)
copy /Y "$(ProjectDir)SDK\CSharp\!Platform!\lib\*.dll" "$(ProjectDir)$(OutDir)"
ENDLOCAL
```


**手順4.3：デバッグ環境の変更**
 TRTCDemo のプロパティページを開き、【ビルド】を選択し、【プラットフォーム(M)】と上方のメニューバーのソリューションプラットフォームが一致するように設定します。

### 手順5： SDK バージョン番号の印刷
1.  Form1.cs のデザイナにラベルコントロールを追加します。
2.  Form1.cs コードファイルを開き、以下のコードを追加します。
	```c#
	using System.Windows.Forms;
	using ManageLiteAV;   // 1.ネームスペースの参照を追加します

	namespace TRTCCSharpDemo
	{
			public partial class Form1 : Form
			{
					public Form1()
					{
							InitializeComponent();
							// 2. ITRTCCloud インスタンスを取得し、 SDK バージョン番号を印刷します
							ITRTCCloud lTRTCCloud = ITRTCCloud.getTRTCShareInstance(); 
							this.label1.Text = "SDK version : " + lTRTCCloud.getSDKVersion();
							// 3.使用を終了する場合は、手動でITRTCCloudインスタンスを破壊する必要があります。
							ITRTCCloud.destroyTRTCShareInstance();
					}
			}
	}
	```
3．F5キーを押して実行し、下図のとおり、SKDのバージョン番号を印刷します。
 ![](https://main.qcloudimg.com/raw/9bfebaac4fa339af6b7c74b0413cde1d.png)


## よくあるご質問

- 以下のエラーが生じた場合は、[プロジェクト設定の変更](#Step4)に従って、SDKの参照がプロジェクトに追加されているか検査してください。
```
エラー CS0246 は、タイプまたはネームスペース名“ManageLiteAV”( using 指令またはアセンブリの参照が不足しているか？)が見つかりませんでした。
```
- 以下のエラーが生じた場合は、[プロジェクト設定の変更](#Step4)に従って、プロジェクト動作プラットフォームの環境をソリューションの現在目標プラットフォームに修正しているか検査してください。
```
System.BadImageFormatException:“ファイルまたはアセンブリ“ManageLiteAV, Version=2.0.7152.18518, Culture=neutral, PublicKeyToken=null”、またはそのある依存関係をまだロードできていません。フォーマットが正しくないプログラムのロードを意図しています。”
```
- 以下のエラーが生じた場合は、[プロジェクト設定の変更](#Step4)に従って、ビルドイベントを動作ディレクトリに正しく追加しているか検査してください。
```
System.IO.FileNotFoundException:“ファイルまたはアセンブリ“ManageLiteAV.dll”、またはその依存関係の一つをまだロードできていません。指定したモジュールが見つかりません。”
```
- 異なるWindowsバージョン間で互換性の問題が発生する可能性があるため、現在は互換性の問題を解決するdllファイルが C# SDK に新たに追加されています。

