### TRTC V1(iLiveSDK)とV2(LiteAVSDK)バージョンの違いは何ですか。
![](https://main.qcloudimg.com/raw/798eb3618bc87eea647e77a97ae48ca7.png)

| 相違項目 | 旧バージョンV1 |  新バージョンV2 |
|:-------:|:-------:|:-------:|
| カーネルアーキテクチャ | iLiveSDK | LiteAVSDK |
| IM SDK   |  埋め込み        |  埋め込みなし       |
| APIインターフェース |  V1 |  V2 |
| CDNプッシュ | REST APIを使用してオン |  クライアントをサポートする |
| クラウド回線  |  V1回線 |   V2回線  |

### TRTC V1(iLiveSDK)をV2(LiteAVSDK)にアップグレードするにはどうすればよいですか。
- お客様の**プロジェクトがTRTCSDKを統合したことがない**場合は、V2(LiteAVSDK)をそのまま使用することを強くお勧めします。V2には、通話品質、回線仕様、アクセスの難易度および機能の拡張といったすべての点でメリットがあります。
- お客様の**プロジェクトが安定していて問題がない場合**、V1とV2のクラウド回線は現在相互運用できないため、プロジェクトが安定した運用段階に入っている場合は、しばらくアップグレードしなくても問題ありません。
- お客様の**プロジェクトが旧バージョンのV1と結合している**場合は、V2バージョンと直接結合することをお勧めします。V2バージョンのAPIインターフェースは新しいデザインを採用しているため、旧バージョンと比べると、結合にかかる時間がはるかに短くて済みます。
- お客様が**旧バージョンのV1を使用しており、通話品質を向上させたい場合**、V1とV2のクラウド回線は今のところ相互運用をしていないので、新しいバージョンのSDKにアップグレードするために、「SDK統合」、「大量展開」および「クラウドの切り替え」といったプロセスを経る必要があります。大まかな手順は次のとおりです。
 1. 新しいバージョンのSDKを既存のプロジェクトに統合し、テストにパスします。
 2. ルームリストにSDKバージョン番号フィールドを追加すると、Appはサーバー側のフィールドに応じてV1バージョンとV2バージョンのどちらを使用するか決定します。
 3. Appの新しいバージョンをパブリッシュし、そのバージョンがユーザーグループを徐々にカバーするのを待ちます。
 4. ルームリストのSDKバージョン番号フィールドをV1からV2に切り替えて、回線の切り替えを完了します。


### Android端末のLiteAVSDKとiLiveSDKを同時に互換・統合するにはどうすればよいですか。

iLiveSDKとLiteAVSDKはどちらも、エコー除去やノイズリダクションなどのオーディオ処理にTRAEを使用します。LiteAVSDKで使用されるTRAEのバージョンが更新され、iLiveSDKで使用されるすべての機能インターフェースが含まれています。そのため、設定項目の中でLiteAVSDKのTRAEライブラリを使用するように設定するだけでOKです。
aarメソッドを使用してプロジェクトを統合し、サブプロジェクト（appディレクトリ）の下のbuild.gradleを変更し、android {}ノードで次のように設定します。
>!引用を追加するときは、LiteAVSDKは必ずiLiveSDKの前に配置してください。

```java
android{
//1、gradleでpackagingoptionsを設定します
packagingOptions {
pickFirst 'lib/armeabi-v7a/libTRAECodec.so'
pickFirst 'lib/armeabi-v7a/libstlport_shared.so'
pickFirst 'lib/armeabi/libTRAECodec.so'
pickFirst 'lib/armeabi/libstlport_shared.so'
}
//2、dempendenciesを導入します
implementation(name:'LiteAVSDK_TRTC_6.4.7108', ext:'aar')  // TRTCは必ずiLiveSDKの前にあるように注意してください
implementation 'com.tencent.ilivesdk:ilivesdk:1.9.4.6.4'
}
```

### iOS端末のLiteAVSDK + iLiveSDK + BeautySDKを同時に互換・統合するにはどうすればよいですか。
TRTC V1バージョンでは、BeautySDKを使用して美顔やアニメーションエフェクトなどの機能を実装します。TRTC V2バージョンでは、BeautySDKの機能をLiteAVSDKに組み込むことにより、ユーザーにとってより使いやすくしました。iLiveSDKが統合され、BeautySDKがプロジェクトに導入されている場合、ファイルの競合が発生します。この場合の解決方法は、次のとおりです。

| バージョン                                   | 処理方法                                                     |
| -------------------------------------- | ------------------------------------------------------------ |
| BeautySDKベーシック版（P画像バージョンなし） | XcodeプロジェクトでBeautySDKのヘッダーファイル検索パスを設定し、BeautySDKのリンクを解除するだけでOKです。 |
| BeautySDKプレミアム版（P画像バージョン付き）    | LiteAVSDKエンタープライズ版を使用し、XcodeプロジェクトでBeautySDKのヘッダーファイルの検索パスを設定するとともに、BeautySDKのリンクを解除する必要があります（LiteAVSDKエンタープライズ版にはP画像コンポーネントがあります。以前に購入したP画像のlicenceはそのまま使用できますので、料金を再度支払う必要はありません）。 |

### Windows端末のLiteAVSDKとiLiveSDKを同時に互換・統合するにはどうすればよいですか。

Windows端末のLiteAVSDKとiLiveSDKはどちらも、エコー除去やノイズリダクションなどのオーディオ処理にTRAEを使用します。しかし、LiteAVSDKで使用されるTRAEのバージョンが更新されており、機能の使い方に違いがあるため、直接交換することはできません。この場合、以下の方法で処理することができます。

#### プロジェクトの構造

プロジェクトには、次の構造を採用することをお勧めします。

	|
	|- メインプログラム.exe
	|- メインプログラム.exeが依存する他のファイル
	|- iLiveSDK.dll
	|- iLiveSDK.dllが依存する他のファイル
	|- LiteAV
	|        |- liteav.dll
	|        |- liteav.dllが依存する他のファイル

#### 初期化方法

使用する場合は、iLiveSDKは直接.libを用いてリンクすることも、次のコードを使用して動的にロードすることもできます。
```cpp
HMODULE hiLive = LoadLibrary("iLiveSDK.dll");
```

LiteAVSDKを使用する必要がある場合は、次のコードを使用してロードと初期化を行ってください。

<dx-codeblock>
::: cpp cpp
typedef ITRTCCloud* (*getTRTCShareInstanceMtd)();
typedef void(*destroyTRTCShareInstanceMtd)();

TCHAR dllPath[MAX_PATH];
GetModuleFileName(nullptr, dllPath, MAX_PATH);
PathRemoveFileSpec(dllPath);
wcscat(dllPath, L"\\LiteAV\\");
SetDllDirectory(dllPath);
HMODULE hLiteAV = LoadLibrary(L"liteav.dll");
if (!hLiteAV) {
printf("liteav.dllのロードに失敗しました: %d", GetLastError());
return;
}

getTRTCShareInstanceMtd pGetTRTCShareInstance = (getTRTCShareInstanceMtd)GetProcAddress(hLiteAV, "getTRTCShareInstance");
if (!pGetTRTCShareInstance) {
printf("関数getTRTCShareInstanceのロードに失敗しました");
return;
}

destroyTRTCShareInstanceMtd pDestroyTRTCShareInstance = (destroyTRTCShareInstanceMtd)GetProcAddress(hLiteAV, "destroyTRTCShareInstance");
if (!pDestroyTRTCShareInstance) {
printf("関数destroyTRTCShareInstanceのロードに失敗しました");
return;
}

ITRTCCloud *pTrtcCloud = m_pGetTRTCShareInstance();
if (!pTrtcCloud) {
printf("TRTCインスタンスの作成に失敗しました");
return;
}
SetDllDirectory(nullptr);

pTrtcCloud->enterRoom(...);
:::
</dx-codeblock>



