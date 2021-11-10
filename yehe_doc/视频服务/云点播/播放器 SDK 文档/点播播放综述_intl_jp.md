Tencent Cloud View Cube Playerは、ユーザーがクラウドサービスに接続し、クラウド統合機能を作成するための重要なコンポーネントです。PlayerはVOD再生シナリオのためにSuper PlayerとSuper Player Adapterの2種類のプレーヤーを提供することができ、Web端末、iOS端末、Android端末、Flutter端末という4大端末をサポートしています。Playerは、VODユーザーが短時間でスムーズな視聴体験を構築できるように支援し、複数の機能を統合した高性能なソリューションを提供します。
このドキュメントでは、ユーザーが自身に適したプレーヤータイプを選択できるよう、さまざまなタイプのPlayerの違いと使用方法を紹介します。



## 基本概念の説明[](id:concept)
### Super Player
Super PlayerはURL再生、FileID再生という2つの再生方式をサポートしています。
<table>
   <tr>
      <th width="178px" style="text-align:center">再生方式</td>
      <th width="0px" style="text-align:center">説明</td>
   </tr>
   <tr>
      <td style="text-align:center">Super Player - URL再生</td>
      <td>ユーザーがURLを介して再生する方式です。この再生方式はFileIDのデータ統計と複雑なメディア資産機能をサポートしていません。<b>ショートビデオ</b>または<b>ショートミディアムビデオ</b>などのその他メディア資産の補助情報を必要としないシナリオで一般的に使用されます。</td>
   </tr>
   <tr>
      <td>Super Player - FileID再生</td>
      <td>ユーザーがVODのFileIDを介してビデオ再生する方式です。この再生方式はVODリソースとPlayer+を深く融合させる機能を提供します。ユーザーはFileIDに基づきデータレポート、モニタリングと複雑なメディア資産のバインディング機能を実現することができます。<b>ロングビデオ</b>などのその他メディア資産の補助情報を同時に再生する必要があるシナリオで一般的に使用されます。</td>
   </tr>
</table>

