標準ライブストリーミング（LVB）は、CSSが通常のライブストリーミングシナリオを対象に提供するプロフェッショナルで、安定的かつスピーディーなクラウドライブストリーミングサービスです。MLVB SDKと組み合わせることで、App、Webなどのマルチプラットフォームでのスピーディーなアクセスを手早く実装できます。

[](id:app)

## APPへのアクセス	
iOS、Androidのアプリの場合、MLVB SDKを統合することで、App端末でのCSSプッシュ/再生機能を実装できます。

- **App端末でのCSSプッシュ**：カメラ画面のキャプチャまたはスマホ画面のキャプチャをサポートし、RTMPプロトコルによって迅速にCSSサービス上にプッシュ可能です。
- **App端末でのライブストリーミング再生**：RTMP、FLV、HLSなどの形式の再生プロトコルをサポートし、CSSのサービスと組み合わせることでライブストリーミングAPPを手早く作成することが可能です。

>? MLVB SDKはCSS、IM、TRTCなどのサービスの力を借りることで、多人数オーディオビデオの低遅延な相互接続・相互通信を実現することが可能です。多人数マイク接続によるインタラクティブな効果を実現し、マイク接続に参加しない視聴者もCSSのサービスを介して視聴することができます。

[](id:web)

## Webへのアクセス
ウェブサイトでCSSプッシュと再生を行う必要がある場合は、次の方式によるアクセスを推奨します。
- **Web端末でのCSSプッシュ**：ブラウザの一般的なWebRTCの規格をベースに設計とカプセル化を行い、コードスニペットを導入することで、ブラウザの中でCSSプッシュを実現させます。詳細については、[WebRTCプッシュ](https://intl.cloud.tencent.com/document/product/267/41620)をご参照ください。
> ! WebRTCプッシュの時、オーディオコーデック方式にはopusコーデックのみをサポートしています。標準ライブストリーミングの再生プロトコル（RTMP、FLV、HLS）を使用して再生を行った場合、正常な視聴を保証するため、CSSバックエンドがオーディオコーデックを自動的に開始してaacに変換し、これによりオーディオトランスコード料金が発生します。詳細については、[オーディオトランスコード料金の説明](https://intl.cloud.tencent.com/document/product/267/39604)をご参照ください。


