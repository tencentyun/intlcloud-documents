>?
>- IPv6 NAT64 CLBは北京、上海、広州の3リージョンのみサポートしています。
>- インターネットのIPv6ネットワークマクロ環境は構築の初期段階のため、SLA保障を提供していません。ネットワークにアクセスできない状態が発生した場合は、[チケットを提出](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=163&source=0&data_title=%E8%B4%9F%E8%BD%BD%E5%9D%87%E8%A1%A1%20LB&step=1)してフィードバックしてください。
>

CLBはIPv6 NAT64 CLBインスタンスの作成をサポートしています。Tencent CloudはインスタンスにIPv6パブリックアドレス（すなわち、IPv6版のVIP）を割り当てます。このVIPはIPv6クライアントからのリクエストをバックエンドのIPv4 CVMに転送します。

## IPv6 NAT64 CLBとは何ですか
IPv6 NAT64 CLBはNAT64 IPv6移行技術をベースにして実現したロードバランサです。IPv6 NAT64 CLBによって、バックエンドCVMはIPv6用の修正を何も行うことなく、スピーディーにIPv6ユーザーからのアクセスに対応できます。

## IPv6 NAT64 CLBのアーキテクチャ
IPv6 NAT64 CLBのアーキテクチャは下図のとおりです。
![](https://main.qcloudimg.com/raw/e86896cc8286b53e8198facc8d28076f.png)
IPv6ネットワークを介してIPv6 NAT64 CLBにアクセスする場合、CLBはIPv6アドレスをIPv4アドレスにスムーズに変換し、既存のサービスに適用させることで、IPv6用の修正をスピーディーに実現します。

## IPv6 NAT64 CLBのメリット
Tencent Cloud IPv6 NAT64 CLBは業務をスピーディーにIPv6に接続させる際に、次のようなメリットを発揮します。
- **クイックアクセス：**秒レベルでIPv6に接続でき、購入後すぐに使用できます。
- **業務のスムーズな移行：**業務上修正が必要なのはクライアントのみで、バックエンドサービスの修正は必要なく、スムーズにIPv6に接続できます。IPv6 NAT64 CLBはIPv6クライアントからのアクセスをサポートし、IPv6メッセージのIPv4メッセージへの変換も行います。バックエンドCVM上のアプリケーションはIPv6であることを感知せず、従来の形式でデプロイを行うことができます。
- **使いやすさ：**IPv6 NAT64 CLBは旧IPv4 CLBのトラフィック操作との間に互換性があり、学習コストがかからないため、使用のハードルが低くなっています。

## 操作ガイド
### IPv6 NAT64 CLBの作成
1. Tencent Cloud公式サイトにログインし、[CLB購入ページ](https://buy.intl.cloud.tencent.com/lb)に進みます。
2. 次のパラメータを正しく選択してください。
 - 課金モデル：従量課金モデルをサポートしています。
 - リージョン：北京、上海、広州の3リージョンのみサポートしています。
 - インスタンスタイプ：CLB。
 - ネットワークタイプ：パブリックネットワーク。
 - IPバージョン：IPv6 NAT64。
 - 所属ネットワーク：VPC。
 - その他の設定は一般的なインスタンスの設定と同様です。
3. 購入ページで各項目の設定を選択し、**今すぐ購入**をクリックします。[CLBインスタンスリストページ](https://console.cloud.tencent.com/loadbalance/index?rid=1&forward=1)に戻ると、IPv6 NAT64 CLBが購入済みになっていることを確認できます。


### IPv6 NAT64 CLBの使用
[CLBコンソール](https://console.cloud.tencent.com/loadbalance/index?rid=1&forward=1)にログインし、インスタンスIDをクリックして詳細ページに進み、「リスナー管理」ページでリスナー、転送ルール、CVMのバインドを設定します。詳細については、[CLBクイックスタート](https://intl.cloud.tencent.com/document/product/214/8975)をご参照ください。
![](https://main.qcloudimg.com/raw/2cacac7c34a7fa241dbd6f9127570391.png)

## 関連ドキュメント
[ハイブリッドクラウドのデプロイシーンでのTOAによるクライアントリアルIPの取得](https://intl.cloud.tencent.com/document/product/214/45530)