<dx-alert infotype="explain" title="">
Super Player機能リストについては、[Super Player機能リスト](https://intl.cloud.tencent.com/document/product/266/38295)をご参照ください。
</dx-alert>


### Super Player Adapter
Super Player Adapter は、サードパーティのプレーヤーまたは自社開発のプレーヤーを使用して開放されたクラウドPAASリソースに接続を希望する顧客向けにVODのためのプレーヤープラグインを提供します。**カスタムプレーヤー機能を強く**必要とするユーザーにおいて一般的に使用されます。技術的なアクセスのしきい値を有し、基本機能はSuper Playerと一致しています。


### プレーヤータイプの比較
<table>
    <tr>
        <th width="120px">プレーヤータイプ</td> 
        <th width="250px">機能</td> 
        <th>特徴</td>
        <th>カスタマイズレベル</td> 
   </tr>
   <tr>
        <td rowspan="2">Super Player</td>    
        <td >再生URLをサポートしています</td>
        <td > VOD再生URLとサードパーティをソースとするURLをサポートしています </td> 
        <td > 低 </td> 
   </tr>
   <tr>
        <td> VOD再生FileIDをサポートしています </td> 
        <td> VOD一体化データのレポート、品質管理サービスを提供します </td> 
        <td > 低 </td> 
   </tr>
     <tr>
        <td >Super Player Adapter</td> 
        <td> VOD再生FileIDのみをサポートしています </td> 
        <td> ユーザーのサードパーティプレーヤーの使用、または自社開発プレーヤーの統合をサポートしています </td> 
        <td> 高 </td>
   </tr>

</table>



## 主な優位性[](id:core)
<table>
   <tr>
      <th width="120px" style="text-align:center">紹介</td>
      <th width="0px" style="text-align:center">説明</td>
   </tr>
   <tr>
      <td style="text-align:center">クラウド一体化</td>
      <td>ユーザーはVOD PAASリソースを手軽に使用して、クラウド一体化機能を構築することができます。</td>
   </tr>
   <tr>
      <td style="text-align:center">ビデオセキュリティ</td>
      <td>ホットリンク防止、URL認証、HLS暗号化、プライベートプロトコル暗号化、ローカル暗号化などの複数の暗号化スキームを提供し、ユーザーメディアのセキュリティを全面的に保証すると同時に、各種シナリオのセキュリティニーズを満たします。</td>
   </tr>
   <tr>
      <td style="text-align:center">ビデオ再生</td>
      <td>最初のフレームのインスタントストリーミング、再生とキャッシュの同時実行、倍速再生、ビデオのキーフレーム、メディアの弾幕および外部字幕など多くの機能を提供します。</td>
   </tr>
   <tr>
      <td style="text-align:center">ビデオアクセラレーション</td>
      <td>Tencent Cloudの大量のアクセラレーションノードにより、完全なビデオアクセラレーション機能を提供します。ミリ秒の遅延がユーザーに遅延を感じさせない超高速ビデオ再生の体験をもたらします。</td>
   </tr>
</table>

## 特色ある機能[](id:function)
Tencent Cloud View Cube Playerを統合することで、多くの機能のクリック統合をサポートしています。その他の機能については、[機能リスト](https://intl.cloud.tencent.com/document/product/266/38295)をご参照ください。
<table>
   <tr>
      <th width="120px" style="text-align:center">機能</td>
      <th width="0px" style="text-align:center">機能説明</td>
      <th width="120px"  style="text-align:center">その他の説明</td>
   </tr>
   <tr>
      <td style="text-align:center">ビデオ暗号化</td>
      <td>標準的なHlS暗号化とTencent Cloudプライベートプロトコルの暗号化をサポートしています</td>
      <td><a href="https://intl.cloud.tencent.com/document/product/266/38131">ビデオ暗号化の概要</a></td>
   </tr>
   <tr>
      <td style="text-align:center">ビデオ再生</td>
      <td>各種シナリオでオンデマンドのメディアと関連のメディア資産の補助情報を組み合わせ、FileIDを介して出力することをサポートし、多様なビデオ再生機能を完成させます</td>
      <td><a href="https://intl.cloud.tencent.com/document/product/266/38295">ビデオ再生の概要</a></td>
   </tr>
   <tr>
      <td style="text-align:center">安全なダウンロード</td>
      <td>ダウンロードしたビデオをローカルで二次暗号化することをサポートし、ユーザーのメディアが唯一のアプリケーションを介してのみ再生されることを保証します</td>
      <td><a href="https://intl.cloud.tencent.com/document/product/266/38295">ビデオ再生の概要</a></td>
   </tr>
</table>

## 関連リンク[](id:link)
Tencent Cloud View Cube Playerは、Web端末、iOS端末、Android端末、Flutter端末という4大端末をサポートしており、その内のFlutter端末はSuper Playerの使用のみをサポートしています。詳細については、表中のドキュメントをご参照ください。


<table>
   <tr>
      <th width="120px" style="text-align:center">端末タイプ</td>
      <th width="70px" style="text-align:center">プレーヤータイプ</td>
      <th width="0px"  style="text-align:center">SDK & Demoダウンロードアドレス</td>
      <th width="0px" style="text-align:center">Demo表示</td>
      <th width="0px"  style="text-align:center">	使用ドキュメント</td>
   </tr>
   <tr>
      <td style="text-align:center" rowspan='2'>Web端末</td>
      <td>Super Player</td>
      <td><a href="https://intl.cloud.tencent.com/document/product/266/33977#transcoding-service-on-vod-platform">SDK</a></td>
      <td><a href="https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod/tcplayer-vod-base.html">Demo</a></td>
      <td><a href="https://intl.cloud.tencent.com/document/product/266/33977">Web - Super Player</a></td>
   </tr>
   <tr>
      <td>Super Player Adapter</td>
      <td><a href="https://intl.cloud.tencent.com/document/product/266/42095">SDK</a></td>
      <td>-</td>
      <td><a href="https://intl.cloud.tencent.com/document/product/266/42095">Web - Super Player Adapter</a></td>
   </tr>
   <tr>
      <td style="text-align:center" rowspan='2'>iOS端末</td>
      <td>Super Player</td>
      <td><a href="https://github.com/tencentyun/SuperPlayer_iOS">SDK + Demo</a></td>
      <td><a><button style="width:120px;height: 120px;border:none;background-image:url(https://main.qcloudimg.com/raw/12c7da97cc910eda673cb19b66fc7cb3.png);background-size: cover;">
</button></a></td>
      <td><a href="https://intl.cloud.tencent.com/document/product/266/33976">iOS - Super Player</a></td>
   </tr>
   <tr>
      <td>Super Player Adapter</td>
      <td><a href="https://mediacloud-76607.gzc.vod.tencent-cloud.com/TXCPlayerAdapter/Release/1.0.0/TXCPlayerAdapterSDK_1.0.0_iOS.zip">SDK</a></td>
      <td>-</td>
      <td><a href="https://intl.cloud.tencent.com/document/product/266/42096">iOS - Super Player Adapter</a></td>
   </tr>
   <tr>
      <td style="text-align:center" rowspan='2'>Android端末</td>
      <td>Super Player</td>
      <td><a href="https://github.com/tencentyun/SuperPlayer_Android">SDK + Demo</a></td>
      <td><a><button style="width:120px;height: 120px;border:none;background-image:url(https://main.qcloudimg.com/raw/6790ddaf4ffe4afd0ceb96b309a16496.png);background-size: cover;">
</button></a></td>
      <td><a href="https://intl.cloud.tencent.com/document/product/266/33975">Android - Super Player</a></td>
   </tr>
   <tr>
      <td>Super Player Adapter</td>
      <td><a href="https://mediacloud-76607.gzc.vod.tencent-cloud.com/TXCPlayerAdapter/Release/1.0.0/TXCPlayerAdapterSDK_1.0.0_Android.zip">SDK</a></td>
      <td>-</td>
      <td><a href="https://intl.cloud.tencent.com/document/product/266/42097">Android- Super Player Adapter</a></td>
   </tr>
   <tr>
      <td  style="text-align:center">Flutter端末</td>
      <td>Super Player</td>
      <td><a href="https://github.com/tencentyun/SuperPlayer/tree/main/Flutter">SDK + Demo</a></td>
	     <td><a href="https://github.com/tencentyun/SuperPlayer/tree/main/Flutter">Demo</a></td>
	     <td><a href="https://intl.cloud.tencent.com/document/product/266/42099">Flutter - Super Player</a></td>
   </tr>
</table>




## アクセスガイド
Super Playerを速やかに統合できるように、Super Playerの[アクセスガイド](https://intl.cloud.tencent.com/document/product/266/38098)を提供し、統合手順について例示して説明しています。
- 再生に問題が発生した場合は、[よくあるご質問ドキュメント](https://intl.cloud.tencent.com/document/product/266/1303)をご参照ください。
- 専門用語については、[用語集](https://intl.cloud.tencent.com/document/product/266/11732)をご参照ください。
  
