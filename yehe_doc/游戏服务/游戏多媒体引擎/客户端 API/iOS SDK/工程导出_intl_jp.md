
iOS開発者のデバッグとTencent Cloud GME製品APIの導入を容易にするために、このドキュメントではiOSプロジェクトのエクスポートに関する注意事項などを紹介します。


##　コンフィギュレーションエクスポートについて

1.　次の図に示すように、必要に応じて **Xcode** > **Link Binary With Libraries** > **Build Setting**に次の依存ライブラリを追加し、Framework Search PathsをSDKディレクトリに設定します。  
<img src="https://main.qcloudimg.com/raw/79355a317302adccd7f96e898bef7845.png"  style="
    width: 80%;
"> 
2.　次の図に示すように、依存ライブラリを追加します。
![](https://main.qcloudimg.com/raw/b6156b8c7a596248c148607070e38f67.png)
3.　Bitcodeはプロジェクトが依存するすべてのクラスライブラリによって同時にサポートされる必要があり、SDKは現時点でBitcodeをサポートしませんので、一応無効にします。   この設定を無効にするには、Targets - Build SettingsからBitcodeを検索して該当オプションを特定し、NOに設定します。
<img src="https://main.qcloudimg.com/raw/7020b4fadc30d29d5760873a53e64124.png"  style="
    width: 80%;
"> 
4.　GMEはiOSプラットフォームで必要なプライバシー権限は以下のとおりです。
 - Required background modes：バックグラウンド実行が許容されます（オプション）。
 - Microphone Usage Description：マイク権限が許容されます。


## GME 2.9以降

2.9以降のSDKを導入する場合は、[iOSプロジェクトのアップグレードガイド](https://intl.cloud.tencent.com/document/product/607/46015)のドキュメントを参照して設定する必要があります。
